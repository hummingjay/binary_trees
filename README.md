
# 0x1D. C - Binary trees

## Learning Objectives


  * What is a binary tree
  * What is the difference between a binary tree and a Binary Search Tree
  * What is the possible gain in terms of time complexity compared to linked lists
  * What are the depth, the height, the size of a binary tree
  * What are the different traversal methods to go through a binary tree
  * What is a complete, a full, a perfect, a balanced binary tree </br>

## MORE INFO

### Data structures

#### Basic Binary Tree

```

/**
 * struct binary_tree_s - Binary tree node
 *
 * @n: Integer stored in the node
 * @parent: Pointer to the parent node
 * @left: Pointer to the left child node
 * @right: Pointer to the right child node
 */
struct binary_tree_s
{
    int n;
    struct binary_tree_s *parent;
    struct binary_tree_s *left;
    struct binary_tree_s *right;
};

typedef struct binary_tree_s binary_tree_t;
```

### Binary Search Tree

```
 typedef struct binary_tree_s bst_t;
```

### AVL

```
typedef struct binary_tree_s avl_t;
```

### Max Binary Heap

```
typedef struct binary_tree_s heap_t;
```

### Print function

To match the examples in the tasks, you are given [this function](https://github.com/holbertonschool/0x1C.c)

This function is used only for visualization purposes. You don’t have to push it to your repo. It may not be used during the correction

## Tasks

### 0. [New node](0-binary_tree_node.c)
Write a function that creates a binary tree node

  * Prototype: binary\_tree\_t \*binary\_tree\_node(binary\_tree\_t \*parent, int value);
  * Where parent is a pointer to the parent node of the node to create
  * And value is the value to put in the new node
  * When created, a node does not have any child
  * Your function must return a pointer to the new node, or NULL on failure </br>

File: [0-binary\_tree\_node.c](0-binary_tree_node.c)
