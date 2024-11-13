### Tree Data Structure

A **tree** is a non-linear hierarchical data structure consisting of nodes. The topmost node in a tree is called the **root** node, and nodes without any children are known as **leaf nodes**.

### Binary Tree

In a **binary tree**, each node has a maximum of two child nodes:
- The left child
- The right child

### Binary Search Tree (BST)

A **Binary Search Tree (BST)** is a binary tree with the following properties:
1. The left subtree of a node contains nodes with values less than the node’s value.
2. The right subtree of a node contains nodes with values greater than the node’s value.
3. Duplicate values are not allowed.

When inserting nodes in a BST:
- If the value to insert is greater than the current node’s value, go to the right subtree.
- If it is less, go to the left subtree.

#### Example:
Consider inserting these values into a BST: `12, 5, 15, 3, 1, 8, 20, 25, 6, 7, 9`.

### Tree Traversal Methods

Tree traversal refers to the process of visiting each node in the tree. The three main traversal methods are:

1. **Inorder Traversal** (Left-Root-Right):
   - Visit the left subtree, then the root, and finally the right subtree.
   - Result: `1 2 3 5 8 9 11 15 16 20` (in ascending order for a BST).

2. **Preorder Traversal** (Root-Left-Right):
   - Visit the root, then the left subtree, and finally the right subtree.
   - Example Result: `5 1 3 2 8 15 9 11 20 16`.

3. **Postorder Traversal** (Left-Right-Root):
   - Visit the left subtree, then the right subtree, and finally the root.
   - Example Result: `2 3 1 11 9 16 20 15 8 5`.

### Traversal Example
Given a tree with nodes `17, 5, 32, 15, 8, 11, 20, 60, 22, 12`, the traversals would produce:

- **Inorder**: `5 8 11 12 15 17 20 22 32 60`
- **Preorder**: `17 5 15 8 11 12 32 20 22 60`
- **Postorder**: `12 11 8 15 5 22 20 60 32 17`

---

### C Program Implementation of a Binary Search Tree (BST)

The following C program implements a binary search tree with insertion and traversal functions for **inorder**, **preorder**, and **postorder** traversals.

```c
#include <stdio.h>
#include <stdlib.h>

// Define the structure of a BST node
typedef struct BST {
    int data;
    struct BST *lchild;
    struct BST *rchild;
} node;

node *root = NULL;

// Allocate memory for a new node
node *memalloc(int d){
    node *new = (node*) malloc(sizeof(node));
    if(new == NULL){
        printf("Memory not allocated \n");
        exit(1);
    }
    new->data = d;
    new->lchild = NULL;
    new->rchild = NULL;
    return new;
}

// Insert a node into the BST
void insert(int d){
    node *new = memalloc(d);
    if(root == NULL){
        root = new;
        return;
    }
    node *temp = root, *parent = NULL;
    while(temp != NULL){
        if(d > temp->data) {
            parent = temp;
            temp = temp->rchild;
        }
        else if(d < temp->data){
            parent = temp;
            temp = temp->lchild;
        }
        else {
            printf("Duplicates are not allowed\n");
            return;
        }
    }
    if (d > parent->data){
        parent->rchild = new;
    } else {
        parent->lchild = new;
    }
}

// Inorder Traversal
void inorder(node *temp) {
    if (temp == NULL) return;
    inorder(temp->lchild);
    printf("%d ", temp->data);
    inorder(temp->rchild);
}

// Preorder Traversal
void preorder(node *temp) {
    if (temp == NULL) return;
    printf("%d ", temp->data);
    preorder(temp->lchild);
    preorder(temp->rchild);
}

// Postorder Traversal
void postorder(node *temp) {
    if (temp == NULL) return;
    postorder(temp->lchild);
    postorder(temp->rchild);
    printf("%d ", temp->data);
}

// Main function to test the BST implementation
int main(){
    insert(17);
    insert(5);
    insert(32);
    insert(15);
    insert(8);
    insert(11);
    insert(20);
    insert(60);
    insert(22);
    insert(12);

    printf("Inorder: ");
    inorder(root);
    printf("\nPreorder: ");
    preorder(root);
    printf("\nPostorder: ");
    postorder(root);

    return 0;
}
```
