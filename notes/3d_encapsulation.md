## 4. Encapsulation & Abstraction: The Heart of OOP

Think about organizing a board game. There are two ways to do it:

**Way 1: Keep pieces and rules separate**

```python
# Scattered pieces and rules
player_health = 100
player_gold = 50

def heal_player(health, amount):
    return health + amount

# Later... which health are we changing?
player_health = heal_player(player_health, 20)
```

**Way 2: Package pieces with their rules**

```java
public class Player {
    private int health = 100;
    
    public void heal(int amount) {
        health += amount;  // This Player's health
    }
}

// Clear which player we're modifying
hero.heal(20);
```

The second way is called **Object-Oriented Programming** (OOP). It bundles data with the code that works on that data. Java helps us do this through:

1. **Encapsulation**: Protect data from invalid changes

   ```java
   private int health;  // Only accessible through methods
   ```

2. **Abstraction**: Hide complex details behind simple commands

   ```java
   player.heal(5);     // Don't care HOW it heals
   ```

Let's learn to write code this way!

---

### 4.1 Beyond Simple Classes

Our `Player` class works, but it has a problem: anyone can break the rules. In a real game, this could be disastrous:

```java
Player hero = new Player(100, 50);

// During gameplay:
hero.health = -999;     // Player becomes invincible!
hero.gold = 1000000;    // Instant millionaire...
monster.health = 0;     // Kill without fighting
```

We need three things:

1. **Protection**: Stop direct access to data

   ```java
   private int health;  // Now hero.health = -999; won't compile!
   ```

2. **Controls**: Provide safe ways to modify data

   ```java
   public void heal(int amount) {
       if (amount > 0) {         // Only positive healing allowed
           health += amount;      // Safely change health
       }
   }
   ```

3. **Rules**: Enforce game mechanics

   ```java
   public void takeDamage(int amount) {
       health = Math.max(0, health - amount);  // Never go below 0
   }
   ```

This is where OOP shines: we can make the compiler help enforce our rules. Let's see how!

---

### 4.2 Understanding Encapsulation

Encapsulation has two key parts:

1. Bundling related data and methods together in a class
2. Protecting that data so it can only be changed in valid ways

When we encapsulate properly:

- Related code stays together (easier to understand)
- Data can only be changed through methods (maintains validity)
- Implementation details can be changed without affecting other code

Let's see how Java helps us achieve this:

1. **Bundling**: Keeping related things together

   ```java
   public class BankAccount {
       // Things that every account needs:
       private double balance;      // How much money you have
       private String accountNum;   // Like your account number at a real bank
       private double interestRate; // How much interest you earn

       // The code that works with these values:
       public void addInterest() {
           // Calculate interest using the account's own values
           double earned = balance * interestRate;  // multiply your money by rate
           balance = balance + earned;              // add it to your balance
       }
   }
   ```

   See how the interest calculation uses both `balance` and `interestRate`? They belong together!

2. **Protection**: Making sure data changes safely

   ```java
   public class Player {
       private int health;  // Only Player methods can change this
       
       // Safe way to take damage - health can't go below 0
       public void takeDamage(int amount) {
           // If health is 10 and damage is 15, health becomes 0, not -5
           if (amount > health) {
               health = 0;  // Player is defeated
           } else {
               health = health - amount;  // Normal damage
           }
       }
   }
   ```

   Now players can't have negative health, which might break game rules!

3. **Interface**: Making your class easy to use

   ```java
   // These method names clearly tell you what they do:
   BankAccount myAccount = new BankAccount("12345");
   myAccount.deposit(100);     // Put money in
   myAccount.withdraw(50);     // Take money out
   double money = myAccount.getBalance();  // Check how much you have

   // Compare to trying to work with raw data:
   myAccount.balance = myAccount.balance + 100;  // Easy to make mistakes!
   ```

   Good method names act like clear labels on buttons!

4. **Invariants**: Rules that must always be true

   ```java
   public class Player {
       private int health;
       private final int MAX_HEALTH = 100;  // Players can't have more than 100 health
       
       public void setHealth(int newHealth) {
           // Check all our rules:
           if (newHealth < 0) {
               // Can't have negative health
               health = 0;
           } else if (newHealth > MAX_HEALTH) {
               // Can't exceed maximum
               health = MAX_HEALTH;
           } else {
               // Value is okay!
               health = newHealth;
           }
       }
   }
   ```

   These rules are always enforced - you can't break them by accident!

