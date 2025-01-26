# Lesson Plan: Lab 4 – Getting Started with VS Code, Java, and Gradle

## 1. Overview and Rationale

### Context
- Students previously used simpler coding environments (online editors or minimal text editors).
- We now want them to install a **professional** environment for more complex Java projects with Gradle.

### Purpose
- Guide students through:
  - **Installing** the Java Coding Pack (or equivalent JDK + VS Code setup)
  - **Opening** a Gradle-based "Hello World" project
  - **Running** the project
  - **Experimenting** with key IDE features (IntelliSense, error underlines, quick fixes)
- Practice **Chapter 2** topics in a "real" IDE environment

### TA/Instructor Role
- Help **troubleshoot** installation issues (permissions, missing JDK, etc.)
- Demonstrate:
  - Opening a **terminal**
  - Running `gradlew run`
  - Interpreting IntelliSense suggestions
  - Understanding red squiggles for errors
- Encourage reflection on IDE benefits
- Ensure students produce a short reflection and screenshot as proof of completion

### End Goal
Students should be able to:
- Open a Java/Gradle project in VS Code
- Run code with `gradlew`
- View output in the integrated terminal
- Feel confident about their environment for upcoming labs

## 2. Lab Learning Objectives

After this lab, students should be able to:

1. **Install** the Java environment (Coding Pack or manual setup: JDK + VS Code + Java extensions)
2. **Open** a Gradle-based Java project in VS Code and recognize these files:
   - `build.gradle.kts`, `gradlew` scripts
   - `src/Main.java` where their code lives
3. **Run** their "Hello World" code in two ways:
   - Using the terminal with the Gradle wrapper (`.\gradlew.bat run` on Windows or `./gradlew run` on Mac/Linux)
   - (Optionally) by clicking the "Run" code lens in the editor
4. **Identify core IDE aids**:
   - IntelliSense (auto-completion for Java)
   - Red "squiggles" for compile errors
   - The Problems panel and possible Quick Fix suggestions
5. **Edit** the Java code to add a second print statement and a variable (from Chapter 2)
6. **Reflect** on their experience (Gradle usage, IntelliSense benefits, error squiggles utility, etc.), providing a screenshot of the final output

## 3. Suggested Flow (Approx. 75 minutes)

1. **(10 min) Intro & Installation Check**
   - Explain lab purpose: "We want a consistent environment—VS Code, JDK, Gradle—to make future labs smoother."
   - Verify Coding Pack for Java installation (or JDK 17 + VS Code setup)
   - TA Help: Assist with installation issues, pair up students if needed

2. **(15 min) Explore the Project Structure**
   - Unzip/Distribute the `hello-world-gradle` folder
   - Students: VS Code → File → Open Folder → choose `hello-world-gradle`
   - Wait for Java extension initialization
   - Discuss folder contents:
     - Gradle files: `build.gradle.kts`, `gradlew`, `gradlew.bat`, `settings.gradle.kts`
     - Source code: `src/Main.java`
   - Emphasize: "Focus on Main.java; don't edit Gradle files now."

3. **(15 min) Running "Hello World"**
   - Open Main.java, verify "Hello, World!" print statement
   - Open Terminal (View → Terminal)
   - Run command:
     - Windows: `.\gradlew.bat run`
     - Mac/Linux: `./gradlew run`
   - Confirm "Hello, World!" output
   - (Optional) Show Run link above `main()`, but emphasize `gradlew run` for future grading

4. **(15–20 min) Practice Java & IDE Features**
   - Edit `Main.java`:
     1. Add another `System.out.println("some message here");`
     2. Create an integer variable: `int score = 10;`
     3. Print it: `System.out.println("Score: " + score);`
   - Save and run after each change
   - Encourage exploration:
     - Type `System.` to see IntelliSense suggestions
     - Introduce an error (e.g., remove a semicolon) to see red underlines and the Problems panel
   - TAs: Circulate and check for error messages and solution suggestions

5. **(10 min) Reflection & Q&A**
   - Distribute reflection questions:
     - Why use Gradle?
     - What is IntelliSense?
     - How to fix "gradlew: command not found"?
   - Optional question: "Code lens 'Run' vs. terminal approach: preferences and reliability?"

6. **(5–10 min) Wrap-Up & Submission**
   - Students: Screenshot VS Code window (Main.java + terminal output)
   - Compile screenshot + reflection answers into a single PDF/docx
   - Remind about submission deadline

## 4. Potential Pitfalls & Issues

1. **Incomplete Coding Pack Installation**
   - Verify with `java -version` in a separate terminal
   - Check "Java Extension Pack" in VS Code's Extensions panel

2. **gradlew Command Not Found**
   - Windows: Use `.\gradlew.bat run`
   - Mac/Linux: Use `./gradlew run`
   - Ensure correct folder is open (project root with `gradlew`)

3. **Slow VS Code Java Extension**
   - Allow time for IntelliSense/error checking to load
   - Instruct to reload window if necessary
   - Ensure "Yes" is selected if prompted to trust the project

4. **Syntax Errors**
   - Encourage use of the Problems panel
   - Remind to save the file (or enable Auto Save)

5. **"Run | Debug" Confusion**
   - Emphasize `gradlew run` for consistency in future labs
   - Explain benefits of terminal approach

## 5. TA Guidance & Socratic Questions

- **Setup**:
  - "Is Coding Pack installed? Does `java -version` show version 17?"
  - "Is 'Extension Pack for Java' visible in VS Code's Extensions panel?"

- **Project Opening**:
  - "Is the folder structure correct? Can you see `src/` and `gradlew` files?"
  - "Any 'Java project initializing...' messages?"

- **Code Running**:
  - "What's your terminal output after `gradlew run`? See `BUILD SUCCESSFUL` and prints?"
  - "What happens with an incorrect run command or missing `./` or `.\`?"

- **IDE Features**:
  - "Meaning of red underlines? Checked the Problems panel?"
  - "How can IntelliSense help with `System` class methods?"

- **Reflection**:
  - "Preferred method to run: Terminal or code lens? Why use `gradlew run` as standard?"

## 6. Expected Outputs and Deliverables

Each student/group should produce:

1. **Screenshot**:
   - VS Code with `Main.java` showing:
     - Original "Hello, World!"
     - Additional `System.out.println` line
     - Integer variable (e.g., `int score = 10;`)
   - Terminal with `gradlew run` results (compile messages + final output)

2. **Short Reflection** (1–2 paragraphs per question):
   - Coding Pack components and JDK necessity
   - Code running methods (at least two) and recommended approach for grading
   - IntelliSense experience and benefits
   - Introduced error and VS Code's response
   - Troubleshooting "'gradlew' not recognized" error

3. **Submission**:
   - Combined screenshot + answers in a single PDF/DOCX
   - Submit by the due date via specified method

## 7. Wrap-Up and Next Steps

### Wrap-Up
- Confirm working environment: VS Code with Java, functional Gradle commands, visible auto-completion
- Students should be prepared for future labs with multiple files, more tasks, or advanced features

### Looking Ahead
- Future labs may introduce:
  - Unit tests
  - Multiple source files
  - Advanced Gradle tasks (e.g., `gradlew test`)
- Encourage keeping this "Hello World" project as a quick environment test

### TA Final Reminders
- Check each student's screenshot and reflection for completeness
- Clarify Windows vs. Mac `gradlew run` command differences
- Direct students to class forum for future setup issues
