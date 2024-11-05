# Stack

A **Stack** is a linear data structure that organizes data in a **Last In, First Out (LIFO)** or **First In, Last Out (FILO)** manner. This means that the last element added to the stack is the first one to be removed. In a stack, insertion and deletion of data happen only at one end, called the **top** or **peek**.

### Key Points:
- **Implementation**: Stacks can be implemented using arrays or linked lists.
- **Push Operation**: Adding data to the top of the stack is called a **push** operation.
- **Pop Operation**: Removing data from the top of the stack is called a **pop** operation.

### Array and Pointer Notation:
- If `arr` represents the base address of an array, `arr + i` refers to the address of the element at the **i-th index**.
- `*(arr + i)` refers to the **element at the i-th index**.

### Array Notation:
- `arr[0]`: Refers to the element at the **0-th index**.
- `arr[i]`: Refers to the element at the **i-th index**.

### Equivalent Notation:
The expression `arr[i]` is equivalent to `*(arr + i)`. Both represent the element at the i-th index in an array.


### Question

Write a C program to implement a stack using an array. The program should allow the user to:
1. **Push** an element onto the stack.
2. **Pop** an element from the stack.
3. **Display** the elements in the stack.
4. **Exit** the program.

---

### Code

Here’s the C program implementing the stack with a menu-driven approach using switch-case.

```c
#include<stdio.h>
#define SIZE 5

int top = -1;
int arr[SIZE];

void push(int d) {
    if (top == SIZE - 1) {
        printf("Stack is full\n");
        return;
    }
    ++top;
    arr[top] = d;
    printf("Element %d pushed onto the stack\n", d);
}


int pop() {
    if (top == -1) {
        printf("Stack is empty\n");
        return -1;
    }
    int d = arr[top];
    --top;
    return d;
}


void display() {
    if (top == -1) {
        printf("Stack is empty\n");
        return;
    }
    printf("The stack elements are: ");
    for (int i = top; i >= 0; i--) {
        printf("%d ", arr[i]);
    }
    printf("\n");
}

int main() {
    int choice, element;

    while (1) {
        // Display menu options
        printf("\nMenu:\n");
        printf("1. Push\n");
        printf("2. Pop\n");
        printf("3. Display\n");
        printf("4. Exit\n");
        printf("Enter your choice: ");
        scanf("%d", &choice);


        switch (choice) {
            case 1:
                printf("Enter element to push: ");
                scanf("%d", &element);
                push(element);
                break;
            case 2:
                element = pop();
                if (element != -1) {
                    printf("The removed (popped) element is: %d\n", element);
                }
                break;
            case 3:
                display();
                break;
            case 4:
                printf("Exiting program...\n");
                return 0;
            default:
                printf("Invalid choice! Please enter a valid option.\n");
        }
    }
}
```


### Question

Write a C program to implement a dynamic stack using pointers and dynamic memory allocation. Free individual memory locations after each pop operation and free the entire stack before exiting the program.

---

### Code


```c

#include<stdio.h>
#include<stdlib.h>

int top = -1;
int *dyarr = NULL;
int size;

void createstack() {
    printf("Enter the number of stack elements: ");
    scanf("%d", &size);
    dyarr = (int *) malloc(size * sizeof(int));
    if (dyarr == NULL) {
        printf("Unable to allocate memory\n");
        exit(1);
    }
    printf("Stack created with size %d\n", size);
}

void push(int d) {
    if (top == size - 1) {
        printf("Stack is full\n");
        return;
    }
    ++top;
    dyarr[top] = d;
    printf("Element %d pushed onto the stack\n", d);
}

void freesinglememory() {
    dyarr[top] = 0;
}

int pop() {
    if (top == -1) {
        printf("Stack is empty\n");
        return -1;
    }
    int d = dyarr[top];
    freesinglememory();
    --top;
    return d;
}

void display() {
    if (top == -1) {
        printf("Stack is empty\n");
        return;
    }
    printf("The stack elements are: ");
    for (int i = top; i >= 0; i--) {
        printf("%d ", dyarr[i]);
    }
    printf("\n");
}

void freestack() {
    free(dyarr);
    dyarr = NULL;
    printf("Stack memory freed\n");
}

int main() {
    int opt, d, ele;

    createstack();

    while (1) {
        printf("\nMenu:\n");
        printf("1. Push\n2. Pop\n3. Display\n4. Exit\n");
        printf("Enter your option: ");
        scanf("%d", &opt);

        switch (opt) {
            case 1:
                printf("Enter the element to push: ");
                scanf("%d", &d);
                push(d);
                break;
            case 2:
                ele = pop();
                if (ele != -1) {
                    printf("The removed (popped) element is: %d\n", ele);
                }
                break;
            case 3:
                display();
                break;
            case 4:
                freestack();
                printf("Exiting program...\n");
                exit(0);
            default:
                printf("Invalid option! Please enter a valid option.\n");
        }
    }
}

```
