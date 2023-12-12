# C Pointers and Addressing

In this lab you will be introduce to pointers and addressing as tool to understand computer memory.

1. Create a new C++ Console project called `PointersAndAddressing`.
2. Remember to rename the `PointersAndAddressing.cpp` to `PointersAndAddressing.c`
3. Open `PointersAndAddressing.c` and modify to look like below: 

    ```c
    #include <stdio.h>

    int main(){

        return 0;
    }
    ```

## Section 1: Pointers

Now it's time to see the why C is used for the basis of nearly all programming languages, operating systems, and embedded code. 

Pointers in C are relativley easy and fun to learn. Some C programming tasks are performed more easily with pointers, and other tasks, such as dynamic memory allocation, cannot be performed without using pointers. 

So it becomes necessary to learn pointers to become a perfect C programmer.

Let's start learning them in simple and easy steps.

Every variable is a memory location and every memory location has its address defined which can be accessed using ampersand `&` operator, which denotes an address in memory. 

4. Modify `main()` by entering the following code:

    ```
    ...
        int a=1, b =2 ,c =0;
    
        printf("Address for the variable a: %lu \n", (long)&a); // long casts the value in &a to a long integer, upto 32 bits
        printf("Address for the variable b: %lu\n", (long)&b);
        printf("Address for the variable c: %lu \n", (long)&c);
        return 0;
    }
    ```

    <details>
    <summary><b>Click for Expected Output</b></summary>
    <p></p>

    ```
    Address for the variable a: 140729126914124 
    Address for the variable b: 140729126914128
    Address for the variable c: 140729126914132 
    ```
    </details>


    So it looks like the address are almost next to each other, we call this **contiguous**.

    > **Notes:**
    >> - We must use format specifiers to tell the `printf()` how we would like our variables to be displayed.
    >> - So, `%` is the character for promising a specifier -> `%lu` means `unsigned long` and is 32 bits in size. 
    >>- memory address are **never** negative.

5. What would happen to the addresses if you ran the code again? **Try it!**

    <details>
    <summary>Well...</summary>

    You should have recieved different memory address locations, this because of the **Address Space Layout Randomiser** (ASLR) which provides a random address space for security reason. Consider if someone wanted to get certain information and new where it was stored all the time?

    </details>


## Section 2: What are Pointers?

A **pointer** is a variable whose value is the address of another variable, i.e., direct address of the memory location. Like any variable or constant, you must declare a pointer before using it to store any variable address. The general form of a pointer variable declaration is `type var-name`.

Here, type is the pointer's base type; it must be a valid C data type and var-name is the name of the pointer variable. The asterisk `*` used to declare a pointer is the same asterisk used for multiplication. 

However, in this statement the asterisk is being used to designate a variable as a pointer. Take a look at some of the valid pointer declarations:

```c
int    *ip;    /* pointer to an integer */
double *dp;    /* pointer to a double */
float  *fp;    /* pointer to a float */
char   *ch     /* pointer to a character */
```

The actual data type of the value of all pointers, whether integer, float, character, or otherwise, is the same, a long hexadecimal number that represents a memory address. The only difference between pointers of different data types is the data type of the variable or constant that the pointer points to.

## Section 3: How to Use Pointers?

There are a few important operations, which we will do with the help of pointers very frequently. **(a)** We define a pointer variable, **(b)** assign the address of a variable to a pointer and **(c)** finally access the value at the address available in the pointer variable. 

This is done by using unary operator `*` that returns the value of the variable located at the address specified by its operand. The following example makes use of these operations.

6. Again edit the contents of `main()` to match below:

    ``` c
    #include <stdio.h>

    int main () {

        int  a = 15;      /* actual variable declaration */
        int  *pointerToA; /* pointer variable declaration */

        pointerToA = &a;  /* store address of var in pointer variable*/

        printf("Address of A variable: %lu\n", (long)&a);

        /* address stored in pointer variable */
        printf("Address stored in pointerToA variable: %lu\n", (long)pointerToA);

        /* access the value using the pointer */
        printf("Value of *pointerToA variable: %d\n", *pointerToA);
        
        /* address of the pointer itself */
            printf("Address of pointerToA: %lu\n", (long)&pointerToA);

        return 0;
    }
    ```

