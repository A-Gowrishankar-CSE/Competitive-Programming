# A_Team_Olympiad

## Platform

Codeforces

## Problem Link

[A. Team Olympiad](https://codeforces.com/problemset/problem/490/A)

## Problem Statement

You are given `n` students, each having a specific skill type:

* Skill `1` — Programming
* Skill `2` — Mathematics
* Skill `3` — Physical Education

Your task is to form as many **teams of three students** as possible such that:

* Each team contains **exactly one student from each skill type**

You must output the maximum number of such teams and the indices of students forming each team.

## Input Format

* The first line contains an integer `n`, the number of students.
* The second line contains `n` integers, where each integer represents the skill type of the corresponding student.

## Output Format

* First line: the maximum number of teams that can be formed.
* Next lines: each line contains three integers — the indices of students in one team.

## Constraints

* `1 ≤ n ≤ 5000`
* Skill values are only `1`, `2`, or `3`

## Examples

### Example 1

Input

```
7
1 3 1 3 2 1 2
```

Explanation

* Students with skill 1: indices `[1, 3, 6]`
* Students with skill 2: indices `[5, 7]`
* Students with skill 3: indices `[2, 4]`

Minimum count among the three skills is `2`, so two teams can be formed.

Output

```
2
1 5 2
3 7 4
```

### Example 2

Input

```
3
1 2 3
```

Output

```
1
1 2 3
```

## Approach (Algorithm Name / Type)

**Greedy Grouping Using Index Buckets**

This approach groups student indices by skill type and then forms teams greedily.

## Intuition

To form one valid team, you need:

* One student with skill `1`
* One student with skill `2`
* One student with skill `3`

Therefore:

* The maximum number of teams is limited by the **least frequent skill**
* Storing indices allows us to directly output team compositions

## Algorithm Steps

* Read the number of students `n`
* Create three vectors:

  * One for skill `1`
  * One for skill `2`
  * One for skill `3`
* Traverse the input:

  * Push each student's index into the corresponding vector
* Compute:

  * `total = min(size(skill1), size(skill2), size(skill3))`
* Print `total`
* For each team:

  * Output one index from each vector at the same position

## Visual Walkthrough

### Input

```
1 3 1 3 2 1 2
```

### Grouping by Skill

* Skill 1 → `[1, 3, 6]`
* Skill 2 → `[5, 7]`
* Skill 3 → `[2, 4]`

### Team Formation

* Team 1 → `(1, 5, 2)`
* Team 2 → `(3, 7, 4)`

Remaining students cannot form a complete team.

## Complexity Analysis

### Time Complexity

**O(n)**

Each student is processed exactly once.

### Space Complexity

**O(n)**

Additional storage is used to keep student indices.

## Solution Explanation

The solution avoids unnecessary comparisons or permutations.

By grouping students based on their skills and then forming teams using the smallest available group size, it guarantees:

* Maximum number of valid teams
* Correct skill distribution
* Efficient execution

This greedy approach is optimal because no team can be formed without one student from each category.

## Full Solution

### C++ Implementation (Heavily Commented)

```cpp
#include <iostream>
#include <vector>
using namespace std;

int main() {

    // Number of students
    int n;
    cin >> n;

    // Vectors to store indices of students by skill
    vector<int> a, b, c;

    // Read skills and store indices
    for (int i = 0; i < n; i++) {
        int num;
        cin >> num;

        // Skill 1
        if (num == 1) {
            a.push_back(i + 1);
        }
        // Skill 2
        else if (num == 2) {
            b.push_back(i + 1);
        }
        // Skill 3
        else {
            c.push_back(i + 1);
        }
    }

    // Maximum number of teams possible
    int total = min(a.size(), min(b.size(), c.size()));

    // Output number of teams
    cout << total << '\n';

    // Output team compositions
    for (int i = 0; i < total; i++) {
        cout << a[i] << ' ' << b[i] << ' ' << c[i] << '\n';
    }

    return 0;
}
```

## Test Cases Analysis

| Skills Input    | Teams Formed |
| --------------- | ------------ |
| `1 2 3`         | 1            |
| `1 1 2 3`       | 1            |
| `1 3 1 3 2 1 2` | 2            |
| `1 1 1 2 2 3`   | 1            |

## Edge Cases to Consider

* One skill completely missing
* Uneven distribution of skills
* Minimum input size

## Common Test Cases

* Equal number of all skills
* One skill dominating
* Random skill distribution

## Common Mistakes to Avoid

* Forgetting to store indices (not values)
* Trying to form teams without checking minimum count
* Incorrect indexing (1-based vs 0-based)

## Interview Relevance

* Demonstrates greedy strategy
* Tests grouping and counting logic
* Common array and vector manipulation problem

## What This Problem Teaches

* Effective use of data structures
* Greedy problem-solving
* Translating constraints into logic

## Key Takeaways

* Always identify limiting factors
* Grouping simplifies complex constraints
* Greedy solutions can be optimal and simple

## Problem Difficulty Analysis

This is an **Easy-level** problem.

It combines basic data structures with greedy reasoning, making it suitable for beginners and competitive programming practice.