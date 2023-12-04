### 1A. Explain different dynamic memory allocation and de-allocation functions with prototype and example to each.

Dynamic memory allocation and deallocation in C and C++ are typically handled using functions from the standard library, such as malloc, calloc, realloc, and free. Here's an explanation of each, along with their prototypes and examples:

**1. malloc:**
   - **Prototype:** `void *malloc(size_t size);`
   - **Explanation:** Allocates a block of memory of the specified size in bytes.
   - **Example:**
     ```c
     int *arr = (int *)malloc(5 * sizeof(int));
     ```

**2. calloc:**
   - **Prototype:** `void *calloc(size_t num_elements, size_t element_size);`
   - **Explanation:** Allocates a block of memory for an array of elements, each initialized to zero.
   - **Example:**
     ```c
     int *arr = (int *)calloc(5, sizeof(int));
     ```

**3. realloc:**
   - **Prototype:** `void *realloc(void *ptr, size_t new_size);`
   - **Explanation:** Changes the size of the memory block pointed to by `ptr` to the specified new size.
   - **Example:**
     ```c
     int *arr = (int *)malloc(5 * sizeof(int));
     // ... (use arr)
     arr = (int *)realloc(arr, 10 * sizeof(int));
     ```

**4. free:**
   - **Prototype:** `void free(void *ptr);`
   - **Explanation:** Deallocates the memory block pointed to by `ptr`, making it available for further allocations.
   - **Example:**
     ```c
     int *arr = (int *)malloc(5 * sizeof(int));
     // ... (use arr)
     free(arr);
     ```

Here's a more detailed example using all these functions together:

```c
#include <stdio.h>
#include <stdlib.h>

int main() {
    // malloc example
    int *arr1 = (int *)malloc(5 * sizeof(int));
    for (int i = 0; i < 5; ++i) {
        arr1[i] = i + 1;
    }

    // calloc example
    int *arr2 = (int *)calloc(5, sizeof(int));

    // realloc example
    arr1 = (int *)realloc(arr1, 10 * sizeof(int));

    // free example
    free(arr1);
    free(arr2);

    return 0;
}
```

----

### 1B. Write a complete C program to illustrate passing and returning structures to and from functions through pointers by to defining a structure FRACTION with numerator and denominator (integers) as its data members. Write the functions with following prototypes. Use type defined structure.
```
void getFr(FRACTION * );
void printFr( FRACTION *) ;
FRACTION * multiFr( FRACTION *, FRACTION *);
```

```c
#include <stdio.h>

// Define the FRACTION structure
typedef struct {
    int numerator;
    int denominator;
} FRACTION;

// Function to get input for a fraction
void getFr(FRACTION *fraction) {
    printf("Enter numerator: ");
    scanf("%d", &(fraction->numerator));

    printf("Enter denominator: ");
    scanf("%d", &(fraction->denominator));
}

// Function to print a fraction
void printFr(FRACTION *fraction) {
    printf("%d / %d\n", fraction->numerator, fraction->denominator);
}

// Function to multiply two fractions and return the result
FRACTION *multiFr(FRACTION *frac1, FRACTION *frac2) {
    static FRACTION result; // Static variable to store the result

    // Multiply numerators and denominators separately
    result.numerator = frac1->numerator * frac2->numerator;
    result.denominator = frac1->denominator * frac2->denominator;

    return &result; // Return a pointer to the result
}

int main() {
    FRACTION fraction1, fraction2, *result;

    // Get input for the first fraction
    printf("Enter details for the first fraction:\n");
    getFr(&fraction1);

    // Get input for the second fraction
    printf("\nEnter details for the second fraction:\n");
    getFr(&fraction2);

    // Multiply fractions and get the result
    result = multiFr(&fraction1, &fraction2);

    // Print the input fractions and the result
    printf("\nFirst fraction: ");
    printFr(&fraction1);

    printf("Second fraction: ");
    printFr(&fraction2);

    printf("Result of multiplication: ");
    printFr(result);

    return 0;
}
```

---

### 1C. Explain the functionality of the following recursive function.
```
int foo(int x, int y)
{
if(x == 0) return y;
else
return foo(x – 1,x +y);
}
```
Base Case
c
Copy code
if (x == 0)
    return y;
If x is equal to 0, the function returns the value of y. This is the base case of the recursion. When x reaches 0, the recursion stops, and the function starts returning values.