7. Run the code and you should see something similar to below,remember to compile first:

    <details>
    <summary><b>Click for Expected Output</b></summary>
    <p></p>

    ```sh
    Address of A variable: 140720967560444
    Address stored in pointerToA variable: 140720967560444
    Value of *pointerToA variable: 15
    Address of pointerToA: 140720967560448
    ```
    </details>

----

## Section 4: Null Pointers

It is always a good practice to assign a `NULL` value to a pointer variable in case you do not have an exact address to be assigned. 

This is done at the time of variable declaration. A pointer that is assigned `NULL` is called a `NULL pointer`.

The `NULL pointer` is a constant with a value of zero defined in several standard libraries. 

8. Modify `main()` and enter the following:

    ``` c
    #include <stdio.h>

    int main () {

    int  *ptr = NULL;

    printf("The value of ptr is : %p\n", ptr  );
    
    return 0;
    }
    ```

9. Run the program:

    <details>
    <summary><b>Click for Expected Output</b></summary>
    <p></p>

    ```
    The value of ptr is : (nil)
    ```

    </details>

    - In most of the operating systems, programs are not permitted to access memory at address `0` because that memory is reserved by the operating system. 

    - However, the memory address 0 has special significance; it signals that the pointer is not intended to point to an accessible memory location. But by convention, if a pointer contains the `null` (zero) value, it is assumed to point to nothing.

    - To check for a null pointer, you can use an `if` statement as follows:

        ``` c
        if(ptr)     /* succeeds if p is not null */
        if(!ptr)    /* succeeds if p is null */
        ```
--------------

## Section 5: Pointers in Detail

Pointers have many but easy concepts and they are very important to `C` programming. The following important pointer concepts should be clear to any C programmer:

-  **Pointer arithmetic**

    There are four arithmetic operators that can be used in pointers:
    - `++` ,`--`, `+`, `-`

-  **Array of pointers**
   -  You can define arrays to hold a number of pointers.

- **Pointer to pointer**
   -  C allows you to have pointer on a pointer and so on.

- **Passing pointers to functions in C**
   -  Passing an argument by reference or by address enable the passed argument to be changed in the calling function by the called function.

-  **Return pointer from functions in C**
   -  C allows a function to return a pointer to the local variable, static variable, and dynamically allocated memory as well.


------------------- 

## Section 6: Exploring the memory

Now we can explore memory in a more detail way.

So one crucial thing to note here is that accessing memory locations and changes their values can be fatal for a system.

It is relativley simple to access memory addresses around your own entry point, let's assume you assign a variable called `a` and then you get the memory address. After you have this address you have a starting pointing to explore.

Modify `main()` with the following code snippets, remember to include the `#include<stdio.h>` and `int main(){return 0;}` lines of code:

1.  Define and assign an integer with the value 10, which we are going to use for looping.

    ``` c
    int bin = 10;
    ```

2.  Create another integer and this time give it the value 123456789.

    ``` c
    int value = 123456789:
    ```

3.  Initialise a new variable in the pointer region of the code to point to the address of `value`

    ``` c
    int* pointer = (&value);
    ```
4. Add the following `printf`s
   
   ```c
    printf("Memory Address        ||    Value        \n");
    printf("------------------------------------------\n");
   ```

5.  Now you need to write of the `for` loop to return the address the pointer holds and the value at that address.

    ``` c
    for (int i = 0; i < bin; ++i)
    {   


    }
    ```

5.  Inside the for loop between the braces { } enter this line to print out the values to console.

    ``` c
    printf(" %lu      ||    %d \t\t \n",(unsigned long)
    
    pointer,(unsigned int)*pointer);
    ```

6.  Finally, we need to take one off of the pointer\'s value thereby decreasing the address. Add the following direcitly on the line below`printf();`

    ``` c
    pointer = pointer - 1;
    ```

    <details>
    <summary><b>Click for Full Code</b></summary>
    <p></p>

    ```c
    #include <stdio.h>
    int main () {
        // define your variables in this region 
        int bin = 10;
        int value = 123456789;
        // end of variabl region
        
        // create a pointer here
        int* pointer = (&value);
        // end of pointer region
        
        printf("Memory Address        ||    Value        \n");
        printf("------------------------------------------\n");
        
        // put the `for` loop here
        for (int i = 0; i < bin; ++i)
        {   
            printf(" %lu      ||    %d \t\t \n",(unsigned long)pointer,(unsigned int)*pointer); 
            pointer = pointer-1;
        }
        // end of for loop
        return 0;
    }
    ```
    </details>


