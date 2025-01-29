## The Multi-Parameter Problem (and Why We Need Something Better Than Methods)

Remember how methods helped us avoid copying and pasting code? That was great! But as our programs grow bigger, we're running into a new problem: **too many separate variables** that really belong together.

### The Problem: Too Many Separate Pieces

Think of it like packing for school. Instead of one backpack, imagine carrying:

- Your math textbook in one hand
- Your pencil case in another
- Your calculator in your pocket
- Your notebook under your arm
- Your lunch box... somehow?

Sure, you *could* do it, but it's awkward and things might fall! This is exactly what's happening in our game code:

```java
int playerHealth  = 100;
int playerGold    = 50;
int playerXp      = 0;
int playerMana    = 75;
int playerStamina = 90;
```

All these variables describe one thing (the player), but we're carrying them separately. This leads to clumsy method calls:

```java
// We have to pass everything one by one
public static int increaseHealth(int currentHealth, int healAmount) {
    return currentHealth + healAmount;
}

public static int increaseGold(int currentGold, int goldReward) {
    return currentGold + goldReward;
}

// Using them gets tedious
playerHealth = increaseHealth(playerHealth, 5);
playerGold   = increaseGold(playerGold, 10);
```

### Why This Is A Problem

1. **Too Many Parameters**: What if we need a method that changes both health AND gold? We'd need:

   ```java
   public static void awardVictory(int health, int gold, int xp, int mana...) 
   ```

   That's a lot to keep track of!

2. **Easy Mistakes**: The compiler can't help us if we mix up the order:

   ```java
   // Oops! Accidentally swapped health and gold
   awardVictory(playerGold, playerHealth);  // This will compile! 😱
   ```

3. **Multiple Players**: It gets worse with two players:

   ```java
   int player1Health = 100;
   int player1Gold = 50;
   int player2Health = 100;
   int player2Gold = 50;
   // ... this is getting out of hand!
   ```

### The Solution: Grouping Related Things Together

Just like how a backpack keeps all your school supplies together, Java has a way to keep related variables together: it's called a **class**.

Instead of juggling separate variables, we can create a `Player` that keeps track of its own stats:

```java
// This is a preview - we'll learn how to write this in the next section!
Player p1 = new Player(100, 50, 0, 75, 90);
p1.increaseHealth(5);   // Much simpler!
```

Think of a class like a blueprint for creating objects that:

1. Keep their related data together (like health, gold, etc.)
2. Include methods that work with that data
3. Protect their data from accidental misuse

### What's Coming Next?

In our next section, we'll learn:

- How to create our own classes (like that `Player` example)
- How to keep data safe inside our classes
- How to write methods that belong to our classes

### Practice Thinking About It

1. **Group Related Things**
   - If you were making a `BankAccount`, what information would belong together?
   - Think: balance, account number, interest rate...

2. **Spot the Problem**
   - How many things could go wrong with:

     ```java
     public static void transferMoney(int fromBalance, int toBalance, int amount)
     ```

   - What if someone mixes up the order of `fromBalance` and `toBalance`?

*Next up: We'll see how to solve these problems by learning about classes - a way to keep related data and methods together, just like a backpack keeps your school supplies organized!*
