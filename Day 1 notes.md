# Data Structures and Algorithms

A data structure is a specialized way of organizing, managing, and storing data in a computer so that it can be accessed and modified efficiently. In C programming, data structures are used to handle data in a more organized and logical manner, enabling efficient access and modification. Data structures can be broadly categorized based on the way they organize and store data. They fall into two main categories: **primitive** and **non-primitive** data structures.

## 1. Primitive Data Structures
Primitive data structures are the basic types of data that are directly supported by the programming language. They are fundamental data types that are typically predefined and serve as building blocks for more complex data structures.

- **Integer (int)**: Stores whole numbers (both positive and negative).
- **Float (float)**: Stores single-precision floating-point numbers.
- **Double (double)**: Stores double-precision floating-point numbers.
- **Character (char)**: Stores a single character.
- **Boolean (bool)**: Represents true/false values (typically 1 for true and 0 for false).

## 2. Non-Primitive Data Structures
Non-primitive data structures are more complex and are derived from primitive data types. These structures are used to organize data in more meaningful ways, depending on the specific needs of the application. They can be further divided into linear and non-linear data structures.

### A. Linear Data Structures
In linear data structures, elements are arranged in a sequence, where each element is connected to its previous and next element. This sequential order allows for easy traversal from one element to the next.

- **Arrays**:
  - A collection of elements of the same data type stored in contiguous memory locations.
  - Allows random access using indices.
  - Syntax: `data_type array_name[size];`

- **Linked Lists**:
  - Consist of nodes, where each node contains data and a pointer to the next node.
  - Types include:
    - **Singly Linked List**: Each node points to the next node.
    - **Doubly Linked List**: Each node points to both the next and the previous nodes.
    - **Circular Linked List**: The last node points back to the first node, forming a circular chain.

- **Stacks**:
  - Follows the Last In First Out (LIFO) principle.
  - Common operations:
    - **push**: Insert an element.
    - **pop**: Remove the top element.
  - Used in function call management, expression evaluation, and undo mechanisms.

- **Queues**:
  - Follows the First In First Out (FIFO) principle.
  - Common operations:
    - **enqueue**: Add an element to the end.
    - **dequeue**: Remove an element from the front.
  - Used in scheduling, buffering, and task management.

### B. Non-Linear Data Structures
Non-linear data structures do not store data in a sequential manner. Instead, they organize data hierarchically or as interconnected networks, which allows for more complex relationships among data elements.

- **Trees**:
  - A hierarchical structure with a root node and child nodes.
  - Types include:
    - **Binary Tree**: Each node has at most two children.
    - **Binary Search Tree (BST)**: A binary tree where the left child is smaller than the parent node, and the right child is larger.
    - **AVL Tree**: A self-balancing binary search tree.
    - **Heap**: A complete binary tree with either a min-heap or max-heap property.
  - Used in applications like file systems, database indexing, and decision-making systems.

- **Graphs**:
  - Consist of nodes (vertices) and edges that connect them.
  - Types of graphs:
    - **Directed Graph (Digraph)**: Edges have a direction (from one vertex to another).
    - **Undirected Graph**: Edges have no direction and connect two vertices bidirectionally.
    - **Weighted Graph**: Each edge has a weight (or cost) associated with it.
    - **Unweighted Graph**: Edges have no weights.
  - Used in modeling networks, social connections, transportation routes, and other complex systems.

### Differences Between Linear and Non-Linear Data Structures

| Aspect                       | Linear Data Structures             | Non-Linear Data Structures         |
|------------------------------|------------------------------------|------------------------------------|
| Storage Structure             | Stored in a sequential, contiguous manner | Stored in a hierarchical or interconnected manner |
| Memory Utilization            | Less flexible, as size is often fixed or difficult to grow efficiently | More flexible; allows dynamic memory usage and more complex relationships |
| Complexity                    | Simpler to implement and understand | More complex, suitable for sophisticated relationships |
| Examples                      | Arrays, Linked Lists, Stacks, Queues | Trees, Graphs |

---



## Function
- A function is a block of organized, reusable code that performs a specific task. 
- In programming, functions help in breaking down code into smaller, manageable, and organized sections.
- Functions can take inputs, process them, and return a result.