7. Run the code and you should see something like below: 


    <details>
    <summary><b>Click for Expected Output</b></summary>
    <p></p>

        Memory Address       ||    Value        
        ------------------------------------------
        140732118813652      ||    123456789 		 
        140732118813648      ||    0 		 
        140732118813644      ||    32582 		 
        140732118813640      ||    1938514379 		 
        140732118813636      ||    0 		 
        140732118813632      ||    2 		 
        140732118813628      ||    21928 		 
        140732118813624      ||    1008046784 		 
        140732118813620      ||    21928 		 
        140732118813616      ||    999510800 		 
    </details>

    >**Note:**
    >
    >> Remember you will get different memory address and other than the `123456789` value the rest of the values will be different.


   - Now that the script has executed you can see we have a list of 10 memory addresses and the values those address hold.

   - Again we see **contiguous** memory seperated by 4 byte address spaces.

   - We can see our the that on the first time the loop executes we get the memory address of our variable `bin` and the subsequent value of stored in the address `123456789`.

   - However, we can also see that as the for loop continues looping through we get our list of memory addresses and values inside those memory addresses.

## Subsection 6.1: Arrays

So lets quickly look at arrays from a memory prespective.

The `C` programming language can store arrays of any data type; `int`, `float`, `char`,... etc.

8.  This time we will store a `char[]` and print out the each element of the array and the corresponding memory address which will be formatted as a hexadecimal number. Modifiy `main()` to look like the following code:

    ``` c
    #include<stdio.h>
    #include<stdlib.h>
    int main ()
    {
        int n = 11, i;
        char ptr[11] = "hello world";
        
        printf ("\nPrinting elements of 1-D array: \n\n");
        for (i = 0; i < n; i++)
        {
            printf ("%c ", ptr[i]);
        }
        printf ("\n\nNow what is the memory location for each index and the array itself: \n\n");
        printf("      Memory Address (HEX)  ||  Element        Value\n");
        printf("----------------------------------------------------\n");
        
        //%p means type pointer
        for (i = 0; i < n; i++)
        {
            printf ("\t%p      ||   ptr[%d]    =    %c\n", &ptr[i], i, ptr[i]);
        }
        printf("----------------------------------------------------\n");
        printf("\t%p      ||   ptr[]     =  %c (this is the array's address too!) \n", &ptr,*ptr);
        
    
        return 0;
    }
    ```

9. Run this code and see the expected output below:

    <details>
    <summary><b>Click for Expected Output</b></summary>
    <p></p>

    ```
    Printing elements of 1-D array: 

    h e l l o   w o r l d 

    Now what is the memory location for each index and the array itself: 

        Memory Address (HEX)  ||  Element        Value
    ----------------------------------------------------
        0x7ffc2407ce9d      ||   ptr[0]    =    h
        0x7ffc2407ce9e      ||   ptr[1]    =    e
        0x7ffc2407ce9f      ||   ptr[2]    =    l
        0x7ffc2407cea0      ||   ptr[3]    =    l
        0x7ffc2407cea1      ||   ptr[4]    =    o
        0x7ffc2407cea2      ||   ptr[5]    =     
        0x7ffc2407cea3      ||   ptr[6]    =    w
        0x7ffc2407cea4      ||   ptr[7]    =    o
        0x7ffc2407cea5      ||   ptr[8]    =    r
        0x7ffc2407cea6      ||   ptr[9]    =    l
        0x7ffc2407cea7      ||   ptr[10]   =    d
    ----------------------------------------------------
    0x7ffc2407ce9d      ||   ptr[]     =  h (this is the array's address too!) 
    ```

    </details>


    - So you should be able to see that arrays are indeed **Contiguous**
    
    - The starting memory address of the array is the same the zeroth element (`h`). 

--------------------------------------

## Section 7: Dynamically Allocation of Memory

As you know, an array is a collection of a fixed number of values. Once the size of an array is declared, you cannot change it.

Sometimes the size of the array you declared may be insufficient. To solve this issue, you can allocate memory manually during run-time. This is known as dynamic memory allocation in C programming.

To allocate memory dynamically, library functions are `malloc()`, `calloc()`, `realloc()` and `free()` are used. These functions are defined in the `<stdlib.h>` header file.

### Subsection 7.1: `malloc()`

The name `malloc` stands for **m**emory **alloc**ation.

