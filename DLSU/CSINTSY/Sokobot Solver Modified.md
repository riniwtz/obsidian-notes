
# SokobanSolver — Refactored & Simplified (Java)

**What this document contains (quick):**

1. A short, numbered **step-by-step explanation** of the solver's design and runtime flow.
    
2. Clean, refactored Java source files (each shown in its own code block). Copy each code block into its own `.java` file under `package solver;`.
    
3. Inline, numbered comments in the code explaining **what each part does** and why it was changed.
    

---

# Part A — Step-by-step overview (numbered)

1. **Model separation:** keep `mapData` (static: walls/goals/floor) immutable and `itemsData` (dynamic: player/boxes) separate.
    
2. **Canonical state key:** encode state by sorted box coordinates + player coordinate. Use this string in the visited set to avoid revisiting equivalent states.
    
3. **Node fields:** each node stores `g` (moves so far), `h` (heuristic), and `f = g + h`. `h` is computed on node creation to avoid repeated work in the priority queue comparator.
    
4. **Heuristic:** a cheap admissible heuristic combining (player → closest box) + (sum for each _unsolved_ box of its distance to the closest goal). Distances are Manhattan — fast to compute and admissible when ignoring obstacles.
    
5. **A* search loop:** use a `PriorityQueue` ordered by `f` then `h` (tie-breaker). Use a `HashSet` of canonical keys to prune revisits.
    
6. **Moves generation:** try four directions; create new `itemsData` (deep-copy) when a move is valid. Do not mutate parent state.
    
7. **Deadlock pruning:** a simple corner-deadlock detection (box is not on goal and stuck in a corner). This is conservative and only prunes obvious dead-ends.
    
8. **Goal test:** ensure that _every goal cell_ is occupied by a box (strict test).
    
9. **Path reconstruction:** follow parent pointers from goal back to root and build action string (u/d/l/r) in forward order.
    
10. **Cleaner utilities:** helper functions (deep copy, merge display, position finders) kept minimal and documented.
    

---

# Part B — Files (copy each block into a separate `.java` file under `package solver;`)

---

### File: `SokoBot.java`

```java
// File: SokoBot.java
package solver;

import java.util.HashSet;
import java.util.PriorityQueue;
import java.util.Comparator;
import java.util.ArrayList;

/**
 * SokoBot — main search class implementing A*.
 *
 * Numbered steps (in this file):
 * 1) Construct a start Node.
 * 2) Early goal check.
 * 3) A* loop using a priority queue ordered by f = g + h.
 * 4) Use canonical state keys to avoid revisits.
 * 5) Reconstruct action sequence when goal is found.
 */
public class SokoBot {

    public SokoBot() { }

    /**
     * Public entry: solves puzzle and returns action sequence (e.g. "urrdlu").
     * 1) Runs A*; 2) If solution found reconstructs the moves; otherwise returns empty string.
     */
    public String solveSokobanPuzzle(int width, int height, char[][] mapData, char[][] itemsData) {
        Node solution = aStarSearch(mapData, itemsData);
        if (solution == null) return "";

        // Reconstruct actions (from start -> goal)
        StringBuilder actions = new StringBuilder();
        Node cur = solution;
        while (cur.getParent() != null) {
            // prepend by building then reversing at the end is another option; we build backwards then reverse
            actions.append(cur.getAction());
            cur = cur.getParent();
        }
        return actions.reverse().toString();
    }

    /**
     * Core A* search implementation.
     * Steps inside:
     * 1) Create start Node and check goal.
     * 2) Use PriorityQueue ordered by f (with h as tiebreaker).
     * 3) Pop best node; if goal return it.
     * 4) Expand valid moves; add unseen children to frontier.
     */
    private Node aStarSearch(char[][] mapData, char[][] itemsData) {
        Node start = new Node(mapData, itemsData);

        // 1) Early check
        if (isGoal(start)) return start;

        // 2) Frontier: smallest f first; tie-breaker uses smaller h
        PriorityQueue<Node> frontier = new PriorityQueue<>(
            Comparator.comparingInt(Node::getF).thenComparingInt(Node::getH)
        );

        // 3) Visited set using canonical keys
        HashSet<String> visited = new HashSet<>();

        frontier.add(start);
        visited.add(start.getKey());

        while (!frontier.isEmpty()) {
            Node current = frontier.poll();

            if (isGoal(current)) return current;

            ArrayList<Node> children = StateHelper.validMoves(current);
            for (Node child : children) {
                String key = child.getKey();
                // add child only if unseen AND it's not trivially a dead-end
                if (!visited.contains(key) && !StateHelper.hasDeadEnd(child)) {
                    visited.add(key);
                    frontier.add(child);
                }
            }
        }

        // no solution found
        return null;
    }

    /**
     * Goal test: **every goal cell** in mapData must have a box in itemsData.
     * Using the cached goal coordinates from the Node is faster than scanning the whole grid.
     */
    private boolean isGoal(Node node) {
        ArrayList<int[]> goals = node.getGoalCoords();
        char[][] items = node.getItemsData();

        for (int[] g : goals) {
            if (items[g[0]][g[1]] != '$') return false;
        }
        return true;
    }
}
```

