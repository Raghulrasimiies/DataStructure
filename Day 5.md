### Doubly Linked List (DLL)

A doubly linked list is a data structure where each element is referred to as a **node**. Each node contains three parts:

1. **Data**: This stores the value of the node.
2. **Next Link (`nlink`)**: This pointer points to the next node in the list.
3. **Previous Link (`plink`)**: This pointer points to the previous node in the list.

### Key Characteristics

- The **head pointer** points to the first node in the list.
- The `plink` of the first node is set to `NULL`, indicating there is no previous node.
- The `nlink` of the last node is set to `NULL`, indicating there is no subsequent node.

![Singly Linked List](images/img.1)
### Node Structure Definition

The structure of a node in a doubly linked list is defined as follows:

```c
typedef struct dll {
    int data;             // Value of the node
    struct dll *nlink;   // Pointer to the next node
    struct dll *plink;   // Pointer to the previous node
} node;
```

