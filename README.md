
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

```
alex@/tmp/binary_trees$ cat 0-main.c 
#include <stdlib.h>
#include "binary_trees.h"

/**
 * main - Entry point
 *
 * Return: Always 0 (Success)
 */
int main(void)
{
    binary_tree_t *root;

    root = binary_tree_node(NULL, 98);

    root->left = binary_tree_node(root, 12);
    root->left->left = binary_tree_node(root->left, 6);
    root->left->right = binary_tree_node(root->left, 16);

    root->right = binary_tree_node(root, 402);
    root->right->left = binary_tree_node(root->right, 256);
    root->right->right = binary_tree_node(root->right, 512);

    binary_tree_print(root);
    return (0);
}
alex@/tmp/binary_trees$ gcc -Wall -Wextra -Werror -pedantic binary_tree_print.c 0-main.c 0-binary_tree_node.c -o 0-node
alex@/tmp/binary_trees$ ./0-node
       .-------(098)-------.
  .--(012)--.         .--(402)--.
(006)     (016)     (256)     (512)
alex@/tmp/binary_trees$
```

File: [0-binary\_tree\_node.c](0-binary_tree_node.c)

### 1. [Insert left](1-binary_tree_insert_left.c)

Write a function that inserts a node as the left-child of another node

  * Prototype: binary\_tree\_t \*binary\_tree\_insert\_left(binary\_tree\_t \*parent, int value);
  * Where parent is a pointer to the node to insert the left-child in
  * And value is the value to store in the new node
  * Your function must return a pointer to the created node, or NULL on failure or if parent is NULL
  * If parent already has a left-child, the new node must take its place, and the old left-child must be set as the left-child of the new node.

```
alex@/tmp/binary_trees$ cat 1-main.c 
#include <stdlib.h>
#include <stdio.h>
#include "binary_trees.h"

/**
 * main - Entry point
 *
 * Return: Always 0 (Success)
 */
int main(void)
{
    binary_tree_t *root;

    root = binary_tree_node(NULL, 98);
    root->left = binary_tree_node(root, 12);
    root->right = binary_tree_node(root, 402);
    binary_tree_print(root);
    printf("\n");
    binary_tree_insert_left(root->right, 128);
    binary_tree_insert_left(root, 54);
    binary_tree_print(root);
    return (0);
}
alex@/tmp/binary_trees$ gcc -Wall -Wextra -Werror -pedantic binary_tree_print.c 1-main.c 1-binary_tree_insert_left.c 0-binary_tree_node.c -o 1-left
alex@/tmp/binary_trees$ ./1-left
  .--(098)--.
(012)     (402)

       .--(098)-------.
  .--(054)       .--(402)
(012)          (128)                                            
alex@/tmp/binary_trees$
```

File: [2-binary\_tree\_insert\_right.c](2-binary_tree_insert_right.c)

### 3. [Delete](3-binary_tree_delete.c)

Write a function that deletes an entire binary tree

  * Prototype: void binary\_tree\_delete(binary\_tree\_t \*tree);
  * Where tree is a pointer to the root node of the tree to delete
  * If tree is NULL, do nothing </br>

```
alex@/tmp/binary_trees$ cat 3-main.c 
#include <stdlib.h>
#include <stdio.h>
#include "binary_trees.h"

/**
 * main - Entry point
 *
 * Return: Always 0 (Success)
 */
int main(void)
{
    binary_tree_t *root;

    root = binary_tree_node(NULL, 98);
    root->left = binary_tree_node(root, 12);
    root->right = binary_tree_node(root, 402);
    binary_tree_insert_right(root->left, 54);
    binary_tree_insert_right(root, 128);
    binary_tree_print(root);
    binary_tree_delete(root);
    return (0);
}
alex@/tmp/binary_trees$ gcc -Wall -Wextra -Werror -pedantic binary_tree_print.c 3-main.c 3-binary_tree_delete.c 0-binary_tree_node.c 2-binary_tree_insert_right.c -o 3-del
alex@/tmp/binary_trees$ valgrind ./3-del
==13264== Memcheck, a memory error detector
==13264== Copyright (C) 2002-2013, and GNU GPL'd, by Julian Seward et al.
==13264== Using Valgrind-3.10.1 and LibVEX; rerun with -h for copyright info
==13264== Command: ./3-del
==13264== 
  .-------(098)--.
(012)--.       (128)--.
     (054)          (402)
==13264== 
==13264== HEAP SUMMARY:
==13264==     in use at exit: 0 bytes in 0 blocks
==13264==   total heap usage: 9 allocs, 9 frees, 949 bytes allocated
==13264== 
==13264== All heap blocks were freed -- no leaks are possible
==13264== 
==13264== For counts of detected and suppressed errors, rerun with: -v
==13264== ERROR SUMMARY: 0 errors from 0 contexts (suppressed: 0 from 0)
alex@/tmp/binary_trees$
```

