# **Lesson Plan: Lab 2 (Steps 1–4 on Zoo Logs)**

## **1. Overview and Rationale**

- **Context**:  
  - In Lab 1, students explored a simpler zoo scenario (or another small domain). Now, Lab 2 focuses on **zoo event logs** and how to apply Steps 1–4 of the Design Recipe thoroughly.  
  - The **student instructions** emphasize that Steps 5–6 (implementation and refinement) will happen in **Lab 3**, so **no final code** is required this time.  
  - Students receive a **text file** of log lines and a **`parse_logs`** Python function. They can also work in another language, but Python is recommended for convenience.

- **TA Role**:  
  - Guide students through data definitions, method signatures/purpose statements, examples/tests, and skeletons—while **not** letting them jump into final code.  
  - Encourage them to reference the *Chapter 7* templates (Steps 1–4) from the textbook, as indicated in the lab instructions.

- **Main Student Deliverable**:  
  - A short document that contains each step of the design recipe: data definitions, method signatures & purpose, examples & tests, and skeletons/method templates for the assigned tasks.

## **2. Lab Learning Objectives**

By the end of Lab 2, students should be able to:

1. **Identify** how each log entry is structured from the `parse_logs` output (list of lists).
2. Write **formal data definitions** for a single log entry (and the entire `logs` data).
3. Create **clear method signatures and purpose statements** for the five (or more) tasks listed:
   - **Count Escapes**  
   - **Gather Feeding Times**  
   - **Earliest Escape Time**  
   - **Count Animal Events**  
   - **List Animals for an Event**  
   - *(Plus the “bulk update” and “add new event” scenarios as additional tasks.)*
4. Provide **examples & tests** for each function, including typical and edge cases.
5. Draft a **method skeleton** (pseudocode or commented outlines) for each function, so they’re ready to implement in Lab 3.

## **3. Suggested Flow (75 minutes)**

Below is a recommended structure. Adapt time as needed.

### **(5 min) Introduce the Lab**

- **Remind** students:  
  - This lab covers *only* Steps 1–4. They’ll implement in Lab 3.  
  - They have **two new tasks** beyond the basic five (the “bulk update in a single statement” and “adding a new log entry”)—they should at least create skeletons or docstrings for those too.  
- **Check** if everyone has the text file and the `parse_logs` function. Encourage them to briefly run `parse_logs` or read its output to see the structure.

### **(10 min) Step 1: Data Definitions**

- Have students **examine** how `parse_logs` organizes each line (should be `["10", "Lion", "feeding"]` or similar as a list of strings, or possibly with integer conversion for the time).
- They **write** a short statement: “A single log entry is a list `[time_since_open, animal_name, event_type]`, where….”
- **Encourage** them to note constraints:
  - `time_since_open` is an integer ≥ 0 (if it’s actually converted to int),  
  - `animal_name` non-empty,  
  - `event_type` might be one of `"feeding"`, `"escape"`, etc.—or any string.
- **Pitfalls** to watch for:  
  - Some might skip specifying that `time_since_open` is an integer or might omit data constraints altogether.

### **(15 min) Step 2: Method Signatures & Purpose Statements**

- Students read the lab instructions and see the **five core tasks** + optional tasks (bulk update, adding new event).
- For each task:  
  1. **Signature** (e.g., `def count_escapes(logs: list[list]) -> int:`)  
  2. **Purpose Statement** explaining what the function does and any assumptions (e.g., “Returns the number of logs where event_type == 'escape'. If none, returns 0.”)  
- **TA Tip**:
  - Ask them how the “bulk update” or “add new event” might be structured. Possibly it’s `def add_event(logs, time, animal, event)` returning an updated list.
  - Emphasize clarity—**no** final code yet, but do specify parameter types, return types, and edge cases.

### **(15 min) Step 3: Examples & Tests**

