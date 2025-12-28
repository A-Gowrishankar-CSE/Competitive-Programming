# A_Police_Recruits

## Platform

Codeforces

## Problem Link

[A. Police Recruits](https://codeforces.com/problemset/problem/427/A)

## Problem Statement

The police department is trying to handle crime events in a city.

You are given a sequence of `n` events:

* A **positive integer** represents the recruitment of that many police officers
* `-1` represents a crime that requires **one police officer** to handle

If there are **no available police officers** when a crime occurs, the crime goes **untreated**.

Your task is to determine how many crimes remain **untreated** after all events are processed.

## Input Format

* The first line contains an integer `n` — the number of events
* The second line contains `n` integers representing the events

## Output Format

* Print a single integer — the number of untreated crimes

## Constraints

* `1 ≤ n ≤ 10⁵`
* Event values are either `-1` or a positive integer

## Examples

### Example 1

Input

```
3
-1 -1 1
```

Explanation

```
Event 1: Crime, no police → untreated (1)
Event 2: Crime, no police → untreated (2)
Event 3: Recruit 1 police
```

Output

```
2
```

---

### Example 2

Input

```
5
3 -1 -1 -1 -1
```

Explanation

```
Police recruited: 3
Crime handled: 1
Crime handled: 1
Crime handled: 1
Crime untreated: 1
```

Output

```
1
```

---

### Example 3

Input

```
4
1 -1 -1 -1
```

Explanation

```
Police recruited: 1
Crime handled: 1
Crime untreated: 2
```

Output

```
2
```

## Approach

**Simulation with counters**

## Intuition

At any moment, the department has a certain number of available police officers.

* When a crime (`-1`) occurs:

  * If police are available, one officer handles it
  * Otherwise, the crime is counted as untreated
* When recruitment occurs, the police count increases

By simulating events in order, we can directly compute the number of untreated crimes.

## Algorithm Steps

* Read the number of events `n`
* Initialize:

  * `police = 0` to track available officers
  * `count = 0` to track untreated crimes
* For each event:

  * If event is `-1`:

    * If `police > 0`, decrement `police`
    * Otherwise, increment `count`
  * Else:

    * Add event value to `police`
* Output `count`

## Visual Walkthrough

### Case 1

Events

```
-1 -1 1
```

Processing

```
Crime → no police → untreated (1)
Crime → no police → untreated (2)
Recruit → police = 1
```

Result

```
2
```

---

### Case 2

Events

```
2 -1 -1 -1
```

Processing

```
Recruit → police = 2
Crime → police = 1
Crime → police = 0
Crime → untreated (1)
```

Result

```
1
```

## Complexity Analysis

### Time Complexity

**O(n)**

Each event is processed exactly once.

### Space Complexity

**O(1)**

Only constant extra variables are used.

## Solution Explanation

The solution maintains a running count of available police officers and untreated crimes.

Each crime event consumes one officer if available; otherwise, it increments the untreated count.

This direct simulation accurately models the problem scenario and adheres to the input order constraint.

## Full Solution

### C++ Implementation

```cpp
#include <iostream>
using namespace std;

int main() {

    int n, police = 0, count = 0;
    cin >> n;

    while (n--) {

        int event;
        cin >> event;

        if (event == -1) {
            if (police > 0)
                police--;
            else
                count++;
        } else {
            police += event;
        }
    }

    cout << count << '\n';
    return 0;
}
```

## Test Cases Analysis

| Events        | Untreated Crimes |
| ------------- | ---------------- |
| -1 -1 1       | 2                |
| 3 -1 -1 -1 -1 | 1                |
| 1 -1 -1 -1    | 2                |
| 5 -1 -1       | 0                |

## Edge Cases to Consider

* All events are crimes
* All events are recruitments
* Crimes occurring before any recruitment
* Large input size

## Common Mistakes to Avoid

* Allowing police count to go negative
* Forgetting to count untreated crimes
* Processing events out of order

## Interview Relevance

* Tests simulation skills
* Evaluates state management
* Common real-world modeling problem

## What This Problem Teaches

* Sequential event processing
* State tracking using counters
* Handling resource constraints

## Key Takeaways

* Simulation is often the simplest correct approach
* Always maintain valid state boundaries
* Order of events is critical

## Problem Difficulty Analysis

This is an **Easy-level** problem.

It focuses on basic simulation and conditional logic, making it ideal for beginners and foundational competitive programming practice.