Recursive Case
c
Copy code
else
    return foo(x - 1, x + y);
If x is not equal to 0, the function calls itself recursively with modified parameters: foo(x - 1, x + y). The value of x is decreased by 1, and the value of y is updated to x + y. This means the function is moving toward the base case by decreasing x in each recursive call.

int result = foo(3, 1);

The function calls would be as follows:

foo(3, 1) calls foo(2, 4)
foo(2, 4) calls foo(1, 6)
foo(1, 6) calls foo(0, 7)
foo(0, 7) returns 7 (base case)
So, the final result is 7.


### 2A. Write a complete C program to perform the following operations on a queue of integers using only standard queue operations,
```
i) Insertq(x): Add an item x to queue.
ii) Deleteq() : Remove an item from queue.
iii) Display(): Displaying queue elements
iv) Reverse() : Contents of queue are reversed using only standard queue operations.
```

```c
#include <stdio.h>
#include <stdlib.h>

#define MAX_SIZE 100

// Define structure for a queue
typedef struct {
    int data[MAX_SIZE];
    int front;
    int rear;
} Queue;

// Function to initialize an empty queue
void initializeQueue(Queue *q) {
    q->front = -1;
    q->rear = -1;
}

// Function to check if the queue is empty
int isEmpty(Queue *q) {
    return q->front == -1;
}

// Function to check if the queue is full
int isFull(Queue *q) {
    return (q->rear + 1) % MAX_SIZE == q->front;
}

// Function to insert an item into the queue
void insertq(Queue *q, int x) {
    if (isFull(q)) {
        printf("Queue is full. Cannot insert %d.\n", x);
    } else {
        if (isEmpty(q)) {
            q->front = 0; // Adjust front if the queue is initially empty
        }
        q->rear = (q->rear + 1) % MAX_SIZE;
        q->data[q->rear] = x;
        printf("%d inserted into the queue.\n", x);
    }
}

// Function to delete an item from the queue
void deleteq(Queue *q) {
    if (isEmpty(q)) {
        printf("Queue is empty. Cannot delete.\n");
    } else {
        int deletedItem = q->data[q->front];
        if (q->front == q->rear) {
            // If there was only one element, reset front and rear
            q->front = -1;
            q->rear = -1;
        } else {
            // Move front to the next element in the queue
            q->front = (q->front + 1) % MAX_SIZE;
        }
        printf("%d deleted from the queue.\n", deletedItem);
    }
}

// Function to display the contents of the queue
void display(Queue *q) {
    if (isEmpty(q)) {
        printf("Queue is empty.\n");
    } else {
        printf("Queue elements: ");
        int i = q->front;
        do {
            printf("%d ", q->data[i]);
            i = (i + 1) % MAX_SIZE;
        } while (i != (q->rear + 1) % MAX_SIZE);
        printf("\n");
    }
}

// Function to reverse the contents of the queue
void reverse(Queue *q) {
    if (isEmpty(q) || q->front == q->rear) {
        // Nothing to reverse if the queue is empty or has only one element
        printf("Queue is empty or has only one element. Cannot reverse.\n");
    } else {
        // Reverse by swapping front and rear while traversing the queue
        int temp;
        while (q->front < q->rear) {
            temp = q->data[q->front];
            q->data[q->front] = q->data[q->rear];
            q->data[q->rear] = temp;
            q->front = (q->front + 1) % MAX_SIZE;
            q->rear = (q->rear - 1 + MAX_SIZE) % MAX_SIZE;
        }
        printf("Queue reversed.\n");
    }
}

int main() {
    Queue myQueue;
    initializeQueue(&myQueue);

    insertq(&myQueue, 10);
    insertq(&myQueue, 20);
    insertq(&myQueue, 30);
    insertq(&myQueue, 40);

    display(&myQueue);

    deleteq(&myQueue);

    display(&myQueue);

    reverse(&myQueue);

    display(&myQueue);

    return 0;
}

```
---

### 2B. Write a complete C program to implement push, pop and display operations of a stack using dynamic array to hold 5 integers. If the stack is full when the push operation is called, it must increase the size of the stack by 5 more integers.

