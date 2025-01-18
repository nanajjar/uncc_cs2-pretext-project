# Lab 1

## Overview

Today, we’re going to start from scratch no templates, no guidelines—just a fresh canvas. Which might feel a bit challenging at first. This exercise will help you understand how much easier it can be to write code (i.e., solve a problem computationally) when we have a clear structure and approach. By the end, you’ll see why having systematic methods in your coding toolkit is so important for tackling more complex problems in the future.

## Instructions

### Part 0: Preliminaries

You are free to choose any programming language you are comfortable with to solve the problem. There is no restriction on which language you must use.

You are not required to install or use specific software, frameworks, or tools. This allows you to use tools you are already familiar with or prefer.

The following are "suggested" web-based tools and programming languages. However, they are not mandatory. You can use them as starting points or ignore them altogether if you have an alternative method that achieves the same goal.

- Python - [https://www.programiz.com/python-programming/online-compiler/](https://www.programiz.com/python-programming/online-compiler/)
- C++ - [https://www.programiz.com/cpp-programming/online-compiler/](https://www.programiz.com/cpp-programming/online-compiler/)
- Java - [https://www.programiz.com/java-programming/online-compiler/](https://www.programiz.com/java-programming/online-compiler/)

### Part 1: Solving the Problem

#### 1. Represent the Animals

- You'll have data for a number of animals (potentially up to 100!)
- Each animal should have at least:
  - Some kind of identifying detail (e.g., name or species)
  - Some information about its needs (e.g., daily food requirement in kilograms, or whether it's indoor/outdoor, etc.)
- The exact way you store or manage these animals is up to you.
- You only need enough sample data to show your code works; you don't have to actually type out 100 animals. Start out with 4 or 5 but you should consider what will happen if someone wants to add more animals.

#### 2. Print Animals Needing Special Attention

- Define a condition (rule) for which animals require special attention. For instance:
  - Those needing more than a certain food amount
  - Those that are "dangerous" or "endangered"
  - Anything else that makes sense to you
- Print a short message listing those animals, so a staff member can quickly see them

#### 3. Do a Bulk Update in a Single Statement

- In one line of code (plus any preparation or follow-up prints), apply some universal change to all or some animals
- Example: If there's a new feeding policy, adjust each animal's daily food requirement by a certain factor in one go
- Show before/after information or at least confirm that the update happened

#### 4. Add a New Animal

- Partway through your script, add at least one brand-new animal to your data
- Print a short confirmation message so it's clear the animal is now included

#### 5. (Optional) Extra Challenge: Animals and Their Favorite Trainers

- Add information about animal trainers at your zoo. Each trainer has:
  - A name (like "Sam" or "Harper")
  - A special skill (like "big cats", "aquatic animals", or "birds of prey")
- For each animal in your zoo:
  - Add a field noting what kind of trainer they need (matching the trainer skills)
  - Create a report that shows:
    - Which animals can work with which trainers
    - Any animals that don't have a matching trainer's skill
    - Any trainers who don't have any matching animals

For example, if Sam specializes in "big cats" and you have three lions but no trainer for your penguins, your report might show:
