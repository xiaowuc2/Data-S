### 2A Write an algorithm that checks whether a sequence of integers read from the keyboard form a palindrome. Return zero, if the sequence does not form a palindrome. Write a C function for the algorithm and trace its output with sequence {44, 12, 64, 32, 32, 64, 12, 44}. Note that you may use stacks and/or queues in an array implementation but cannot use any other structures such as arrays, trees or linked lists. The input sequence is not available as an array but should be read from the keyboard and cannot be stored in a temporary array. All the functions to implement stack/queue functionalities need not be shown. Provide type definition for your data structure.

```
#include <stdio.h>
#include <stdlib.h>

// Define a structure for the stack
typedef struct {
    int capacity;
    int top;
    int* array;
} Stack;

// Function to initialize a stack
Stack* createStack(int capacity) {
    Stack* stack = (Stack*)malloc(sizeof(Stack));
    stack->capacity = capacity;
    stack->top = -1;
    stack->array = (int*)malloc(capacity * sizeof(int));
    return stack;
}

// Function to check if the stack is empty
int isEmpty(Stack* stack) {
    return stack->top == -1;
}

// Function to push an element onto the stack
void push(Stack* stack, int item) {
    stack->array[++stack->top] = item;
}

// Function to pop an element from the stack
int pop(Stack* stack) {
    return stack->array[stack->top--];
}

// Function to check whether a sequence is a palindrome
int isPalindrome() {
    // Create a stack to store the sequence
    Stack* stack = createStack(100); // Adjust the capacity as needed

    // Read integers from the keyboard until -1 is encountered
    int num;
    printf("Enter a sequence of integers (enter -1 to stop):\n");
    scanf("%d", &num);

    while (num != -1) {
        push(stack, num);
        scanf("%d", &num);
    }

    // Reset num to read the sequence again
    scanf("%d", &num);

    // Check if the sequence is a palindrome
    while (num != -1) {
        if (isEmpty(stack) || pop(stack) != num) {
            free(stack->array);
            free(stack);
            return 0; // Not a palindrome
        }
        scanf("%d", &num);
    }

    // Clean up and return 1 if the sequence is a palindrome
    free(stack->array);
    free(stack);
    return 1;
}

int main() {
    // Check if the sequence is a palindrome
    if (isPalindrome()) {
        printf("The sequence is a palindrome.\n");
    } else {
        printf("The sequence is not a palindrome.\n");
    }

    return 0;
}

```

### 2B Complete the following table by translating the given infix form. Also draw the expression tree in each case.
```
Infix expression: P*Q+R/S
Postfix expression: PQ*RS/+
Prefix expression: +*PQ/RS
Expression tree:
        +
       / \
      *   /
     / \  |
    P   Q R
             \
              S

Infix expression: P*(Q+R)/S
Postfix expression: PQR+*S/
Prefix expression: /*P+QRS
Expression tree:
       *
      / \
     P   /
        / \
       +   S
      / \
     Q   R

Infix expression: P*(Q+R/S)
Postfix expression: PQRS/+*
Prefix expression: *P/+QRS
Expression tree:
        *
       / \
      P   /
         / \
        +   S
       / \
      Q   /
         /
        R

```



