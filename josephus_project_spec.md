# Personal Project: Josephus Problem

## Overview
In this project, you will implement and analyze multiple approaches to solving the Josephus problem.

Given `n` participants arranged in a circle and a step size `k`, the program eliminates every `k`th participant until only one remains.

This project emphasizes comparing **different algorithmic approaches** to the same problem.

## Implemented Approaches

You will implement **three distinct methods**:

1. **Simulation (Container-Based Iteration)**  
   - Models the elimination process explicitly

2. **Recursive Definition (Top-Down)**  
   - Direct implementation of the mathematical recurrence

3. **Iterative Recurrence (Bottom-Up, Optimized)**  
   - Efficient implementation derived from the recurrence relation

## Learning Goals
By completing this project, you will:

- Model circular behavior using data structures
- Translate recurrence relations into code
- Compare algorithmic approaches and tradeoffs
- Analyze time and space complexity
- Design modular, testable C++ code
- Build a command-line interface with input validation


## Specifications

### Input
Your program will accept command-line arguments:

```
./josephus.exe [n] [k] [simulation|recursion|recurrence] [show|hide]
```

### Required arguments:
- `n`: number of participants (integer ≥ 1)
- `k`: step size (integer ≥ 1)
- Method:
  - `simulation`
  - `recursion`
  - `recurrence`
- Output mode:
  - `show`: print elimination order
  - `hide`: print only survivor

### Output

#### Required output:
- The position (1-indexed) of the survivor

Example:
```
Survivor: 4
```

#### If `show` is specified upon execution:
```
1 eliminates 3
4 eliminates 6
7 eliminates 2
4 eliminates 7
1 eliminates 5
4 eliminates 1

Survivor: 4
```

## Functional Requirements

### 1. Simulation Implementation
Implement a function:

```cpp
int josephus_simulation(int n, int k);
```

Requirements:
- Use a standard container (e.g., `std::vector` or `std::list`)
- Simulate circular elimination using a form of iteration
- Time complexity may be O(n · k) or O(n²)

### 2. Recursion Implementation
Implement a function:

```cpp
int josephus_recursion(int n, int k);
```

Use the recurrence relation:

$$
J(n, k) =
\begin{cases}
0 & n = 1 \\
\big(J(n-1, k) + k\big) \bmod n & n > 1
\end{cases}
$$

Requirements:
- Compute result recursively
  - There is no restriction on recursion style (e.g., linear, tail, etc.)
- Convert from 0-indexed result to 1-indexed output

### 3. Iterative Recurrence Implementation
Implement a function:

```cpp
int josephus_recurrence(int n, int k);
```

- Produces the same result as the recursive function while eliminating call stack overhead

Requirements:
- Compute result using the recurrence relation iteratively
  - Avoids the stack overhead of explicit recursion
  - Maintains O(1) space complexity
- Convert from 0-indexed result to 1-indexed output

### 4. Elimination Order
If `show` is specified:
- Print the order in which participants are eliminated in this manner until the "winner" is determined, followed by a newline:
```
a eliminates b
c eliminates d
...
```
- **Note**: Elimination order is only supported by the simulation method.

### 5. Input Validation
Your program must:
- Reject missing arguments
  - `MissingArgumentException()`
  - Utilize a usage print with expected arguments:
  ```cpp
  std::cout << "Usage: josephus.exe N K [simulation|recursion|recurrence] [show|hide]\n"
            << "N and K must be integers greater than or equal to 1" << std::endl;
  ```
- Reject non-integer input
  - `NonIntegerInputException()`
  - Print the usage message, followed by:
  ```
  Please input an integer for [n|k]
  ```
  - Incorrect argument determines which version of the message is printed
- Reject values < 1
  - `IntegerLessThanOneException()`
  - Print the usage message, followed by:
  ```
  Please input an integer for [n|k] such that [n|k] >= 1
  ```
- Exit the program upon errors

## Design Requirements

### Modularity
Organize your code into multiple files:
```
josephus.cpp       // main + CLI handling
josephus.hpp       // function declarations
simulation.cpp     // simulation implementation
simulation.hpp     // simulation interface
recursion.cpp      // recursion implementation
recursion.hpp      // recursion interface
recurrence.cpp     // iterative recurrence implementation 
recurrence.hpp     // iterative recurrence interface
```
### Style
- Follow consistent naming conventions
- Avoid global variables
- Use meaningful variable names
- Keep functions small and focused

## Testing Requirements

Create a test file (or separate executable) that:
- Verifies correctness for small inputs
- Tests edge cases:
  - n = 1
  - k = 1
  - k = 2 (Bitwise pattern)
  - n = k
- Cross-validates all implementations:
  - simulation vs recursion vs iterative recurrence methods
- (Recommended) Randomized testing to verify consistency across methods  

Example test:
n = 7, k = 3 → survivor = 4

## Performance Expectations

- Simulation should work for n up to ~10<sup>4</sup>
- Explicit recursion is limited by stack depth and intended for smaller inputs (typically ≤ 10<sup>5</sup>, but may be lower depending on system limits)
- Iterative recurrence should support n up to ~10<sup>7</sup>+

## Extra Credit (Optional)

### EC1: Circular Linked List
- Implement simulation using a custom circular linked list

### EC2: Benchmarking
- Measure runtime of both methods for increasing n
- Output timing results

### EC3: Step-by-Step Mode
- Print state of circle after each elimination

### EC4: Generalized Output
- Support 0-indexed or 1-indexed output via flag

### EC5: Special Case Testing
- For k = 2, use the known bitwise pattern:
  - Move the most significant bit of n (in binary) to the least significant position (cyclic shift)
  - This directly yields the survivor position

## Example Runs

### Example 1:

```
$ ./josephus.exe 7 3 simulation hide
```

#### Expected Output:

```
Survivor: 4
```
### Example 2:

```
$ ./josephus.exe 7 3 simulation show
```
#### Expected Output:
```
1 eliminates 3
4 eliminates 6
7 eliminates 2
4 eliminates 7
1 eliminates 5
4 eliminates 1

Survivor: 4
```

### Example 3:

```
$ ./josephus.exe 5 2 recursion hide
```
#### Expected Output:
```
Survivor: 3
```

## Submission Guidelines (GitHub Version)

Your repository should include:
- Source code
- A README.md with:
  - Description of the problem
  - Build/run instructions
  - Example usage
- (Optional) performance discussion

## Final Note
This project is designed to emphasize:
- Clean structure
- Clear logic
- Thoughtful implementation

Focus on writing code that is readable, modular, and correct.
