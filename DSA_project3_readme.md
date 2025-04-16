# 🧩 Ludo Game in C++

A fully-featured console-based **Ludo Game** implemented in **C++**, bringing the classic board game to life within your terminal window. The project supports up to **4 players**, mimicking real Ludo game mechanics including token movement, knockout, home stretch, dice logic, and turn handling.

---

## 📜 Table of Contents
- [Project Summary](#-project-summary)
- [Features](#-key-features)
- [Game Controls](#-game-controls)
- [Compilation & Execution](#-compilation--execution)
- [Code Structure](#-code-structure)
- [Game Loop Overview](#-game-loop-overview)
- [Key Functionalities](#-key-functionalities)
- [Screenshots](#-screenshots)
- [File Structure](#-file-structure)
- [Author](#-author)
- [Future Improvements](#-future-improvements)
- [License](#-license)
- [Acknowledgements](#-acknowledgements)
- [Feedback](#-feedback)

---

## 🧬 Project Summary

This project aims to replicate the **classic Ludo board game** entirely in C++ using structured programming principles. It's ideal for beginners learning arrays, structures, control flows, and terminal graphics.

Key mechanics implemented:
- Four colored teams: **Red, Green, Yellow, Blue**
- Turn-based dice rolling
- Movement across a board grid
- Knockout mechanism
- Home zone tracking
- Center win condition

---

## 🎮 Key Features

- ✅ 4 Player support
- 🎲 Dice-based movement with `rand()`
- 🏠 Final home stretch handling
- 🛡️ Safe zones on board
- 💢 Knockout of opponent tokens
- 🔁 Extra turn on rolling 6
- 🎨 Color-coded board layout
- 📐 11x11 cell board grid
- 🎯 Game ends when a player's 4 tokens reach home

---

## 🕹️ Game Controls
- Players are prompted for which token (1 to 4) to move.
- Dice rolls are automatic on each player's turn.
- Invalid moves are rejected with prompts.
- Rolling a 6 gives an extra turn.

---

## 🚀 Compilation & Execution

Use the following commands in your terminal:

```bash
g++ ludo.cpp -o ludo
./ludo
```

Ensure the terminal supports ANSI color codes.

---

## 🧱 Code Structure

### 🔹 Player Structure
```cpp
struct Player {
    int x, y;      // Position on the board
    int index;     // Index in movement array (-1 if inactive)
    int team;      // Team ID (0 to 3)
    int id;        // Token ID (1 to 4)
};
```

### 🔹 Game Board
```cpp
char board[11][11];
void initBoard(char b[11][11]);
```
Sets up a symbolic Ludo board with 'r', 'g', 'b', 'y', and 'O' markers.

### 🔹 Token Initialization
```cpp
for (int i = 0; i < MAX_PLAYER; i++) {
    for (int j = 0; j < 4; j++) {
        players[i][j].x = houses[i][j].x;
        players[i][j].y = houses[i][j].y;
        players[i][j].index = -1;
        players[i][j].team = i;
        players[i][j].id = j + 1;
    }
}
```
Initializes player tokens at their house positions.

### 🔹 Dice Function
```cpp
int rollDice() {
    return 1 + rand() % 6;
}
```
Returns a number between 1 and 6.

### 🔹 Movement Logic
```cpp
if (players[turn][choice - 1].index == -1 && result == 6) {
    players[turn][choice - 1].index = getIndexByTurn(turn);
    players[turn][choice - 1].x = cells[...].x;
    players[turn][choice - 1].y = cells[...].y;
}
```
Activates a token if it gets a 6.

---

## 🔁 Game Loop Overview

The main game loop manages the entire gameplay lifecycle:
```cpp
while (!isGameOver(players)) {
    int result = rollDice();
    displayBoard(...);
    int choice = getTokenChoice(...);
    moveToken(...);
    checkKnockout(...);
    if (result != 6) nextTurn();
}
```

---

## 🧠 Key Functionalities

### 🎲 Dice
```cpp
int rollDice() {
    return rand() % 6 + 1;
}
```

### 🧍 Token Movement
```cpp
if (isFinalWay(turn, index)) {
    // Move through final colored path
} else {
    // Move on common path
}
```

### 💥 Knockouts
```cpp
if (players[i][j].x == players[turn][choice - 1].x &&
    players[i][j].y == players[turn][choice - 1].y) {
        // Knock out
}
```

### 🎯 Win Check
```cpp
bool hasWon(Player team[4]) {
    int finished = 0;
    for (auto p : team) {
        if (p.index == FINAL_INDEX)
            finished++;
    }
    return finished == 4;
}
```

---

## 📸 Screenshots

> A terminal view of the game board:

![Preview](preview.png)

---

## 📂 File Structure

```
📦 Ludo-Game/
 ┣ 📜 ludo.cpp         # Game implementation
 ┣ 📄 README.md        # Documentation
 ┗ 🖼️ preview.png      # Game screenshot
```

---

## 📦 Sample Board Rendering
```cpp
void displayCurrent(char board[SIZE][SIZE], Player players[MAX_PLAYER][4]) {
    // Uses escape codes for colors
    for (int i = 0; i < MAX_PLAYER; i++) {
        for (int j = 0; j < 4; j++) {
            // Assign player's ID to board cell
            currentBoard[players[i][j].y][players[i][j].x] = '0' + players[i][j].id;
        }
    }
    // Print board row by row
}
```

---



## 🚧 Future Improvements
- ✅ Add player vs computer mode
- ✅ Implement a GUI version using SFML
- ✅ Game sound support
- ✅ Configurable board sizes
- ✅ Save/Load game states
- ✅ Multiplayer over LAN
- ✅ Improved AI pathfinding for single-player

---

## 🧾 License

This project is licensed under the **MIT License**.

---

## 🙌 Acknowledgements

Inspired by various Ludo console games and programming communities. Special thanks to contributors of open-source board games.

---

## 📣 Feedback

If this project helped you or you enjoyed playing it:
- ⭐ Star it on GitHub
- 📢 Share with friends
- 🛠️ Contribute improvements

---

> "Roll the dice. Trust your move. Knock them all!"

---

Enjoy the nostalgic charm of Ludo
