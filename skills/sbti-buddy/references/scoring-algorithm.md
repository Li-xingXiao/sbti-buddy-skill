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

## Step 3: Euclidean Distance Calculation

For all 25 standard types (excluding HHHH and DRUNK), calculate the Euclidean distance between the user's **raw scores** (0-100) and each type's **centroid** (see "25 Type Centroids" table below):

```
distance(user, type) = sqrt( Σ (user_raw[i] - centroid[i])^2 / 15 )  for i = 0..14
exact_hits = count(user_lmh_vector[i] == type_lmh_vector[i])  for i = 0..14
similarity = max(0, round(100 - distance))
```

- `user_raw[i]`: The 0-100 raw score from conversation analysis
- `centroid[i]`: The type's centroid value from the centroid table (0-100)
- `exact_hits`: Computed using L/M/H vectors (from Step 1) as a tiebreaker
- **Typical similarity**: 80-95% for good matches, 60-75% for moderate, <60% for poor

> **Why Euclidean on raw scores?** The L/M/H quantization (Step 1) collapses 0-100 scores into only 3 levels, losing critical information. Types like CTRL and GOGO had L/M/H vectors differing by only 2 dimensions (93% similarity), making them nearly indistinguishable. With raw-score centroids, personality-specific positioning within each L/M/H band creates meaningful separation (e.g., CTRL A2=90 vs GOGO A2=15).

## Step 4: Sort and Select

Sort all 25 standard types by the following priority:
1. `distance` **ascending** (lower is better)
2. `exact_hits` **descending** (more L/M/H matches is better, as tiebreaker)
3. `similarity` **descending** (higher is better)

Rank #1 = primary type, ranks #2-5 = candidate types.

## Step 5: Special Rules

### HHHH Fallback (The Happy Coder)

If the best match has `similarity < 60%` (i.e., average per-dimension deviation > 40 points):
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

The following are the L/M/H pattern and numeric vectors for the 25 original SBTI types. These are used for pattern display and exact_hits tiebreaker calculation (not for primary matching — see centroids below):

```
CTRL    HHH-HMH-MHH-HHH-MHM  [3,3,3,3,2,3,2,3,3,3,3,3,2,3,2]
ATM-er  HHH-HHM-HHH-HMH-MHL  [3,3,3,3,3,2,3,3,3,3,2,3,2,3,1]
Dior-s  MHM-MMH-MHM-HMH-LHL  [2,3,2,2,2,3,2,3,2,3,2,3,1,3,1]
BOSS    HHH-HMH-MMH-HHH-LHL  [3,3,3,3,2,3,2,2,3,3,3,3,1,3,1]
THAN-K  MHM-HMM-HHM-MMH-MHL  [2,3,2,3,2,2,3,3,2,2,2,3,2,3,1]
OH-NO   HHL-LMH-LHH-HHM-LHL  [3,3,1,1,2,3,1,3,3,3,3,2,1,3,1]
GOGO    HHM-HLH-MLH-HHH-MHM  [3,3,2,3,1,3,2,1,3,3,3,3,2,3,2]
SEXY    HMH-HHL-HMM-HMM-HLH  [3,2,3,3,3,1,3,2,2,3,2,2,3,1,3]
LOVE-R  MLH-LHL-HLH-MLM-MLH  [2,1,3,1,3,1,3,1,3,2,1,2,2,1,3]
MUM     MMH-MHL-HMM-LMM-HLL  [2,2,3,2,3,1,3,2,2,1,2,2,3,1,1]
FAKE    HLM-MML-MLM-MLM-HLH  [3,1,2,2,2,1,2,1,2,2,1,2,3,1,3]
OG8K    MMH-MMM-HML-LMM-MML  [2,2,3,2,2,2,3,2,1,1,2,2,2,2,1]
MALO    MLH-MHM-MLH-MLH-LMH  [2,1,3,2,3,2,2,1,3,2,1,3,1,2,3]
JOKE-R  LLH-LHL-MML-LLM-MLM  [1,1,3,1,3,1,2,2,1,1,1,2,2,1,2]
WOC!    HHL-HMH-MMH-HHM-LHH  [3,3,1,3,2,3,2,2,3,3,3,2,1,3,3]
THIN-K  HHL-HHH-MLH-MMM-LHH  [3,3,1,3,3,3,2,1,3,2,2,2,1,3,3]
SHIT    HHL-HLH-LMM-HHH-LHH  [3,3,1,3,1,3,1,2,2,3,3,3,1,3,3]
ZZZZ    MHL-MLH-LML-MML-LHM  [2,3,1,2,1,3,1,2,1,2,2,1,1,3,2]
POOR    HHL-MLH-LMH-HHH-LHL  [3,3,1,2,1,3,1,2,3,3,3,3,1,3,1]
MONK    HHL-LLH-LLM-MML-LHM  [3,3,1,1,1,3,1,1,2,2,2,1,1,3,2]
IMSB    LLM-LMM-LLL-LLL-MLM  [1,1,2,1,2,2,1,1,1,1,1,1,2,1,2]
SOLO    LML-LLH-LHL-LML-LHM  [1,2,1,1,1,3,1,3,1,1,2,1,1,3,2]
FU?K    MLL-LHL-LLM-MLL-HLH  [2,1,1,1,3,1,1,1,2,2,1,1,3,1,3]
DEAD    LLL-LLM-LML-LLL-LHM  [1,1,1,1,1,2,1,2,1,1,1,1,1,3,2]
IMFW    LLH-LML-LML-LLL-MLL  [1,1,3,1,2,1,1,2,1,1,1,1,2,1,1]
```

