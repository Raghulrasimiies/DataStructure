### Question:
**Write a program to modify an `m x n` matrix such that if an element is `0`, then its entire row and column are set to `0`.**

#### Example:
**Input:**
```
1 2 3
4 0 8
3 1 8
```

**Output:**
```
1 0 3
0 0 0
3 0 8
```

---

```c
#include <stdio.h>
void get_mat(int n, int m, int arr[m][n]);
void display_mat(int n, int m, int arr[m][n]);
void updated_mat(int n, int m, int arr[m][n]);

int main() {
    int n, m;
    printf("Enter the number of rows: ");
    scanf("%d", &m);
    printf("Enter the number of columns: ");
    scanf("%d", &n);
    int arr[m][n];
    get_mat(m, n, arr);
    display_mat(m, n, arr);
    updated_mat(m, n, arr);
    display_mat(m, n, arr);
    return 0;
}
void get_mat(int n, int m, int arr[m][n]) {
    for(int i = 0; i < m; i++) {
        for(int j = 0; j < n; j++) {
            scanf("%d", &arr[i][j]);
        }
    }
}
void display_mat(int n, int m, int arr[m][n]) {
    printf("\nYour Matrix is:\n\t");
    for(int i = 0; i < m; i++) {
        for(int j = 0; j < n; j++) {
            printf("%d ", arr[i][j]);
        }
        printf("\n\t");
    }
}

void updated_mat(int n, int m, int arr[m][n]) {
    int row[100] = {0}, col[100] = {0};
    for(int i = 0; i < m; i++) {
        for(int j = 0; j < n; j++) {
            if(arr[i][j] == 0) {
                printf("\nThe zero is in the position of arr[%d][%d]\n", i, j);
                row[i] = 1;
                col[j] = 1;
            }
        }
    }
    for(int i = 0; i < m; i++) {
        if(row[i] == 1) {
            for(int j = 0; j < n; j++) {
                arr[i][j] = 0;
            }
        }
    }
    for(int i = 0; i < n; i++) {
        if(col[i] == 1) {
            for(int j = 0; j < m; j++) {
                arr[j][i] = 0;
            }
        }
    }
}
```

---

### Assignment Questions

1. What is a struct in C, and how is it different from an array?
2. Can we have a pointer to a struct? Provide an example.
3. How do you access struct members using a pointer to a struct?
4. What is the difference between struct and typedef in C?
5. Can a struct contain a pointer to itself? Provide an example.
6. What happens when a struct is passed to a function by value?
7. What is a union in C, and how is it different from a struct?
8. What are the advantages of using a union?
9. What is an enum in C, and why is it used?
10. How can you define an enum and use it in a program?
11. What are the different storage classes in C?
12. What is the default storage class of a local variable in C?
13. What is the purpose of the register storage class?
14. Explain the difference between the static and extern storage classes.
15. Write a program to demonstrate the behavior of a static variable inside a function.

---
