Is a [[Data Structure#Non-Linear|non-linear data structure]] which the elements are stored and organized in a hierarchical way. Each element are called as *node*, where each one can have a parent or/and children nodes. Easy way to navigate or search and only one path between any two node of the tree, are important characteristics of tree data structure.

The first node of tree (the ones that doesn't have any parent) is called the *root*. Including the root each node can have multiple child nodes, and these child nodes can also have their own child nodes recursively.

![[Treedatastructure.png]]
## Basic Terminologies In Tree Data Structure:
- **Parent Node:** The node which is a predecessor of a node is called the parent node of that node. ****{B}**** is the parent node of ****{D, E}****.
- **Child Node:** The node which is the immediate successor of a node is called the child node of that node. Examples: ****{D, E}**** are the child nodes of ****{B}.****
- **Root Node:** The topmost node of a tree or the node which does not have any parent node is called the root node. ****{A}**** is the root node of the tree. A non-empty tree must contain exactly one root node and exactly one path from the root to all other nodes of the tree.
- **Leaf Node or External Node:** The nodes which do not have any child nodes are called leaf nodes. ****{K, L, M, N, O, P, G}**** are the leaf nodes of the tree.
- **Ancestor of a Node:** Any predecessor nodes on the path of the root to that node are called Ancestors of that node. ****{A,B}**** are the ancestor nodes of the node ****{E}****
- **Descendant:** Any successor node on the path from the leaf node to that node. ****{E,I}**** are the descendants of the node ****{B}.****
- **Sibling:** Children of the same parent node are called siblings. ****{D,E}**** are called siblings.
- **Level of a node:*** The count of edges on the path from the root node to that node. The root node has level ****0****.
- **Internal node:** A node with at least one child is called Internal Node.
- **Neighbor of a Node:** Parent or child nodes of that node are called neighbors of that node.
- **Sub-tree**: Any node of the tree along with its descendant.
### Basic Operations on Tree Data Structure:
1. [Height of Tree](https://www.geeksforgeeks.org/depth-n-ary-tree/)
2. [Height and Depth of Node](https://www.geeksforgeeks.org/height-and-depth-of-a-node-in-a-binary-tree/)
3. [Level of a Given Node in Tree](https://www.geeksforgeeks.org/get-level-of-a-node-in-a-binary-tree/)
4. [Search a Node in Tree](https://www.geeksforgeeks.org/search-a-node-in-binary-tree/)
5. [Find the Parent of a Node](https://www.geeksforgeeks.org/find-the-parent-of-a-node-in-the-given-binary-tree/)
6. [Diameter of a Tree](https://www.geeksforgeeks.org/diameter-n-ary-tree/)
7. [Find all Leaf nodes](https://www.geeksforgeeks.org/print-leaf-nodes-left-right-binary-tree/)
8. [Find Siblings of a Node](https://www.geeksforgeeks.org/print-siblings-of-given-node-in-an-n-ary-tree/)
9. [Find Children of a Node](https://www.geeksforgeeks.org/number-children-given-node-n-ary-tree/)
10. [Tree Traversals (Inorder, Preorder and Postorder)](https://www.geeksforgeeks.org/tree-traversals-inorder-preorder-and-postorder/)
### Types of Tree Data Structure:
- [**Binary tree**](https://www.geeksforgeeks.org/types-of-trees-in-data-structures/): In a binary tree, each node can have a maximum of two children linked to it. Some common types of binary trees include full binary trees, complete binary trees, balanced binary trees, and degenerate or pathological binary trees.
- [**Ternary Tree**](https://www.geeksforgeeks.org/ternary-tree/): A Ternary Tree is a tree data structure in which each node has at most three child nodes, usually distinguished as “left”, “mid” and “right”.
- [**N-ary Tree or Generic Tree**](https://www.geeksforgeeks.org/generic-treesn-array-trees/): Generic trees are a collection of nodes where each node is a data structure that consists of records and a list of references to its children(duplicate references are not allowed). Unlike the linked list, each node stores the address of multiple nodes.

