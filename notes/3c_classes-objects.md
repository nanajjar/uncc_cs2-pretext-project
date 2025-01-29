## 3. Introducing Classes: Building From The Ground Up

So far, we've battled this messy situation:

```java
// Player 1's stats
int player1Health = 100;
int player1Gold = 50;

// Player 2's stats (getting messy...)
int player2Health = 100;
int player2Gold = 50;

// Whoops, which health am I changing?
player1Health = healPlayer(player2Health, 5); // Easy mistake!
```

Methods helped a bit, but we still pass variables around separately. **Wouldn't it be great** if all these stats lived in **one** place?

### 3.1 A Single “Entity” That Owns Its Data

Let’s pretend we want to treat the player as a single *entity*, storing *all* of that player’s stats in one “box.” We also want that “box” to have special “buttons” (like “heal” or “add gold”) that automatically change *that* player’s stats.

That’s exactly what Java’s **class** feature will let us do. But let’s build it slowly so it’s not mysterious.

---

### 3.2 Step 1: An Empty "Container" Called `Player`

Let's start with the most basic version of this feature. Here's the smallest possible container we can make:

```java
public class Player {
    // We'll fill details in soon!
}
```

- **`public class Player`** — This line starts defining our container
- The `{ }` braces mark what belongs inside it

This might look empty and useless, but we've just done something powerful: we've created a new *type* in Java. Just like `int` lets us create numbers and `String` lets us create text, `Player` will let us create... well, players! We'll fill in what that means exactly, but the key idea is there: Java lets us create our own types to represent anything we need in our programs.

Right now our container is empty—like an empty box. It compiles, but doesn't hold anything yet. Let's fix that next.

---

### 3.3 Step 2: Putting Variables Inside That Box

Remember how we used to write:

```java
int playerHealth;
int playerGold;
```

in our `main` method? Instead of having these floating around separately, we can put them *inside* our container:

```java
public class Player {
    // These belong to the Player now
    int health;
    int gold;
}
```

This is like saying "every Player has their own health and gold." When we create a Player (using `new Player()`), Java sets aside space for both variables. They'll start at 0 by default, which isn't great—we usually want to pick starting values like `(10, 50)`. We'll fix that next, but first appreciate what we've done: we've moved from separate, floating variables to a single container that keeps related data together.

---

### 3.4 Step 3: Setting Initial Values

Remember how our variables defaulted to 0? That's not great for a game—we want to choose starting values. If this was a method, we'd write something like:

```java
public static Player createPlayer(int startHealth, int startGold) {
    // ... somehow make a Player with these values ...
}
```

Since creating objects with initial values is something we do constantly, Java gives us special syntax for it—a shorter, cleaner way to write this common task:

```java
public class Player {
    int health;
    int gold;

    // Like createPlayer, but special syntax!
    // Constructor syntax:
    // 1. Same name as the class
    // 2. No return type (not even void) (implicitly returns an value of type Player)
    // 3. public ClassName(parameters) { ... }
    public Player(int startHealth, int startGold) {
        health = startHealth;  // set this Player's health
        gold   = startGold;    // set this Player's gold
    }
}
```

Now instead of calling `createPlayer(10, 50)`, we write:

```java
Player p = new Player(10, 50);
```

What happens when you write `new Player(10, 50)`?

1. `new` tells Java to create space in memory
2. Java fills that space with default values (0 for numbers)
3. The constructor runs to set up the object properly
4. You get back a reference to your new Player

Let's break down what `new Player(10, 50)` means:

- `new` tells Java "create space for a fresh Player" (allocate memory)
- `Player(10, 50)` says "use these values to initialize it" (set values for the newly allocated memory)

This special method is called a **constructor**. You might wonder: "Doesn't it return a Player?" It does, but Java's grammar treats constructors specially—they implicitly return the new object without needing a return type. That's why:

1. The name matches the class (`Player`)
2. There's no return type (Java handles that for us)

You'll see this pattern everywhere in Java:

```java
String name = new String("Alice");      // Make new String with "Alice"
Scanner input = new Scanner(System.in); // Make new Scanner reading System.in
```

The constructor tells Java "when someone asks for a new Player, here's how to set it up." Much better than default 0s!

---