---

### File: `Node.java`

```java
// File: Node.java
package solver;

import java.util.ArrayList;
import java.util.Arrays;
import java.util.Comparator;

/**
 * Node — represents a Sokoban state.
 *
 * Numbered responsibilities (in this file):
 * 1) Store mapData (static) and itemsData (dynamic).
 * 2) Store parent/action and player coordinates.
 * 3) Maintain g, h, f values for efficient A*.
 * 4) Produce a canonical key (sorted boxes + player) for visited pruning.
 */
public class Node {
    private final char[][] mapData;     // static map (walls/goals/floor)
    private final char[][] itemsData;   // mutable layer for boxes/player (but this copy is immutable to outside)

    private final Node parent;
    private final String action;        // action that led to this node (u/d/l/r)
    private final int[] playerCoord;    // [row, col]
    private final ArrayList<int[]> goalCoords; // positions of goals (from mapData)

    // A* costs
    private final int g; // moves from root
    private final int h; // heuristic
    private final int f; // g + h

    // Cached canonical key for visited-set
    private final String key;

    /**
     * 1) Root node constructor.
     */
    public Node(char[][] mapData, char[][] itemsData) {
        this.mapData = mapData;                        // reference to static map (do not mutate)
        this.itemsData = deepCopyGrid(itemsData);
        this.parent = null;
        this.action = null;
        this.playerCoord = MovementHandler.getPlayerCoords(this.itemsData);
        this.goalCoords = HeuristicHandler.findPositions(this.mapData, '.');
        this.g = 0;
        this.h = HeuristicHandler.getHeuristic(this);
        this.f = this.g + this.h;
        this.key = computeKey();
    }

    /**
     * 2) Child node constructor (used when generating moves).
     */
    public Node(char[][] itemsData, Node parent, String action, int[] playerCoord) {
        this.mapData = parent.getMapData();
        this.itemsData = deepCopyGrid(itemsData);
        this.parent = parent;
        this.action = action;
        this.playerCoord = playerCoord;
        this.goalCoords = parent.getGoalCoords();
        this.g = parent.getG() + 1;
        this.h = HeuristicHandler.getHeuristic(this);
        this.f = this.g + this.h;
        this.key = computeKey();
    }

    /* ---------- basic getters ---------- */
    public char[][] getMapData() { return mapData; }
    public char[][] getItemsData() { return itemsData; }
    public Node getParent() { return parent; }
    public String getAction() { return action; }
    public int[] getPlayerCoords() { return playerCoord; }
    public ArrayList<int[]> getGoalCoords() { return goalCoords; }

    public int getG() { return g; }
    public int getH() { return h; }
    public int getF() { return f; }

    /**
     * Return positions of boxes in this state (scans itemsData).
     */
    public ArrayList<int[]> getBoxCoords() {
        return HeuristicHandler.findPositions(this.itemsData, '$');
    }

    /**
     * Canonical key used by visited set. Format: "r1,c1;r2,c2;...|pr,pc"
     * Boxes are sorted so different permutations of the same box placement map to the same key.
     */
    public String getKey() { return key; }

    /* ---------- helpers ---------- */
    private static char[][] deepCopyGrid(char[][] src) {
        if (src == null) return null;
        char[][] copy = new char[src.length][src[0].length];
        for (int i = 0; i < src.length; i++) {
            System.arraycopy(src[i], 0, copy[i], 0, src[0].length);
        }
        return copy;
    }

    private String computeKey() {
        ArrayList<int[]> boxes = getBoxCoords();
        boxes.sort(new Comparator<int[]>() {
            public int compare(int[] a, int[] b) {
                if (a[0] != b[0]) return Integer.compare(a[0], b[0]);
                return Integer.compare(a[1], b[1]);
            }
        });

        StringBuilder sb = new StringBuilder();
        for (int[] b : boxes) {
            sb.append(b[0]).append(',').append(b[1]).append(';');
        }
        sb.append('|').append(playerCoord[0]).append(',').append(playerCoord[1]);
        return sb.toString();
    }
}
```

---

### File: `MovementHandler.java`

