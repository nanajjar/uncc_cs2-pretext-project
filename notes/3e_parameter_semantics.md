## **5. How Java Stores Data: Primitives vs Objects**

To write effective Java code, we need to understand how Java actually stores different types of data in memory. This explains why sometimes changing a value in a method affects the original variable, and other times it doesn't.

### **5.1 Two Ways Java Stores Data**

Java has two fundamentally different ways of handling data:

1. **Primitive Types** (`int`, `double`, `boolean`, etc.)
   - Stored directly in memory as their actual value
   - When copied, you get a completely independent copy
   - Examples: numbers, true/false values
   - The name of type starts with lowercase letter

2. **Reference Types** (Objects)
   - Stored as a reference (like an address) that points to data elsewhere in memory
   - When copied, you copy the reference but both still point to the same data
   - Examples: `String`, `ArrayList`, your own classes
   - The name of type starts with uppercase letter

Think of it like this:

#### Real World Analogy: School Lockers

**Primitives** are like writing on a sticky note:

- The actual number is right there on the note
- If you copy the note, each person has their own independent copy
- Changing one copy doesn't affect the other

**Objects** are like using a school locker:

- Instead of carrying everything, you just carry the locker number
- If you share that locker number, you're both using the same locker
- When one person changes something in the locker, everyone with that number sees the change

Let's see both perspectives in code:

```java
// PRIMITIVES: Direct values
int x = 42;          // x stores 42 directly
int y = x;           // y gets its own copy of 42
y = 100;             // changing y doesn't affect x
System.out.println(x);  // still prints 42

// OBJECTS: References to data
Player p1 = new Player(100);     // p1 stores a reference to the Player
Player p2 = p1;                  // p2 gets a copy of the reference
p2.reduceHealth(50);            // affects the one shared Player
System.out.println(p1.getHealth()); // prints 50 - both see the change
```

In memory, it looks like this:

```
Primitives:           Objects:
x: [42]              p1 ────┐
y: [100]                    └──> [Player data]
                    p2 ────┘
```

This fundamental difference affects everything from variable assignment to method parameters, which we'll explore next.

---

### **5.2 How Primitives Work: Independent Copies**

Remember our sticky note analogy? Let's see exactly how primitives work with a game score example:

```java
// Initial score
int score = 100;                  // Write "100" on first sticky note

// Try to create a backup
int backupScore = score;          // Copy "100" to a new sticky note

// Change the backup
backupScore = 50;                 // Change only the backup note to "50"

// Check both scores
System.out.println("Original: " + score);      // Shows 100
System.out.println("Backup: " + backupScore);  // Shows 50
```

Let's watch how memory changes at each step:

```
Step 1: Create score          Step 2: Create backup         Step 3: Change backup
┌─────────────┐              ┌─────────────┐               ┌─────────────┐
│score: [100] │              │score: [100] │               │score: [100] │
└─────────────┘              │backup:[100] │               │backup:[50]  │
                             └─────────────┘               └─────────────┘
```

This works the same for all primitive types:

```java
double price = 9.99;              // One sticky note
double salePrize = price;         // New independent sticky note
salePrize = 7.99;                // Only changes salePrize

boolean gameOver = false;         // One sticky note
boolean lastState = gameOver;     // New independent sticky note
lastState = true;                // Only changes lastState
```

🚫 Common Mistake: Thinking variables are connected

```java
int lives = 3;
int extraLives = lives;     // Creates a copy, not a connection!
extraLives--;              // Only extraLives becomes 2
System.out.println(lives); // Still 3!
```

Remember: With primitives, each variable gets its own independent sticky note. Changes to one never affect the other!

---

### **5.3 How Objects Work: Sharing Access Through References**

Remember our locker analogy? Let's see how it works with a simple game character:

```java
public class Player {
    private int health;
    public Player(int h) { health = h; }
    public void damage(int amt) { health -= amt; }
    public int getHealth() { return health; }
}
```

When you create and share a Player object, here's what happens:

```java
// Step 1: Create new Player (like getting a new locker)
Player hero = new Player(100);    // Get locker #123 with 100 health inside

// Step 2: Share the locker number
Player sidekick = hero;          // Give sidekick the same locker number (#123)

// Step 3: Either person can affect the shared Player
sidekick.damage(25);            // Sidekick opens locker #123 and reduces health
System.out.println(hero.getHealth());   // Hero checks same locker, sees 75 health
```

The memory looks like this:

```
Before damage:                After damage:
hero     ────┐               hero     ────┐
             └─> [100]                    └─> [75]
sidekick ────┘               sidekick ────┘
```

