# Introducing Methods

**Prerequisites**:

- Basic Java syntax (if statements, loops)
- Understanding of variables and types
- Familiarity with the Design Recipe approach

Think of methods like your favorite recipes - write them once, use them many times! Just as you wouldn't want to write down a cookie recipe every time you bake, Java methods let us write code once and reuse it wherever needed.

**Note**: You might hear these called "functions" in other languages like Python or JavaScript. In Java, we typically say "methods" when the code belongs to a class.

In this chapter, we'll learn:

- How to spot code that could be turned into methods (using our Design Recipe skills)
- How Java handles method parameters (it's like passing notes in class!)
- Why methods are just the first step toward organizing our code

---

## 1. Why Do We Need Methods?

Let's start with a real problem. Imagine you're making a simple game where a player gains health and gold after winning fights:

```java
public class IntroMethods1 {
    public static void main(String[] args) {
        int playerHealth = 10;
        int playerGold   = 50;

        // First victory
        playerHealth += 5;
        playerGold   += 10;

        // Second victory
        playerHealth += 5;
        playerGold   += 10;

        System.out.println("Health: " + playerHealth);
        System.out.println("Gold:   " + playerGold);
    }
}
```

**Hold up!** Did you notice we wrote the same code twice? Just like copying homework isn't the best idea, copying code can lead to problems. What if we need to change how much gold a player gets? We'd have to find and update every copy!

**Key Insight**: When you find yourself copy-pasting code, it's usually a sign you need a method!

## Quick Check ✓

Before moving on, make sure you can answer:

- Why is copy-pasting code problematic?
- What happens if the reward amount changes?
- How does this relate to the Design Recipe's "repeated logic" warning?

---

## 2. Creating Your First Method

Think of a method like a vending machine:

- You put something in (parameters)
- It does some work (method body)
- You get something back (return value)

Here's the basic recipe:

```java
public static returnType methodName(parameters) {
    // method body
    return something; // if needed
}
```

Let's break this down:

- `public` - Makes the method accessible to other code. Think of it like making a public library that anyone can use.
- `static` - Means this method belongs to the class itself, not to any specific instance. We'll explore this more when we learn about objects and classes.
- `returnType` - Specifies what kind of value the method gives back:
  - Use `void` if it doesn't return anything
  - Use `int`, `double`, `String`, etc. if it returns that type of value
- `methodName` - The name we use to call the method. Like variable names:
  - Must start with a lowercase letter
  - Use camelCase for multiple words (like `calculateTotal`)
  - Should clearly describe what the method does
- `parameters` - The inputs the method needs to do its job:
  - Each parameter needs both a type and a name
  - Can have zero or more parameters
  - Multiple parameters are separated by commas

For example, in `public static int addNumbers(int first, int second)`:

- It's `public` so other code can use it
- It's `static` so we can call it directly from `main`
- It returns an `int`
- It's named `addNumbers`
- It takes two `int` parameters named `first` and `second`

**Example**:

```java
public static int addTwoNumbers(int a, int b) {
    int sum = a + b;
    return sum;  // must match the 'int' return type
}
```

**Compiler moment**: If you accidentally do

```java
public static int addTwoNumbers(String a, int b) { ... }
```

the compiler flags an **incompatible type** error when you try `addTwoNumbers(3, 5)`. It expects `(String, int)`, not `(int, int)`. The compiler is your “early alert system” for mismatched parameter types.

---

## 3. Trying a `void` Method—Why Doesn't It Work?

Let's trace what happens when we run this code:

```java
public static void awardVictory(int health, int gold) {
    // health is now a COPY of playerHealth (10)
    health += 5;  // health becomes 15, but only inside this method
    // gold is a COPY of playerGold (50)
    gold += 10;   // gold becomes 60, but only inside this method
    // When method ends, copies are discarded!
}

// In main:
playerHealth = 10;  // Original stays 10
playerGold = 50;    // Original stays 50
```

Think about it: If you make a photocopy of a document and write on the copy, does it change the original? That's what Java does with `int` parameters—it makes copies!

**The Fiasco**: What options do we have? Let's think through this like the Design Recipe taught us...

1. Could we use `void` and hope Java changes the originals? (No—we just saw why!)
2. Could we return both values somehow? (Not directly—methods return one thing)
3. Could we... *wait*... what if we return the new value and store it back? (Yes!)

## Understanding Pass-By-Value

Picture this:

```
In main():           │ In method:
─────────────────    │    ─────────────────
playerHealth = 10 ───┼──► health = 10 (copy)
                    │    health += 5
                    │    health is now 15
playerHealth still 10│    (copy discarded)
```

---

## 4. Returning New Values to Fix It

(*Implementation, Step 3 & 4: We refine and retest*)

We can fix it by **returning** the new integer and storing it in the caller. Let’s do two separate methods for clarity:

```java
public class IntroMethods3 {
    // Return updated health
    public static int increaseHealth(int currentHealth, int healAmount) {
        return currentHealth + healAmount;
    }

    // Return updated gold
    public static int increaseGold(int currentGold, int goldReward) {
        return currentGold + goldReward;
    }

    public static void main(String[] args) {
        int playerHealth = 10;
        int playerGold   = 50;

        // First victory
        playerHealth = increaseHealth(playerHealth, 5);
        playerGold   = increaseGold(playerGold, 10);

        // Second victory
        playerHealth = increaseHealth(playerHealth, 5);
        playerGold   = increaseGold(playerGold, 10);

        System.out.println("Health: " + playerHealth);
        System.out.println("Gold:   " + playerGold);
    }
}
```

**Output**:

```
Health: 20
Gold:   70
```

Now, each method returns the updated `int`, and we assign it back into `playerHealth` or `playerGold`. If you wanted “gold +12” instead of “+10,” you’d edit `increaseGold()` in *one* place.

---

## 5. Many Fields → Multiple Parameters Fiasco

Remember how the Design Recipe warned us about code that's "trying to do too much"? Let's count the ways this approach can go wrong:

1. What if we add more player stats? `awardVictory(health, gold, xp, mana, stamina, luck...)`
2. What if we need two players? `awardVictory(player1Health, player1Gold, player1Xp...)`
3. What if we accidentally mix up the order? `awardVictory(gold, health)`—oops!

The compiler can't save us here—it sees `(int, int)` and thinks "looks good!" even if we've mixed up which `int` is which. There must be a better way...

**Design Recipe perspective**:  

- We identified repeated logic → used methods.  
- But we still juggle many separate variables. The next step? “Bundle them in one container.” In Java, that container is a **class**. Then we can do `player1.heal(5)` without passing `(health1, xp1, gold1, … )`.

We’ll see that in the upcoming *Introducing Classes* lesson, including how **encapsulation** protects those fields from accidental misuse.

---

## 6. What We've Learned

**Big Ideas**:

1. Methods help us avoid copying code
2. Java makes copies of numbers we pass to methods
3. When methods need to update values, they should return them
4. Too many parameters = time to learn about classes!

**Coming Up Next**: We'll learn about classes - a way to keep related data and methods together, like keeping all your school supplies in one backpack instead of carrying them separately!

---

## Your Turn

Try these exercises to practice what you've learned. Remember: it's okay if you don't get it perfect the first time - that's how we learn!

1. **Convert Fahrenheit**  
   Define `public static double convertFtoC(double tempF)`, returning the Celsius result. Test by printing `convertFtoC(32)`.
2. **Improve Award Victory**  
   Suppose we want gold only on every *second* victory in a row. Write a method that returns the new “victory streak,” letting the caller track how many consecutive wins.
3. **XP Gains**  
   Each victory also awards +20 xp. Show how you might incorporate xp into the method calls, being mindful of pass-by-value issues.

Here's some starter code to get you going:

```java
public class MethodPractice {
    public static double convertFtoC(double tempF) {
        // Your code here
        // Formula: (F - 32) * 5/9
    }

    public static int awardVictoryStreak(int currentStreak) {
        // Your code here
        // Return updated streak count
    }

    public static void main(String[] args) {
        // Test your methods here
        System.out.println("32°F = " + convertFtoC(32) + "°C");
    }
}
```

## Common Pitfalls to Watch Out For

1. **Forgetting to Return**: If your method declares a return type, every path must return something

   ```java
   public static int bad(int x) {
       if (x > 0) {
           return x;
       }
       // Error! What if x <= 0?
   }
   ```

2. **Return Type Mismatch**:

   ```java
   public static int oops() {
       return 3.14; // Error! Can't return double where int expected
   }
   ```

3. **Parameter Type Confusion**:

   ```java
   public static void example(int x) { }
   
   // Later:
   double d = 3.14;
   example(d);  // Error! Can't pass double where int expected
   ```

## Quick Reference

**Method Syntax**:

```java
public static returnType methodName(type1 param1, type2 param2) {
    // method body
    return value;  // if non-void
}
```

**Key Points**:

- Methods reduce code duplication
- Parameters are passed by value (copies)
- Return type must match declaration
- void methods don't return anything
- static methods belong to the class

**Design Recipe Steps**:

1. Identify repeated code
2. Write method signature
3. Test with examples
4. Implement and verify

---

### Bonus: More on Naming

- **Method names** typically start with a lowercase letter and use “camelCase” for additional words: `increaseGold()`, `addTwoNumbers()`.
- They must follow Java’s identifier rules (no spaces, can’t start with a digit, etc.).

If you forget these rules, or pass arguments of the wrong type, your **compiler** is your first line of defense—**helping** you spot errors early, in true design-recipe spirit.
