**Question:**

A service center receives customers in the order of their arrival. However, at times, a high-priority customer needs to be served before others. Write a C program that simulates a queue management system to handle both normal and priority customers using linked lists.

### Requirements:

1. **Queue Operations**: Implement the following queue operations:
   - **enqueue**: Add a customer to the queue.
   - **dequeue**: Remove the next customer in line and display their details.
   - **peek**: Display the customer at the front of the queue without removing them.
   - **display**: Show all customers in the queue, in the order they will be served.

2. **Priority Handling**:
   - When a priority customer arrives, they should be placed at the front of the queue.
   - If multiple priority customers arrive, they should be served in the order they were added (FIFO within priority).
   - Normal customers should be served in the order they arrive, after any priority customers.

3. **Data Structure**:
   - Use a linked list to implement the queue.
   - Each node in the linked list should contain:
     - `cusID` (integer): The customer ID.
     - `priority` (integer): The priority level of the customer (0 for normal, 1 for priority).
     - A pointer to the next node in the list.

4. **Operation Menu**:
   - Your program should provide a menu with the following options:
     1. **Add Customer**: Add a new customer to the queue (specify if they are normal or priority).
     2. **Serve Next Customer**: Remove and display the next customer in line (dequeue).
     3. **View Next Customer**: Display the details of the customer at the front of the queue (peek).
     4. **Display Queue**: Display all customers currently in the queue.
     5. **Exit**: Exit the program.

5. **Constraints**:
   - Assume a maximum of 100 customers can be handled.
   - Use dynamic memory allocation and handle memory management carefully to avoid memory leaks.
   - Display clear and informative messages for each operation.

**Write a C program that fulfills the above requirements and simulates the queue management system as described.**



```C
#include <stdio.h>
#include <stdlib.h>
typedef struct sll{
    int cusID;
    int priority;
    struct sll *link;
}node;

node *front = NULL;
node *rear = NULL;

node *memalloc(int id,int pri){
    node *new = (node*) malloc (sizeof(node));
    if(new == NULL){
        printf("Memory not allocated");
        exit(1);
    }
    new->cusID = id;
    new->priority= pri;
    new->link = NULL;
    return new;
}

void enqueue(int id,int pri){
    node *new = memalloc(id,pri);
    if(pri == 1){
        if(front == NULL){
            front = rear = new;
        }else{
            new->link = front;
            front = new;
        }
    }else{
        if(rear == NULL){
            front = rear = new;
        }
        else{
            rear->link =new;
            rear = new;
        }
    }
    printf("Customer %d (Priority: %d) added to the queue.\n", id, pri);
}

void dequeue(){
    if(front == NULL){
            printf("Queue is empty");
            return;
    }
    node *temp = front;
    front = front->link;
    if(front == NULL){
        rear = NULL;
    }
    printf("Customer %d (Priority: %d) removed to the queue.\n",temp->cusID,temp->priority);
    free(temp);
}

void peek() {
    if (front == NULL) {
        printf("Queue is empty.\n");
    } else {
        printf("Next Customer: %d (Priority: %d)\n", front->cusID, front->priority);
    }
}

void display(){
    if(front == NULL){
        printf("Queue is Empty\n");
        return;
    }
    node *temp = front;
    while(temp != NULL){
        printf("Customer id : %d (Priority : %d)\n\n", temp->cusID, temp->priority);
        temp = temp->link;
    }
    printf("\n");
}

void freeQueue() {
    Node* temp;
    while (front != NULL) {
        temp = front;
        front = front->next;
        free(temp);
    }
}

int main(){
    int opt,id,pri;
    while(1){
        printf("\n\n.....Welcome to Rasim Rockers Service Center.....\n\n");
        printf("1. Adding the Customer\n2. Remove in Queue\n3. View the First Customer\n4. Display the Customer\n5. Exit");
        printf("\nEnter Your option : ");
        scanf("%d",&opt);

        switch(opt){
            case 1:
                printf("Enter the Customer ID : ");
                scanf("%d",&id);
                printf("Enter the Customer Priority (0 means Normal Priority and 1 means High Priority): ");
                scanf("%d",&pri);
                enqueue(id,pri);
                break;
            case 2:
                dequeue();
                break;
            case 3:
                peek();
                break;
            case 4:
                display();
                break;
            case 5:
                freeQueue();
                printf("Exiting program.\n");
                exit(0);
            default:
                printf("Enter the Valid Option\n");
        }
    }
}

```
