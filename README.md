# Snake Game in C++

This project is a simple text-based Snake game written in C++. The game features a snake that moves around a 9x9 grid, collecting food ('o'), growing in size, and avoiding collisions. The player controls the snake's direction using the arrow keys and can adjust the speed of the game.

## Table of Contents
- [Features](#features)
- [How to Run](#how-to-run)
- [Gameplay Instructions](#gameplay-instructions)
- [Code Explanation](#code-explanation)
- [License](#license)

## Features
- A 9x9 grid representing the game board.
- Movement controls for the snake using arrow keys (`up`, `down`, `left`, `right`).
- Collect food ('o') to increase the snake's length and score.
- Adjustable game speed using `w` (increase speed) and `s` (decrease speed).
- Score and speed displayed on the screen.

## How to Run

1. Navigate to the project directory:
   ```bash
   cd snake-game-cpp
   ```
2. Compile the code using a C++ compiler:
   ```bash
   g++ -o snake_game snake_game.cpp
   ```
3. Run the game:
   ```bash
   ./snake_game
   ```

## Gameplay Instructions
- Use the arrow keys (`↑`, `↓`, `←`, `→`) to control the snake's movement.
- The snake will grow longer each time it eats food ('o').
- The score will increase by 10 points each time the snake eats food.
- The game speed can be adjusted during gameplay by pressing the `w` key to increase the speed or `s` key to decrease it.
- The game ends if the snake collides with itself or the edges of the board.

## Code Explanation

### Libraries

```cpp
#include <iostream>
#include <conio.h>
#include <algorithm>
#include <string>
#include <windows.h>
#include <stdio.h>
```

- **`#include <iostream>`**: Includes the standard input-output stream library for handling output to the console and user input.
- **`#include <conio.h>`**: A library used for console input-output operations such as capturing key presses (`_kbhit()` and `_getch()`).
- **`#include <windows.h>`**: Used to access Windows-specific functions like `Sleep()` to control the speed of the game (game loop delay).
- **`#include <stdio.h>`**: Includes standard input/output functions, like `printf`, though it's not heavily used in the code.

### Main Game Variables

```cpp
char f[9][9] = {
    {' ', ' ', ' ', ' ', ' ', ' ', ' ', ' ', ' '},
    {' ', ' ', ' ', ' ', ' ', ' ', ' ', ' ', ' '},
    {' ', ' ', ' ', ' ', ' ', ' ', ' ', ' ', ' '},
    {' ', ' ', ' ', 'r', 'r', 'r', ' ', ' ', ' '},  // Snake body (initially three parts)
    {' ', ' ', ' ', ' ', ' ', ' ', ' ', ' ', ' '},
    {' ', ' ', ' ', ' ', ' ', ' ', ' ', ' ', ' '},
    {' ', ' ', ' ', ' ', ' ', ' ', ' ', ' ', ' '},
    {' ', ' ', ' ', ' ', ' ', ' ', ' ', ' ', ' '},
    {' ', ' ', ' ', ' ', ' ', ' ', ' ', ' ', ' '}
};
```

- **`f[9][9]`**: A 2D array representing the game board. It's a 9x9 grid where:
  - `' '` represents an empty space.
  - `'r'` represents a part of the snake's body.
  - `'o'` represents food that the snake can eat.
  
The initial snake body is represented by three `'r'` characters starting at coordinates (3,4), (3,5), and (3,6) on the board.

### Functions

#### `printBoard`

```cpp
void printBoard(char board[9][9]) {
    std::cout << ' '; for (int i = 0; i < 17; i++) { std::cout << '_' ; }std::cout << std::endl;
    for (int i = 0; i < 9; i++) {
        std::cout << '|';
        for (int j = 0; j < 9; j++) {
            std::cout << board[i][j] << " ";
        }std::cout << '|';
        std::cout << std::endl;
    }
    std::cout << ' '; for (int i = 0; i < 17; i++) { std::cout <<'-'; }std::cout << std::endl;
}
```

- **`printBoard`**: This function prints the game board to the console. It loops through the 2D array `board` and displays the grid with vertical borders (`|`) and horizontal separators (`-` and `_`).

### Main Game Loop

The game begins by initializing the board and setting the snake's initial position. The game loop continuously runs, updating the game state based on the player's input and checking for collisions or food collection.

```cpp
int x, y, a, b, e;
e = 0;  // This indicates if food has been eaten
a = 3;  // Initial x-coordinate of the snake head
b = 5;  // Initial y-coordinate of the snake head
f[a][b] = 'r';  // Snake's head position
int wert = 0;  // Player's score
```

- **`x, y, a, b`**: These variables keep track of the snake's head position on the grid.
- **`wert`**: This variable holds the player's score. It increments when the snake eats food.

### Snake Movement and Input

The snake moves using the arrow keys, and the movement is handled by checking the player's input:

```cpp
if (ki == 80) { // Down Arrow Key
    a++; // Move down
    if (a > 8) a = 0; // Wrap around if the snake reaches the bottom
    f[a][b] = 'd'; // Mark the new snake head position as 'd'
    // Other logic follows...
}

if (ki == 72) { // Up Arrow Key
    a--; // Move up
    if (a < 0) a = 8; // Wrap around if the snake reaches the top
    f[a][b] = 'u'; // Mark the new snake head position as 'u'
    // Other logic follows...
}
```

- **Movement keys**:
  - **Down Arrow (`ki == 80`)**: Moves the snake down.
  - **Up Arrow (`ki == 72`)**: Moves the snake up.
  - **Left Arrow (`ki == 75`)**: Moves the snake left.
  - **Right Arrow (`ki == 77`)**: Moves the snake right.
  
When the snake moves, it places the new head in the appropriate direction (using 'd', 'u', 'r', 'l' for down, up, right, and left respectively) and updates the grid. The body of the snake follows behind.

### Eating Food and Growing

When the snake moves to a grid position that contains food (`'o'`), the score increases, and the snake grows by adding a new part to its body.

```cpp
if (f[a][b] == 'o') {
    e = 1; // Food is eaten
    wert += 10; // Increase score by 10 points
}
```

After the snake eats food, a new piece of food is randomly placed on the grid.

### Speed Adjustment

The player can adjust the game speed during the game by pressing the `w` (increase speed) or `s` (decrease speed) keys. The speed is controlled by the `Sleep()` function.

```cpp
if (ki == 's') {
    if (speed < 300) speed += 20;  // Decrease delay (increase speed)
} 
if (ki == 'w') {
    if (speed > 50) speed -= 20;  // Increase delay (decrease speed)
}
```

### Game End Condition

The game continues as long as the snake doesn't collide with itself. If a collision happens, the game will stop and the player can restart.

```cpp
if (z > 200) goto neu; // If the snake doesn't move correctly after 200 iterations, restart
```

### Conclusion

- **Main Loop**: The game continuously checks for key presses, updates the game state (movement, food, score), and renders the updated board. 
- **Control**: The user controls the snake's movement using the arrow keys, and can adjust the speed of the game with the `w` and `s` keys.
- **Wrap-around**: The snake can wrap around the grid (i.e., when it goes off one edge, it appears on the opposite edge).

## License
This project is open-source and licensed under the MIT License.
