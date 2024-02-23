Is a specific kind of [[Tree]] data structure where each node can have at most two  nodes as children. The children node are commonly called as right node and left node.

At the computer science area, the binary trees has many application including data storage and retrieval systems, expression evaluation, network routing, compilers, interpreters and many others. Furthermore trees are used to implement algorithms of searching, sorting and graphs.

## Representation of Binary Tree

#### Node structure:
- Data
- Pointer to the left node child
- Pointer to the right node child
![[binarytree.png]]

## Node implementation
#### C example:
```c
struct node {
	int data;
	struct node* left;
	struct node* right;
};
```
#### Java example:
```java
class Node {
	int key;
	Node left, right;
	
	public Node(int item)
	{
		key = item;
		left = right = null;
	}
}
```

## Basic Operations On Binary Tree:
- Inserting an element.
- Removing an element.
- Searching for an element.
- Deletion for an element.
- Traversing an element. There are four (mainly three) types of traversals in a binary tree which will be discussed ahead.
## Auxiliary Operations On Binary Tree:
- Finding the height of the tree
- Find the level of the tree
- Finding the size of the entire tree.
## Applications of Binary Tree:
- In compilers, Expression Trees are used which is an application of binary trees.
- Huffman coding trees are used in data compression algorithms.
- Priority Queue is another application of binary tree that is used for searching maximum or minimum in O(1) time complexity.
- Represent hierarchical data.
- Used in editing software like Microsoft Excel and spreadsheets.
- Useful for indexing segmented at the database is useful in storing cache in the system,
- Syntax trees are used for most famous compilers for programming like GCC, and AOCL to perform arithmetic operations.
- For implementing priority queues.
- Used to find elements in less time (binary search tree)
- Used to enable fast memory allocation in computers. 
- Used to perform encoding and decoding operations.
- Binary trees can be used to organize and retrieve information from large datasets, such as in inverted index and k-d trees.
- Binary trees can be used to represent the decision-making process of computer-controlled characters in games, such as in decision trees.
-  Binary trees can be used to implement searching algorithms, such as in binary search trees which can be used to quickly find an element in a sorted list.
- Binary trees can be used to implement sorting algorithms, such as in heap sort which uses a binary heap to sort elements efficiently.
[source](https://www.geeksforgeeks.org/)

## Some binary tree types:

## Full Binary Tree
Is a tree where each node should have two or no children. In other words, all nodes, except leaf nodes should has two children. It is also known as **Proper Binary Tree**.

![[fullbt.png]]

## Degenerate (or pathological) tree  
In this tree, every node has just one child node. That is considered pathological, because this tree will store data as a [[Linked List]], so it will not enjoy the complexity that trees offer.

![[degeneratetree.png]]
## Skewed Binary Tree
This is an specific type of degenerate trees, where in Skewed binary tree, all nodes should has only one child and each one should be linked at the same side. In other words every child should be on the left or all of them on the right. 

![[skewed1.png]]