Think about a vending machine:

- It bundles the snacks, prices, and coin slot together
- It protects the snacks behind glass
- It has a simple interface (insert money, press B4)
- It maintains rules (no free snacks!)

When we write classes this way:

- Related data and code stay together (like snacks and prices)
- Data can't be changed incorrectly (like reaching through the glass)
- Other code has clear ways to interact (like the coin slot and buttons)
- Rules are always followed (like "no money = no snack")

Now you're not just hiding data - you're building a reliable, easy-to-use machine!

---

### 4.3 Different Ways to Enforce Rules

When protecting data, we have several tools:

1. **Constructor Checks**: Stop invalid objects from being created

   ```java
   public Player(int startHealth) {
       if (startHealth < 0) {
           startHealth = 1;  // Fix invalid input
       }
       health = startHealth;
   }
   ```

2. **Method Guards**: Fix invalid inputs

   ```java
   public void heal(int amount) {
       if (amount < 0) {
           amount = 0;  // Ignore negative healing
       }
       health += amount;
   }
   ```

3. **Range Enforcement**: Keep values in bounds

   ```java
   public void setHealth(int newHealth) {
       health = Math.max(0, Math.min(newHealth, MAX_HEALTH));
   }
   ```

4. **Complete Rejection**: Return success/failure

   ```java
   // return a boolean value– true = success, false = failure
   public boolean withdraw(int amount) {
       if (amount > balance) {
           return false;  // Can't withdraw more than you have
       }
       balance -= amount;
       return true; // true = Successful withdrawal
   }
   ```

Choose based on what makes sense for your situation. Sometimes you fix bad inputs, sometimes you reject them entirely.

---

### 4.4 Abstraction: What Users Need vs. What Code Does

Imagine walking into a restaurant:

- You order "a cheeseburger"
- Kitchen handles complex details (grill temp, cooking time, assembly order)
- You don't need to know HOW they make it

That's abstraction in code:

```java
public class Restaurant {
    // Store kitchen details inside the class (encapsulation)
    private double grillTemp;   // Current temperature of grill
    private int burgerCount;    // How many burgers we can make
    private int grillSpace;     // How many burgers fit on grill
    
    // Simple interface for customers:
    public boolean orderCheeseburger() {
        // First check if we can make the burger
        if (burgerCount <= 0) {
            return false;    // Can't make burger - out of ingredients
        }
        
        // Complex steps hidden from customer:
        setGrillTemp(375);              // Heat the grill
        boolean success = cookPatty();   // Try to cook the burger
        
        if (success) {
            burgerCount = burgerCount - 1;  // Use up ingredients
            return true;                     // Burger ready!
        }
        return false;                        // Something went wrong
    }
    
    // Helper method - customers don't need to see this
    private boolean cookPatty() {
        if (grillSpace > 0) {           // If there's room on grill
            grillSpace = grillSpace - 1; // Take up one spot
            return true;                 // Cooking successful
        }
        return false;                    // Grill is full
    }
}

// Customer just needs to know:
Restaurant store = new Restaurant();
boolean gotBurger = store.orderCheeseburger();  // Don't care about the details!
```

Abstraction lets us:

1. Hide complex details (`grill`, `inventory`, cooking steps)
2. Show simple interfaces (just "orderCheeseburger")
3. Change implementation (new grill, different recipe) without affecting users

Why is this different from encapsulation?

- Encapsulation: Protects data from invalid changes
- Abstraction: Hides complexity behind simple interfaces

Together they create reliable, easy-to-use code:

```java
public class Player {
    private int health;            // Encapsulation
    private double healBonus;      // (protect the data)
    
    public void heal(int amount) { // Abstraction
        // Complex healing logic hidden from users:
        applyHealingBuffs();
        checkStatusEffects();
        updateHealth(amount);      // Users don't see these steps
    }
}
```

---

### 4.5 Looking Ahead: More OOP Features

You might notice some repetition in our game:

```java
class Player {
    private int health;
    public void takeDamage(int amount) { ... }
}

class Monster {
    private int health;
    public void takeDamage(int amount) { ... }
}

class Building {
    private int health;
    public void takeDamage(int amount) { ... }
}
```

