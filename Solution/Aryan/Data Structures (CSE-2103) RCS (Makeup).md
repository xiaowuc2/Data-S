### 1A. Explain different dynamic memory allocation and de-allocation functions with prototype and example to each.

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

#### 
