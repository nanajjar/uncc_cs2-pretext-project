# **Lesson Plan: Lab 3 (Zoo Logs, Steps 5 & 6)**

## **1. Overview & Context**

- **Where We Left Off**  
  - In Lab 2, students created Steps 1–4 (data definitions, method signatures & purpose, examples/tests, and skeletons) for the **zoo-event-logs** tasks. They should come to Lab 3 **with** those design artifacts in hand.
- **Today’s Focus (Steps 5 & 6)**  
  - **Step 5**: Implementation & Testing  
    - Students will **convert** their skeleton outlines into actual Python (or another language) code.  
    - They’ll add `assert`-based tests (in Python) to validate each function with typical and edge-case scenarios.  
  - **Step 6**: Refinement  
    - Students will **eliminate duplication** or enhance clarity without changing the functions’ expected behavior.  
    - They’ll update tests if needed but confirm all previous tests still pass.

- **Files**:  
  - Students must produce two versions:
    1. **`step-5.py`**: The initial working code (post-implementation).  
    2. **`step-6.py`**: The refined/improved version, ensuring all tests still pass.

## **2. Learning Objectives**

By the end of this lab, students should be able to:

1. **Translate** a skeleton (Step 4) into fully working functions (Step 5), confirming correctness with `assert` tests.
2. **Apply** the examples/tests from their Lab 2 deliverables to systematically check each function’s behavior.
3. **Identify duplication** (e.g., repeated loops or conditionals across multiple tasks) and **refactor** it into helper functions or simpler logic (Step 6).
4. **Demonstrate** that the same tests pass *before and after* refinement, proving that they haven’t broken core functionality.

## **3. Suggested Flow (75 minutes)**

Below is a recommended **time breakdown** for TAs. Adapt as you see fit.

1. **(5 min) Lab Intro & Recap**  
   - Remind students they should bring their Lab 2 design (Steps 1–4).  
   - Quickly outline the plan: “Implement your functions, write test code, then refine them.”

2. **(10–15 min) Step 5: Starting Implementation**  
   - **Goal**: Have students open a fresh file (e.g., `step-5.py`) and paste in their skeletons from Lab 2.  
   - They fill in actual logic for each function.  
   - **TA Tips**:  
     - Encourage them to follow the structure from their skeleton, not to deviate too far.  
     - If they realize their skeleton missed something, they can revise it, but keep them mindful of time.

3. **(15 min) Step 5: Testing with `assert`**  
   - Students create test functions (like `test_count_escapes()`), referencing the examples from Lab 2.  
   - Each test calls a function with sample data and uses `assert` to confirm the result.  
   - Then they run `python step-5.py` (or analogous) to see if everything passes.  
   - **Encourage** them to add messages to each assert, e.g.:  

     ```python
     assert result == 2, f"Expected 2 but got {result}"
     ```

   - If any test fails, they debug. This clarifies the difference between an actual logic mistake and a flawed test.

4. **(5–10 min) Debugging & Checking Edge Cases**  
   - Some students might pass all tests quickly; others will discover logic issues or incomplete coverage.  
   - TAs can circulate and **remind** them to handle edge cases (e.g., empty logs, no escape events).

5. **(15 min) Step 6: Refinement**  
   - **Goal**: Students look for repeated code or logic. For instance:  
     - Repeated loops that filter by `event_type`.  
     - Repeated checks for `time_since_open`.  
   - They create `step-6.py` by copying their working `step-5.py` code, then factoring out duplication. Examples:  
     - A helper `filter_logs_by_event(logs, event)` to unify repeated loops.  
     - More descriptive variable names or reorganizing if–else statements.  
   - **TA Guidance**:  
     - Emphasize that they should keep the *same tests*. The tests must still pass if the refactoring is correct.  
     - If they discover new edge cases, they can add tests too.

6. **(5–10 min) Final Testing & Wrap-Up**  
   - Students run their test suite again on `step-6.py`.  
   - Confirm everything still passes.  
   - TAs can prompt: “Are there *further* improvements you see? Or is the code good enough for now?”  
   - Encourage them to comment in `step-6.py` about what changed.

## **4. Potential Pitfalls & Issues**

1. **Skipping Tests**  
   - Some students might just write code without systematically checking it. Remind them to test thoroughly, referencing Lab 2 examples.  
2. **Over-Refactoring**  
   - They might attempt overly advanced patterns (like higher-order functions) if it’s not within their comfort. Gently guide them to simpler “helper function” approaches.  
3. **Changing Function Behavior**  
   - Students might accidentally alter the function’s return type or edge-case handling while refactoring. Remind them the original tests must still pass.  
4. **Time Management**  
   - Some might spend all the time debugging Step 5. TAs should nudge them to do a minimal working version, so they have *some* time for Step 6 (even a small refactoring).

## **5. TA Q&A / Socratic Prompts**

- **During Implementation (Step 5)**:
  - “Does your code reflect the logic from your skeleton step by step?”  
  - “Are you handling empty logs or missing event types as you planned in Lab 2?”  
- **During Testing**:
  - “Which examples from Lab 2 are you turning into `assert` calls? Did you include at least one typical scenario and one edge scenario?”  
  - “When a test fails, how do you isolate whether the function or the test is incorrect?”
- **During Refinement (Step 6)**:
  - “Do you see similar loops repeated across multiple functions? Could a helper function or small utility reduce duplication?”  
  - “After you refactor, do your existing tests still pass? If you need new tests, what do they check?”

## **6. Final Deliverables**

By the end of **Lab 3**, each student should have:

1. **`step-5.py`**:  
   - Working code that matches their Lab 2 design (Steps 1–4).  
   - `assert`-based tests for each function (or a single test function that calls them all).
2. **`step-6.py`**:  
   - A refined version removing duplication or clarifying logic.  
   - The same (or enhanced) tests that confirm no regression.

Encourage them to comment or briefly document the changes they made between `step-5.py` and `step-6.py`.

## **7. Wrap-Up**

- **Reinforce the Complete Design Recipe**:  
  - Step 1–4 from Lab 2 gave them stable definitions and tests.  
  - Step 5–6 in Lab 3 results in correct, maintainable, *tested* code.  
- **Future Work**:  
  - The “zoo logs” scenario might inspire further expansions (like storing these logs in a file or adding more event-based analytics). But for now, they should submit `step-5.py` and `step-6.py` as directed.
- **TA’s Final Advice**:  
  - Double-check each function’s docstring or signature remains consistent with Lab 2’s design.  
  - Resist the urge to skip testing or shortchange the refinement step—these are crucial aspects of real-world coding.
