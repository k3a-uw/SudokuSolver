SudokuSolver
============

An intelligent NxN Sudoku Solver

Overview
--------

The intelligent NxN Sudoku Solver will allow a user to select the size of a 
Sudoku Board (the standard size is 3x3 but any NxN will work.) The system will
allow a user to input any number of starting integers into the board, or allow
the system to generate one randomly.  The system will then present the user the
option to solve the puzzle on their own, or let the system solve it for them.

Method
-------
A brute force method can be used for 3x3 and 4x4 sized boards.  However, the
search space grows exponentially and begins to take far too long to solve for
n > 4.  To solve this problem an intelligent design must be implemented.

### Brute Force
The brute force approach is simple.  Start in square 0,0 and attempt to place a 
the first integer. (Typically a 1) if it can be placed.  Place it and move on to
square 0,1 and try and place the next integer.  If a square is reached and no
integers can be placed, the square is emptied and the next possible integer is
placed.  This is a recursive process.

### Cell Confidence
Using a confidence measurement for each cell, the system can solve the puzzle
much like a human would.  The algorithm will look at each cell and calculate how
many options exist for populating that cell.  The cells are then ordered by
descending confidence levels (any 100% confidences played together).  New levels
are then calculated and the process repeats.  If any play is made that results
in a stuck board, (no moves available) previously played pieces are removed.
This too is a recusive process.

Considerations from HCI
-----------------------
The articles provided for our reading this week altered my decision making only
slightly.  I chose this problem as it is one that I have been thinking about for
some time and have already completed a brute force algorithm for it.  The UI is
non-existent and therefore the algorithm provides little value to the public.
The algorithm was implemented in Java 6 and could be exposed to the web using
.jsp.  The complexity of webdesign using Java as it was described in Plat_forms
led me to the conclusion that I had better implement this tool in PHP.

MVC Framework
---------
### Model
The model will consist of several PHP classes:
1. SudokuBoard
2. SudokuCell
3. SudokuMove*
4. CellConfidence*

 *Simple Data Structure
 
### View
The view will be constructed using BootStrap 3.2.0.  Some helper classes may
be constructed to draw certain aspects of the page.  There will be several
containers that will be place holders for results of AJAX Calls.
1. ViewBoard
2. ViewCell
3. ViewStatus
4. ContainerBoard
5. ContainerStatus

### Controller
The controller will very simple, as there aren't very many ways to manipulate
the model of a simple Sudoku puzzle.  Essentially be a series of AJAX calls to
check certain moves or to update the board as the solver works to solve the
problem.
1. SendMove
2. UpdateBoard
3. UpdateStatus

Folder Structure
----------------
root/

--bootstrap-3.2.0-dist/  [includes bootstrap framework]

----css/

----fonts/

----js

--src/

----class/    [includes all class files]

----ajax/     [includes all ajax response files]
