## **C Programming Cheat Sheet**

### **1. Basics**

- **Hello World**
  ```c
  #include <stdio.h>
  
  int main() {
      printf("Hello, World!\n");
      return 0;
  }
  ```

- **Data Types**
  ```c
  int a = 10;        // Integer
  float b = 5.5f;    // Floating point
  double c = 3.1415; // Double precision floating point
  char d = 'A';      // Character
  ```

- **Constants**
  ```c
  #define PI 3.14159
  ```

- **Variables**
  ```c
  int x = 5;
  ```

- **Operators**
  ```c
  int sum = a + b;        // Addition
  int diff = a - b;       // Subtraction
  int product = a * b;    // Multiplication
  int quotient = a / b;   // Division
  int remainder = a % b;  // Modulus
  ```

- **Control Flow**
  - **If-Else**
    ```c
    if (x > 0) {
        printf("Positive\n");
    } else if (x < 0) {
        printf("Negative\n");
    } else {
        printf("Zero\n");
    }
    ```

  - **Switch-Case**
    ```c
    switch (x) {
        case 1:
            printf("One\n");
            break;
        case 2:
            printf("Two\n");
            break;
        default:
            printf("Other\n");
    }
    ```

  - **Loops**
    - **For Loop**
      ```c
      for (int i = 0; i < 10; i++) {
          printf("%d\n", i);
      }
      ```

    - **While Loop**
      ```c
      int i = 0;
      while (i < 10) {
          printf("%d\n", i);
          i++;
      }
      ```

    - **Do-While Loop**
      ```c
      int i = 0;
      do {
          printf("%d\n", i);
          i++;
      } while (i < 10);
      ```

### **2. Functions**

- **Function Definition**
  ```c
  int add(int a, int b) {
      return a + b;
  }
  ```

- **Function Declaration**
  ```c
  int add(int, int);  // Function prototype
  ```

- **Calling a Function**
  ```c
  int result = add(5, 3);
  ```

### **3. Pointers**

- **Pointer Basics**
  ```c
  int x = 10;
  int *ptr = &x;     // Pointer to x
  ```

- **Dereferencing**
  ```c
  int value = *ptr;  // value is 10
  ```

- **Pointer Arithmetic**
  ```c
  int arr[5] = {1, 2, 3, 4, 5};
  int *p = arr;
  p++;               // p points to arr[1]
  ```

### **4. Arrays and Strings**

- **Array Declaration**
  ```c
  int arr[5] = {1, 2, 3, 4, 5};
  ```

- **String Declaration**
  ```c
  char str[] = "Hello";
  ```

- **String Functions**
  ```c
  #include <string.h>
  
  int len = strlen(str);   // Length of the string
  ```

### **5. Structs and Unions**

- **Struct Definition**
  ```c
  typedef struct {
      int id;
      char name[50];
  } Person;
  ```

- **Union Definition**
  ```c
  typedef union {
      int i;
      float f;
  } Data;
  ```

### **6. File I/O**

- **Opening a File**
  ```c
  FILE *file = fopen("file.txt", "r");
  ```

- **Reading from a File**
  ```c
  char buffer[100];
  fread(buffer, sizeof(char), 100, file);
  ```

- **Writing to a File**
  ```c
  fwrite(buffer, sizeof(char), 100, file);
  ```

- **Closing a File**
  ```c
  fclose(file);
  ```

### **7. Error Handling**

- **Error Checking**
  ```c
  if (file == NULL) {
      perror("Error opening file");
      return -1;
  }
  ```

### **8. Advanced Data Types and Structures**

- **Structs with Functions**
  ```c
  typedef struct {
      int id;
      char name[50];
      void (*print)(struct Person*);
  } Person;

  void print_person(Person *p) {
      printf("ID: %d, Name: %s\n", p->id, p->name);
  }
  ```

- **Bitfields**
  ```c
  typedef struct {
      unsigned int isOn : 1;
      unsigned int level : 7;
  } Device;
  ```

### **9. Memory Management**

- **Dynamic Allocation**
  ```c
  int *arr = (int *)malloc(10 * sizeof(int));
  ```

- **Reallocation**
  ```c
  arr = (int *)realloc(arr, 20 * sizeof(int));
  ```

- **Freeing Memory**
  ```c
  free(arr);
  ```

### **10. Advanced Techniques**

- **Inline Assembly**
  ```c
  __asm__("movl $0, %eax");
  ```

- **Volatile Keyword**
  ```c
  volatile int flag;
  ```

- **Setjmp and Longjmp**
  ```c
  #include <setjmp.h>
  
  jmp_buf buf;

  void func() {
      if (setjmp(buf) != 0) {
          // Code to run after longjmp
      }
  }

  void longjmp_func() {
      longjmp(buf, 1);
  }
  ```

### **11. Concurrency**

- **Threads (POSIX)**
  ```c
  #include <pthread.h>
  
  void *thread_function(void *arg) {
      // Thread code
  }

  pthread_t thread;
  pthread_create(&thread, NULL, thread_function, NULL);
  pthread_join(thread, NULL);
  ```

- **Mutexes**
  ```c
  pthread_mutex_t mutex;
  pthread_mutex_init(&mutex, NULL);
  pthread_mutex_lock(&mutex);
  // Critical section
  pthread_mutex_unlock(&mutex);
  pthread_mutex_destroy(&mutex);
  ```

### **12. Macros and Preprocessor Directives**

- **Macros**
  ```c
  #define MAX(x, y) ((x) > (y) ? (x) : (y))
  ```

- **Conditional Compilation**
  ```c
  #ifdef DEBUG
      printf("Debug mode\n");
  #endif
  ```

- **Include Guards**
  ```c
  #ifndef HEADER_H
  #define HEADER_H
  // header file contents
  #endif
  ```

### **13. Debugging and Profiling**

- **GDB Commands**
  ```gdb
  break main     // Set a breakpoint at main
  run            // Start execution
  next           // Step over
  step           // Step into
  print var      // Print variable
  continue       // Continue execution
  ```

- **Valgrind**
  ```bash
  valgrind --leak-check=full ./my_program
  ```

### **14. Best Practices**

- **Code Formatting**
  ```c
  // Use consistent indentation and spacing
  void example_function(int param) {
      if (param > 0) {
          printf("Positive\n");
      }
  }
  ```

- **Error Handling**
  ```c
  if (some_condition) {
      perror("Error message");
      exit(EXIT_FAILURE);
  }
  ```

- **Documentation**
  ```c
  /**
   * Function description.
   * @param param Description of parameter
   * @return Description of return value
   */
  int example_function(int param);
  ```

### **15. Common Algorithms**

- **Sorting (Quick Sort)**
  ```c
  void quicksort(int arr[], int low, int high) {
      // Quicksort implementation
  }
  ```

- **Binary Search**
  ```c
  int binary_search(int arr[], int size, int target) {
      int low = 0, high = size - 1;
      while (low <= high) {
          int mid = low + (high - low) / 2;
          if (arr[mid] == target) return mid;
          if (arr[mid] < target) low = mid + 1;
          else high = mid - 1;
      }
      return -1;
  }
  ```

---

This cheat sheet provides a comprehensive overview of both basic and advanced C programming concepts. Feel free to use it as a reference or expand upon it based on your specific needs!