### 3.5 Step 4: Adding "Operations" for That Player

Remember how we wrote methods before? Each had a return type (like `int` or `void`) and parameters in parentheses. We'll do the same here, but inside our class:

Why not just use static methods? Let's compare approaches:

```java
// Static approach - explicitly pass everything
public static void healPlayer(int currentHealth, int healAmount) {
    currentHealth += healAmount;
}

// Instance method approach - data comes along automatically!
public void heal(int amount) {
    this.health += amount;  // 'this' refers to current Player
}
```

The instance method might look simpler, but what's really happening? When you write:

```java
player1.heal(5);
```

Java secretly translates this to something like:

```java
// What Java effectively does behind the scenes
heal(player1's data bundle, 5);
```

That's what `this` means in an instance method—it's a reference to "the object we're calling this method on." So:

```java
public void heal(int amount) {
    this.health += amount;  // explicitly say "this object's health"
}
```

is the same as:

```java
public void heal(int amount) {
    health += amount;      // 'this.' is implicit
}
```

The instance method approach is:

1. More intuitive ("tell the player to heal")
2. Safer (data bundle stays together)
3. Less typing (no need to pass every field)

Much better than juggling separate variables and explicit parameters!

```java
public class Player {
    int health;
    int gold;

    // ...constructor as before...
    public Player(int startHealth, int startGold) {
        health = startHealth;
        gold   = startGold;
    }

    // Much better: the method is right next to the data it changes
    public void heal(int amount) {
        health += amount;  // directly use this Player's health!
    }

    public void addGold(int amount) {
        gold += amount;    // same for gold
    }
}

// Usage is cleaner and safer:
Player p = new Player(10, 50);
p.heal(5);  // can't mix up which health we're changing!
```

### The 'this' Keyword: Who Am I?

When writing instance methods, you might wonder: "How does Java know which Player's health to change?" The answer is the `this` keyword.

```java
public class Player {
    int health;
    // ...other fields...

    public void heal(int health) {  // Uh oh, parameter named same as field!
        health = health;    // Which health is which? 😕
    }

    // Better: use 'this' to be clear
    public void heal(int health) {
        this.health = health;  // "THIS object's health = parameter health"
    }
}
```

When you call `player1.heal(5)`, Java secretly passes `player1` to the method as `this`. You can think of it like:

```java
// What you write:
player1.heal(5);

// What Java effectively does:
heal(player1, 5);  // player1 becomes 'this' inside the method
```

The `this` keyword is especially useful when:

1. Parameter names match field names (like above)
2. You need to pass the current object to another method
3. You want to be extra clear about which variable you're using