Writing the same health/damage code for every destructible thing seems wasteful! OOP has two more powerful features that will help:

1. **Inheritance**: Write the health/damage code once, share it with all destructible things
2. **Polymorphism**: Treat Players, Monsters, and Buildings the same when dealing damage

We'll explore these later. For now, focus on:

- **Encapsulation**: Protect your data (like `private health`)
- **Abstraction**: Hide complex details (like how damage is calculated)

These fundamentals will prepare you for the advanced features ahead!

---

### 4.6 Encapsulation & Abstraction in Practice

Let's build a `BankAccount` that's both safe and easy to use. We'll add features step by step:

```java
public class BankAccount {
    // Step 1: Protect the data (Encapsulation)
    private double balance;
    private List<Transaction> history;  // Track all changes
    private double interestRate;

    // Step 2: Control object creation
    public BankAccount(double initBalance) {
        if (initBalance < 0) {
            initBalance = 0;  // Start at 0 if negative
        }
        this.balance = initBalance;
        this.history = new ArrayList<>();
        this.interestRate = 0.01;  // 1% interest
    }

    // Step 3: Simple interface, complex implementation (Abstraction)
    public boolean deposit(double amount) {
        // Validate input
        if (amount < 0) {
            return false;  // Can't deposit negative amounts
        }

        // Complex logic hidden from users:
        balance += amount;
        history.add(new Transaction("deposit", amount));
        checkForInterest();
        notifyOwner("Deposit: $" + amount);
        return true; // true = Success!
    }

    // Step 4: Hide implementation details
    private void checkForInterest() {
        if (balance > 1000) {
            double interest = balance * interestRate;
            balance += interest;
            history.add(new Transaction("interest", interest));
        }
    }

    private void notifyOwner(String message) {
        // Send email, update app, etc.
    }
}
```

Try using it:

```java
BankAccount acct = new BankAccount(100);
acct.deposit(50);   // Simple to use!
```

What's happening behind the scenes?

1. Input validation
2. Balance update
3. Transaction logging
4. Interest calculation
5. Owner notification

But users don't need to know any of that! They just see:

- `deposit(amount)` → money goes in
- `withdraw(amount)` → money comes out
- `getBalance()` → check total

This is the power of combining encapsulation and abstraction:

- Encapsulation keeps the data safe
- Abstraction keeps the usage simple

---

### 4.7 From Design Recipe to OOP

Remember the design recipe steps?

1. Data definitions
2. Constraints
3. Methods that work with that data

OOP helps enforce these:

```java
// Design Recipe says: "health must be ≥ 0"
public class Player {
    private int health;        // Data definition + protection
    
    public void heal(int amt) {    // Methods enforce constraints
        if (amt < 0) return;       // No negative healing
        health = Math.min(100,     // Can't exceed max
                         health + amt);
    }
}
```

The compiler becomes your ally:

- Private fields → Can't break data definitions
- Methods → Enforce constraints automatically
- Tests → Verify that rules work

### 4.8 What's Next: Objects in Memory

When we do:

```java
Player hero = new Player(100);
Player backup = hero;        // What happens here?
backup.health -= 50;        // Does this affect hero?
```

We need to understand:

- How Java stores objects
- What happens when we copy them
- How method calls work with objects

That's our next topic: Object References!

### 4.9 Practice: Put It All Together

1. **Unbreakable Player**

```java
public class Player {
    private int health;
    private int maxHealth = 100;
    
    public void heal(int amount) {
        // TODO: Implement healing that:
        // 1. Rejects negative amounts
        // 2. Won't exceed maxHealth
        // 3. Returns true if healing worked
    }
    
    public boolean takeDamage(int amount) {
        // TODO: Implement damage that:
        // 1. Won't go below 0
        // 2. Returns true if player still alive
    }
}
```

2. **Safe Bank Account**

```java
public class BankAccount {
    private double balance;
    private List<String> transactions;
    
    public void deposit(double amount) {
        // TODO: Add validation and logging
    }
    
    public boolean withdraw(double amount) {
        // TODO: Add validation and logging
    }
}
```

For each challenge:

1. Think about what could go wrong
2. Use encapsulation to prevent it
3. Use abstraction to hide the details
4. Test edge cases!
