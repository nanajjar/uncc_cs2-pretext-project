# Design Recipe for Java

## 1. Understand and Restate the Problem

- **Goal**: Precisely clarify what needs to be computed or solved.  
- **Activities**:  
  1. Carefully re-read the problem statement.  
  2. Paraphrase it in your own words to ensure understanding.  
  3. Identify inputs, outputs, constraints (e.g., null inputs, special edge cases).  
- **Deliverables**:  
  - A short restatement of the problem’s requirements.  
  - A list of known edge cases or special conditions.  

<details>
<summary>Example Deliverable</summary>

> **Problem Restatement**: We need a method that, given a list of integer temperatures, computes the average temperature. We assume the input list cannot be `null` or empty.  
> **Edge Case**: If the list is empty, we throw `IllegalArgumentException`.  
</details>

---

## 2. Data Definitions and Representations

- **Goal**: Specify which Java types or classes your method (or class) will receive, produce, or manipulate.  
- **Activities**:  
  1. Decide on the appropriate types (e.g., `int`, `String`, `List<String>`, custom classes).  
  2. If the data is complex, define new classes or records (e.g., a `Point` class).  
  3. Document assumptions (e.g., “list will never be empty” or “string can contain any Unicode character”).  
- **Deliverables**:  
  - A concise description of the data structures (including any new classes).  
  - Notes on invariants (e.g., “index must be >= 0”).  

<details>
<summary>Example Deliverable</summary>

> **Data Definition**:  
>
> - Inputs: `List<Integer> temperatures`  
> - Output: `double` representing the average temperature  
> - Invariants: `temperatures` is not `null` or empty  
>
</details>2

---

## 3. Method Signature and Purpose Statement

- **Goal**: Provide a clear contract (signature) and a succinct explanation of what the method does and why.  
- **Activities**:  
  1. Choose the method name and parameter/return types.  
  2. Write a brief purpose statement or Javadoc comment describing intended functionality and constraints.  
  3. Indicate any expected exceptions or error conditions.  
- **Deliverables**:  
  - A well-defined method header and its Javadoc-style documentation.  

<details>
<summary>Example Deliverable</summary>

```java
/**
 * Computes the average of a non-empty list of integer temperatures.
 *
 * @param temperatures a non-null, non-empty list of integer temperatures in Celsius
 * @return the average temperature as a double
 * @throws IllegalArgumentException if the list is null or empty
 */
public static double averageTemp(List<Integer> temperatures) {
    ...
}
```

</details>

---

## 4. Examples and Tests (Before the Implementation)

- **Goal**: Clarify expected behavior by enumerating concrete input-output examples—often the first pass of a test suite.  
- **Activities**:  
  1. Identify typical and edge-case inputs (e.g., empty list, list with one element).  
  2. For each input, specify the expected output (in plain language or code).  
  3. Implement tests (e.g., using JUnit) or at least outline them if you’re not yet coding.  
- **Deliverables**:  
  - A set of input-output pairs as examples.  
  - Automated tests (if using a framework like JUnit).  

<details>
<summary>Example Deliverable</summary>

```java
@Test
public void testAverageTemp_Typical() {
    List<Integer> temps = Arrays.asList(10, 20, 30);
    assertEquals(20.0, averageTemp(temps), 0.001);
}

@Test
public void testAverageTemp_EmptyList() {
    List<Integer> temps = Collections.emptyList();
    assertThrows(IllegalArgumentException.class, () -> averageTemp(temps));
}
```

</details>

---

## 5. Method Template / Skeleton

- **Goal**: Lay out a simple outline of the method, reflecting how you will process the data.  
- **Activities**:  
  1. Translate your data definition into structural steps (e.g., if it’s a list, you might plan a loop).  
  2. Write placeholder comments or pseudocode for each step in the logic.  
  3. Ensure this skeleton matches the assumptions you documented (e.g., handle empty list by throwing an exception).  
- **Deliverables**:  
  - A commented or pseudocode skeleton showing how you’ll implement the solution.  

<details>
<summary>Example Deliverable</summary>

```java
public static double averageTemp(List<Integer> temperatures) {
    // 1. Check for null or empty input -> throw exception
    // 2. Initialize a sum variable
    // 3. Loop through temperatures, accumulate the sum
    // 4. Divide sum by the size of the list
    // 5. Return the result
}
```

</details>

---

## 6. Implementation

- **Goal**: Fill in the skeleton with a correct, readable solution that meets the stated purpose.  
- **Activities**:  
  1. Write the Java code in alignment with the outlined steps.  
  2. Keep things clear and straightforward—avoid unnecessary complexity.  
  3. Use helper methods if needed for readability.  
- **Deliverables**:  
  - A fully functioning method or class that compiles and runs.  
  - Comments explaining non-obvious parts of the code.  

<details>
<summary>Example Deliverable</summary>

```java
public static double averageTemp(List<Integer> temperatures) {
    if (temperatures == null || temperatures.isEmpty()) {
        throw new IllegalArgumentException("List cannot be null or empty.");
    }

    double sum = 0.0;
    for (int t : temperatures) {
        sum += t;
    }

    return sum / temperatures.size();
}
```

</details>

---

## 7. Testing and Refinement

- **Goal**: Confirm correctness and consistency with your initial examples; refine if necessary.  
- **Activities**:  
  1. Run all tests you wrote in Step 4.  
  2. If a test fails, debug and adjust the code or assumptions.  
  3. Possibly add more tests if you discover new cases or clarifications.  
- **Deliverables**:  
  - A passing test suite demonstrating correctness across typical and edge scenarios.  
  - Updates to the code or documentation if your assumptions change.  

<details>
<summary>Example Deliverable</summary>

> **Test Results**: All tests (`testAverageTemp_Typical`, `testAverageTemp_EmptyList`, etc.) have passed.  
> **New Insight**: If the list contains negative numbers, the average could be negative—documented in the Javadoc.
</details>

---

## 8. Reflection and Documentation

- **Goal**: Evaluate the process, ensure maintainability, and note any performance or design considerations.  
- **Activities**:  
  1. Reflect on whether the final method meets the original problem statement.  
  2. Check code for readability, clarity, and compliance with style guidelines.  
  3. Document any lessons learned or remaining open questions (e.g., performance constraints).  
- **Deliverables**:  
  - Updated Javadoc or comments reflecting new insights or constraints.  
  - A brief “lessons learned” or reflection section (especially in a collaborative or educational context).  

<details>
<summary>Example Deliverable</summary>

> **Reflection**:  
>
> - The solution is O(n) with respect to the list size, which is acceptable for typical usage.  
> - If large lists are expected, consider parallelizing or using Java Streams.  
> - The approach is easy to maintain, thanks to concise code and thorough tests.
>
</details>

---

## Final Summary

1. **Understand/Restate the Problem**  
2. **Define the Data (Types/Structures)**  
3. **Write the Method Signature & Purpose Statement**  
4. **Draft Examples & Tests** (before coding)  
5. **Outline a Skeleton/Template**  
6. **Implement the Method**  
7. **Test & Refine**  
8. **Reflect & Document**
