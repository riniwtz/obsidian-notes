---

---
---
**Map Mappings**
\# - walls
' ' - empty
. - goals
$ - box
@ - player

---
**My Pseudocode Interpretation**
Since there are multiple target goals, it must find a path to each of the goal. But it must select a box 

---
**Accumulated Lectures**

- **Greedy Best-First Search (GBFS)**

- **Uniform Cost Search (UCS)**

- **Priority Queue**
	- It is a FIFO data structure that serves elements with the highest priorities first before elements with lower priority. It auto-sorts the values per insert. It can also be reversed.

---
**Implementation and Algorithm**
Each cell will be stored in a variable $f$ which is the formula $f=g+h$. The $g$ stands for distance which describes how long it took us to get to that cell, and the $h$ stands for heuristic which is the guess or the estimated distance from current cell to the destination.

Every iteration of the search, there will always be a winner cell and it is called the lowest $F$ score. If you search again and find a cell with a lower $F$ score then that will be the new winner, and this continues until the $F$ score gets to $F=0$. It means that we found the optimal path.


1. Calculate the surrounding nodes of the starting node by getting its $G$ cost, $H$ cost, and the total combined cost.
2. Explore the surrounded node that has the lowest combined total cost.
	1. If there are multiple surrounded nodes that has the same value of combined total cost, then pick out the closest surrounded node to the end node which is the lowest $H$ cost.
	2. If there are multiple surrounded nodes that has the same value of combined total cost, and the same value of $H$ cost then, then those nodes can be chose randomly.
3. Recalculate the surrounding nodes of the explored node.
4. Repeat exploring the surrounded node.


Each cell in a grid is a node. The algorithm begins by calculating the values of the surrounding nodes of the starting node. Each calculated node has fields of $G$ cost, $H$ cost and the total cost combined.

The $G$ cost is the distance from the starting node, while the $H$ cost (heuristic) is the distance from the end node. It then combines the total cost $F(c)=G(c)+H(c)$.


Since this is a state-based algorithm, in this Sokoban game, we will not modify the map data to be an array of nodes, instead we can create a separate array of nodes but this is not yet been tested. There are other ways such as creating functions for checking or identifying the map data, to build the foundational checks of the A* algorithm.



**Code Implementation Outline**
1. Insert the starting node to open set





---

# Rechecking for Better Paths
```java
private void openNode(Node node) {
    if (!node.isOpen() && !node.isChecked() && !node.isSolid()) {
        node.setAsOpen();
        node.setParentNode(currentNode);
        node.setGCost(currentNode.getGCost() + 1);
        node.setHCost(manhattanDistance(node.getCol(), goalNode.getCol(),
                                        node.getRow(), goalNode.getRow()));
        openList.add(node);
    } 
    else if (node.isOpen()) {
        int newG = currentNode.getGCost() + 1;
        if (newG < node.getGCost()) {
            node.setGCost(newG);
            node.setParentNode(currentNode);
        }
    }
}
```

# Dynamic Costs
```java
private void openNode(Node node) {
    if (!node.isOpen() && !node.isChecked() && !node.isSolid()) {
        node.setAsOpen();
        node.setParentNode(currentNode);

        // Dynamic G-cost (cost from start to this node)
        node.setGCost(currentNode.getGCost() + 1);

        // Heuristic H-cost (distance to goal)
        node.setHCost(manhattanDistance(node.getCol(), goalNode.getCol(),
                                        node.getRow(), goalNode.getRow()));

        openList.add(node);
    }
}
```