FIle: [3-binary\_tree\_delete.c](3-binary_tree_delete.c)

### 4. [Is leaf](4-binary_tree_is_leaf.c)

Write a function that checks if a node is a leaf

  * Prototype: int binary\_tree\_is\_leaf(const binary\_tree\_t \*node);
  * Where node is a pointer to the node to check
  * Your function must return 1 if node is a leaf, otherwise 0
  * If node is NULL, return 0

```
alex@/tmp/binary_trees$ cat 4-main.c 
#include <stdlib.h>
#include <stdio.h>
#include "binary_trees.h"

/**
 * main - Entry point
 *
 * Return: Always 0 (Success)
 */
int main(void)
{
    binary_tree_t *root;
    int ret;

    root = binary_tree_node(NULL, 98);
    root->left = binary_tree_node(root, 12);
    root->right = binary_tree_node(root, 402);
    binary_tree_insert_right(root->left, 54);
    binary_tree_insert_right(root, 128);
    binary_tree_print(root);

    ret = binary_tree_is_leaf(root);
    printf("Is %d a leaf: %d\n", root->n, ret);
    ret = binary_tree_is_leaf(root->right);
    printf("Is %d a leaf: %d\n", root->right->n, ret);
    ret = binary_tree_is_leaf(root->right->right);
    printf("Is %d a leaf: %d\n", root->right->right->n, ret);
    return (0);
}
alex@/tmp/binary_trees$ gcc -Wall -Wextra -Werror -pedantic binary_tree_print.c 4-binary_tree_is_leaf.c 4-main.c 0-binary_tree_node.c 2-binary_tree_insert_right.c -o 4-leaf
alex@/tmp/binary_trees$ ./4-leaf 
  .-------(098)--.
(012)--.       (128)--.
     (054)          (402)
Is 98 a leaf: 0
Is 128 a leaf: 0
Is 402 a leaf: 1
alex@/tmp/binary_trees$
```

File: [4-binary\_tree\_is\_leaf.c](4-binary_tree_is_leaf.c)

### 5. [Is root](5-binary_tree_is_root.c)

Write a function that checks if a given node is a root

  * Prototype: int binary\_tree\_is\_root(const binary\_tree\_t \*node);
  * Where node is a pointer to the node to check
  * Your function must return 1 if node is a root, otherwise 0
  * If node is NULL, return 0

```
alex@/tmp/binary_trees$ cat 5-main.c 
#include <stdlib.h>
#include <stdio.h>
#include "binary_trees.h"

/**
 * main - Entry point
 *
 * Return: Always 0 (Success)
 */
int main(void)
{
    binary_tree_t *root;
    int ret;

    root = binary_tree_node(NULL, 98);
    root->left = binary_tree_node(root, 12);
    root->right = binary_tree_node(root, 402);
    binary_tree_insert_right(root->left, 54);
    binary_tree_insert_right(root, 128);
    binary_tree_print(root);

    ret = binary_tree_is_root(root);
    printf("Is %d a root: %d\n", root->n, ret);
    ret = binary_tree_is_root(root->right);
    printf("Is %d a root: %d\n", root->right->n, ret);
    ret = binary_tree_is_root(root->right->right);
    printf("Is %d a root: %d\n", root->right->right->n, ret);
    return (0);
}
alex@/tmp/binary_trees$ gcc -Wall -Wextra -Werror -pedantic binary_tree_print.c 5-binary_tree_is_root.c 5-main.c 0-binary_tree_node.c 2-binary_tree_insert_right.c -o 5-root
alex@/tmp/binary_trees$ ./5-root 
  .-------(098)--.
(012)--.       (128)--.
     (054)          (402)
Is 98 a root: 1
Is 128 a root: 0
Is 402 a root: 0
alex@/tmp/binary_trees$
```

