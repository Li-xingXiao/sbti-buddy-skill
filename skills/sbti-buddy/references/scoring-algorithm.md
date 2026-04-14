# SBTI Scoring Algorithm

Reuses the original SBTI Manhattan distance matching algorithm, adapted for continuous score inputs from conversation analysis.

---

## Step 1: Raw Scores → L/M/H

Conversation analysis produces a 0-100 raw score per dimension. Mapping rules:

| Raw Score Range | Level | Value |
|----------------|-------|-------|
| 0 - 33 | L | 1 |
| 34 - 66 | M | 2 |
| 67 - 100 | H | 3 |

> Difference from original SBTI: The original has 2 questions per dimension, total score 2-6, mapped as 2-3→L, 4→M, 5-6→H.
> We use equal-thirds, providing a more uniform distribution.

## Step 2: Build Vector and Pattern String

In dimension order `[S1, S2, S3, E1, E2, E3, A1, A2, A3, Ac1, Ac2, Ac3, So1, So2, So3]`, build:

- **Numeric vector**: `[3, 2, 1, 3, 3, 2, ...]` (15 elements)
- **Pattern string**: `"HML-HHM-..."` (groups of 3 separated by `-`, corresponding to 5 models)

Example:
```
Numeric vector: [3, 3, 2, 3, 2, 3, 2, 2, 3, 3, 3, 3, 2, 3, 2]
Pattern string: HHM-HMH-MMH-HHH-MHM
```

## Step 3: Manhattan Distance Calculation

For all 25 standard types (excluding HHHH and DRUNK), calculate:

```
distance(user, type) = Σ |user_vector[i] - type_vector[i]|  for i = 0..14
exact_hits = count(user_vector[i] == type_vector[i])  for i = 0..14
similarity = max(0, round((1 - distance / 30) * 100))
```

- **Theoretical max distance**: 30 (max difference of 2 per dimension, 15 dimensions)
- **similarity**: Percentage, higher = better match

## Step 4: Sort and Select

Sort all 25 standard types by the following priority:
1. `distance` **ascending** (lower is better)
2. `exact_hits` **descending** (more is better)
3. `similarity` **descending** (higher is better)

Rank #1 = primary type, ranks #2-5 = candidate types.

## Step 5: Special Rules

### HHHH Fallback (The Happy Coder)

If the best match has `similarity < 60%` (i.e., distance > 12):
- Set primary type to **HHHH**
- Show original best match as secondary type
- Use HHHH's programmer-specific description

### Late Night Coder Easter Egg

Replaces the original SBTI "drunk" easter egg (original triggered via questionnaire; we trigger via behavior):

**Trigger condition**: If conversation history has timestamp information and >50% of messages were sent between 00:00-05:00 (local time).

**Effect**:
- Does not override the normal match result
- Displays an additional "Late Night Coder" badge in the result
- Unlocks the "Night Owl" achievement
- Adds a dark circles expression variant to the buddy avatar

> Note: Timestamps may not be available in some data sources. Skip this detection if timestamps are unavailable.

## Step 6: Confidence Level

Based on total messages analyzed:

| Messages | Confidence | Description |
|----------|-----------|-------------|
| < 20 | Do not generate | Tell user to accumulate more conversations |
| 20-50 | "Early Sketch" | Results are preliminary |
| 50-200 | "Clear Portrait" | Reasonably reliable |
| > 200 | "Deep Portrait" | Highly reliable |

## 25 Standard Type Pattern Vectors

The following are the pattern and numeric vectors for the 25 original SBTI types, used for distance calculation:

```
CTRL    HHH-HMH-MHH-HHH-MHM  [3,3,3,3,2,3,2,3,3,3,3,3,2,3,2]
ATM-er  HHH-HHM-HHH-HMH-MHL  [3,3,3,3,3,2,3,3,3,3,2,3,2,3,1]
Dior-s  MHM-MMH-MHM-HMH-LHL  [2,3,2,2,2,3,2,3,2,3,2,3,1,3,1]
BOSS    HHH-HMH-MMH-HHH-LHL  [3,3,3,3,2,3,2,2,3,3,3,3,1,3,1]
THAN-K  MHM-HMM-HHM-MMH-MHL  [2,3,2,3,2,2,3,3,2,2,2,3,2,3,1]
OH-NO   HHL-LMH-LHH-HHM-LHL  [3,3,1,1,2,3,1,3,3,3,3,2,1,3,1]
GOGO    HHM-HMH-MMH-HHH-MHM  [3,3,2,3,2,3,2,2,3,3,3,3,2,3,2]
SEXY    HMH-HHL-HMM-HMM-HLH  [3,2,3,3,3,1,3,2,2,3,2,2,3,1,3]
LOVE-R  MLH-LHL-HLH-MLM-MLH  [2,1,3,1,3,1,3,1,3,2,1,2,2,1,3]
MUM     MMH-MHL-HMM-LMM-HLL  [2,2,3,2,3,1,3,2,2,1,2,2,3,1,1]
FAKE    HLM-MML-MLM-MLM-HLH  [3,1,2,2,2,1,2,1,2,2,1,2,3,1,3]
OG8K    MMH-MMM-HML-LMM-MML  [2,2,3,2,2,2,3,2,1,1,2,2,2,2,1]
MALO    MLH-MHM-MLH-MLH-LMH  [2,1,3,2,3,2,2,1,3,2,1,3,1,2,3]
JOKE-R  LLH-LHL-LML-LLL-MLM  [1,1,3,1,3,1,1,2,1,1,1,1,2,1,2]
WOC!    HHL-HMH-MMH-HHM-LHH  [3,3,1,3,2,3,2,2,3,3,3,2,1,3,3]
THIN-K  HHL-HMH-MLH-MHM-LHH  [3,3,1,3,2,3,2,1,3,2,3,2,1,3,3]
SHIT    HHL-HLH-LMM-HHM-LHH  [3,3,1,3,1,3,1,2,2,3,3,2,1,3,3]
ZZZZ    MHL-MLH-LML-MML-LHM  [2,3,1,2,1,3,1,2,1,2,2,1,1,3,2]
POOR    HHL-MLH-LMH-HHH-LHL  [3,3,1,2,1,3,1,2,3,3,3,3,1,3,1]
MONK    HHL-LLH-LLM-MML-LHM  [3,3,1,1,1,3,1,1,2,2,2,1,1,3,2]
IMSB    LLM-LMM-LLL-LLL-MLM  [1,1,2,1,2,2,1,1,1,1,1,1,2,1,2]
SOLO    LML-LLH-LHL-LML-LHM  [1,2,1,1,1,3,1,3,1,1,2,1,1,3,2]
FU?K    MLL-LHL-LLM-MLL-HLH  [2,1,1,1,3,1,1,1,2,2,1,1,3,1,3]
DEAD    LLL-LLM-LML-LLL-LHM  [1,1,1,1,1,2,1,2,1,1,1,1,1,3,2]
IMFW    LLH-LHL-LML-LLL-MLL  [1,1,3,1,3,1,1,2,1,1,1,1,2,1,1]
```

## Incremental Update Algorithm

When performing an incremental update (reading only new messages):

```
new_raw_scores[i] = analyze(new_messages)  // 15-dimension analysis of new messages
old_raw_scores[i] = historical scores from profile.json
old_count = messageCount from profile.json
new_count = number of new messages

merged_score[i] = (old_raw_scores[i] * old_count + new_raw_scores[i] * new_count) / (old_count + new_count)
```

Then re-run Steps 1-5 on `merged_score`.
