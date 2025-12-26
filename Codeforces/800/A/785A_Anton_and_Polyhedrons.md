# A_Anton_and_Polyhedrons

## Platform

Codeforces

## Problem Link

[A. Anton and Polyhedrons](https://codeforces.com/problemset/problem/785/A)

## Problem Statement

Anton has several polyhedrons. Each polyhedron has a fixed number of faces depending on its type.

The possible polyhedrons and their number of faces are:

* **Tetrahedron** — 4 faces
* **Cube** — 6 faces
* **Octahedron** — 8 faces
* **Dodecahedron** — 12 faces
* **Icosahedron** — 20 faces

You are given the names of `n` polyhedrons.
Your task is to determine the **total number of faces** among all the given polyhedrons.

## Input Format

* The first line contains an integer `n` — the number of polyhedrons
* The next `n` lines each contain a string representing the name of a polyhedron

## Output Format

* Print a single integer — the total number of faces

## Constraints

* `1 ≤ n ≤ 200`
* Each polyhedron name is one of the five valid types listed above

## Examples

### Example 1

Input

```
3
Tetrahedron
Cube
Icosahedron
```

Explanation

```
Tetrahedron  → 4 faces
Cube         → 6 faces
Icosahedron  → 20 faces
```

Total faces

```
4 + 6 + 20 = 30
```

Output

```
30
```

---

### Example 2

Input

```
2
Dodecahedron
Octahedron
```

Explanation

```
Dodecahedron → 12 faces
Octahedron   → 8 faces
```

Total faces

```
20
```

Output

```
20
```

## Approach

**First-character based identification with conditional branching**

## Intuition

Each polyhedron name starts with a **unique uppercase letter**, which makes identification straightforward:

* `T` → Tetrahedron
* `C` → Cube
* `O` → Octahedron
* `D` → Dodecahedron
* `I` → Icosahedron

By checking only the **first character** of each name, the correct number of faces can be added efficiently without performing full string comparisons.

## Algorithm Steps

* Read the integer `n`
* Initialize a variable `sum` to store the total number of faces
* For each polyhedron:

  * Read its name as a string
  * Check the first character of the string
  * Add the corresponding number of faces to `sum`
* Output `sum`

## Visual Walkthrough

### Case 1

Input

```
Tetrahedron
Cube
Octahedron
```

Processing

```
T → +4
C → +6
O → +8
```

Total

```
18
```

---

### Case 2

Input

```
Icosahedron
Icosahedron
```

Processing

```
I → +20
I → +20
```

Total

```
40
```

---

### Case 3

Input

```
Dodecahedron
```

Processing

```
D → +12
```

Total

```
12
```

## Complexity Analysis

### Time Complexity

**O(n)**

Each polyhedron name is processed once using a constant-time check.

### Space Complexity

**O(1)**

Only a few integer and string variables are used.

## Solution Explanation

The solution reads each polyhedron name and determines its type by inspecting the first character.

An `if–else if` chain ensures that exactly one condition matches for each polyhedron, and the corresponding face count is added to the running total.

This approach is simple, efficient, and perfectly suited to the given constraints.

## Full Solution

### C++ Implementation

```cpp
#include <iostream>
using namespace std;

int main() {

    // Number of polyhedrons
    int n, sum = 0;
    cin >> n;

    // Process each polyhedron
    while (n--) {

        // Read polyhedron name
        string s;
        cin >> s;

        // Identify polyhedron by first character
        if (s[0] == 'T')       sum += 4;   // Tetrahedron
        else if (s[0] == 'C')  sum += 6;   // Cube
        else if (s[0] == 'O')  sum += 8;   // Octahedron
        else if (s[0] == 'D')  sum += 12;  // Dodecahedron
        else                   sum += 20;  // Icosahedron
    }

    // Output total number of faces
    cout << sum << endl;

    return 0;
}
```

## Test Cases Analysis

| Polyhedrons              | Total Faces |
| ------------------------ | ----------- |
| Tetrahedron              | 4           |
| Cube, Cube               | 12          |
| Octahedron, Dodecahedron | 20          |
| Icosahedron × 3          | 60          |

## Edge Cases to Consider

* Minimum value of `n`
* All polyhedrons of the same type
* Maximum value of `n`
* Repeated polyhedron names

## Common Test Cases

* Mixed polyhedron types
* Single polyhedron input
* Large number of identical polyhedrons

## Common Mistakes to Avoid

* Using full string comparisons unnecessarily
* Forgetting to handle all five polyhedron types
* Incorrect face count mapping

## Interview Relevance

* Tests string handling and conditional logic
* Evaluates observation-based optimization
* Common beginner-level competitive programming problem

## What This Problem Teaches

* Leveraging constraints to simplify logic
* Efficient mapping using unique identifiers
* Writing clean and readable conditional code

## Key Takeaways

* Small observations can eliminate complex logic
* First-character checks can be powerful when safe
* Simpler solutions are often more reliable

## Problem Difficulty Analysis

This is an **Easy-level** problem.

It focuses on basic string processing and conditional branching, making it ideal for beginners and early interview preparation.