File: [5-binary\_tree\_is\_root.c](5-binary_tree_is_root.c)

### 6. [Pre-order traversal](6-binary_tree_preorder.c)

Write a function that goes through a binary tree using pre-order traversal

  * Prototype: void binary\_tree\_preorder(const binary\_tree\_t \*tree, void (\*func)(int));
  * Where tree is a pointer to the root node of the tree to traverse
  * And func is a pointer to a function to call for each node. The value in the node must be passed as a parameter to this function.
  * If tree or func is NULL, do nothing
```
alex@/tmp/binary_trees$ cat 6-main.c
#include <stdlib.h>
#include <stdio.h>
#include "binary_trees.h"

/**
 * print_num - Prints a number
 *
 * @n: Number to be printed
 */
void print_num(int n)
{
    printf("%d\n", n);
}

/**
 * main - Entry point
 *
 * Return: Always 0 (Success)
 */
int main(void)
{
    binary_tree_t *root;

    root = binary_tree_node(NULL, 98);
    root->left = binary_tree_node(root, 12);
    root->right = binary_tree_node(root, 402);
    root->left->left = binary_tree_node(root->left, 6);
    root->left->right = binary_tree_node(root->left, 56);
    root->right->left = binary_tree_node(root->right, 256);
    root->right->right = binary_tree_node(root->right, 512);

    binary_tree_print(root);
    binary_tree_preorder(root, &print_num);
    return (0);
}
alex@/tmp/binary_trees$ gcc -Wall -Wextra -Werror -pedantic binary_tree_print.c 6-main.c 6-binary_tree_preorder.c 0-binary_tree_node.c -o 6-pre
alex@/tmp/binary_trees$ ./6-pre
       .-------(098)-------.
  .--(012)--.         .--(402)--.
(006)     (056)     (256)     (512)
98
12
6
56
402
256
512
alex@/tmp/binary_trees$
```
File: [6-binary\_tree\_preorder.c](6-binary_tree_preorder.c)

### 7. [In-order traversal](7-binary_tree_inorder.c)

Write a function that goes through a binary tree using in-order traversal

  - Prototype: void binary\_tree\_inorder(const binary\_tree\_t \*tree, void (\*func)(int));
  - Where tree is a pointer to the root node of the tree to traverse
  - And func is a pointer to a function to call for each node. The value in the node must be passed as a parameter to this function.
  - If tree or func is NULL, do nothing
```
alex@/tmp/binary_trees$ cat 7-main.c
#include <stdlib.h>
#include <stdio.h>
#include "binary_trees.h"

/**
 * print_num - Prints a number
 *
 * @n: Number to be printed
 */
void print_num(int n)
{
    printf("%d\n", n);
}

/**
 * main - Entry point
 *
 * Return: Always 0 (Success)
 */
int main(void)
{
    binary_tree_t *root;

    root = binary_tree_node(NULL, 98);
    root->left = binary_tree_node(root, 12);
    root->right = binary_tree_node(root, 402);
    root->left->left = binary_tree_node(root->left, 6);
    root->left->right = binary_tree_node(root->left, 56);
    root->right->left = binary_tree_node(root->right, 256);
    root->right->right = binary_tree_node(root->right, 512);

    binary_tree_print(root);
    binary_tree_inorder(root, &print_num);
    return (0);
}
alex@/tmp/binary_trees$ gcc -Wall -Wextra -Werror -pedantic binary_tree_print.c 7-main.c 7-binary_tree_inorder.c 0-binary_tree_node.c -o 7-in
alex@/tmp/binary_trees$ ./7-in
       .-------(098)-------.
  .--(012)--.         .--(402)--.
(006)     (056)     (256)     (512)
6
12
56
98
256
402
512
alex@/tmp/binary_trees$
```
File: [7-binary\_tree\_inorder.c](7-binary_tree_inorder.c)