### Advantages of Functions
- Code Reusability
- Easier Debugging
- Improved Code Readability
- Scalability
  
## Feature Comparison: Call by Value vs. Call by Reference

| Feature                      | Call by Value                     | Call by Reference                 |
|------------------------------|-----------------------------------|-----------------------------------|
| Definition                    | Passes a copy of the value to the function | Passes the address of the variable to the function |
| Parameter Type                | Actual values of arguments are passed | Memory addresses (pointers) of arguments are passed |
| Effect on Original Data       | No effect on original data; only copies are modified | Modifies the original data directly |
| Memory Usage                  | Requires more memory (for copying data) | Requires less memory (only addresses are passed) |
| Performance                   | Can be slower for large data due to copying | Typically faster for large data, as no copying is needed |
| Side Effects                  | No side effects; original data remains unchanged | Can have side effects, as original data is modified |
| Example Syntax                | `modifyValue(num);`              | `modifyValue(&num);`              |
---

## Arrays
An array is a collection of elements of the same data type stored in contiguous memory locations.

### 1. Arrays are Always Passed by Address
- When you pass an array to a function in C, you are actually passing a pointer to the first element of the array (i.e., the base address of the array).
- This means that the function receives a reference to the original array, allowing it to modify the array elements directly.

### 2. Array Name Refers to Base Address
- The name of the array represents the address of the first element, often referred to as the base address.

### Example 1: C Program to Store and Display Array Elements
```c
#include <stdio.h>
int getting_arr_ele(int arr[]);
void display_arr(int arr[], int len);

int main() {
    int arr[10];
    int len = getting_arr_ele(arr);
    display_arr(arr, len);
    return 0;
}

int getting_arr_ele(int arr[]) {
    int n;
    printf("Enter the number of Array elements: ");
    scanf("%d", &n);
    for (int i = 0; i < n; i++) {
        scanf("%d", &arr[i]);
    }
    return n;
}

void display_arr(int arr[], int len) {
    for (int i = 0; i < len; i++) {
        printf("%d ", arr[i]);
    }
}
```

### Example 2: Find Leaders in an Array
**Question**: Write a C program to find all the leaders in an array. An element is considered a leader if it is greater than all the elements to its right.

**Input**: A single line containing integers representing the elements of the array (e.g., 16 17 4 3 5 2).

**Output**: Print all the leaders in the array, separated by spaces (e.g., 17 5 2).

**Note**: The rightmost element is always considered a leader.

```c
#include <stdio.h>
void lea_in_arr(int arr[], int len);

int main() {
    int arr[10], n;
    printf("Enter the number of Array elements: ");
    scanf("%d", &n);
    for (int i = 0; i < n; i++) {
        scanf("%d", &arr[i]);
    }
    lea_in_arr(arr, n);
    return 0;
}

void lea_in_arr(int arr[], int len) {
    int max = arr[len - 1];
    for (int i = len - 1; i >= 0; i--) {
        if (max <= arr[i]) {
            printf("%d ", arr[i]);
            max = arr[i];
        }
    }
}
```

---

## Assignment Questions
1. How do you declare and initialize arrays in C? Provide an example.
2. Write a C program to find the sum of all elements in an array.
3. What is the difference between static and dynamic memory allocation in C? Which one do you prefer and why?
4. Explain how multi-dimensional arrays are stored in memory and how you access their elements.
5. What is dynamic memory allocation in C? How do you allocate and deallocate memory?
6. What are `calloc`, `malloc`, `realloc`, and `free`? Provide examples for each.
7. What are the common problems associated with dynamic memory allocation, and how can you avoid them?
8. What are the types of loops in C? Explain with syntax and examples.
9. Write a C program using a nested loop to print Pascal's triangle.
10. What is the difference between `switch` and `if-else` statements? When would you prefer one over the other?
11. Can you use floating-point numbers in a `switch` statement? Why or why not?
12. What is modularity in programming? How does C support modularity?
13. Provide examples of pass by value and pass by reference in C.
14. Explain the difference between pointers and arrays in C.

---