## 25 Type Centroids (Raw Score Space)

These centroids are used for primary matching via Euclidean distance (Step 3). Each value is in 0-100 and stays within its L/M/H band (L: 5-33, M: 34-66, H: 67-95). Personality-specific positioning within each band maximizes separation between similar types.

```
Type     S1  S2  S3  E1  E2  E3  A1  A2  A3  Ac1 Ac2 Ac3 So1 So2 So3
CTRL     80  80  80  80  60  80  50  90  80  80  80  80  45  80  55
ATM-er   80  80  80  80  85  45  80  80  80  80  50  80  50  80  20
Dior-s   50  80  50  50  50  80  50  85  50  80  55  80  20  80  20
BOSS     80  80  80  80  50  80  50  65  90  80  80  80  15  80  15
THAN-K   50  80  50  80  55  50  80  80  50  50  50  80  50  80  20
OH-NO    80  80  20  20  55  80  20  80  80  80  80  50  20  80  20
GOGO     80  80  50  80  15  80  50  15  80  90  80  90  50  80  50
SEXY     80  50  80  80  85  20  80  55  50  80  50  50  80  20  80
LOVE-R   50  20  80  20  85  20  80  20  80  50  20  50  50  20  80
MUM      50  50  80  50  85  20  80  50  50  20  50  50  80  20  20
FAKE     80  20  50  50  50  20  50  25  50  50  20  50  80  20  80
OG8K     50  50  80  50  50  50  80  50  20  20  50  50  50  50  20
MALO     50  20  80  50  80  50  50  15  80  50  20  80  20  50  80
JOKE-R   20  20  80  20  75  20  45  50  20  20  20  45  50  20  50
WOC!     80  80  20  80  55  80  50  50  80  80  85  60  20  80  80
THIN-K   80  80  20  80  90  80  50  20  80  45  40  40  20  80  80
SHIT     80  80  20  80  25  80  20  50  50  85  80  90  20  80  80
ZZZZ     50  80  20  50  20  80  20  50  20  45  50  20  20  80  50
POOR     80  80  20  50  25  80  20  50  80  80  80  80  20  80  20
MONK     80  80  20  20  20  80  20  20  50  50  50  20  20  80  50
IMSB     20  20  50  20  50  50  20  20  20  20  20  20  50  20  45
SOLO     20  50  20  20  20  80  20  80  20  20  50  20  15  80  45
FU?K     50  20  20  20  80  20  20  15  50  50  20  20  80  20  80
DEAD     20  20  20  20  20  50  20  50  20  15  20  20  20  80  50
IMFW     20  20  80  20  40  20  20  50  20  20  20  20  50  20  15
```

Key centroid separation rationale:
- **CTRL** A2=90 (architect: highest code standards) vs **GOGO** A2=15 (velocity: ships fast, ignores standards)
- **BOSS** So1=15, So3=15 (commanding, blunt) vs **CTRL** So1=45, So3=55 (collaborative)
- **THIN-K** E2=90, Ac2=40 (deep conversations, slow deliberation) vs **WOC!** E2=55, Ac2=85 (moderate engagement, fast instinct)
- **JOKE-R** A1=45, Ac3=45 (humor requires optimism + delivery) vs **IMFW** E2=40, So3=15 (withdrawn ghost)

> When implementing `sbti match <pattern>` with a L/M/H pattern string input, convert to base values (L=20, M=50, H=80) and compute Euclidean distance to centroids. This is less precise than raw-score matching but still better than L/M/H vector matching.

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
