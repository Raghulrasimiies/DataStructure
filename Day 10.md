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
