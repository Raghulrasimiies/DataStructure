### Question

Write a C program to implement a stack using a doubly linked list. The program should allow the user to perform the following operations:
1. **Push** an integer onto the stack.
2. **Pop** an integer from the stack.
3. **Display** all elements currently in the stack.
4. **Exit** the program.


---

### Code


```c
#include <stdio.h>
#include <stdlib.h>

typedef struct dll {
    int data;
    struct dll *plink;
    struct dll *nlink;
} node;

node *top = NULL;

node *memalloc(int d) {
    node *new = (node *)malloc(sizeof(node));
    if (new == NULL) {
        printf("Memory not allocated\n");
        exit(1);
    }
    new->data = d;
    new->plink = NULL;
    new->nlink = NULL;
    return new;
}

void push(int d) {
    node *new = memalloc(d);
    if (top == NULL) {
        top = new;
        return;
    }
    new->plink = top;
    top->nlink = new;
    top = new;
    printf("Pushed %d onto stack\n", d);
}

int pop() {
    if (top == NULL) {
        printf("Stack is empty\n");
        return -1;
    }
    int value = top->data;
    node *temp = top;
    top = top->plink;
    if (top != NULL) {
        top->nlink = NULL;
    }
    free(temp);
    printf("Popped %d from stack\n", value);
    return value;
}

void display() {
    if (top == NULL) {
        printf("Stack is empty\n");
        return;
    }
    node *temp = top;
    printf("The stack elements are: ");
    while (temp != NULL) {
        printf("%d ", temp->data);
        temp = temp->plink;
    }
    printf("\n");
}

int main() {
    int d, opt;
    while (1) {
        printf("\nMenu:\n");
        printf("1. Push\n2. Pop\n3. Display\n4. Exit\n");
        printf("Enter your option: ");
        scanf("%d", &opt);
        switch (opt) {
            case 1:
                printf("Enter the data: ");
                scanf("%d", &d);
                push(d);
                break;
            case 2:
                pop();
                break;
            case 3:
                display();
                break;
            case 4:
                exit(0);
            default:
                printf("Invalid option! Please enter a valid option.\n");
        }
    }
}
```

---

### Question

Write a C program to check if a given string of parentheses is **balanced**. The string may contain the following types of brackets: `()`, `[]`, and `{}`. A string is considered balanced if:
1. Every opening bracket has a corresponding closing bracket.
2. The brackets are closed in the correct order.

### Example Input and Output

- **Input**: `{[()]}`
  - **Output**: Balanced

- **Input**: `[(])`
  - **Output**: Not Balanced

---

### Code

```c
#include <stdio.h>
#include <stdlib.h>
typedef struct dll{
    char data;
    struct dll *plink;
    struct dll *nlink;
}node;

node *top = NULL;
int size;
node *memalloc(char d){
    node *new = (node *) malloc (sizeof(node));
    if(new == NULL){
        printf("Memory no allocated");
        exit(1);
    }
    new->data = d;
    new -> plink =NULL;
    new -> nlink =NULL;
    return new;
}

void push(char d){
    node *new = memalloc(d);
    if(top == NULL){
            top  = new;
            return;
    }
    new -> nlink = top;
    top -> plink = new;
    top = new;
    printf("Pushed %c onto stack \n",d);
}
char pop(){
    if(top == NULL){
        printf("Stack is empty\n");
        return -1;
    }
    char value = top->data;
    node *temp = top;
    top = top -> nlink;
    if(top != NULL){
        top->plink = NULL;
    }
    free(temp);
    return value;
}
void display(){
    if(top == NULL){
        printf("Stack is Empty");
        return;
    }
    node *temp = top;
    printf("The list Elements are : ");
    while (temp != NULL){
        printf("%c ",temp->data);
        temp = temp->nlink;
    }
    printf("\n");
}
void check_bra(char *str){
    for(int i = 0 ;str[i]!='\0';i++){
        char ch = str[i];
        if(ch == '{' || ch == '['||ch=='('){
            push(str[i]);
        }
        else if(ch == '}' || ch == ']'||ch==')'){
            if(top == NULL){
                printf("No element to compare empty Stack\n");
            }
            char c = pop();
            if(!(c== '{' && ch == '}' ||c== '[' && ch == ']' ||c== '(' && ch == ')')){
                printf("Not Balanced\n");
                return;
            }
        }
    }
    if (top == NULL) {
        printf("Balanced\n");
    } else {
        printf("Not Balanced\n");
    }
}
int main(){
    printf("Size of String : ");
    scanf("%d",&size);
    char str[size];
    printf("Enter the String Value :");
    scanf("%s",&str);
    check_bra(str);
}

```
## Assignment