---

### **5.4 Methods with References: The Right and Wrong Ways**

Let's look at a real game scenario: damaging multiple players in an area effect spell:

```java
public class Player {
    private int health;
    private String name;
    
    public Player(String name, int health) {
        this.name = name;
        this.health = health;
    }
    public void damage(int amt) { 
        health = Math.max(0, health - amt); 
    }
    public int getHealth() { return health; }
}

// Two approaches to area damage:
public class Game {
    // ❌ WRONG WAY: Tries to work with copies of numbers
    public static void wrongAreaDamage(int health1, int health2, int damage) {
        health1 -= damage;  // Only changes local copies
        health2 -= damage;  // Original players unaffected
    }
    
    // ✅ RIGHT WAY: Works with the actual players
    public static void rightAreaDamage(Player p1, Player p2, int damage) {
        p1.damage(damage);  // Changes real player health
        p2.damage(damage);  // Changes real player health
    }
}
```

Let's see what happens in memory when we use these:

```java
Player hero = new Player("Hero", 100);
Player ally = new Player("Ally", 80);

// Wrong way - nothing changes:
wrongAreaDamage(hero.getHealth(), ally.getHealth(), 30);
System.out.println(hero.getHealth());  // Still 100
System.out.println(ally.getHealth());  // Still 80

// Right way - both players take damage:
rightAreaDamage(hero, ally, 30);
System.out.println(hero.getHealth());  // Now 70
System.out.println(ally.getHealth());  // Now 50
```

Memory during `rightAreaDamage`:

```
Outside method:          Inside rightAreaDamage:
hero ────┐               p1 ────┐
         └─> [H:100]            └─> [H:100] -> [H:70]
ally ────┐               p2 ────┐
         └─> [H:80]             └─> [H:80]  -> [H:50]
```

🚫 Common Mistakes:

```java
// Mistake 1: Passing number instead of Player
healPlayer(hero.getHealth(), 50);   // Wrong! Passes copy of health
healPlayer(hero, 50);               // Right! Passes player reference

// Mistake 2: Thinking new variables mean new objects
Player backup = hero;               // Same player, two references
Player clone = new Player(hero.getHealth()); // Different player!
```

---

### **5.5 What Really Happens Inside Methods**

Let's watch exactly what happens in both the wrong and right approaches:

#### Wrong Way: Passing Health Value

```
Step 1: Starting state
┌─────────────────┐
│Hero's Locker    │
│health = 100     │
└─────────────────┘

Step 2: Call wrongReduce(hero.getHealth(), 5)
┌─────────────────┐    ┌─────────────┐
│Hero's Locker    │    │Method's Copy│
│health = 100     │    │health = 100 │
└─────────────────┘    └─────────────┘
                          ↓
                       health = 95
                          ↓
Hero unchanged!        Copy discarded

Result: Hero still at 100 health
```

#### Right Way: Passing Player Reference

```
Step 1: Starting state         Step 2: Inside rightReduce
hero──┐                        hero──┐
      └→[health: 100]               └→[health: 100]
                              p  ──┘
                              
Step 3: After p.reduce(5)     Step 4: Method ends
hero──┐                       hero──┐
      └→[health: 95]               └→[health: 95]
p  ──┘                       (p is discarded)
```

Quick Comparison:

| Action | Wrong Way | Right Way |
|--------|-----------|-----------|
| What's passed | Copy of 100 | Locker number |
| Method sees | New note | Same locker |
| Changes affect | Only the copy | Real player |
| After method | Original unchanged | Player modified |

Remember: When you pass a Player, you're sharing the locker number!

---

### **5.6 Sharing Multiple Lockers: Group Methods**

Think of a method that works with multiple objects like a person with multiple locker numbers. Let's see what happens in a boss battle:

```java
public static void bossFight(Player hero, Player boss, int damage) {
    // Inside method: we have copies of both locker numbers
    hero.damage(damage);    // Open hero's locker, reduce health
    boss.damage(damage*2);  // Open boss's locker, reduce health more
}

// Create two separate lockers
Player hero = new Player("Hero", 100);   // Locker #1: 100 health
Player boss = new Player("Boss", 200);   // Locker #2: 200 health

// Share both locker numbers with bossFight
bossFight(hero, boss, 30);
```

Memory changes during the fight:

```
Before battle:                After battle:
hero ────┐                    hero ────┐
         └─> [H:100]                  └─> [H:70]
boss ────┐                    boss ────┐
         └─> [H:200]                  └─> [H:140]

Inside bossFight method:
hero & p1 ────┐
              └─> [Same Hero object]
boss & p2 ────┐
              └─> [Same Boss object]
```

