# **Lab 4: Getting Started with VS Code, Java, and Gradle**

Welcome to your very first journey into coding with a "real" Java development environment! Until now, you may have used simple online editors or minimal text files. In this lab, you'll get familiar with:

- **VS Code** – a friendly editor that provides color-coding, auto-completion, and error checks.
- **Gradle** – a build tool that automates compiling and running Java projects (we'll use it in future labs, too).
- **Java 17** – the version we'll use for your code.

**By the end**, you'll have run a simple "Hello World" project, practiced adding a few Java lines from Chapter 2, and seen how VS Code helps you spot mistakes before you even run the code.

---

## **1. Installing the Coding Pack for Java**

1. **What's the "Coding Pack for Java"?**  
   This special bundle installs **everything** needed for Java development in one go:
   - **Visual Studio Code** (the text editor / IDE)
   - **Java Development Kit (JDK) 17** (tools to compile and run Java code)
   - **Recommended Java Extensions** for VS Code (auto-complete, error detection, etc.)

2. **Download and Install**  
   - **Windows**: [Coding Pack for Java (Windows)](https://aka.ms/vscode-java-installer-win)  
   - **macOS**: [Coding Pack for Java (Mac)](https://aka.ms/vscode-java-installer-mac)  

   Start the installer, click "Next" or "Continue" on each step, and accept defaults. After finishing, you'll have VS Code and a JDK set up. On Linux, or if you prefer manual steps, see your instructor's notes.

3. **Confirm Installation**  
   Once done, open **VS Code** from your Start menu (Windows) / Applications folder (macOS), or via your chosen method.  
   - If you see the **Java Extension Pack** or "Java" mention in the bottom status bar, that's a good sign.
   - If you open a "Command Prompt" or "Terminal" and type `java -version`, you might see something like "openjdk version 17…"  

---

## **2. Open the "Hello World" Gradle Project**

We've prepared a tiny Gradle-based Java project. You'll see how it's structured and how we run it in VS Code.

1. **Get the Provided Project**  
   - Your instructor should give you a `.zip` file, e.g., `lab-4-hello-world.zip`.
   - Unzip it to a convenient folder (like `Documents/lab-4-hello-world`).

2. **Start VS Code and Open the Folder**  
   - **In VS Code**: Go to **File → Open Folder...**  
   - Select the **`lab-4-hello-world`** folder you just unzipped (the folder that contains `build.gradle.kts` and `src/`).
   - If prompted about **trusting** the authors of the code, click "Yes, I trust…" since it's your own code.
   - Wait a moment for a "Java project initializing…" message in the bottom-right or bottom status bar. This is the extension scanning the files so your IntelliSense will work.

3. **Check Out the Files**  
   - In the **Explorer** panel (click the folder icon in the left Activity Bar if it's hidden), you'll see:
     ```
     lab-4-hello-world/
     ├── build.gradle.kts
     ├── gradlew
     ├── gradlew.bat
     ├── settings.gradle.kts
     └── src
         └── Main.java
     ```
   - **`Main.java`** is your actual Java code.  
   - The rest are Gradle build scripts—**don't worry** if they look strange. We'll focus on `Main.java`.

---

## **3. Running "Hello World!"**

1. **Open `Main.java`**  
   ```java
   public class Main {
       public static void main(String[] args) {
           System.out.println("Hello, World!");
       }
   }
   ```
2. **Open the VS Code Terminal**  
   - **View → Terminal**, or press <kbd>Ctrl + `</kbd> (Windows) or <kbd>Cmd + `</kbd> (Mac).  
   - This will open a panel at the bottom showing a prompt like `PS C:\Users\YourName\lab-4-hello-world>` or something similar.

3. **Run the Project via Gradle**  
   - **Windows**: Type `.\gradlew.bat run` and press Enter.  
   - **macOS/Linux**: Type `./gradlew run` and press Enter.  
   - You'll see Gradle compile your code, then:

     ```
     > Task :run
     Hello, World!
     BUILD SUCCESSFUL in ...
     ```
   - If you see "Hello, World!" in the output, **congrats**—you just ran your first Gradle-based Java code in VS Code!

4. **Optional**: You might notice a "Run | Debug" link above the `main` method in the editor. Clicking "Run" also works, but **we recommend** using the terminal command so you get comfortable with the approach we'll use in future labs.

---

## **4. Explore IDE Features**

### A. **Syntax Highlighting**  
Observe how `public`, `class`, `System` are in different colors. This helps you see keywords, classes, and strings at a glance.

### B. **IntelliSense** (Auto-Complete)  
- Try typing:  
  ```java
  System.
  ```
  A mini menu may pop up with `out`, `err`, etc. That's IntelliSense. If you don't see it, press <kbd>Ctrl+Space</kbd> (Windows/Linux) or <kbd>Cmd+Space</kbd> (Mac).

### C. **Error Underlines** (Red Squiggles)  
- If you remove a semicolon from `System.out.println("Hello, World!")`, the text will get underlined and you might see an error message like "`;` expected."

### D. **Problems Panel**  
- If you see red underlines, open the **Problems** tab (usually at the bottom, or **View → Problems**). It should list any compile issues ("; expected" on line 5, for example).

### E. **Quick Fix**  
- If a **light bulb** icon appears next to the error, click it or press <kbd>Ctrl + .</kbd> to see if a fix is suggested (like "Insert semicolon").

These **core IDE features** save you a ton of time: you'll fix mistakes *before* running the code.

---

## **5. Practice Chapter 2: Simple Edits**

Let's do a few mini-tasks to confirm everything works and to see IntelliSense in action:

1. **Add Another Print**  
   ```java
   System.out.println("My name is Ada Lovelace!");
   ```
   Save the file (<kbd>Ctrl+S</kbd> / <kbd>Cmd+S</kbd>), run `gradlew run` again. You should see two lines now.

2. **Add a Variable**  
   ```java
   int score = 100;
   System.out.println("Score: " + score);
   ```
   As you type, watch for IntelliSense suggestions. Then run again to see "Score: 100".

3. **Intentionally Introduce an Error**  
   - Remove the `;` from your `score` line.  
   - Notice the red underline. Hover or open the **Problems** panel. You'll see something like `';' expected`.  
   - If a light bulb appears, see if it suggests "Insert semicolon." Accept the fix or type it back in yourself.

4. **Try Another Summation** (Optional)  
   ```java
   int newScore = score + 50;
   System.out.println("New Score: " + newScore);
   ```

Every time, **save and run** with Gradle. Observe your output as it changes.

---

## **6. Reflection & Deliverables**

When you're done exploring, please gather the following **deliverables**:

1. **Screenshot**  
   - Show your *Main.java* in VS Code, with at least:
     - **Two print statements** (the original "Hello, World!" and your new custom message).
     - **One variable** (like `score`) used in a print.
   - Also capture the **Terminal** output from running `gradlew run`.  
   - Make sure the screenshot shows the VS Code window, so we can see the color-coding and structure.

2. **Short-Answer Questions** (a paragraph or a few sentences each):
   1. **Installation Insight**: Summarize **what** the Coding Pack installed (VS Code, JDK, etc.) and **why** each part is necessary for Java development.  
   2. **Two Ways to Run**: You used the **Gradle command** in the Terminal (`gradlew run`) and possibly the **Run** code lens. Which one are we using for official labs, and why might the Terminal approach be valuable?  
   3. **IntelliSense**: How did IntelliSense help you while typing code? Did it suggest methods, or help you correct mistakes?  
   4. **Encountering Errors**: Describe the error you introduced (missing semicolon or something else). How did VS Code notify you? Did the Quick Fix help?  
   5. **Troubleshooting**: If someone said "I typed `gradlew run` but it says 'command not found!'," what might you tell them to try or check? (Reflect on what you learned.)

3. **Formatting & Submission**  
   - You can compile your screenshot and answers into **one PDF or DOCX**.  
   - Submit this document to your course's usual submission platform by the due date.

### Additional Reflection (Optional)
- **What do you like** about having real-time error checks and highlights?  
- **Any frustrations** or confusions about the editor you want to note?  

Please feel free to include these thoughts in your write-up if you have them!

---

## **7. Troubleshooting Tips**

Here are common issues first-timers face, **plus** how to handle them:

1. **"`gradlew run` not recognized**" or "**No such file or directory**."  
   - On **Windows**: Use `.\gradlew.bat run` (notice the `. \`).  
   - On **Mac/Linux**: Use `./gradlew run` (a `./` at the start).  
   - Check that you opened the *correct folder* in VS Code (the one containing `gradlew`).

2. **No Java extension** or IntelliSense**?  
   - Wait a few seconds after opening the folder so the Java extension finishes initializing.  
   - Look at the bottom-right corner for any "Java extension installing" or "Loading…" messages.  
   - If it's still not showing, open the Extensions panel (the square icon in the Activity Bar) and look for "Extension Pack for Java." Install or enable it if missing.

3. **Red Underlines but Code Compiles Fine**  
   - Sometimes the extension lags behind. Close and reopen `Main.java` or reload the window (Command Palette → "Developer: Reload Window").  
   - If it persists, do **File → Save All**. Usually, the extension catches up quickly.

4. **"Could not trust the workspace"** or "Do you trust the authors?"**  
   - If it prompts for trust, you can select "Yes, I trust them" if you're sure it's your own code or from a safe place.  
   - If you select "Restricted Mode," some auto-complete or debugging features might not work fully.

5. **Any other weird errors**?  
   - Sometimes just **closing** VS Code and reopening your project fixes a random glitch. 
   - Or open a new Terminal (the old one might have a leftover environment setting). 
   - If in doubt, talk to classmates or TAs to see if it's a known quirk.

---

## **8. Next Steps & Conclusion**

Hooray—you've successfully:
1. Installed a **full Java environment** (VS Code + JDK + Extensions).
2. Explored **Hello World** in a Gradle-based project.
3. Practiced **Chapter 2** Java features in an IDE that highlights errors and suggests fixes in real time.

Going forward, you'll use these same steps for bigger labs and more advanced code, but the essential workflow remains:
1. Write or edit code in `Main.java` (or other `.java` files).
2. Use IntelliSense and Quick Fix to catch mistakes early.
3. Run with `./gradlew run` (or the Windows equivalent).

**Please submit** your screenshot + short answers according to instructions above. Then you'll be ready for deeper Java lessons in the next labs. **Great job** taking your first steps in a real IDE environment—this will streamline your coding in the long run!