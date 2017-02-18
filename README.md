# Artificial Intelligence Nanodegree
## Introductory Project: Diagonal Sudoku Solver

# Question 1 (Naked Twins)
Q: How do we use constraint propagation to solve the naked twins problem?  
A: The naked twins problem uses pairs of possible solutions to eliminate those solutions from all other records in the same column or row. Our implementation searches columns first, eliminates any double results and then repeats the same process over the rows.

Stepwise the process is;
1. Locate all the boxes with 2 potential solutions.
2. For each of those boxes, search along the column for boxes with the same value (twin)
3. If there is a match, find all the matches in columns where there is more than two values
4. Eliminate the two solutions from all the matches in 3
5. Repeat the same process for all the rows


# Question 2 (Diagonal Sudoku)
Q: How do we use constraint propagation to solve the diagonal sudoku problem?  
A: The diagonal constraint is an easier solution to add into the solution. Since we already have constraints on rows, columns and 3x3 boxes, we can simply layer on the diagonal constraint before the `units` and `peers` arrays are calculated.

```python
grid = np.array(boxes).reshape(len(rows),len(cols))
diag_units = [grid.diagonal().tolist(),np.rot90(grid).diagonal().tolist() ]

unitlist = row_units + column_units + square_units + diag_units
units = dict((s, [u for u in unitlist if s in u]) for s in boxes)
peers = dict((s, set(sum(units[s],[]))-set([s])) for s in boxes)
```

The `only_once`, `eliminate` and `naked_twins` functions will all use the additional constraint


### Install

This project requires **Python 3**.

We recommend students install [Anaconda](https://www.continuum.io/downloads), a pre-packaged Python distribution that contains all of the necessary libraries and software for this project.
Please try using the environment we provided in the Anaconda lesson of the Nanodegree.

##### Optional: Pygame

Optionally, you can also install pygame if you want to see your visualization. If you've followed our instructions for setting up our conda environment, you should be all set.

If not, please see how to download pygame [here](http://www.pygame.org/download.shtml).

### Code

* `solutions.py` - You'll fill this in as part of your solution.
* `solution_test.py` - Do not modify this. You can test your solution by running `python solution_test.py`.
* `PySudoku.py` - Do not modify this. This is code for visualizing your solution.
* `visualize.py` - Do not modify this. This is code for visualizing your solution.

### Visualizing

To visualize your solution, please only assign values to the values_dict using the ```assign_values``` function provided in solution.py

### Data

The data consists of a text file of diagonal sudokus for you to solve.
