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

### 3B. Given a singly linked list, write a complete C program to find and display the middle element of the linked list. If there are even number nodes, display the second middle element.

```c
#include <stdio.h>
#include <stdlib.h>

// Define structure for a node in the linked list
typedef struct Node {
    int data;
    struct Node* next;
} Node;

// Function to insert a node at the end of the linked list
Node* insertAtEnd(Node* head, int value) {
    Node* newNode = (Node*)malloc(sizeof(Node));
    if (newNode == NULL) {
        fprintf(stderr, "Memory allocation failed.\n");
        exit(EXIT_FAILURE);
    }
    newNode->data = value;
    newNode->next = NULL;

    if (head == NULL) {
        // If the list is empty, the new node becomes the head
        head = newNode;
    } else {
        // Traverse to the end of the list and add the new node
        Node* current = head;
        while (current->next != NULL) {
            current = current->next;
        }
        current->next = newNode;
    }

    return head;
}

// Function to find and display the middle element of the linked list
void findAndDisplayMiddle(Node* head) {
    if (head == NULL) {
        printf("Linked list is empty.\n");
        return;
    }

    Node* slow = head;
    Node* fast = head;

    // Move slow by one step and fast by two steps until fast reaches the end
    while (fast != NULL && fast->next != NULL) {
        slow = slow->next;
        fast = fast->next->next;
    }

    printf("Middle element(s): ");

    // If the number of nodes is odd, there is only one middle element
    if (fast == NULL) {
        printf("%d\n", slow->data);
    } else {
        // If the number of nodes is even, display the second middle element
        printf("%d and %d\n", slow->data, slow->next->data);
    }
}

// Function to display the linked list
void displayList(Node* head) {
    printf("Linked list: ");
    while (head != NULL) {
        printf("%d ", head->data);
        head = head->next;
    }
    printf("\n");
}

// Function to free the memory allocated for the linked list
void freeList(Node* head) {
    Node* current = head;
    while (current != NULL) {
        Node* next = current->next;
        free(current);
        current = next;
    }
}

int main() {
    Node* head = NULL;

    // Insert elements into the linked list
    head = insertAtEnd(head, 1);
    head = insertAtEnd(head, 2);
    head = insertAtEnd(head, 3);
    head = insertAtEnd(head, 4);
    head = insertAtEnd(head, 5);

    // Display the linked list
    displayList(head);

    // Find and display the middle element(s)
    findAndDisplayMiddle(head);

    // Free the memory allocated for the linked list
    freeList(head);

    return 0;
}

```

---

### 3C. Write a C function to invert a singly linked list. The function should accept a pointer to the given list and return a pointer to the inverted list.

```c
#include <stdio.h>
#include <stdlib.h>

// Define structure for a node in the linked list
typedef struct Node {
    int data;
    struct Node* next;
} Node;

// Function to insert a node at the end of the linked list
Node* insertAtEnd(Node* head, int value) {
    Node* newNode = (Node*)malloc(sizeof(Node));
    if (newNode == NULL) {
        fprintf(stderr, "Memory allocation failed.\n");
        exit(EXIT_FAILURE);
    }
    newNode->data = value;
    newNode->next = NULL;

    if (head == NULL) {
        // If the list is empty, the new node becomes the head
        head = newNode;
    } else {
        // Traverse to the end of the list and add the new node
        Node* current = head;
        while (current->next != NULL) {
            current = current->next;
        }
        current->next = newNode;
    }

    return head;
}

// Function to invert a singly linked list
Node* invertList(Node* head) {
    Node* prev = NULL;
    Node* current = head;
    Node* nextNode = NULL;

    while (current != NULL) {
        // Save the next node
        nextNode = current->next;

        // Reverse the link
        current->next = prev;

        // Move one step forward in the list
        prev = current;
        current = nextNode;
    }

    // At the end, 'prev' will be the new head of the inverted list
    return prev;
}

// Function to display the linked list
void displayList(Node* head) {
    printf("Linked list: ");
    while (head != NULL) {
        printf("%d ", head->data);
        head = head->next;
    }
    printf("\n");
}

// Function to free the memory allocated for the linked list
void freeList(Node* head) {
    Node* current = head;
    while (current != NULL) {
        Node* next = current->next;
        free(current);
        current = next;
    }
}

int main() {
    Node* originalList = NULL;

    // Insert elements into the linked list
    originalList = insertAtEnd(originalList, 1);
    originalList = insertAtEnd(originalList, 2);
    originalList = insertAtEnd(originalList, 3);
    originalList = insertAtEnd(originalList, 4);
    originalList = insertAtEnd(originalList, 5);

    // Display the original linked list
    printf("Original ");
    displayList(originalList);

    // Invert the linked list
    Node* invertedList = invertList(originalList);

    // Display the inverted linked list
    printf("Inverted ");
    displayList(invertedList);

    // Free the memory allocated for both lists
    freeList(originalList);
    freeList(invertedList);

    return 0;
}

```

---

### Write a complete C program to do the following,
```
i) Create a binary tree
ii) Convert the created binary tree into binary search tree without changing structure of
the tree.
iii) Traverse the tree in preorder
```

