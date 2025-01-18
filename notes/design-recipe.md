# Design Recipe for Java

This structure offers a systematic approach to writing robust, maintainable Java methods. Each step builds on the previous, ensuring you tackle the right problem with clear data definitions, thorough tests, and a well-organized implementation.

Step 0. Understand & Restate the Problem

 1. Purpose: Ensure that you genuinely know what needs to be solved or computed.
 2. Activities:
 • Re-read the problem statement or prompt carefully.
 • Paraphrase it in your own words. Identify inputs, outputs, and any relevant constraints or assumptions.
 • List potential edge cases that might cause confusion, and note any clarifications you might need (e.g., “What if the input is null?”).
 3. Deliverables:
 • A short restatement of the problem’s requirements.
 • A summary of any ambiguous details or special conditions you plan to handle.

<details>
<summary>Example Deliverable</summary>

 Short Restatement:
  • We want a method that, given a list of integer temperatures, computes the average temperature.
 • We will assume the list is never null or empty. If it is, we throw an IllegalArgumentException.
 • The method returns a double representing the computed average.

</details>

Why It Matters:
 • Starting with a clear restatement of the problem ensures everything you do afterwards (data definitions, tests, code) aligns with the actual requirement, rather than an unverified assumption.

Step 1. Data Definitions & Representations

 1. Purpose: Specify which Java types or classes the method will use or produce.
 2. Activities:
 • Decide on appropriate types (e.g., int, String, List<String>, custom classes).
 • If the data is non-trivial, define new classes or records (e.g., a Point class with x and y).
 • Document invariants or constraints (e.g., “Rating must be in [1..5]” or “Title is non-empty”).
 3. Deliverables:
 • A concise description of the data structures.
 • Clear assumptions (e.g., “the list is never null,” “the number of elements is at least one,” etc.).

<details>
<summary>Example Deliverable</summary>

 Data Definition:
  • Inputs: List<Integer> temperatures
 • Output: double (the average temperature)
 • Invariants:
 • The input list is not null.
 • The input list is not empty.

</details>

Why It Matters:
 • Having explicit data definitions prevents hidden assumptions—like forgetting to handle an empty list or incorrectly assuming integer indices will never exceed the list’s size.

Step 2. Method Signature & Purpose Statement

 1. Purpose: Provide a clear contract describing the method’s signature (name, parameters, return type) and intent.
 2. Activities:
 • Choose the method name and precisely define parameter and return types in Java.
 • Write a succinct purpose statement or Javadoc comment explaining what the method is intended to do and under what conditions it operates.
 • Indicate expected exceptions if inputs are invalid or if certain edge cases arise.
 3. Deliverables:
 • A method header (e.g., public static double averageTemp(List<Integer> temps)) and Javadoc explaining input constraints and what is returned.

<details>
<summary>Example Deliverable</summary>

/**

* Computes the average of a non-empty list of integer temperatures.
*
* @param temperatures a non-null, non-empty list of integers
* @return the average temperature as a double
* @throws IllegalArgumentException if the list is null or empty
 */
public static double averageTemp(List<Integer> temperatures) {
    ...
}

</details>

Why It Matters:
 • A clear signature/purpose statement acts as a contract: it tells other developers exactly how to call your method, what results to expect, and what errors might arise.

Step 3. Examples & Tests

 1. Purpose: Pin down the method’s behavior with real examples before (or while) coding. Convert these examples into tests for continuous validation.
 2. Activities:
 • Identify typical inputs, plus edge cases (e.g., empty list, negative numbers).
 • For each, specify the expected outcome.
 • Write your tests using a framework like JUnit or simple assertions in Java.
 3. Deliverables:
 • A set of input-output pairs or usage examples.
 • Automated tests that confirm behavior under normal and edge conditions.

<details>
<summary>Example Deliverable</summary>

@Test
public void testAverageTemp_Typical() {
    List<Integer> temps = Arrays.asList(10, 20, 30);
    assertEquals(20.0, averageTemp(temps), 0.001);
}

@Test
public void testAverageTemp_EmptyList() {
    List<Integer> temps = Collections.emptyList();
    assertThrows(IllegalArgumentException.class,
        () -> averageTemp(temps));
}

</details>