```c
#include <stdio.h>
#include <stdlib.h>

#define INITIAL_CAPACITY 5

// Define structure for a stack
typedef struct {
    int *array;
    int top;
    int capacity;
} Stack;

// Function to initialize an empty stack
void initializeStack(Stack *stack) {
    stack->array = (int *)malloc(INITIAL_CAPACITY * sizeof(int));
    if (stack->array == NULL) {
        fprintf(stderr, "Memory allocation failed.\n");
        exit(EXIT_FAILURE);
    }
    stack->top = -1;
    stack->capacity = INITIAL_CAPACITY;
}

// Function to check if the stack is empty
int isEmpty(Stack *stack) {
    return stack->top == -1;
}

// Function to push an item onto the stack
void push(Stack *stack, int value) {
    if (stack->top == stack->capacity - 1) {
        // Stack is full, need to increase its size
        stack->capacity += 5;
        stack->array = (int *)realloc(stack->array, stack->capacity * sizeof(int));
        if (stack->array == NULL) {
            fprintf(stderr, "Memory allocation failed.\n");
            exit(EXIT_FAILURE);
        }
    }
    stack->top++;
    stack->array[stack->top] = value;
    printf("%d pushed onto the stack.\n", value);
}

// Function to pop an item from the stack
void pop(Stack *stack) {
    if (isEmpty(stack)) {
        printf("Stack is empty. Cannot pop.\n");
    } else {
        printf("%d popped from the stack.\n", stack->array[stack->top]);
        stack->top--;
    }
}

// Function to display the contents of the stack
void display(Stack *stack) {
    if (isEmpty(stack)) {
        printf("Stack is empty.\n");
    } else {
        printf("Stack elements: ");
        for (int i = 0; i <= stack->top; i++) {
            printf("%d ", stack->array[i]);
        }
        printf("\n");
    }
}

// Function to deallocate memory used by the stack
void deallocateStack(Stack *stack) {
    free(stack->array);
}

int main() {
    Stack myStack;
    initializeStack(&myStack);

    push(&myStack, 10);
    push(&myStack, 20);
    push(&myStack, 30);
    push(&myStack, 40);
    push(&myStack, 50);

    display(&myStack);

    push(&myStack, 60);
    push(&myStack, 70);
    push(&myStack, 80);

    display(&myStack);

    pop(&myStack);

    display(&myStack);

    // Deallocate memory used by the stack
    deallocateStack(&myStack);

    return 0;
}


```

---

### 3A. Write a function to add two polynomials, polynomial A, and polynomial B, represented as singly linked lists. The function should accept pointers to linked lists representing two polynomials and return a pointer to the linked list representing the sum.

```c
#include <stdio.h>
#include <stdlib.h>

// Define structure for a node in the linked list representing a term in a polynomial
typedef struct Node {
    int coefficient;
    int exponent;
    struct Node* next;
} Node;

// Function to add two polynomials represented as linked lists
Node* addPolynomials(Node* polyA, Node* polyB) {
    Node* result = NULL; // Resultant polynomial
    Node* tail = NULL;   // Pointer to the last node in the result polynomial

    while (polyA != NULL || polyB != NULL) {
        // Create a new node for the result
        Node* newNode = (Node*)malloc(sizeof(Node));
        if (newNode == NULL) {
            fprintf(stderr, "Memory allocation failed.\n");
            exit(EXIT_FAILURE);
        }
        newNode->next = NULL;

        // Add the terms of polynomial A and B
        if (polyA == NULL) {
            newNode->coefficient = polyB->coefficient;
            newNode->exponent = polyB->exponent;
            polyB = polyB->next;
        } else if (polyB == NULL) {
            newNode->coefficient = polyA->coefficient;
            newNode->exponent = polyA->exponent;
            polyA = polyA->next;
        } else {
            // Both polynomials have terms
            if (polyA->exponent > polyB->exponent) {
                newNode->coefficient = polyA->coefficient;
                newNode->exponent = polyA->exponent;
                polyA = polyA->next;
            } else if (polyA->exponent < polyB->exponent) {
                newNode->coefficient = polyB->coefficient;
                newNode->exponent = polyB->exponent;
                polyB = polyB->next;
            } else {
                // Exponents are equal, add coefficients
                newNode->coefficient = polyA->coefficient + polyB->coefficient;
                newNode->exponent = polyA->exponent;
                polyA = polyA->next;
                polyB = polyB->next;
            }
        }

        // Append the new node to the result polynomial
        if (result == NULL) {
            result = newNode;
            tail = result;
        } else {
            tail->next = newNode;
            tail = newNode;
        }
    }

    return result;
}

```

---

###
