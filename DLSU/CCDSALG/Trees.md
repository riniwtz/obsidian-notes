### Trees
- A **tree** is a connected, acyclic (no cycle), undirected graph.
- A **free tree** is also referred to as a **Tree**.
- A **forest** is an undirected graph that is acyclic but possibly disconnected.
- A forest can also be defined as a set of disjoint trees.

### Rooted and Ordered Trees
- A **rooted tree** is a free tree where one vertex/node is distinguished from others.
  - The distinguished vertex is known as the **root node**.
  - In a rooted tree, the remaining nodes are divided into $$n \ge 0$$ disjoint sets ($$T_1, T_2, ..., T_n$$), where each set is a tree known as a **subtree** of the root.
  - A tree must contain at least one node (the root node).
  - A tree can have no subtrees.
- An **ordered tree** is a rooted tree where the children of each node are ordered.
  - The position of children in an ordered tree is significant.

### Rooted and Ordered Trees - Terms
- **Vertex/Node**: An item of information along with branches to other items.
- **Children of a node**: The roots of the subtrees of a node.
- **Parent of a node**: The immediate root of a node.
- **Siblings**: Children of the same parent.
- **Ancestors of a node**: All nodes along the path from the root to that node.
- **Descendants of a node**: All nodes of the subtrees of a node.
- **Degree of a node**: The number of children/subtrees of a node.
- **Root node**: The only node in a tree with no parent or proper ancestors.
- **Leaf/Terminal/External node**: A node with no children or proper descendants; a node with degree = 0.
- **Non-leaf/Non-terminal/Internal node**: A node with at least one child or descendant; a node with degree not equal to 0.
- **Depth of a node**: The length of the path from the root to that node.
- **Height of a node**: The number of edges on the longest simple downward path from the node to a leaf.
- **Height of a tree**: The height of the root, which is equal to the largest depth of any node in the tree.
- **Degree of a tree**: The maximum degree among all nodes in the tree.
- **Weight of a tree**: The number of leaf nodes in the tree.

### Binary and Positional Trees
- A **binary tree** is a structure defined on a finite set of nodes that either:
  - Contains no nodes.
  - Is composed of three disjoint sets of nodes: a **root node**, a binary tree called its **left subtree**, and a binary tree called its **right subtree**.
- A binary tree is an ordered tree with a degree of at most 2.
- **Empty Tree/Null Tree**: A binary tree that contains no nodes, denoted by NIL.
  - If a subtree is NIL, it means the child is absent/missing.
- **Full Binary Tree**: Each node is either a leaf or has a degree of exactly 2.
- **k-ary Tree**: A positional tree where for every node, all children with labels greater than $$k$$ are missing.
  - A binary tree is a k-ary tree with $$k = 2$$.
- **Complete k-ary Tree**: A k-ary tree where all leaves have the same depth and all internal nodes have degree $$k$$.
  - Number of leaves in a complete k-ary tree of height $$h$$:
    $$
    k^h
    $$
  - Height of a complete k-ary tree with $$n$$ leaves:
    $$
    \log_k n
    $$

### Traversal Strategies
- **Breadth-First Search (BFS)**: Inspects every node on a level starting at the top of the tree and then moves to the next level.
  - In a BFS tree, all inclusion numbers at level $$i$$ are lower than numbers at level $$i+1$$.
- **Depth-First Search (DFS)**: (Implied as the counterpart to BFS, described by the walk operations).

### Tree Walk Operations
- **INORDER-TREE-WALK(x)**:
  1. Recursively calls INORDER-TREE-WALK on the left child of x.
  2. Prints the key of x.
  3. Recursively calls INORDER-TREE-WALK on the right child of x.
  - Worst case time complexity:
    $$
    O(n)
    $$

- **PREORDER-TREE-WALK(x)**:
  1. Prints the key of x.
  2. Recursively calls PREORDER-TREE-WALK on the left child of x.
  3. Recursively calls PREORDER-TREE-WALK on the right child of x.
  - Worst case time complexity:
    $$
    O(n)
    $$

- **POSTORDER-TREE-WALK(x)**:
  1. Recursively calls POSTORDER-TREE-WALK on the left child of x.
  2. Recursively calls POSTORDER-TREE-WALK on the right child of x.
  3. Prints the key of x.
  - Worst case time complexity:
    $$
    O(n)
    $$