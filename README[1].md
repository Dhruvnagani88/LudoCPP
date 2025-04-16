# 🧩 Ludo Game in C++

A complete console-based **Ludo game** made in **C++** using basic arrays, structures, control statements, and logical game mechanics. This project allows up to **4 players** to play a colorful and interactive Ludo game right in the terminal.

---

## 🧬 Project Summary

This project simulates the classic board game **Ludo**, with every rule and condition implemented carefully:
- Players: Red, Green, Yellow, Blue
- Dice mechanics
- Token movement and turns
- Knockouts and safe zones
- Final home path
- Winning condition

The game board is drawn using characters and Unicode symbols, and is updated dynamically to reflect player moves.

---

## 🎮 Key Features

- 🎲 Realistic **dice rolling** using `rand()`
- 🔢 **Up to 4 players** can play simultaneously
- 🟩 **Safe zones** and home area logic
- 🎯 **Winning condition** based on all 4 tokens reaching home
- 🔁 **Extra turn** on rolling a 6
- 💢 **Knockout** opponent pieces
- 🎨 **Color-coded board** for better visuals
- 🧼 Input validation to prevent crashes
- 📏 Board layout: **11x11 grid** with Ludo pathways

---

## 🚀 Compilation & Execution

To compile and run the game:

```bash
g++ ludo.cpp -o ludo
./ludo
```

Ensure your terminal supports ANSI escape codes for color rendering.

---

## 🕹️ Game Controls

- Dice rolls automatically on each player's turn.
- You select which token (1 to 4) to move by input.
- Only tokens that are eligible will be allowed to move.

---

## 🧠 Game Mechanics

### 🎲 Dice Rolling

The dice generates a random number between 1 and 6 using:
```cpp
int result = 1 + rand() % 6;
```
If the result is 6, the player gets another turn.

---

### 🏁 Entering the Board
Tokens only enter the board if the dice roll is 6. The logic looks like:
```cpp
if (players[turn][choice - 1].index == -1 && result == 6) {
    players[turn][choice - 1].index = getIndexByTurn(turn);
    players[turn][choice - 1].x = cells[getIndexByTurn(turn)].x;
    players[turn][choice - 1].y = cells[getIndexByTurn(turn)].y;
}
```

---

### 🧍 Token Movement

Once the token is on the board, it moves based on the dice value:
```cpp
while (step > 0) {
    // logic for normal path or final path
    step--;
}
```
If the token reaches its final path, it begins moving toward the center home.

---

### 💥 Knockouts

If a player lands on a cell where another player's token is located (and it's not a safe zone), the other player's token is sent home:
```cpp
if (players[i][j].x == players[turn][choice - 1].x &&
    players[i][j].y == players[turn][choice - 1].y) {
        players[i][j].index = -1;
        players[i][j].x = houses[i][j].x;
        players[i][j].y = houses[i][j].y;
}
```

---

### 🏠 Final Path and Win Logic

Each team has its own final colored path leading to the center. Tokens must move through this path and end exactly on the center cell to count as a win.

A player wins when all 4 of their tokens reach home.

---

## 🧱 Code Structure

### 🔹 Board Initialization
```cpp
void initBoard(char b[SIZE][SIZE]) {
    char newBoard[SIZE][SIZE] = {
        {'r','r',' ','O','O','O','O','g',' ','g','g'},
        ...
    };
    for (int i = 0; i < SIZE; i++) {
        for (int j = 0; j < SIZE; j++) {
            b[i][j] = newBoard[i][j];
        }
    }
}
```
**Purpose**: Prepares the visual layout of the board.

### 🔹 Player Struct
```cpp
struct Player {
    int x, y; // position
    int index; // current index on path
    int team; // 0-3 for R, G, Y, B
    int id; // token number (1-4)
};
```
**Purpose**: Holds data about each token of every player.

### 🔹 Move Logic
Handles movement across normal path and final path.
```cpp
if (isFinalWay(team, index)) {
    // final path movement
}
```

---

## 🧭 Game Loop

The main loop manages turns, handles dice rolls, takes input, and updates the board.
```cpp
while (!isGameOver(players)) {
    int result = rollDice();
    displayCurrent(...);
    int choice = getPlayerInput(...);
    movePlayer(...);
    // check knockout, update board, repeat turn if 6
}
```

---

## 📸 Screenshots

> Terminal render of a running Ludo game with color-coded tokens and board

![Terminal Ludo Preview](preview.png)

---

## 📂 File Organization
```
📦 Ludo-Game/
 ┣ 📜 ludo.cpp         # Main source code
 ┣ 📄 README.md        # Project documentation


---

## 🛡️ Safety & Validations
- Ensures invalid token inputs are rejected
- Prevents moving inactive tokens (not on board)
- Only allows valid movements based on position
- Ensures turn rotation unless 6 is rolled

---

## 👨‍💻 Author

**Urvish Babariya**
- 📧 Email: urvishbabariya06@gmail.com
- 🐙 GitHub: [Urvish2007](https://github.com/Urvish2007)
- 🔗 LinkedIn: [Urvish Babariya](https://www.linkedin.com/in/urvish-babariya-b38180305)

---

## 💡 Future Improvements

- AI bot support for 1-player mode
- GUI-based version using SDL or SFML
- Sound effects and background music
- Save and load game states

---

## 🧾 License

This project is licensed under the **MIT License**.

---

## 🙌 Acknowledgements

Thanks to everyone contributing to open-source Ludo simulations. This version draws inspiration from various terminal-based games.

---

## 📣 Feedback

If you enjoyed this project, please ⭐ it on GitHub and consider contributing! Feel free to open issues or submit pull requests.

---

Enjoy the nostalgic fun of Ludo in your terminal! 🎲

