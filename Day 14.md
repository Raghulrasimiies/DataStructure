### Binary Search Tree (BST) Operations and Programs

This document provides information and programs on binary search trees, covering key operations such as insertion, searching, finding minimum and maximum values, and deleting a node.

---

### 1. Binary Search Tree (BST)

A **Binary Search Tree (BST)** is a binary tree with the following properties:
1. **Left Subtree**: Contains only nodes with values less than the node's value.
2. **Right Subtree**: Contains only nodes with values greater than the node's value.
3. **No Duplicates**: Duplicate values are generally not allowed in a BST.

### 2. Key BST Operations

The main operations on a BST include:
- **Insertion**: Adding a node to the BST while maintaining BST properties.
- **Search**: Finding a node with a given key.
- **Finding Minimum and Maximum**: Finding nodes with the smallest and largest values.
- **Deletion**: Removing a node, handling cases where the node has zero, one, or two children.

---

### 1. Program to Insert and Search an Element in a BST

The following program inserts elements into a BST and searches for a specified key.

```c
#include <stdio.h>
#include <stdlib.h>

typedef struct BST {
    int data;
    struct BST *lchild;
    struct BST *rchild;
} node;

node *root = NULL;

node *memalloc(int d) {
    node *newNode = (node*) malloc(sizeof(node));
    if (newNode == NULL) {
        printf("Memory not allocated\n");
        exit(1);
    }
    newNode->data = d;
    newNode->lchild = NULL;
    newNode->rchild = NULL;
    return newNode;
}

void insert(int d) {
    node *newNode = memalloc(d);
    if (root == NULL) {
        root = newNode;
        return;
    }
    node *temp = root, *parent = NULL;
    while (temp != NULL) {
        parent = temp;
        if (d > temp->data)
            temp = temp->rchild;
        else if (d < temp->data)
            temp = temp->lchild;
        else {
            printf("Duplicates are not allowed\n");
            return;
        }
    }
    if (d > parent->data)
        parent->rchild = newNode;
    else
        parent->lchild = newNode;
}

node *search(node *root, int key) {
    node *temp = root;
    while (temp != NULL) {
        if (key == temp->data)
            return temp;
        else if (key > temp->data)
            temp = temp->rchild;
        else
            temp = temp->lchild;
    }
    return NULL;
}

int main() {
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
    
    int key;
    printf("Enter the key to search: ");
    scanf("%d", &key);
    node *ptr = search(root, key);
    
    if (ptr == NULL)
        printf("Element not found\n");
    else
        printf("Element found: %d\n", key);

    return 0;
}
```

### 2. Program to Find Minimum and Maximum Values in a BST

The following program finds the minimum and maximum values in a BST, returning the nodes containing these values.

```c
node *findMin(node *root) {
    node *temp = root;
    while (temp && temp->lchild != NULL) {
        temp = temp->lchild;
    }
    return temp;
}

node *findMax(node *root) {
    node *temp = root;
    while (temp && temp->rchild != NULL) {
        temp = temp->rchild;
    }
    return temp;
}

int main() {
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

    node *minNode = findMin(root);
    if (minNode != NULL)
        printf("Minimum element: %d\n", minNode->data);

    node *maxNode = findMax(root);
    if (maxNode != NULL)
        printf("Maximum element: %d\n", maxNode->data);
}
```

---

### 3. Program to Delete a Node from a BST

This program demonstrates deleting a node from a BST. It handles cases where the node has:
- **0 Children**: Simply removes the node.
- **1 Child**: Replaces the node with its child.
- **2 Children**: Finds the in-order successor (smallest value in the right subtree), replaces the node’s value with the successor, and deletes the successor node.

```c
node *deleteNode(node *root, int key) {
    if (root == NULL)
        return root;

    if (key < root->data)
        root->lchild = deleteNode(root->lchild, key);
    else if (key > root->data)
        root->rchild = deleteNode(root->rchild, key);
    else {
        if (root->lchild == NULL) {
            node *temp = root->rchild;
            free(root);
            return temp;
        } else if (root->rchild == NULL) {
            node *temp = root->lchild;
            free(root);
            return temp;
        }

        node *temp = findMin(root->rchild);
        root->data = temp->data;
        root->rchild = deleteNode(root->rchild, temp->data);
    }
    return root;
}

int main() {
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

    printf("Inorder traversal before deletion: ");
    inorderTraversal(root);
    int key;
    printf("\nEnter the key to delete: ");
    scanf("%d", &key);

    root = deleteNode(root, key);

    printf("Inorder traversal after deletion: ");
    inorderTraversal(root);

    return 0;
}
```

---
