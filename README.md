# Space Invaders — Design Patterns Edition

A Java implementation of the classic Space Invaders arcade game, built as a software design patterns showcase. The game features selectable difficulty levels, a live scoreboard, an undo system, and cheat codes — all driven by Singleton, Observer, Memento, Builder, Factory, Strategy, and State patterns.

---

## What It Does

Defend against waves of alien invaders using your ship. Shoot projectiles to destroy enemies before they reach you. Use cheat codes to clear threats instantly, or undo your last shot if things go sideways.

---

## Prerequisites

- Java 17+
- Gradle (or use the included `gradlew` wrapper — no installation needed)

---

## How to Run

```bash
cd Invader_A3_Codebase
./gradlew clean build run
```

On Windows:

```bat
gradlew.bat clean build run
```

---

## Controls

| Key / Button | Action |
|---|---|
| Arrow keys / WASD | Move your ship |
| Space | Shoot |
| `U` | Undo last shot (restores previous game state) |
| `1` | Cheat — delete all slow projectiles |
| `2` | Cheat — delete all fast projectiles |
| `3` | Cheat — delete all slow enemies |
| `4` | Cheat — delete all fast enemies |
| Difficulty buttons | Change difficulty at start or mid-game |

---

## Features

### Difficulty Levels
Select a difficulty at the start of the game or change it at any time using the on-screen buttons. `DifficultyManager` (Singleton) ensures a single consistent difficulty state throughout.

### Score & Time Tracking
A live scoreboard tracks your score in real time. The `ScoreBoard` (ConcreteObserver) updates automatically whenever the game state changes via the Observer pattern.

### Undo System
The game saves a snapshot every time the player fires. Press `U` to restore the previous state. Powered by the **Memento** pattern — `GameEngine` acts as the Originator, `Caretaker` manages the history.

### Cheat Codes
Instantly remove specific types of enemies or projectiles from the field using keys `1`–`4`.

### Enemy & Bunker Construction
Enemies and bunkers are assembled using the **Builder** pattern (`EnemyBuilder`, `BunkerBuilder`, `Director`), allowing flexible construction of game objects.

### Projectile System
Projectiles are created via a **Factory** pattern (`PlayerProjectileFactory`, `EnemyProjectileFactory`) and move according to a **Strategy** pattern (`SlowProjectileStrategy`, `FastProjectileStrategy`, `NormalProjectileStrategy`).

### Bunker States
Bunkers degrade through hit states using the **State** pattern (`GreenState`, `YellowState`, `RedState`), giving visual feedback as they take damage.

---

## Design Patterns Reference

| Pattern | Classes |
|---|---|
| Singleton | `DifficultyManager`, `GameWindow` |
| Observer | `Observer`, `Subject`, `ScoreBoard`, `GameEngine` |
| Memento | `Memento`, `Caretaker`, `GameEngine` |
| Builder | `EnemyBuilder`, `BunkerBuilder`, `Director` |
| Factory | `ProjectileFactory`, `PlayerProjectileFactory`, `EnemyProjectileFactory` |
| Strategy | `ProjectileStrategy`, `SlowProjectileStrategy`, `FastProjectileStrategy`, `NormalProjectileStrategy` |
| State | `BunkerState`, `GreenState`, `YellowState`, `RedState` |

---

## Project Structure

```
Invader_A3_Codebase/
├── build.gradle
└── src/main/java/
    ├── App.java                      # Entry point
    ├── GameEngine.java               # Core game loop (Originator + ConcreteSubject)
    ├── GameWindow.java               # Singleton window/renderer
    ├── Player.java                   # Player entity
    ├── Enemy.java / EnemyBuilder.java
    ├── Bunker.java / BunkerBuilder.java / BunkerState.java
    ├── Projectile.java / *Factory.java / *Strategy.java
    ├── ScoreBoard.java               # Observer-based score display
    ├── DifficultyManager.java        # Singleton difficulty controller
    ├── Memento.java / Caretaker.java # Undo system
    ├── Menu.java                     # Difficulty selection screen
    └── ...                           # Supporting entities and utilities
```