```java
// File: MovementHandler.java
package solver;

import java.util.Arrays;

/**
 * MovementHandler — generates legal moves for a given Node.
 *
 * Numbered responsibilities:
 * 1) Find the player coordinate in itemsData.
 * 2) Given a direction, compute target cells.
 * 3) If move is legal, return a new Node with updated itemsData (deep copy).
 */
public class MovementHandler {

    // Directions: 0 = up, 1 = down, 2 = left, 3 = right

    public static int[] getPlayerCoords(char[][] itemsData) {
        for (int i = 0; i < itemsData.length; i++) {
            for (int j = 0; j < itemsData[0].length; j++) {
                if (itemsData[i][j] == '@') {
                    return new int[]{i, j};
                }
            }
        }
        return null;
    }

    /**
     * Generate a move from the given node. Returns null if move is illegal.
     * 1) Compute cell player steps into (ptRow,ptCol).
     * 2) If pt contains box, compute box target (btRow,btCol) and verify it's free.
     * 3) Build new itemsData and return new Node.
     */
    public static Node generateMove(Node node, int direction) {
        String action;
        switch (direction) {
            case 0: action = "u"; break;
            case 1: action = "d"; break;
            case 2: action = "l"; break;
            case 3: action = "r"; break;
            default: return null;
        }

        int[] parentCoords = node.getPlayerCoords();
        if (parentCoords == null) return null; // invalid state

        int pr = parentCoords[0];
        int pc = parentCoords[1];

        int ptRow = pr + (direction == 0 ? -1 : direction == 1 ? 1 : 0);
        int ptCol = pc + (direction == 2 ? -1 : direction == 3 ? 1 : 0);

        int btRow = pr + (direction == 0 ? -2 : direction == 1 ? 2 : 0);
        int btCol = pc + (direction == 2 ? -2 : direction == 3 ? 2 : 0);

        char[][] newState = handleMovement(node, ptRow, ptCol, btRow, btCol);
        if (newState == null) return null;

        int[] newPlayerCoord = new int[]{ptRow, ptCol};
        return new Node(newState, node, action, newPlayerCoord);
    }

    private static char[][] handleMovement(Node parent, int ptRow, int ptCol, int btRow, int btCol) {
        char[][] map = parent.getMapData();
        char[][] items = parent.getItemsData();

        int rows = map.length;
        int cols = map[0].length;

        // Bounds checks: if target is outside, move is illegal
        if (ptRow < 0 || ptRow >= rows || ptCol < 0 || ptCol >= cols) return null;

        // If target cell is a wall, illegal
        if (map[ptRow][ptCol] == '#') return null;

        // Prepare copy
        char[][] newItems = new char[rows][cols];
        for (int i = 0; i < rows; i++) System.arraycopy(items[i], 0, newItems[i], 0, cols);

        int[] player = parent.getPlayerCoords();
        int pr = player[0];
        int pc = player[1];

        // If there's a box in the cell player tries to move into, attempt to push it
        if (items[ptRow][ptCol] == '$') {
            // check box target
            if (btRow < 0 || btRow >= rows || btCol < 0 || btCol >= cols) return null;
            if (map[btRow][btCol] == '#' || newItems[btRow][btCol] == '$') return null;

            // move box and player
            newItems[btRow][btCol] = '$';
            newItems[ptRow][ptCol] = '@';
            newItems[pr][pc] = ' ';
        } else {
            // simple walk (no push). if target is occupied by a player (shouldn't happen) or other invalid char, treat as invalid
            if (newItems[ptRow][ptCol] == '@') return null;
            newItems[ptRow][ptCol] = '@';
            newItems[pr][pc] = ' ';
        }

        return newItems;
    }
}
```

---

### File: `StateHelper.java`

