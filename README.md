# Strategy Design Pattern Implementation

## Overview

The **Strategy Design Pattern** defines a family of algorithms (or strategies), encapsulates each one, and makes them interchangeable. This allows the behavior of a class to be changed at runtime without altering the class itself. 

![image](https://github.com/user-attachments/assets/dde79d05-0bc6-4710-8943-78b507005e1e)

This implementation illustrates a scenario where a `DragonSlayer` can employ different strategies to defeat a dragon, demonstrating the flexibility and reusability provided by the Strategy pattern.

---

## Class Diagram Explanation

### **Core Classes**

1. **`DragonSlayer`**:
   - **Purpose**: Represents the hero who slays dragons.
   - **Attributes**:
     - `strategy`: An instance of `DragonSlayingStrategy`, which defines the behavior for slaying the dragon.
   - **Methods**:
     - `DragonSlayer(DragonSlayingStrategy strategy)`: Constructor that initializes the slayer with a specific strategy.
     - `changeStrategy(DragonSlayingStrategy strategy)`: Allows switching to a different strategy at runtime.
     - `goToBattle()`: Executes the current strategy.

---

2. **`DragonSlayingStrategy`** (Interface):
   - **Purpose**: Defines the contract for dragon-slaying strategies.
   - **Methods**:
     - `execute()`: Abstract method implemented by concrete strategies.

---

3. **Concrete Strategies**:
   These classes implement the `DragonSlayingStrategy` interface, providing different algorithms for slaying the dragon:
   - **`MeleeStrategy`**:
     - Strategy for attacking the dragon with melee weapons.
     - Implements the `execute()` method with melee-specific behavior.
   - **`ProjectileStrategy`**:
     - Strategy for attacking the dragon using projectiles.
     - Implements the `execute()` method with projectile-specific behavior.
   - **`SpellStrategy`**:
     - Strategy for attacking the dragon using spells.
     - Implements the `execute()` method with spell-specific behavior.

---

4. **`LambdaStrategy`**:
   - **Purpose**: Represents an advanced implementation of strategies using lambda expressions, simplifying the strategy definition for modern Java programming.

---

5. **`Strategy`** (Enum):
   - **Purpose**: Provides predefined strategies for the dragon slayer.
   - **Attributes**:
     - `dragonSlayingStrategy`: Encapsulates a specific `DragonSlayingStrategy` instance.
   - **Methods**:
     - `execute()`: Executes the encapsulated strategy.
     - `values()`: Returns all possible strategies.
     - `valueOf(String name)`: Retrieves a strategy by its name.

---

6. **`App`**:
   - **Purpose**: Demonstrates the usage of the `DragonSlayer` and strategy classes.
   - **Methods**:
     - `main(String[] args)`: Executes the application logic by initializing a `DragonSlayer` with different strategies and demonstrating runtime strategy switching.

---

### **Relationships**

1. **`DragonSlayer` and `DragonSlayingStrategy`**:
   - `DragonSlayer` depends on a `DragonSlayingStrategy` to define its behavior during battle.

2. **Concrete Strategies and `DragonSlayingStrategy`**:
   - `MeleeStrategy`, `ProjectileStrategy`, and `SpellStrategy` implement the `DragonSlayingStrategy` interface, providing different algorithms.

3. **`Strategy` and `DragonSlayingStrategy`**:
   - The `Strategy` enum encapsulates predefined `DragonSlayingStrategy` implementations.

4. **`LambdaStrategy` and `Strategy`**:
   - Demonstrates how modern lambda-based approaches can be used to simplify the implementation of strategies.

---

## How It Works

1. **Initialization**:
   - A `DragonSlayer` is initialized with a specific strategy, such as `MeleeStrategy`, `ProjectileStrategy`, or `SpellStrategy`.

2. **Behavior Execution**:
   - The `DragonSlayer` executes the `goToBattle()` method, which delegates the behavior to the currently selected strategy's `execute()` method.

3. **Runtime Strategy Switching**:
   - The `changeStrategy()` method allows switching to a different strategy at runtime, enabling dynamic behavior changes.

---

## Example Usage

```java
public class App {
    public static void main(String[] args) {
        DragonSlayer slayer = new DragonSlayer(new MeleeStrategy());
        slayer.goToBattle(); // Output: "With your sword, you strike the dragon down!"

        slayer.changeStrategy(new ProjectileStrategy());
        slayer.goToBattle(); // Output: "You shoot the dragon with your arrows!"

        slayer.changeStrategy(new SpellStrategy());
        slayer.goToBattle(); // Output: "You cast a powerful spell to defeat the dragon!"
    }
}
```

### **Output**
```
With your sword, you strike the dragon down!
You shoot the dragon with your arrows!
You cast a powerful spell to defeat the dragon!
```

---

## Benefits of the Strategy Pattern

1. **Open/Closed Principle**:
   - New strategies can be added without modifying the existing code.
   
2. **Behavior Encapsulation**:
   - Encapsulates different algorithms in their own classes, promoting code clarity and maintainability.

3. **Dynamic Behavior Changes**:
   - Enables switching strategies at runtime, making the system highly flexible.