The `malloc()` function reserves a block of memory of the specified number of bytes. And, it returns a pointer of `void` which can be casted into pointers of any form.

```c
ptr = (castType*) malloc(size);
```

Example:

```c
ptr = (float*) malloc(100 * sizeof(float));
```

The above statement allocates 400 bytes of memory. It's because the size of `float` is 4 bytes. And, the pointer `ptr` holds the address of the first byte in the allocated memory.

The expression results in a `NULL` pointer if the memory cannot be allocated.

### Subsection 7.2: `calloc()`

The name `calloc` stands for contiguous allocation.

The `malloc()` function allocates memory and leaves the memory uninitialized, whereas the `calloc()` function allocates memory and initialises all bits to zero.

```c
ptr = (castType*)calloc(n, size);
```

Example:

```c
ptr = (float*) calloc(25, sizeof(float));
```

The above statement allocates contiguous space in memory for 25 elements of type `float`.

### Subsection 7.3: `free()`

Dynamically allocated memory created with either `calloc()` or `malloc()` doesn't get freed on their own. You must explicitly use `free()` to release the space.

```c
free(ptr);
```

This statement frees the space allocated in the memory pointed by `ptr`.

#### Example 1:

10. Modify `main()` again so that and reproduce the following code  so that the program dynamically allocates the memory for `n` number of `int`s using `malloc()` and `free()`:

    ```c
    // Program to calculate the sum of n numbers entered by the user

    #include <stdio.h>
    #include <stdlib.h>

    int main() {
    int n, i, *ptr, sum = 0;

    printf("Enter number of elements: ");
    scanf("%d", &n);

    ptr = (int*) malloc(n * sizeof(int));
    
    // if memory cannot be allocated
    if(ptr == NULL) {
        printf("Error! memory not allocated.");
        exit(0);
    }

    printf("Enter elements: ");
    for(i = 0; i < n; ++i) {
        scanf("%d", ptr + i);
        sum += *(ptr + i);
    }

    printf("Sum = %d", sum);
    
    // deallocating the memory
    free(ptr);

    return 0;
    }

    ```


11. Run the program and try to enter a number equal to or than greater that zero:

    <details>
    <summary>Output...</summary>

        ```
        Enter number of elements: 3
        Enter elements: 100
        20
        36
        Sum = 156
        ```
    </details>

### Example 2:

12. Modify `main()` again so that and reproduce the following code that dynamically allocates the memory for `n` number of `int` using `calloc()` and `free()`:

    ```c
    // Program to calculate the sum of n numbers entered by the user

    #include <stdio.h>
    #include <stdlib.h>

    int main() {
    int n, i, *ptr, sum = 0;
    printf("Enter number of elements: ");
    scanf("%d", &n);

    ptr = (int*) calloc(n, sizeof(int));
    if(ptr == NULL) {
        printf("Error! memory not allocated.");
        exit(0);
    }

    printf("Enter elements: ");
    for(i = 0; i < n; ++i) {
        scanf("%d", ptr + i);
        sum += *(ptr + i);
    }

    printf("Sum = %d", sum);
    free(ptr);
    return 0;
    }

    ```

13. Now, run the code and you should see the following output, remember to enter a number equal to or greater than zero:

    ```
    Enter number of elements: 3
    Enter elements: 100
    20
    36
    Sum = 156
    ```

### Subsection 7.4: `realloc()`

If the dynamically allocated memory is insufficient or more than required, you can change the size of previously allocated memory using the `realloc()` function.

```c
ptr = realloc(ptr, x);
```

Here, `ptr` is reallocated with a new size `x`.

### Example 3:

14. Modify `main()` again so that and reproduce the following code that dynamically allocates the memory for `n` number of `int` using `malloc()`, `realloc()` and `free()`:

    ```c
    #include <stdio.h>
    #include <stdlib.h>

    int main() {
    int *ptr, i , n1, n2;
    printf("Enter size: ");
    scanf("%d", &n1);

    ptr = (int*) malloc(n1 * sizeof(int));

    printf("Addresses of previously allocated memory:\n");
    for(i = 0; i < n1; ++i)
        printf("%pc\n",ptr + i);

    printf("\nEnter the new size: ");
    scanf("%d", &n2);

    // rellocating the memory
    ptr = realloc(ptr, n2 * sizeof(int));

    printf("Addresses of newly allocated memory:\n");
    for(i = 0; i < n2; ++i)
        printf("%pc\n", ptr + i);
    
    free(ptr);

    return 0;
    }
    ```