- Students create:
  - A small example `logs` list, e.g. `[["10","Lion","feeding"], ["20","Elephant","escape"], ...]`.
  - For each function, they show **expected output**. E.g.,
    - `count_escapes(logs) == 1`  
    - `list_animals_for_event(logs, "feeding") == ["Lion", "Penguin", ...]`  
  - Edge cases:
    - Empty logs → `count_escapes` = 0, etc.
    - No “escape” → earliest escape time is `None` (or a sentinel).
- **Encourage** them to show these as bullet points or pseudo-assert statements.
- **Possible Pitfall**: Some might only do a single example. Encourage at least one normal example *and* one edge case per task.

### **(15 min) Step 4: Skeleton / Method Templates**

- Students outline each function’s logic in pseudocode or commented placeholders.
  - For instance:

    ```python
    def earliest_escape_time(logs):
        # 1. Track a variable for earliest_time, init to None
        # 2. Loop over each log
        #    - if event_type == "escape"...
        # 3. Return earliest_time
    ```

- **Remind** them not to fill in final code—**Lab 3** is for actual coding.
- They should do this for the “bulk update” approach and the “add new event” approach as well.
- **TA Tip**: If a student starts writing full code, gently redirect them to keep it skeleton-level.

### **(10 min) Peer Review & Q&A**

- Encourage pairs/groups to **swap designs** or read each other’s docstrings.
- **Potential discussion points**:
  - “Does your data definition match what you actually see from `parse_logs`?”  
  - “Are your purpose statements too vague or do they specify input and output clearly?”  
  - “Do your example tests consider at least one tricky scenario?”

- **Wrap Up**:
  - Remind them that all final code is for Lab 3, where they’ll do Step 5 (implementation) and Step 6 (refinement).
  - Suggest that they keep their write-ups: they’ll need them next week to avoid redoing design steps.

## **4. TA Guidance and Socratic Questions**

1. **Check data definitions**:
   - “Did you verify that your function `parse_logs` might store the time as a string or integer? Are you sure which it is?”  
   - “If time is stored as a string, do you want to note that in your data definition?”

2. **Push for complete signatures**:
   - “What happens if the logs are empty? Does your method specify that it returns 0, an empty list, etc.?”  
   - “Are you consistent about returning the same type (e.g., always an `int` or sometimes `None`)?”

3. **Encourage thorough examples**:
   - “What if there are no `escape` events? You said earliest time is `None`—did you add that scenario to your examples?”

4. **Steer them away from final code**:
   - If students jump to writing loops, remind them: “Implementation is Lab 3. For now, just outline the steps.”

## **5. Potential Pitfalls to Watch For**

1. **Mismatch with `parse_logs`**:
   - Students might guess the log structure incorrectly. Prompt them to actually run the function or read its docstring.
2. **Not addressing the new tasks**:
   - They may ignore the “bulk update” or “add new event.” Remind them those tasks also need Steps 1–4, even if simpler or more open-ended.
3. **Under-specifying method signatures**:
   - Some might write “`def count_escapes(logs)`” with no return type or docstring. Nudge them for more detail.
4. **Time Overrun**:
   - They might get stuck on data definition or writing too many examples. Gently move them along to skeletons so each step is at least attempted.

## **6. Expected Outputs**

By the end of the lab, each student (or group) should produce:

- **Data Definition**: A concise statement of how a single log entry is shaped. Possibly mention how the time field is stored (int vs. string).
- **Method Signatures & Purpose**: For all tasks (A–E + optional ones), a short docstring or purpose snippet.
- **Examples & Tests**: At least one typical example and one edge case per function.
- **Skeletons**: Clear, commented outlines for each function, including handling of edge cases.

## **7. Wrap-Up & Next Steps**

- **Preview Lab 3**:  
  - Students will implement the skeletons, see duplication, and refine the code.
  - Emphasize how thorough design now pays off next time—less confusion and faster coding.

- **Encourage** students to keep final versions of their Step 1–4 documents in an accessible place. They’ll iterate on them in Lab 3.