Usually you can skip writing `this.` (it's implicit), but it's there if you need it!

---

### 3.6 Using Our New Type

Let's add a `main` method right to our `Player` class to try it out:

```java
public class Player {
    int health;
    int gold;

    // Constructor and instance methods as before
    public Player(int startHealth, int startGold) {
        health = startHealth;
        gold = startGold;
    }

    public void heal(int amount) {
        health += amount;
    }

    public void addGold(int amount) {
        gold += amount;
    }

    // Let's test our Player right here!
    public static void main(String[] args) {
        // Make a new Player named "p1"
        Player p1 = new Player(10, 50);

        // Tell p1 to perform actions
        p1.heal(5);      // "Hey p1, heal by 5"
        p1.addGold(10);  // "Hey p1, add 10 gold"

        // Look at p1's current state
        System.out.println("p1 health: " + p1.health); // 15
        System.out.println("p1 gold: " + p1.gold);     // 60

        // We can make many players!
        Player p2 = new Player(20, 100);  // different player, different stats
        p2.heal(10);  // only affects p2's health
    }
}
```

Look how natural this is:

1. `new Player(10, 50)` creates a fresh Player with starting values
2. `p1.heal(5)` tells *that specific Player* to heal itself
3. Each Player keeps track of its own stats

Now that we've seen it in action, let's give these ideas their proper names:

- A Player we create (like `p1` or `p2`) is called an **object** or **instance**
- The methods inside Player (like `heal`) are called **instance methods** because they work on a specific instance
- The setup code (like `Player(10, 50)`) is called a **constructor**

Think of it like this: You wrote a recipe (`Player` class), and now you can bake as many cookies (`Player` objects) as you want. Each cookie has its own ingredients (health/gold), but they all follow the same recipe!

---

### 3.7 One Blueprint, Many Objects

Think about how games like Minecraft work:

```java
// Define the blueprint once
public class Player {
    int health;
    int gold;
    // ...constructor and methods as before...
}

// Create many different players from it
Player steve = new Player(20, 0);    // Steve starts with 20 health, 0 gold
Player alex  = new Player(20, 100);  // Alex starts with 20 health, 100 gold
```

When `steve.heal(5)` runs, it only changes Steve's health. Alex's stats stay the same. Each object is independent, just like:

- One house blueprint → many different houses
- One recipe → many different cookies
- One character class in a game → many different players

When we say `Player p1 = new Player(...)`, we say p1 is an "instance" of that class. That's just fancy talk for "a house built from the blueprint." No big mystery!

The class is just the instructions ("Players have health and gold"). The objects are the actual things we create using those instructions. That's why we say "class is the blueprint, objects are the houses."

---

### 3.8 Putting It All Together

Let's see how all the pieces work together. Here's our complete `Player` class:

```java
public class Player {
    // Part 1: The Data
    // Every Player object gets its own copy of these
    int health;
    int gold;

    // Part 2: The Setup
    // How to create a new Player with starting values
    public Player(int startHealth, int startGold) {
        health = startHealth;
        gold = startGold;
    }

    // Part 3: The Actions
    // Things this Player can do
    public void heal(int amount) {
        health += amount;
    }

    public void addGold(int amount) {
        gold += amount;
    }

    // Part 4: Testing it out
    public static void main(String[] args) {
        Player hero = new Player(10, 50);   // Create hero: health=10, gold=50
        hero.heal(5);                       // hero's health: 10 → 15
        
        Player enemy = new Player(20, 100); // Create enemy: health=20, gold=100
        enemy.heal(10);                     // enemy's health: 20 → 30
                                           // (doesn't affect hero's health!)
    }
}
```

The magic is in how it all fits together:

1. Create objects using the blueprint (`new Player(...)`)
2. Each object gets its own variables (`health`, `gold`)
3. Methods work on the object you call them on (`hero.heal(5)` vs `enemy.heal(10)`)

No more "which health am I changing?" Everything belongs to a specific Player!

---

### 3.9 Practice and Next Steps

**One Last Thing**: Notice how anyone can write `p1.health = -999;`? That's not great—players shouldn't have negative health! If our game allows negative health, that could cause weird glitches like invincible players or healing that kills you. We'll fix this by making variables `private`, letting only the `Player` class control how they change:

```java
public class Player {
    private int health;  // Only Player methods can touch this now
    private int gold;    // This too!
    
    // Methods control how these values change
    public void heal(int amount) {
        if (amount > 0) {  // Only allow positive healing
            health += amount;
        }
    }
}
```

But first, let's practice what we've learned:

### Practice 1: Extend the Player

Add experience points to track player progress:

```java
public class Player {
    int health;
    int gold;
    int xp;      // New!

    public Player(int startHealth, int startGold, int startXp) {
        health = startHealth;
        gold = startGold;
        xp = startXp;
    }

    public void gainXp(int amount) {
        xp += amount;
    }

    public static void main(String[] args) {
        Player p = new Player(10, 50, 0);
        p.gainXp(20);  // gained some XP!
        System.out.println("XP: " + p.xp);  // prints 20
    }
}
```

### Practice 2: Create a Monster

Try creating a completely different type:

```java
public class Monster {
    int health;
    String name;

    public Monster(int startHealth, String startName) {
        health = startHealth;
        name = startName;
    }

    public void takeDamage(int dmg) {
        health -= dmg;
    }

    public static void main(String[] args) {
        Monster dragon = new Monster(100, "Dragon");
        Monster goblin = new Monster(20, "Goblin");
        
        dragon.takeDamage(25);  // dragon: 100 → 75
        goblin.takeDamage(10);  // goblin: 20 → 10
    }
}
```

If you can write these, you've got the basics! Next up:

- Making variables `private` for safety
- Adding methods to read values (`getHealth()`)
- Learning about references and object memory

See you in the next chapter!