Why It Matters:
 • Turning examples into automated tests locks in your understanding of how the method should behave. You’ll spot mismatches early—before finishing the entire implementation.

Step 4. Skeleton / Method Template

 1. Purpose: Outline the logical flow of the solution without diving into detailed code.
 2. Activities:
 • Translate data definitions and test scenarios into high-level steps (validate input, loop over data, accumulate results, etc.).
 • Use comments or pseudocode to mark each step.
 • Confirm you can see exactly where each test scenario would be addressed in these steps.
 3. Deliverables:
 • A commented skeleton of your method, showing step-by-step logic or placeholders.

<details>
<summary>Example Deliverable</summary>

public static double averageTemp(List<Integer> temperatures) {
    // 1. Validate input (throw exception if null or empty)
    // 2. Initialize a sum
    // 3. Loop through list, accumulate sum
    // 4. Compute sum / size
    // 5. Return result
}

</details>

Why It Matters:
 • Writing an outline first keeps your logic organized. If you realize a step is missing, it’s much easier to fix in a skeleton than in full code riddled with half-finished loops and conditionals.

Step 5. Implementation, Testing & Reflection

In practice, these three sub-steps often happen in a cycle: you fill in part of the code, run tests, fix issues, and reflect on whether the solution meets the original problem statement. Grouping them ensures you see these activities as closely linked.

5.1 Implementation
 • Goal: Write the actual Java code that satisfies the skeleton and data definitions.
 • Activities:

 1. Fill in each skeleton comment with working code.
 2. Keep it simple and readable; avoid unnecessary complexity.
 3. Use helper methods if they clarify the main logic.

5.2 Testing & Refinement
 • Goal: Confirm the code behaves as intended, refine if any test fails.
 • Activities:

 1. Run all examples/tests from Step 3.
 2. If a test fails, debug: did we misunderstand the problem, or is the code incorrect?
 3. Adjust the implementation or test if you discover new insights (e.g., a previously overlooked edge case).
 • Deliverables:
 • A passing test suite (all Step 3 tests now succeed).
 • Potentially new or updated tests if you discovered additional scenarios.

5.3 Reflection
 • Goal: Assess the final solution in terms of performance, maintainability, and alignment with Step 0.
 • Activities:

 1. Check if the final code meets the originally stated requirements.
 2. Note performance constraints or potential optimizations.
 3. Update comments or docstrings to reflect any new assumptions.

<details>
<summary>Example Deliverable</summary>

public static double averageTemp(List<Integer> temperatures) {
    if (temperatures == null || temperatures.isEmpty()) {
        throw new IllegalArgumentException("List cannot be null or empty.");
    }

    double sum = 0.0;
    for (int t : temperatures) {
        sum += t;
    }
    double result = sum / temperatures.size();

    // (Optional) Reflection: time complexity is O(n). 
    // This is acceptable for typical usage. 
    // If we expect extremely large lists, we might consider parallel streams.

    return result;
}

// After implementing, we run our tests:
@Test
public void testAverageTemp() {
    // Reuse or expand the tests we outlined in Step 3.
}

 All tests now pass. We also added a negative-temperatures test to confirm the result is correct if the list has negative integers. Our code handles it fine, so we’re done here.

</details>

Why It Matters:
 • “Implementation, Testing & Reflection” is an iterative loop: you write code, confirm correctness, and reflect. This ensures your solution truly aligns with the original problem.

Summary of All Steps

 1. Step 0: Understand & Restate the Problem
 2. Step 1: Data Definitions & Representations
 3. Step 2: Method Signature & Purpose Statement
 4. Step 3: Examples & Tests
 5. Step 4: Skeleton / Method Template
 6. Step 5: Implementation, Testing & Reflection

Following this sequence offers a repeatable process for building robust Java methods:
 • You begin by clarifying the core problem (Step 0).
 • You define data (Step 1) and the method contract (Step 2).
 • You illustrate expected behavior with examples/tests (Step 3).
 • You sketch a method skeleton (Step 4).
 • Finally, you implement, test, and reflect (Step 5), refining until everything matches the requirements stated in Step 0.

This approach dramatically reduces guesswork, prevents overlooked edge cases, and fosters high-quality code that’s easier to understand, debug, and maintain.
