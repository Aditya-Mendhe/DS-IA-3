# Trace-Match Report

**Student:** Aditya Avinash Mendhe
**PRN:** 202501100058
**Subject:** Data Structures
**Project:** Internal Activity 3 – Question 2

## Configuration

- Scenario: Mango Varieties
- Personalization seed: `S = 58`
- Dataset formula: `v[i] = (S + 13*i) % 100`, for `i = 0..19`
- Table size: 29, retained from the existing project; no assignment PDF was
  present in the workspace
- Hash function: `h(key) = key % 29`
- Collision resolution: linear probing, wrapping from index 28 to index 0
- Dataset: `58, 71, 84, 97, 10, 23, 36, 49, 62, 75, 88, 1, 14, 27, 40, 53, 66, 79, 92, 5`

## Independent hand prediction

Starting with 29 empty slots, each key was placed at its remainder modulo 29;
when that slot was occupied, the next slots were checked in order. The
collisions move `10` from 10 to 11, `1` from 1 to 2, `40` from 11 to 12, and
`5` from 5 to 6. This independent trace predicts:

| Index | Expected value | Index | Expected value | Index | Expected value |
|---:|:---|---:|:---|---:|:---|
| 0 | 58 | 10 | 97 | 20 | 49 |
| 1 | 88 | 11 | 10 | 21 | 79 |
| 2 | 1 | 12 | 40 | 22 | Empty |
| 3 | Empty | 13 | 71 | 23 | 23 |
| 4 | 62 | 14 | 14 | 24 | 53 |
| 5 | 92 | 15 | Empty | 25 | Empty |
| 6 | 5 | 16 | Empty | 26 | 84 |
| 7 | 36 | 17 | 75 | 27 | 27 |
| 8 | 66 | 18 | Empty | 28 | Empty |
| 9 | Empty | 19 | Empty |  |  |

Expected counts: 20 inserted keys, 4 collisions, 20 occupied positions, 9 empty
positions, and load factor `20 / 29 = 0.689655...`, displayed to four decimal
places as `0.6897`.

## Actual program output

Captured by compiling and running `IA3_Q2.cpp` with the required C++17 warning
flags. Whitespace in the code block is normalized for readability (the dataset
line's trailing space and the table's tab separators are omitted):

```text
DATA STRUCTURES IA 3 - QUESTION 2
Student: Aditya Avinash Mendhe
PRN: 202501100058
Scenario: Mango Varieties
Personalization: v[i] = (58 + 13*i) % 100
Hash Function: h(key) = key % 29
Collision Handling: Linear Probing
Table Size: 29

Personalized Dataset:
58 71 84 97 10 23 36 49 62 75 88 1 14 27 40 53 66 79 92 5

========== INSERTION PROCESS ==========
Inserting 58 | Hash index = 0 | Inserted at index 0
Inserting 71 | Hash index = 13 | Inserted at index 13
Inserting 84 | Hash index = 26 | Inserted at index 26
Inserting 97 | Hash index = 10 | Inserted at index 10
Inserting 10 | Hash index = 10 | Collision at index 10 | Inserted at index 11
Inserting 23 | Hash index = 23 | Inserted at index 23
Inserting 36 | Hash index = 7 | Inserted at index 7
Inserting 49 | Hash index = 20 | Inserted at index 20
Inserting 62 | Hash index = 4 | Inserted at index 4
Inserting 75 | Hash index = 17 | Inserted at index 17
Inserting 88 | Hash index = 1 | Inserted at index 1
Inserting 1 | Hash index = 1 | Collision at index 1 | Inserted at index 2
Inserting 14 | Hash index = 14 | Inserted at index 14
Inserting 27 | Hash index = 27 | Inserted at index 27
Inserting 40 | Hash index = 11 | Collision at index 11 | Inserted at index 12
Inserting 53 | Hash index = 24 | Inserted at index 24
Inserting 66 | Hash index = 8 | Inserted at index 8
Inserting 79 | Hash index = 21 | Inserted at index 21
Inserting 92 | Hash index = 5 | Inserted at index 5
Inserting 5 | Hash index = 5 | Collision at index 5 | Inserted at index 6

========== DUPLICATE KEY TEST ==========
Duplicate key 58 ignored.

========== INVALID KEY TEST ==========
Invalid key -10. Negative values are not allowed.

========== INSERTION SUMMARY ==========
Total input values: 20
Successfully inserted: 20
Total collisions: 4
Occupied positions: 20
Empty positions: 9
Load factor: 0.6897

========== FINAL HASH TABLE ==========
Index   Value
0       58
1       88
2       1
3       Empty
4       62
5       92
6       5
7       36
8       66
9       Empty
10      97
11      10
12      40
13      71
14      14
15      Empty
16      Empty
17      75
18      Empty
19      Empty
20      49
21      79
22      Empty
23      23
24      53
25      Empty
26      84
27      27
28      Empty
```

## Match and collision analysis

The actual output matches the hand-predicted value at every index from 0
through 28. All 20 dataset keys were inserted. The four collisions are exactly
the occupied initial slots encountered when inserting `10`, `1`, `40`, and `5`.
The duplicate test and negative-key test are rejected before probing and do not
change the occupied-slot or collision counts.

| Measure | Expected | Actual | Match |
|:---|---:|---:|:---:|
| Input values | 20 | 20 | Yes |
| Successfully inserted | 20 | 20 | Yes |
| Collisions | 4 | 4 | Yes |
| Occupied positions | 20 | 20 | Yes |
| Empty positions | 9 | 9 | Yes |
| Load factor | 0.6897 | 0.6897 | Yes |

There were no mismatches to explain.