1. What is a stack, and how does it differ from other data structures? 

2. Explain the LIFO principle in the context of stacks.

3. What are the primary operations of a stack, and how do they work?

4. Describe a few real-world examples where stacks are used.

5. Write a program to implement a stack using an array in C.

6. How do you implement a stack using a linked list in C?

7. What are the advantages and disadvantages of array-based and linked list-based stacks?

8. How would you handle stack overflow and underflow conditions in code?

9. Write a function to check if a stack is empty or full.

10. How could you dynamically resize an array-based stack if it reaches capacity?

11. Write a program to reverse a string using a stack.

12. What is stack overflow, and how can we prevent it?

13. Describe how stack frames work when a function is called, including local variable storage, function parameters, and the return address.


## Practice Questions

### 1. Find Two Indices for Sum

**Description:**  
Given an array of integers, your task is to find two indices such that the numbers at those indices add up to a specific target value. Return the indices of these two numbers. If no such indices exist, return an indication (e.g., `-1`).

**Test Cases:**
- **Input:** `[1, 2, 1, 5, 6]`, **Target:** `7`  
  **Output:** `[3, 4]` (since `5 + 6 = 11`)

- **Input:** `[2, 7, 11, 15]`, **Target:** `9`  
  **Output:** `[0, 1]` (since `2 + 7 = 9`)

- **Input:** `[1, 3, 4, 2]`, **Target:** `6`  
  **Output:** `[-1]` (no such indices exist)

### 2. Check Anagrams

**Description:**  
Write a program that reads two strings from the user and checks if they are anagrams of each other. Anagrams are words or phrases that contain the same characters in a different order.

**Test Cases:**
- **Input:** `"listen"`, `"silent"`  
  **Output:** `True` (they are anagrams)

- **Input:** `"hello"`, `"world"`  
  **Output:** `False` (they are not anagrams)

- **Input:** `"rail safety"`, `"fairy tales"`  
  **Output:** `True` (they are anagrams)

### 3. FizzBuzz Program

**Description:**  
Write a program that prints numbers from `1` to `n`. For multiples of `3`, print "Fizz"; for multiples of `5`, print "Buzz"; and for numbers that are multiples of both, print "FizzBuzz".

**Test Cases:**
- **Input:** `n = 15`  
  **Output:** `1 2 Fizz 4 Buzz Fizz 7 8 Fizz Buzz 11 Fizz 13 14 FizzBuzz`

- **Input:** `n = 5`  
  **Output:** `1 2 Fizz 4 Buzz`

- **Input:** `n = 20`  
  **Output:** `1 2 Fizz 4 Buzz Fizz 7 8 Fizz Buzz 11 Fizz 13 14 FizzBuzz 16 17 Fizz 19 Buzz`

### 4. Maximize Stock Profit

**Description:**  
Given an array `prices` where `prices[i]` is the price of a stock on the `i`-th day, write a program to maximize the profit by buying one stock on one day and selling it on a different day in the future. Return the maximum profit you can achieve. If no profit can be made, return `0`.

**Test Cases:**
- **Input:** `[7, 1, 5, 3, 6, 4]`  
  **Output:** `5` (buy at `1` and sell at `6`)

- **Input:** `[7, 6, 4, 3, 1]`  
  **Output:** `0` (no profit can be made)

- **Input:** `[1, 2, 3, 4, 5]`  
  **Output:** `4` (buy at `1` and sell at `5`)

- **Input:** `[3, 2, 6, 5, 0, 3]`  
  **Output:** `4` (buy at `2` and sell at `6`)
