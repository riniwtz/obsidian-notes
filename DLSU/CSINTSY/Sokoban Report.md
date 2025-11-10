

## Board Instantiation
It first starts with instantiating a Board which accepts the width, height, mapData, and itemsData, it has the capability to set the board. 

The values in the board ranged from 0 - 6, which maps the mapData and itemData symbols to these numbers.

| Number | Symbol | Description    |
| ------ | ------ | -------------- |
| 0      |        | empty space    |
| 1      | @      | player         |
| 2      | $      | box            |
| 3      | .      | goal           |
| 4      | #      | wall           |
| 5      |        | box on goal    |
| 6      |        | player on goal |

## Visited and Deadlocked Sets

## Zobrist Instantiation

## A* Implementation
The implementation starts with a Node Default Minimum Heap PriorityQueue which compares T cost for getting the lowest T cost of the node for pathfinding. If a tie-breaker was occurred then it will just continue polling from the nodes in the set.

It then computes the starting hash for the player position and box position of the board which will then be used for the instantiation of the a State that accepts the box, and player position, and the hash.

The box positions, and the board will then be used to calculate the heuristics that starts off as a Node.

## Heuristic Computation





----
- [ ] `board.setBoard()` to `board.initBoard()` (SokoBot::167)
- [ ] `setBoard()` has two `for` loops for iterating over the board. Can be simplified to one pass loop. The method implementation seems unclear.
- [ ] `Zobrist::initialize` must accept `width` and `height` instead of `rows` and `cols` respectively. (Zobrist::8)
- [ ] 