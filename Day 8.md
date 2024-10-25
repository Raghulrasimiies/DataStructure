### 1. Write a program to find the node where two singly linked lists intersect.
```c
#include <stdio.h>
#include <stdlib.h>
typedef struct s1{
    int data;
    struct s1 *link;
}node;
node *head1 = NULL;
node *head2 = NULL;
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
void insertend(int d,node **head){
    node *new = memalloc(d);
    node *temp = *head;
    if(*head == NULL){
        *head = new;
        return;
    }
    while(temp->link != NULL){
        temp = temp->link;
    }
    temp->link = new;
}
void sort_data(node **head) {
    int swapped, tempData;
    node *temp;
    node *ptr1 = *head;
    if (ptr1 == NULL) {
        return;
    }
    do {
        swapped = 0;
        temp = *head;
        while (temp->link != NULL) {
            if (temp->data > temp->link->data) {
                tempData = temp->data;
                temp->data = temp->link->data;
                temp->link->data = tempData;
                swapped = 1;
            }
            temp = temp->link;
        }
    } while (swapped);
}


node* intersection(node *head1, node *head2){
    if (head1 == NULL || head2 == NULL){
        printf("One of the list is empty");
        return;
    }
    sort_data(&head1);
    sort_data(&head2);
    printf("\nSorted List : ");
    display(head1);
    printf("\nSorted List : ");
    display(head2);
    node *temp1 = head1;
    node *temp2 = head2;
    printf("The two list intersection elements are : ");
    while (temp1 != NULL && temp2 != NULL){
        if(temp1 -> data == temp2->data){
            printf("%d",temp1->data);
            temp1 = temp1->link;
            temp2 = temp2 -> link;
        }
        else if(temp1 ->data < temp2 -> data){
            temp1 = temp1->link;
        }
        else{
            temp2 = temp2->link;
        }
    }
}

void display(node *head){
    printf("Your data Elements are : ");
    node *temp = head;
    while(temp != NULL){
        printf("%d ",temp->data);
        temp = temp->link;
    }
    printf("\n");
}

int main(){
    int d,n,m;
    printf("Enter the number of nodes : ");
    scanf("%d",&n);
    for(int i=0;i<n;i++){
            printf("Enter the Value : ");
            scanf("%d",&d);
            insertend(d,&head1);
    }
    printf("Enter the number of nodes : ");
    scanf("%d",&m);
    for(int i=0;i<m;i++){
            printf("Enter the Value : ");
            scanf("%d",&d);
            insertend(d,&head2);
    }
    display(head1);
    display(head2);
    intersection(head1,head2);
    return 0;
}
```

### 2. Implement a function to merge two sorted linked lists into one sorted list.
```c
#include <stdio.h>
#include <stdlib.h>
typedef struct s1{
    int data;
    struct s1 *link;
}node;
node *head1 = NULL;
node *head2 = NULL;
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
void insertend(int d,node **head){
    node *new = memalloc(d);
    node *temp = *head;
    if(*head == NULL){
        *head = new;
        return;
    }
    while(temp->link != NULL){
        temp = temp->link;
    }
    temp->link = new;
}
void sort_data(node **head) {
    int swapped, tempData;
    node *temp;
    node *ptr1 = *head;
    if (ptr1 == NULL) {
        return;
    }
    do {
        swapped = 0;
        temp = *head;
        while (temp->link != NULL) {
            if (temp->data > temp->link->data) {
                tempData = temp->data;
                temp->data = temp->link->data;
                temp->link->data = tempData;
                swapped = 1;
            }
            temp = temp->link;
        }
    } while (swapped);
}

void mergelist(node *head1,node *head2){

    if (head1 == NULL || head2 == NULL){
        printf("One of the list is empty");
        return;
    }
    sort_data(&head1);
    sort_data(&head2);

    node *temp1 = head1;
    while(temp1->link != NULL){
        temp1 = temp1->link;
    }
    temp1->link = head2;
    printf("\n\nMerged List before Sorting\n");
    display(head1);
    printf("\n\nMerged List After Sorting\n");
    sort_data(&head1);
    display(head1);

}


void display(node *head){
    printf("Your data Elements are : ");
    node *temp = head;
    while(temp != NULL){
        printf("%d ",temp->data);
        temp = temp->link;
    }
    printf("\n");
}

int main(){
    int d,n,m;
    printf("Enter the number of nodes : ");
    scanf("%d",&n);
    for(int i=0;i<n;i++){
            printf("Enter the Value : ");
            scanf("%d",&d);
            insertend(d,&head1);
    }
    printf("Enter the number of nodes : ");
    scanf("%d",&m);
    for(int i=0;i<m;i++){
            printf("Enter the Value : ");
            scanf("%d",&d);
            insertend(d,&head2);
    }
    display(head1);
    display(head2);
    mergelist(head1,head2);
    return 0;
}
```
