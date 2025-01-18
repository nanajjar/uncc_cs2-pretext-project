# Lab 2: Zoo Logs (Design Recipe Steps 1–4)

## Overview

In this lab, you will practice **Steps 1–4 of the Design Recipe**—Data Definitions, Method Signatures & Purpose Statements, Examples & Tests, and Skeleton / Method Template—on a new zoo-event-logs scenario.

Before beginning, **read Chapter 7** of your textbook. You will reference its final template (in subsubsections `dr-step1-template` through `dr-step4-template`) throughout this exercise.

> **Important**: We are **not** implementing or refining (Steps 5–6) in this lab. That will happen in **Lab 3**, just as in Lab 1 you postponed final coding until you had a solid design.

---

## Part 0: Preliminaries

1. **Programming Language Choice**  
   You may use Python or any other language to complete your design. **Python** is recommended, because we provide a `parse_logs` function (see below). If you prefer a different language, that’s fine—just ensure your final data definitions and skeletons make sense there.

2. **Running Your Code**  
   As in Lab 1, you’re free to use an online compiler or a local environment. For Python, a convenient option is:
   - [https://www.programiz.com/python-programming/online-compiler](https://www.programiz.com/python-programming/online-compiler)

3. **Sample Logs & `parse_logs`**  
   You’ll receive:
   - A plain-text file containing lines such as:

     ```
     10  Lion       feeding
     20  Elephant   escape
     25  Lion       health_check
     30  Penguin    feeding
     ...
     ```

   - A `parse_logs` function in Python that reads that file and returns a data structure (e.g., a list of entries).  
   This function has minimal documentation. You’ll notice a comment in it saying, *“Wouldn’t it be nice to have documentation here?”* This is a nudge to make you think about **data definitions** (Step 1).

   After you run the script, observe how the data is structured. You’ll need that understanding for your design. **We are not** fully explaining `parse_logs` here; you must examine its source and output to figure out exactly how the logs are stored.

---

## The Zoo Logs Scenario

We’ve switched from **listing animals** (Lab 1) to recording **events** that happen in a zoo throughout the day. An “event” might be a feeding, an escape, a health check, or something else. Each line in the logs file has three pieces of data—time, animal, and event—representing when something happened, who it involved, and what occurred.

### Step 0 Example: Restating the Problem

In Lab 1, you tackled a simpler zoo scenario. Now, we’ll **show you** a short example of how to restate a problem (Step 0) before diving into Steps 1–4. We’re doing Step 0 for you here, so you can see how clarity prevents confusion:

1. **In our own words**:  
   We have a text file listing zoo events. Each event has a time (integer, presumably ≥ 0), an animal name (string), and an event type (e.g., feeding, escape, health_check). We want to analyze this log to answer questions such as “How many escapes happened?” or “Which animals were fed?”

2. **Ambiguities**:  
   - We’re not sure which event types might appear. The file could contain any strings.  
   - Times could be any integer (including duplicates).  
   - Animal names might vary in length, but we assume one ‘word’ (no spaces).  
   - The file could be empty, or missing certain events entirely.

3. **Assumptions**:  
   - Each line in the text file has exactly three columns: `<time> <animal> <event>`.  
   - The `parse_logs` function gives us a valid structure we can iterate over without error.

4. **Edge Cases**:  
   - Possibly an empty log file.  
   - No “escape” events at all.  
   - Multiple feedings at the same time.  

This restatement clarifies the data’s shape, possible pitfalls, and we now know **exactly** what we’ll design in Steps 1–4.

---

## Part 1: Solving the Problem (Steps 1–4)

You have **five tasks** for these zoo logs, each similar to Lab 1’s tasks but applied to log entries. **Do not** finalize code! Your job is to produce:

1. **Data Definitions** (Step 1)  
2. **Method Signatures & Purpose Statements** (Step 2)  
3. **Examples & Tests** (Step 3)  
4. **Skeleton / Method Template** (Step 4)

> **All actual coding (Steps 5–6)** comes in Lab 3.  

### Task A: Count Escapes

A staff member needs to know how many “escape” events appear in the logs. Design a function that returns the total number of lines whose event type is `"escape"`.

### Task B: Gather Feeding Times

We want to see all the **times** at which a “feeding” event occurred. Collect those time values in a list (or another structure), so staff can quickly see the schedule of feeding throughout the day.

### Task C: Earliest Escape Time

Find the **smallest time value** among all “escape” events. If the log has no escape events, decide how your function should handle that (e.g., return `None` or `-1`).

### Task D: Count Animal Events

Given the name of an animal, count how many lines involve that animal (regardless of event type). For example, “How many total entries mention `Lion`?”

### Task E: List Animals for an Event

Given an event type, produce a **list of distinct** animals that had that event. For instance, “Which animals had a `feeding` event?” might return `[Lion, Penguin]`.

### Do a Bulk Update in a Single Statement

Just as you did in Lab 1, also plan how you’d do some “bulk update” in one line. Maybe you:

- Mark all events of a certain type with a status like “checkNeeded.”
- Offset or adjust times if the log was recorded incorrectly.

Include this plan in your method skeleton or docstrings (Steps 2–4). You’ll implement it in Lab 3.

### Adding a New Log Entry

Also, as in Lab 1, we’d like to see how you’d **add a new event** mid-script. Maybe at `time=55`, `Elephant` had a `play` event. In your Step 4 skeleton, outline how you’d do that and confirm it’s included.

---

## Deliverables for Lab 2

**Follow the Chapter 7 template** (Steps 1–4) to create a **short document** covering each function:

1. **Step 1: Data Definitions**  
   - How you represent a **single log entry** (what fields exist, constraints).  
   - The structure of your entire `logs` data (e.g., a list of entries).  
   - Any relevant assumptions (“times are ≥ 0,” “strings are non-empty,” etc.).

2. **Step 2: Method Signatures & Purpose**  
   - For **each** of the five tasks (and the optional bulk update/add-new-entry if you handle them as separate methods), write:  
     - A function signature (in Python or your chosen language)  
     - A one- or two-sentence docstring/purpose statement referencing your data definitions  
     - Mention any error conditions or constraints  
   - Keep it short but precise.

3. **Step 3: Examples & Tests**  
   - Provide at least one typical example **and** one edge case for each function.  
   - You can show them as bullet points (“For logs = [...], `count_escapes(logs)` = 2”) or as code-like asserts.  
   - The goal is to confirm you’ve considered normal and tricky scenarios.

4. **Step 4: Skeleton / Method Template**  
   - Outline your approach for each function in pseudocode or heavily commented placeholders.  
   - No final code! Just show how you’ll structure loops, conditionals, or accumulators.  
   - For instance:  

     ```python
     def count_escapes(logs):
         # 1. Initialize a counter to 0
         # 2. Loop over each log entry
         #    - If event == "escape", increment counter
         # 3. Return counter
     ```

   - This helps you ensure every step (like checking empty logs or updating times) is accounted for **before** writing full code.

---

## Submission Instructions

1. **Format**: Compile your responses (Steps 1–4) into a PDF or DOCX file. Label each section clearly:  
   - “Step 1: Data Definitions”  
   - “Step 2: Method Signatures & Purpose Statements”  
   - “Step 3: Examples & Tests”  
   - “Step 4: Skeleton / Method Template”  

2. **Upload**: Submit your file to Gradescope by the due date posted on the course site.

3. **Length & Style**:  
   - Aim for **clarity**: Provide enough detail to show you’ve thought through each step.  
   - There’s no strict page limit, but typically 1–2 pages can suffice if you’re concise.

4. **No Final Code Yet**: Remember, **implementation** (Step 5) and **refinement** (Step 6) come in **Lab 3**. Focus on the **design** here.

---

## Conclusion

By the end of this lab, you’ll have a thorough design for handling zoo-event logs—mirroring the structured approach you used in Lab 1, but now with more variety in the data and tasks.

**In Lab 3**, you’ll finally implement (Step 5) and refine (Step 6) these methods, confirming how much time and confusion you save by designing first.

Feel free to revisit Chapter 7’s subsections (`dr-step1-template`, `dr-step2-template`, etc.) whenever you need examples. Good luck, and enjoy your logical deep-dive into the zoo logs!
