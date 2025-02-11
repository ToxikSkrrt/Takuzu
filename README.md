# Takuzu

## Description
This project is a single-player logic puzzle game made in C. You can see the rules below.

## How to use
1) Open a terminal in the "build" folder
2) Type `cmake ..` then `make`
3) Then you can chose to execute 2 versions of the game : one in the terminal (`game_text`) or one in a graphic window (`game_sdl`)

### Terminal version
type `./game_text <filename>` to play a game (the `<filename>` parameter is optionnal, if you don't set a .txt file, you will play the default game).
- Type `w <i> <j>` to put a zero/white at square (i,j)
- Type `b <i> <j>` to put a one/black at square (i,j)
- Type `e <i> <j>` to empty square (i,j)
- Type `z` to undo a move
- Type `y` to redo a move
- Type `r` to restart
- Type `q` to quit
- Type `s <filename>` to save the current game inside a file named `<filename>` 
- Type `h` to display help

You can also play a solver version with `game_solve` :
- type `./game_solve -s <filename_game> <filename_save>` to display a possible solution (if there is at least one) for a game (the game is inside a .txt file). You can also set a second file to save the results in this file.
- type `./game_solve -c <filename_game> <filename_save>` to display the number of possible solutions for a game. You can also set a second file to save the results in this file.

### Graphic version
Type `./game_sdl <filename>` to play a game (the `<filename>` parameter is optionnal, if you don't set a .txt file, you will play the default game).  
You will see 2 types of fruits : watermelons and oranges. Oranges correspond to zero/white and watermelons correspond to one/black.  
Full fruits are immutable squares and sliced fruits are the zeros and ones you set in the game.

- Click on a square to rotate between orange, watermelon or empty.
- Press `z` to undo a move
- Press `y` to redo a move
- Press `r` to restart
- Press `ESCAPE` to quit
- Press `s` to solve the game
- Press `h` to display help

---

## Rules
Given a grid of squares, you must fill it with zeros and ones. Some squares are initially provided as clues and are immutable. You must complete the remaining empty squares, according to the following rules.

Each row and column must contain the same number of zeros and ones.
No row or column may contain three consecutive squares of the same number.
Some game also include an extra rule (named uniqueness), stating that no two rows or two columns may contain the same exact sequence of zeros and ones. (A row and a column can match, though.) But we will not consider ths rule here.

Moreover, we will limit our game to square grid of size 6x6.

This puzzle is known under several names including Takuzu, Tohu-Wa-Vohu, Binairo or Unruly. There are some variations in the symbols used for this game, as for instance X and O letters, white and black colours, though 0 and 1 are the most common symbols used.

You can try this game here : https://www.chiark.greenend.org.uk/~sgtatham/puzzles/js/unruly.html#6x6

By convention, the square in the i-th row and j-th column of the grid is referred to as the coordinate (i,j), and the coordinate (0,0) corresponds to the top left corner (like in matrices).

The squares are stored as an C array in memory using row-major storage.

In summary, the game uses 5 different square states, that can be printed in a terminal as a single character:
- empty (`' '),
- zero/white ('w'),
- one/black ('b'),
- immutable zero/white ('W'),
- immutable one/black ('B'`).

Note that immutable squares are represented with an uppercase character.

## Example
As an example, let's see the instance of the game, considered thereafter as the default game:
```
   012345
   ------
0 | BW   |
1 |      |
2 | W  W |
3 | WB   |
4 |  B  W|
5 |     W|
   ------
```
Hereafter, its solution:
```
   012345
   ------
0 |wBWbwb|
1 |wbbwbw|
2 |bWwbWb|
3 |bWBwwb|
4 |wbBwbW|
5 |bwwbbW|
   ------
```
This text representation will be the one used in our game, and more especially in the game_print() function used by the game_text program.

## Project Architecture
Our project is based on a single library named game library (libgame.a), whose interface is divided into several header files:

- Basic Game Functions: game.h
- Auxiliarry Game Functions: game_aux.h
- Extended Game Functions: game_ext.h
- This interface manipulates an opaque data type, that is the structure game, by means of pointers or const pointers (cgame).

About Const Pointer:

- See also: http://www.geeksforgeeks.org/const-qualifier-in-c/
- See also this more technical discussion: http://stackoverflow.com/questions/8504411/typedef-pointer-const-weirdness

Based on this library, our project will provide several programs, including but not limited to the following:

- game_text: a simple text-based program to play our game in a terminal ;
- game_test: a program with many tests to check the validity of the library functions ;
- game_solve: a program that computes the solution of a given game instance (not yet implemented) ; 
- game_sdl: a program to play our game in graphic mode (based on the SDL library) (not yet implemented).

## References
- https://en.wikipedia.org/wiki/Takuzu
- https://www.chiark.greenend.org.uk/~sgtatham/puzzles/js/unruly.html

---

## Other projects
Check all my projects on this [page](https://github.com/ToxikSkrrt/Projects).