🔑 Key Point: A method can receive multiple locker numbers (references) and modify all those objects. Each parameter is a copy of the reference, but they all point to the real objects.

---

### **5.7 Summary: What You Need to Remember**

Let's wrap up with the most important points and common mistakes to avoid:

#### 🎯 Key Concepts

1. **Primitives are Like Sticky Notes**

   ```java
   int x = 42;
   int y = x;     // New note with copy of 42
   y = 10;        // Only changes y's note
   ```

2. **Objects are Like Lockers**

   ```java
   Player p1 = new Player(100);  // New locker
   Player p2 = p1;               // Shared locker number
   Player p3 = new Player(100);  // Different locker!
   ```

#### 🚫 Common Mistakes to Avoid

1. **Wrong: Passing the Number Instead of the Locker**

   ```java
   // ❌ WRONG - passes copy of health number
   void healPlayer(int health, int amount) {
       health += amount;  // Changes thrown away
   }
   
   // ✅ RIGHT - passes locker number (reference)
   void healPlayer(Player player, int amount) {
       player.heal(amount);  // Changes real player
   }
   ```

2. **Wrong: Thinking New Variables Mean New Objects**

   ```java
   // ❌ WRONG assumption: thinking these are different players
   Player backup = hero;  // Just sharing same locker!
   backup.damage(10);     // Hero also loses health!
   
   // ✅ RIGHT way to make a separate player
   Player clone = new Player(hero.getHealth());  // New locker
   ```

3. **Wrong: Misunderstanding Pass-by-Value**

   ```java
   // Java always passes copies, but:
   primitiveMethod(score);      // Copies the number
   objectMethod(player);        // Copies the locker number
   ```

Remember:

- Primitives: Each variable has its own independent value
- Objects: Variables can share access to the same object
- Methods: Get copies of what you pass, but copies of locker numbers still open the same locker!

---

### **5.8 Practice Exercises**

Try these exercises to reinforce your understanding. For each one, predict what will happen before running the code!

#### Exercise 1: Gold Stealing Game

```java
class Player {
    private int gold;
    private String name;
    
    public Player(String name, int startingGold) {
        this.name = name;
        this.gold = startingGold;
    }
    public int getGold() { return gold; }
    // TODO: Add methods needed for gold stealing
}

class Game {
    // TODO: Implement this method
    public static void stealGold(Player thief, Player victim, int amount) {
        // Your code here: Move gold from victim to thief
    }
    
    public static void main(String[] args) {
        Player robin = new Player("Robin", 0);    // Starts with no gold
        Player sheriff = new Player("Sheriff", 100);  // Rich sheriff!
        
        stealGold(robin, sheriff, 50);
        System.out.println("Robin's gold: " + robin.getGold());     // Should be 50
        System.out.println("Sheriff's gold: " + sheriff.getGold()); // Should be 50
    }
}
```

🔍 Hint: You'll need to add methods to change a Player's gold. Think about what the Player class needs!

#### Exercise 2: Spell System

```java
class Spell {
    private int charges;
    public Spell(int charges) { this.charges = charges; }
    // TODO: Add method to use a charge
}

class Player {
    private int mana;
    public Player(int startingMana) { this.mana = startingMana; }
    
    // TODO: Implement castSpell
    public void castSpell(Spell spell) {
        // Your code here: Reduce spell charges AND player's mana
    }
}

// Test your implementation:
Player mage = new Player(100);
Spell fireball = new Spell(3);
mage.castSpell(fireball);  // Should affect both mage AND spell
```

🔍 Hint: Remember both objects (Player and Spell) need to be modified!

#### Exercise 3: Spot the Bug

```java
class Player {
    private int health = 100;
    
    // Bug: This method won't work! Why?
    public static void wrongHeal(int health, int amount) {
        health += amount;  // Try to increase health
    }
    
    // TODO: Write the correct version
    public static void rightHeal(Player player, int amount) {
        // Your code here
    }
}

// Test code - what prints and why?
Player hero = new Player();
wrongHeal(hero.getHealth(), 50);
System.out.println(hero.getHealth());  // Still 100! Why?

rightHeal(hero, 50);
System.out.println(hero.getHealth());  // Should be 150
```

🎯 Success Checklist:

- [ ] Gold stealing changes both players' gold
- [ ] Spell casting reduces both charges and mana
- [ ] Healing only works when passing Player object

Remember: Changes only "stick" when you modify the actual object through its reference!

---
