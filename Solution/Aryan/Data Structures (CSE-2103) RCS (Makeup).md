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