```c
#include <stdio.h>
#include <stdlib.h>

// Define structure for a node in the binary tree
typedef struct Node {
    int data;
    struct Node* left;
    struct Node* right;
} Node;

// Function to create a new node in the binary tree
Node* createNode(int value) {
    Node* newNode = (Node*)malloc(sizeof(Node));
    if (newNode == NULL) {
        fprintf(stderr, "Memory allocation failed.\n");
        exit(EXIT_FAILURE);
    }
    newNode->data = value;
    newNode->left = NULL;
    newNode->right = NULL;
    return newNode;
}

// Function to insert a node into the binary tree
Node* insertNode(Node* root, int value) {
    if (root == NULL) {
        return createNode(value);
    }

    if (value < root->data) {
        root->left = insertNode(root->left, value);
    } else {
        root->right = insertNode(root->right, value);
    }

    return root;
}

// Function to convert binary tree to binary search tree
void binaryTreeToBST(Node* root, int* sortedArray, int* index) {
    if (root == NULL) {
        return;
    }

    // Traverse the tree in in-order
    binaryTreeToBST(root->left, sortedArray, index);

    // Update the node data with the sorted values
    root->data = sortedArray[(*index)++];

    // Continue traversing the tree
    binaryTreeToBST(root->right, sortedArray, index);
}

// Function to traverse the tree in preorder
void preorderTraversal(Node* root) {
    if (root != NULL) {
        printf("%d ", root->data);
        preorderTraversal(root->left);
        preorderTraversal(root->right);
    }
}

// Function to free the memory allocated for the tree
void freeTree(Node* root) {
    if (root != NULL) {
        freeTree(root->left);
        freeTree(root->right);
        free(root);
    }
}

int main() {
    Node* root = NULL;

    // Create a binary tree
    root = insertNode(root, 8);
    root = insertNode(root, 3);
    root = insertNode(root, 10);
    root = insertNode(root, 1);
    root = insertNode(root, 6);
    root = insertNode(root, 14);
    root = insertNode(root, 4);
    root = insertNode(root, 7);
    root = insertNode(root, 13);

    // Traverse and display the original binary tree in preorder
    printf("Original Binary Tree (Preorder): ");
    preorderTraversal(root);
    printf("\n");

    // Count the number of nodes in the tree
    int nodeCount = 0;
    preorderTraversal(root); // Traversing in preorder to get the count
    printf("\n");

    // Store the values of the tree in an array
    int *sortedArray = (int *)malloc(nodeCount * sizeof(int));
    int index = 0;
    binaryTreeToBST(root, sortedArray, &index);

    // Traverse and display the modified binary search tree in preorder
    printf("Binary Search Tree (Preorder): ");
    preorderTraversal(root);
    printf("\n");

    // Free the memory allocated for the tree
    freeTree(root);

    return 0;
}

```
---

###


Certainly! We'll start with an empty tree and insert each number from the given set {100, 80, 90, 88, 200, 150, 179, 300, 400} into the binary search tree in the order they are read from left to right.

Here's the step-by-step construction of the binary search tree:

```
Insert 100 (Root)

Copy code
   100
Insert 80

Copy code
   100
  /
 80
Insert 90

Copy code
   100
  /   \
 80   90
Insert 88

markdown
Copy code
   100
  /   \
 80    90
       /
     88
Insert 200

markdown
Copy code
   100
  /   \
 80    200
       /   
     90
       \
       88
Insert 150

markdown
Copy code
   100
  /   \
 80    200
       /   
     90
       \
       88
        \
       150
Insert 179

markdown
Copy code
   100
  /   \
 80    200
       /   
     90
       \
       88
        \
       150
          \
        179
Insert 300

markdown
Copy code
   100
  /   \
 80    200
       /   \
     90    300
       \
       88
        \
       150
          \
        179
Insert 400

markdown
Copy code
   100
  /   \
 80    200
       /   \
     90    300
       \      \
       88     400
        \
       150
          \
        179
```
The constructed binary search tree is now complete.

Now, let's find the postorder traversal sequence:

Postorder Traversal Sequence: 80, 88, 179, 150, 90, 400, 300, 200, 100

So, the postorder traversal sequence of the constructed tree is 80, 88, 179, 150, 90, 400, 300, 200, 100.

---

### 5B Define B-tree of order m and also mention its properties. What do you mean by 2-3-4 tree, explain with an example?

B-Tree of Order m:
A B-tree of order m is a self-balancing tree data structure that maintains sorted data and allows searches, insertions, and deletions in logarithmic time. In a B-tree of order  m, each internal node can have a variable number of keys, typically ranging from m/2

m/2 to m−1
m−1, and each internal node has 1
1 more child than the number of keys it contains.

Properties of a B-Tree:
Degree and Keys:

Each internal node can have at most m−1 m−1 keys.
Each internal node can have at most m children.
Each internal node, except for the root, must have at least m/2 m/2 children.
Keys and Values:

Keys in a node are stored in sorted order.
The keys of a node divide its children into ranges, with the leftmost child having keys less than the leftmost key, and so on.
Leaf Nodes:

All leaf nodes are at the same level, providing a balanced structure.
Root Node:

The root node can have as few as 1 key.
Search, Insertion, and Deletion:

Search, insertion, and deletion operations are efficient with logarithmic time complexity.

#### 2-3-4 Tree:

A 2-3-4 tree is a specific type of B-tree of order 

m = 4

m=4, where each internal node can have 2, 3, or 4 children. It is a balanced search tree that maintains sorted data and has the following properties:

Nodes:

Each internal node can have 2, 3, or 4 children.
Leaf nodes contain data and have no children.
Keys:

Internal nodes can have 1, 2, or 3 keys.
Balanced Structure:

All leaf nodes are at the same level, providing a balanced structure.
Search and Insertion:

Search and insertion operations are efficient with logarithmic time complexity.
Example of a 2-3-4 Tree:
Consider the following 2-3-4 tree:

```
                [40, 80]
              /       |        \
       [20]    [60]     [100, 120]
      /   \    /  \     /    |    \
  [10] [30] [50] [70] [90] [110] [130]

```
#### In this 2-3-4 tree:

Each internal node can have 2, 3, or 4 children.
Leaf nodes contain the actual data.
The tree is balanced, and all leaf nodes are at the same level.
Search and insertion operations are efficient.

