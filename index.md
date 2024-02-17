One-Shot Maze-Solving with Meta-Interpretive Learning
=====================================================

Here's how to learn a maze-solving program with Louise, a Meta-Interpretive
Learning (MIL) system. This demo can be considered as one-shot or zero-shot
learning, depending on how you look at it. The learned program is capable of
solving any maze created with the _recursive backtracker_ algorithm (a
randomised version of depth-first search).

Maze representation
-------------------

We represent a maze as a Prolog list-of-lists where each sub-list is a row in a
grid of map tiles and each element is a tile in the grid. We store the map as
the third argument of a Prolog term `maze/3`, like this:

```Prolog
 maze(tessera_1,
      7-7,
      [ [s, f, f, w, f, f, f],
        [w, w, f, w, f, w, f],
        [f, w, f, w, f, w, f],
        [f, w, f, w, w, w, f],
        [f, w, f, w, f, f, f],
        [f, w, f, w, f, w, f],
        [f, f, f, f, f, w, e]
      ]).

```

The first argument of `maze/3` is an identifier for the map and the second
argumen are the `x` and `y` dimensions of the map, so we don't have to
re-calculate them each time.

Tiles are textual constants: `f, w, s, e`, that stand for floor, wall, start and
exit tiles, respectively. All but wall tiles (`w`) are passable, meaning an
agent can move over them in trying to find the exit to the maze.
