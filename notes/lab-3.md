# Lab 3: Zoo Logs (Design Recipe Steps 5 & 6)

## Introduction

In **Lab 2**, you produced Steps 1–4 for the Zoo Logs scenario, outlining data definitions, writing method signatures, drafting examples/tests, and creating skeletons. Now, in **Lab 3**, you'll turn those plans into fully working code (Step 5: Implementation & Testing) and polish them for clarity (Step 6: Refinement).

> **Note**: The examples below use a **generic list-of-integers** scenario to demonstrate Python's `assert` and the refinement process. You should apply the **same** techniques to your **zoo logs** tasks — but without giving away an actual solution to those tasks.

## Part 0: Preliminaries

### Required Materials

1. **Python Focus**
    - Although you may have used any language for Lab 2, this lab demonstrates testing in **Python** specifically
    - We encourage switching to Python if you haven't already
    - If you still prefer another language, ensure you have a comparable system for writing and running tests

2. **Two Files to Submit**
    - You will submit:
        1. `step-5.py` — your code **after Step 5** (initial implementation and testing)
        2. `step-6.py` — your **refined** code after you remove duplication or apply any improvements (Step 6)

3. **Revisit Lab 2 Plans**
    - Keep your Lab 2 deliverables (Steps 1–4) nearby
    - They're your roadmap for writing code that aligns with your earlier data definitions, signatures, and test examples
    - We won't give away code for your zoo tasks here—just show how to apply **assert** and refinement in a simpler example

## Quick Primer on Testing with `assert` in Python

Python's built-in `assert` statement helps check if something is true. If the expression after `assert` is false, Python raises an `AssertionError` and stops the program.

### Example (Generic "Sum of Integers")

Below is **not** part of the zoo logs scenario—just a **generic** demonstration:

```python
def sum_of_integers(numbers):
    """Return the sum of a list of integers."""
    total = 0
    for n in numbers:
        total += n
    return total

def test_sum_of_integers():
    # Typical usage
    data = [1, 2, 3]
    result = sum_of_integers(data)
    assert result == 6, f"Expected 6, but got {result}"

    # Edge case: empty list
    data2 = []
    result2 = sum_of_integers(data2)
    assert result2 == 0, f"Expected 0, but got {result2}"

def main():
    test_sum_of_integers()
    print("All sample tests passed!")

if __name__ == "__main__":
    main()
```

### Key Testing Points

- We create sample data in `test_sum_of_integers`
- Call `sum_of_integers(data)`
- Use `assert` to check if the result matches the expectation
- If assert fails, Python shows an AssertionError indicating which check was false
- If all asserts pass, we see "All sample tests passed!"

> **Tip**: Always add a short error message after assert, so if it fails, you know which test broke and why.

## Step 5: Implementation & Testing

### 5.1 Convert Skeleton to Real Code

1. Open a new file named `step-5.py`
2. Copy your Lab 2 skeletons for the zoo logs tasks
3. Replace pseudocode with actual Python logic, just like the generic example above

For instance, if your skeleton says:

```python
def count_escapes(logs):
    # 1. Validate input
    # 2. Loop over entries, checking if event == "escape"
    # 3. Return a count
```

...now fill it in with real code.

### 5.2 Create Tests with assert

Use your Step 3 examples from Lab 2 to form real test functions. Here's how you might structure them, analogous to our "sum_of_integers" example:

```python
def test_count_escapes():
    # typical usage with several logs
    logs = [
        # ...
    ]
    result = count_escapes(logs)
    assert result == 2, f"Expected 2, got {result}"

    # edge case: empty logs or logs with no "escape" events
    logs2 = []
    result2 = count_escapes(logs2)
    assert result2 == 0, f"Expected 0, got {result2}"

def main():
    test_count_escapes()
    # test_gather_feeding_times()
    # test_earliest_escape()
    # etc.
    print("All tests in step-5.py passed successfully!")
```

Run `python step-5.py`. If any assert fails, Python will tell you which condition was false so you can debug your logic or the test.

### 5.3 Submit or Save Step 5

At this point, `step-5.py` should contain:
- Full implementations of your zoo logs functions
- Basic test functions checking each one with at least one typical and one edge case

If everything passes, you have a working first draft. If you discover extra edge cases, note them for refinement.

## Step 6: Refinement

Refinement is about making your code "better" (e.g., removing duplication, improving naming) without changing its essential behavior.

### 6.1 Example of Refinement (Generic Case)

Here's a generic sample refinement on our sum-of-integers code. Suppose we see duplication in how we iterate over the list. We might introduce a helper:

```python
def sum_of_integers_helper(numbers, index):
    """Recursively sum the list starting at the given index."""
    if index >= len(numbers):
        return 0
    return numbers[index] + sum_of_integers_helper(numbers, index + 1)

def sum_of_integers_refined(numbers):
    """Refined approach that delegates to a helper function."""
    return sum_of_integers_helper(numbers, 0)
```

We haven't changed the outcome—just the implementation style. The same `test_sum_of_integers()` from before should still pass.

### 6.2 Final Implementation in step-6.py

For your zoo logs, open a new file `step-6.py`:
- Copy (or refactor) your code from `step-5.py`
- Factor out loops or repeated logic if needed (e.g., `filter_logs_by_event(logs, event)`)
- Keep or update your tests. They must still pass if you haven't changed the function's promises.

### 6.3 Document Changes

Add inline comments about why you refined things:

```python
# step-6.py

# We added filter_logs_by_event(...) to reduce duplicate loops
def filter_logs_by_event(logs, event_type):
    ...
```

Then rerun your tests. If they all succeed, you have your refined final code.

## Deliverables

1. `step-5.py`
    - Your initial zoo logs implementation (Step 5) with working code and assert-based tests
2. `step-6.py`
    - Your refined code (Step 6), addressing duplication or design improvements
    - The same tests (or new ones) should still pass

## Submission Instructions

1. Upload `step-5.py` and `step-6.py` to Gradescope (or as directed by your instructor)
2. Check that all assert statements pass before submission
3. Include any optional notes or instructions if your instructor asked for them

## Wrap-Up

Congratulations on completing the full Design Recipe:
1. Understand & Restate
2. Data Definitions
3. Signatures & Purpose
4. Examples & Tests
5. Implementation & Testing
6. Refinement & Reflection

We hope the generic examples here clarify how to use Python's assert and how to refactor code. Apply these principles to your zoo logs tasks and submit your final solutions in `step-5.py` and `step-6.py`. Good luck!