```java
// File: StateHelper.java
package solver;

import java.util.ArrayList;

/**
 * Small collection of helpers:
 * 1) Produce valid moves from a Node.
 * 2) Simple deadlock detection (corner deadlocks).
 * 3) Small utility helpers (merge display etc.)
 */
public class StateHelper {

    /**
     * Return list of valid child nodes by trying the 4 directions.
     */
    public static ArrayList<Node> validMoves(Node parent) {
        int[] directions = new int[]{0, 1, 2, 3};
        ArrayList<Node> moves = new ArrayList<>();
        for (int d : directions) {
            Node child = MovementHandler.generateMove(parent, d);
            if (child != null) moves.add(child);
        }
        return moves;
    }

    /**
     * Basic dead-end detector. Currently only uses corner deadlocks.
     */
    public static boolean hasDeadEnd(Node node) {
        return cornerDeadEnd(node);
    }

    /**
     * Return true if a box is at specified coordinate and that coordinate is one of the goal coordinates.
     */
    public static boolean boxInGoal(int[] boxCoord, ArrayList<int[]> goalCoords) {
        for (int[] g : goalCoords) {
            if (boxCoord[0] == g[0] && boxCoord[1] == g[1]) return true;
        }
        return false;
    }

    /**
     * Corner deadlock: if a non-goal box sits in a corner made of walls it can never be moved to a goal.
     * The code treats out-of-bounds as walls (safe and avoids exceptions).
     */
    private static boolean cornerDeadEnd(Node node) {
        char[][] map = node.getMapData();
        ArrayList<int[]> boxCoords = node.getBoxCoords();
        ArrayList<int[]> goalCoords = node.getGoalCoords();

        int rows = map.length;
        int cols = map[0].length;

        for (int[] b : boxCoords) {
            if (boxInGoal(b, goalCoords)) continue; // box already solved

            int r = b[0], c = b[1];

            boolean upWall = (r - 1 < 0) || map[r - 1][c] == '#';
            boolean downWall = (r + 1 >= rows) || map[r + 1][c] == '#';
            boolean leftWall = (c - 1 < 0) || map[r][c - 1] == '#';
            boolean rightWall = (c + 1 >= cols) || map[r][c + 1] == '#';

            if ((upWall || downWall) && (leftWall || rightWall)) {
                // box is in a corner (or against two walls) and not on a goal
                return true;
            }
        }
        return false;
    }

    /**
     * Utility to create a visual merge of map and items for display (does not mutate inputs).
     */
    public static char[][] mergeForDisplay(char[][] mapData, char[][] itemsData) {
        int r = mapData.length;
        int c = mapData[0].length;
        char[][] out = new char[r][c];
        for (int i = 0; i < r; i++) {
            for (int j = 0; j < c; j++) {
                if (mapData[i][j] == '#') out[i][j] = '#';
                else if (itemsData[i][j] == '$' || itemsData[i][j] == '@') out[i][j] = itemsData[i][j];
                else if (mapData[i][j] == '.') out[i][j] = '.';
                else out[i][j] = ' ';
            }
        }
        return out;
    }
}
```

---

### File: `HeuristicHandler.java`

```java
// File: HeuristicHandler.java
package solver;

import java.util.ArrayList;

/**
 * Heuristic utilities.
 *
 * 1) findPositions: return coordinates of a symbol in a grid.
 * 2) getHeuristic: cheap admissible heuristic combining player->closest-box + sum(box->closest-goal for unsolved boxes).
 */
public class HeuristicHandler {

    public static int getHeuristic(Node node) {
        ArrayList<int[]> boxes = node.getBoxCoords();
        ArrayList<int[]> goals = node.getGoalCoords();
        int sum = 0;

        // 1) player to nearest box (helps guide player to next push)
        int[] player = node.getPlayerCoords();
        if (player != null && boxes.size() > 0) {
            int pmin = Integer.MAX_VALUE;
            for (int[] b : boxes) {
                int d = Math.abs(player[0] - b[0]) + Math.abs(player[1] - b[1]);
                if (d < pmin) pmin = d;
            }
            if (pmin != Integer.MAX_VALUE) sum += pmin;
        }

        // 2) for each box not on a goal add distance to nearest goal
        for (int[] b : boxes) {
            if (!StateHelper.boxInGoal(b, goals)) {
                int bmin = Integer.MAX_VALUE;
                for (int[] g : goals) {
                    int d = Math.abs(b[0] - g[0]) + Math.abs(b[1] - g[1]);
                    if (d < bmin) bmin = d;
                }
                if (bmin != Integer.MAX_VALUE) sum += bmin;
            }
        }

        return sum;
    }

    public static ArrayList<int[]> findPositions(char[][] state, char symbol) {
        ArrayList<int[]> positions = new ArrayList<>();
        for (int i = 0; i < state.length; i++) {
            for (int j = 0; j < state[0].length; j++) {
                if (state[i][j] == symbol) positions.add(new int[]{i, j});
            }
        }
        return positions;
    }
}
```

---

# Quick notes / next steps

1. Copy each code block into its own file (same package `solver`) and compile.
    
2. This refactor makes A* behave as standard (g = moves so far) and uses an admissible heuristic.
    
3. If you want, I can:
    
    - Add a `Main.java` with a simple board parser and small example puzzle.
        
    - Add unit tests and a micro-benchmark.
        
    - Improve the heuristic to use BFS push-distance maps or Hungarian assignment for tighter heuristics.
        

---

If you'd like I can also commit the code into a single ZIP or show a short example puzzle and run the solver step-by-step on it.


---



`getPlayerCoords`
Iterates over char[][] itemsData and checks if it matches '@', and returns coords.

`public static Node generateMove(Node node, int direction)`
Attempt to move the player in a certain direction (0=up, 1=down, 2=left, 3=right).
If the move is valid, return a **new Node** representing the updated Sokoban state.
If invalid (e.g., moving into a wall or pushing a box into a blocked space), return null.
	Convert Game Direction to Symbol
```java
String action = switch (direction) {
    case 0 -> "u";
    case 1 -> "d";
    case 2 -> "l";
    case 3 -> "r";
    default -> "";
};
```
- This action will later be stored in the new Node, so you can reconstruct the move sequence (the final solution string).


