**Problem Statement: Simple Social Network Model in C**

Design a simple social network model in C using an undirected graph. In this network:
- Each person is represented as a node (or vertex).
- Each friendship between two people is represented as an undirected edge between their respective nodes.

**Requirements:**
1. **Graph Representation**: Use an adjacency list to represent the graph structure.

2. **Core Functions**:
   - **`addFriend(int user1, int user2)`**: Establish a friendship between `user1` and `user2`. This function should create an undirected edge between the two users, indicating a friendship. Self-friendships (i.e., a user being friends with themselves) should not be allowed.
   
   - **`viewConnections(int user)`**: List all direct friends of a given user.
   
   - **`suggestFriends(int user)`**: Suggest potential friends for the given user based on mutual connections. A mutual friend is defined as someone who is a friend of a friend but not a direct friend of the user.

3. **Program Execution**:
   - Input the number of users in the network.
   - Input an initial list of friendships to initialize the graph.
   - Display a menu allowing the user to:
     1. View friends of a specific user.
     2. Add a new friendship between two users.
     3. Get friend suggestions for a user based on mutual connections.
---
```c
#include<stdio.h>
#include<stdlib.h>
#define MAX 100
int person[MAX][MAX];
void intialize_person(int numuser){
    for(int i = 0;i<numuser;i++){
            for(int j = 0;j<numuser;j++){
                person[i][j] = 0;
            }
        }
}
void addFriend(int user1,int user2)
{
    if(user1 != user2){
        person[user1][user2]=1;
        person[user2][user1]=1;
    }
}
void viewConnections(int user,int numuser)
{
    printf("    ");
    for(int i = 0;i<numuser;i++){
            printf("%d  ",i);
    }printf("\n----");
    for(int i = 0;i<numuser;i++){
            printf("---");
    }printf("\n");
    for(int i = 0;i<numuser;i++){
            if(person[user][i]==1){
                printf("%d | ",i);
                for(int j = 0;j<numuser;j++){
                    printf("%d  ",person[i][j]);
                }printf("\n");
            }
        }printf("\n\n");
    for(int i = 0;i<numuser;i++){
            if(person[user][i]==1){
                printf("person %d is friend of person %d\n",user,i);
                }
            }
    printf("\n\n");
}
void viewAllConnections(int numuser)
{
    printf("    ");
    for(int i = 0;i<numuser;i++){
            printf("%d  ",i);
    }printf("\n----");
    for(int i = 0;i<numuser;i++){
            printf("---");
    }printf("\n");
    for(int i = 0;i<numuser;i++){
            printf("%d | ",i);
            for(int j = 0;j<numuser;j++){
                printf("%d  ",person[i][j]);
            }printf("\n");

        }printf("\n\n");
}
void suggestFriends(int user,int numuser){
    printf("Suggest Friends for user %d : ", user);
    int suggested[MAX] = {0};
    for(int i = 0;i<numuser;i++){
        if(person[user][i]==1){
            for(int j=0;j<numuser;j++){
                if(person[i][j]==1 && j != user && person[user][j]==0){
                    suggested[j]= 1;
                }
            }
        }
    }
    for(int i = 0;i<numuser;i++){
        if(suggested[i]){
            printf("%d ",i);
        }
    }
    printf("\n\n");
}
int main() {
    int user1,user2,user,opt;
    int numuser;
    printf("Enter the number of User : ");
    scanf("%d",&numuser);
    if(numuser>MAX || numuser<0){
        printf("Number of user should be in between 0 to %d",MAX);
        return 1;
    }
    intialize_person(numuser);
    while(1){
        printf("1. Add new Friends \n2. View User\n3. Friends suggestions\n4. View All User \n5. Exit\n");
        printf("Enter your option : ");
        scanf("%d",&opt);
        switch(opt){
            case 1:
                printf("Enter the User1 id : ");
                scanf("%d",&user1);
                printf("Enter the User2 id : ");
                scanf("%d",&user2);
                if(user1 == user2 || user1 > numuser || user2 > numuser || user1<0||user2<0){
                    printf("Invalid Request.... Try Again\n\n");
                    break;
                }
                else{
                    addFriend(user1,user2);
                }
                break;
            case 2:
                printf("Enter the User id : ");
                scanf("%d",&user);
                if(user < 0 || user > MAX){
                    printf("Invalid Request.... Try Again\n\n");
                }
                else{
                    viewConnections(user,numuser);
                }
                break;
            case 3:
                printf("Enter the User id : ");
                scanf("%d",&user);
                if(user < 0 || user > MAX){
                        printf("Invalid Request.... Try Again\n\n");
                }
                else{
                    suggestFriends(user,numuser);
                }
                break;
            case 4:
                viewAllConnections(numuser);
                break;
            case 5:
                exit(0);
            default :
                printf("\nOOPS! ... invalid Options... Try again %c\n\n",2);
        }
    }

    return 0;
}

```