15. Run the program and remeber the enter a number equal to or greater than zero:

    ```
    Enter size: 2
    Addresses of previously allocated memory:
    26855472
    26855476

    Enter the new size: 4
    Addresses of newly allocated memory:
    26855472
    26855476
    26855480
    26855484
    ```


## Section 8: Memory Allocations (System Calls)

If you are a computer programmer, (which all of you will be) you should know more about memory allocation. When looking at the allocation process, it is necessary to go into a little detail on Linux and the `glibc` library.

When applications need memory, they have to request it from the operating system. This request from the kernel will naturally require a system call. You cannot allocate memory yourself in user mode.

The `malloc()` family of functions is responsible for memory allocation in the `C` language(which we have been doing for a few exercises). The question to ask here is whether `malloc()`, as a glibc function, makes a direct system call.

There is no system call called `malloc()` in the Linux kernel. However, there are two system calls for applications memory demands, which are `brk` and `mmap`.

Since you will be requesting memory in your application via glibc functions, you may be wondering which of these system calls glibc is using at this point. The answer is both.

Here is the graphic for memory allocation that we looked at the in the lecture, to remind you of key concepts.

![](./figures/process_memory_application_graphic)


### Subsection 8.1: The First System Call: `brk()`

- Each process has a contiguous data field. With the `brk()`system call, the program break value, which determines the limit of the data field, is increased and the allocation process is performed.

- Although memory allocation with this method is very fast, it is not always possible to return unused space to the system.

- For example, consider that you allocate five fields, each 16KB in size, with the brk system call via the `malloc()` function. When you are done with number two of these fields, it is not possible to return the relevant resource (deallocation) so that the system can use it. Because if you reduce the address value to show the place where your field number two starts, with a call to `brk()`, you will have done deallocation for fields numbers three, four, and five.

- To prevent memory loss in this scenario, the `malloc()` implementation in glibc monitors the places allocated in the process data field and then specifies to return it to the system with the `free()` function, so that the system can use the free space for further memory allocations.

- In other words, after five 16KB areas are allocated, if the second area is returned with the `free()` function and another 16KB area is requested again after a while, instead of enlarging the data area through the `brk()` system call, the previous address is returned.

- However, if the newly requested area is larger than 16KB, then the data area will be enlarged by allocating a new area with the `brk()` system call since area two cannot be used. Although area number two is not in use, the application can't use it because of the size difference. Because of scenarios like this, there is a situation called internal fragmentation, and in fact, you can rarely use all parts of the memory to the fullest.

16. For better understanding, modify `main()` and try running the following sample application:

    ```c
    #include <stdio.h>
    #include <stdlib.h>
    #include <unistd.h> /*for system calls, sbrk*/

    int main(int argc, char* argv[]) /* an array of inputs*/
    {
        char *ptr[7];
        int n;
        // pid is the process ID, every process has an ID. 
        // argv[0] is always the name of the file being run...
        printf("\nPid of %s: %d", argv[0], getpid());
        printf("Initial program break   : %p", sbrk(0));
        for(n=0; n<5; n++) ptr[n] = malloc(16 * 1024);
        printf("After 5 x 16kB malloc   : %p", sbrk(0));
        free(ptr[1]);
        printf("After free of second 16kB       : %p", sbrk(0));
        ptr[5] = malloc(16 * 1024);
        printf("After allocating 6th of 16kB    : %p", sbrk(0));
        free(ptr[5]);
        printf("After freeing last block        : %p", sbrk(0));
        ptr[6] = malloc(18 * 1024);
        printf("After allocating a new 18kB     : %p", sbrk(0));
        getchar();
        return 0;
    }
    ```

17. When you run the application you will get a result similar to the following output:

```
Pid of ./systemCallMemoryAllocation.exe: 31990
0Initial program break   : 0x55ebcadf4000
After 5 x 16kB malloc   : 0x55ebcadf4000
After free of second 16kB       : 0x55ebcadf4000
After allocating 6th of 16kB    : 0x55ebcadf4000
After freeing last block        : 0x55ebcadf4000
After allocating a new 18kB     : 0x55ebcadf4000
```

## Section 9: Extra work

Combine what you have learnt in this lab advance your understanding of what you have achieved. 