### Question: Evaluate a Postfix Expression

**Description:**  
Write a program to evaluate a postfix expression using a stack data structure. In postfix notation (also known as Reverse Polish Notation), operators follow their operands. The program should read a postfix expression consisting of single-digit integers and operators (`+`, `-`, `*`, `/`, `%`), evaluate the expression, and print the result. The program should handle invalid input gracefully.

**Key Operations:**
1. **Push:** Add an operand to the stack.
2. **Pop:** Remove the top operand from the stack for evaluation.
3. **Evaluate:** Perform the operation when an operator is encountered, using the two most recent operands.

**Test Cases:**

1. **Test Case 1:**
   - **Input:** `23*54*+`
   - **Explanation:** The expression evaluates as follows: `(2 * 3) + (5 * 4) = 6 + 20 = 26`.

2. **Test Case 2:**
   - **Input:** `53+82-*`
   - **Explanation:** The expression evaluates as follows: `(5 + 3) * (8 - 2) = 8 * 6 = 48`.

3. **Test Case 3:**
   - **Input:** `92/3-`
   - **Explanation:** The expression evaluates as follows: `9 / 2 - 3 = 4 - 3 = 1`.

4. **Test Case 4:**
   - **Input:** `54+2*`
   - **Explanation:** The expression evaluates as follows: `(5 + 4) * 2 = 9 * 2 = 18`.

5. **Test Case 5 (Invalid Input):**
   - **Input:** `12a+`
   - **Output:** `INVALID`
   - **Explanation:** The expression contains an invalid character (`a`), which should prompt the program to output "INVALID".

6. **Test Case 6 (Insufficient Operands):**
   - **Input:** `42+*`
   - **Explanation:** The expression does not have enough operands for the multiplication operation after the addition.

  
---

### Code

```c
#include<stdio.h>
#include<stdlib.h>
#define size 10

int top = -1;
int arr[size];

void push(int d){
    if(top == size - 1){
        printf("Stack is Full\n");
        return;
    }
    ++top;
    arr[top] = d;
}

int pop(){
    if(top == -1){
        return -1;
    }
    int d = arr[top];
    --top;
    return d;
}

void arith(){
    char arr[20];
    int a,b,i=0;
    printf("Enter the expression : ");
    scanf("%s",arr);

    while(arr[i] != '\0'){

        if(arr[i]=='+'||arr[i]=='-'||arr[i]=='*'||arr[i]=='/'||arr[i]=='%'){
            b = pop();
            a = pop();
            switch(arr[i]){
            case '+':
                push(a+b);
                break;
            case '-':
                push(a-b);
                break;
            case '*':
                push(a*b);
                break;
            case '/':
                push(a/b);
                break;
            case '%':
                push(a%b);
                break;
            }
        }
        else if(arr[i]>='0' && arr[i]<='9'){
            push(arr[i]-'0');
        }
        else{
            printf("INVALID\n");
        }
        i++;
    }
    printf("The Value is : %d\n",pop());
}

void display(){
    if(top == -1){
        printf("Stack is empty\n");
        return;
    }
    printf("The stack elements are  : ");
    for(int i = top; i >= 0 ; i--){
        printf("%d ",arr[i]);
    }
}

int main(){
    arith();
}
```






# Queue

- **Definition:**  
  A queue is a linear data structure that organizes data in a specific order.

- **Order of Organization:**  
  Queues operate on a First-In-First-Out (FIFO) or Last-In-Last-Out (LILO) principle, meaning that the first element added to the queue will be the first one to be removed.

- **Operations:**
  - **Insertion (Enqueue):**  
    New elements are added to the rear (or back) of the queue.
  
  - **Deletion (Dequeue):**  
    Elements are removed from the front of the queue.

- **Usage:**  
  Queues are commonly used in scenarios such as scheduling processes in operating systems, managing requests in web servers, and handling asynchronous data transfer in communication systems.

--- 

Here’s a structured question based on the provided code:

### Question: Implement a Queue Using a Linked List

**Description:**  
Write a program to implement a queue data structure using a singly linked list in C. The program should support the following operations:

1. **Enqueue:** Insert an element at the rear of the queue.
2. **Dequeue:** Remove an element from the front of the queue.
3. **Display:** Print all elements in the queue.

---

### Code

```c
#include <stdio.h>
#include <stdlib.h>
typedef struct s1{
    int data;
    struct s1 *link;
}node;
node *front = NULL;
node *rear = NULL;
node *memalloc(int d){
    node *new = (node*)malloc(sizeof(node));
    if(new == NULL){
        printf("Memory not allocated");
        exit (0);
    }
    new -> data = d;
    new -> link = NULL;
    return new;
}
void enqueue(int d){
    node *new = memalloc(d);
    if(front == NULL){
        front = new;
        rear = new;
        return;
    }
    rear->link = new;
    rear = new;
}
void dequeue(){
    if (front == NULL) {
        printf("Queue is empty, nothing to dequeue.\n");
        return;
    }
    node *temp = front;
    front = temp->link ;
    free(temp);
}
void display(){
    printf("Your data Elements are : ");
    node *temp = front;
    while(temp != NULL){
        printf("%d ",temp->data);
        temp = temp->link;
    }
    printf("\n");
}
int main(){
    int d,n;
    printf("Enter the number of nodes : ");
    scanf("%d",&n);
    for(int i=0;i<n;i++){
            printf("Enter the Value : ");
            scanf("%d",&d);
            enqueue(d);
    }
    display();
    dequeue();
    dequeue();
    display();
    return 0;
}

```
Here’s a well-structured question based on the provided code:

### Question: Implement a Queue Using a Doubly Linked List

**Description:**  
Write a program to implement a queue data structure using a doubly linked list in C. The program should support the following operations:

1. **Enqueue:** Insert an element at the rear of the queue.
2. **Dequeue:** Remove an element from the front of the queue.
3. **Handle Empty Queue:** Properly manage situations when attempting to dequeue from an empty queue.

---

### Code

```c
#include <stdio.h>
#include <stdlib.h>

typedef struct dll {
    int data;
    struct dll *nlink;
    struct dll *plink;
} node;

node *rear = NULL;
node *front = NULL;

node *memalloc(int d) {
    node *new = (node *)malloc(sizeof(node));
    if (new == NULL) {
        printf("Memory not allocated\n");
        exit(0);
    }
    new->data = d;
    new->nlink = NULL;
    new->plink = NULL;
    return new;
}

void enqueue(int d) {
    node *new = memalloc(d);
    if (rear == NULL) {
        front = rear = new;
    } else {
        rear->nlink = new;
        new->plink = rear;
        rear = new;
    }
    printf("Enqueued %d into Queue\n", d);
}

int dequeue() {
    if (front == NULL) {
        printf("Queue is empty\n");
        return -1;
    }

    int value = front->data;
    node *temp = front;
    front = front->nlink;

    if (front != NULL) {
        front->plink = NULL;
    } else {
        rear = NULL;
    }

    printf("Dequeued %d from Queue\n", value);
    free(temp);
    return value;
}

int main() {
    enqueue(10);
    enqueue(20);
    enqueue(30);
    dequeue();
    dequeue();
    dequeue();
    dequeue();
    return 0;
}
```
