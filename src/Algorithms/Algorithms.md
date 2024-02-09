## Lab 9: Algorithms 

- Quick sort Example, \\( O(n log n)\\)

- Bubble sort Example, \\( O(n^2)\\)

- Selection Sort Example, \\( O(n^2)\\)

- Insertion Sort Example, \\(O(n^2) \\)


> Note: 
>> - All timings are based on an 11th Gen Intel Core i5-11500 @ 2.70GHz 6 Cores.
>> - The C library function `clock_t clock(void)` returns the number of `clock ticks` elapsed since the program was launched. To get the number of seconds used by the CPU, you will need to divide by `CLOCKS_PER_SEC`, which will be implemented in `main()`.


In this lab we are going to explore various sorting algorithms sorting a small dataset that is meant to describe heights of various people: 

-  `int array1[] = {90, 65, 70, 55, 60, 80};`


## Quick Sort Algorithm \\(O(n\ log\ n)\\): 

1. Create a new C++ Console Application call it `Algorithms`. Remember to modify the `Algorithms.cpp` so that it is a c file `Algorithms.c`

2. Creat a header and C file called `Sort.h` and `Sort.c`. 

    - The algorithm works by first: 

      - **Divide and Conquer**: Quicksort is a fast, efficient sorting algorithm, that uses a divide-and-conquer strategy to sort an array.

      - **Picking a Pivot:** It starts by selecting a 'pivot' element from the array, usually the middle element

      - **Partitioning:** The array is then partitioned into two parts – elements less than the pivot are moved before it, and elements greater than the pivot are moved after it.

      - **Recursive Sorting:** This partitioning creates a "partial order". The algorithm then recursively applies the same process to the sub-arrays formed by the partition.

3. Reproduce the following code in `Sort.h`:

    ```c
    #pragma once
    #ifndef SORT_H
    #define SORT_H

    #include <stdio.h>
    #include <stdlib.h>
    #include <time.h> // For measuring the time complexity of the algorithms, utilised in the main()

    void quicksortMiddle(int arr[], int low, int high);

    void printArray(int arr[], int size);
    #endif // SORT_H
    ```
4. Reproduce the following code in `Sort.c`:

    ```c
    #include "Sort.h"

    void quicksortMiddle(int arr[], int low, int high) {
        if (low < high) {
            int pivot = arr[(low + high) / 2]; // Selecting the middle element as the pivot
            int i = low; // lower bounds of array
            int j = high; // upper bounds of array
            int temp; // for swapping elements around

            // while low is less than hight (number of elements)
            while (i <= j) {
                while (arr[i] < pivot) i++; // Moving elements smaller than pivot to the left
                while (arr[j] > pivot) j--; // Moving elements greater than pivot to the right

                if (i <= j) {
                    temp = arr[i];         // Swapping elements
                    arr[i] = arr[j];
                    arr[j] = temp;
                    i++; // move up the array 0 to n 
                    j--; // move down the array n to 0
                }
            }

            // Recursively sort the two partitions
            if (low < j) quicksortMiddle(arr, low, j);
            if (i < high) quicksortMiddle(arr, i, high);
        }
    }

    // Utility function to print array
    void printArray(int arr[], int size)
    {
        for (int i = 0; i < size; i++)
        {
            printf("%d ", arr[i]);
        }
        printf("\n");
    }
    ```

5. Now you have the first sorting algorithm is set up we need get the `Algorithms.c` file ready to invoke the sorting function and calcualte the how long it took. Modify the code, `Algorithms.c`, to include the following, pay close attention to the comments as they provide verbose guidance:

    ```c
    #include "Sort.h"

    int main()
    {

        int array1[] = {90, 65, 70, 55, 60, 80}; // partially sorted array of heights
        
        int n = sizeof(array1) / sizeof(array1[0]); // get the middle of the array

        printf("Original Array: \n");
        printArray(array1, n);

        clock_t start, end; // Set up variables to time the algorithm
        start = clock(); // start the timer
        
        // We are iterating over a large number , 10 million times, as this will take nano seconds, and without a lot more code time.h does not go below a micro seconds.  We are going turn millseconds and then convert to nano seconds.  
        for (int i = 0; i < 10000000; i++) {
            // Using the Middle Element as Pivot    
            quicksortMiddle(array1, 0, n - 1);
        }

        end = clock(); // end the timer
        
        // calculate the time taken -  CLOCKS_PER_SEC is time.h macro 
        double cpu_time_used = ((double)((double)end - (double)start)) / CLOCKS_PER_SEC; 

        printf("Sorted with Middle Element as Pivot:\n");
        printArray(array1, n);
        printf("Time taken: %lf", cpu_time_used); 

        return 0;
    }
    ```
6. If you have reproduce the above you should see the following output:

    ![](./figures/quicksort.png)
    
    - You should see that the original array is sorted and the the time taken.
     - Time taken currentlty shows as milliseconds, however this 10^6 times larger than actual time. Remember we repeat the algorithm \\(10\cdot10^6\\) times, so we need to divide by the same to get the actual time. 
Timing:  \\[33.5ns \equiv 33.5 \cdot 10^{-8} =  \frac{335 \cdot 10^{-3}}{10 \cdot 10^6}  \leftarrow \frac{0.335000}{10000000}\\]

7. The graphic below illustrates how the sorting was performed: 

    ![](./figures/quick_sort.gif)

---------------------------- 

## Bubble Sort Algorithm \\(O(n\ log\ n)\\): 

The Bubble sort works by repeatedly stepping through the list to be sorted, comparing each pair of adjacent items and swapping them if they are in the wrong order. This process is repeated until no more swaps are needed, indicating that the list is sorted.

- Here's how bubble sort works:

  - Start at the beginning of the array.
   
  - Compare the first two elements. If the first element is greater than the second element, swap them.

  - Move to the next pair of elements and repeat step 2.

  - Continue this process until the end of the array is reached.

  - If any swaps were made during the previous pass through the array, repeat steps 1-4. Otherwise, the array is sorted.

  - Bubble sort works by "bubbling" the largest elements to the end of the array in each pass, hence its name.

1. To implement the bubble sort algorithm, revist the Sort.h and add the prototype `void bubblesort(int )`


6. If you have reproduce the above you should see the following output:

    ![](./figures/bubblesort.png)
    
    - You should see that the original array is sorted and the the time taken.
    
    - Time taken currentlty shows as milliseconds, however this 10^6 times larger than actual time. Remember we repeat the algorithm \\(10\cdot10^6\\) times, so we need to divide by the same to get the actual time. 
  
    - Timing:  \\[33.2ns \equiv 33.2 \cdot 10^{-8} =  \frac{332 \cdot 10^{-3}}{10 \cdot 10^6}  \leftarrow \frac{0.332000}{10000000}\\]

7. The graphic below illustrates how the sorting was performed: 

    ![](./figures/bubble_sort.gif)

---------------------------------

## Selection Sort

Selection sort works by repeatedly finding the minimum element from the unsorted part of the array and moving it to the beginning.

- How it works:

  - Start with the entire array considered as unsorted.
  
  - Find the minimum element in the unsorted portion of the array.
  
  - Swap the minimum element with the first element of the unsorted portion.
  
  - Move the boundary of the unsorted portion one element to the right.
  
  - Repeat steps 2-4 until the entire array is sorted.
  
  - Selection sort is called "selection" because it repeatedly selects the smallest (or largest, depending on the sorting order) element and moves it to its correct position.

1. To implement the bubble sort algorithm, revist the Sort.h and add the prototype `void selectionsort(int )`

6. If you have reproduce the above you should see the following output:

    ![](./figures/selectionsort.png)
    
    - You should see that the original array is sorted and the the time taken.
    
    - Time taken currentlty shows as milliseconds, however this 10^6 times larger than actual time. Remember we repeat the algorithm \\(10\cdot10^6\\) times, so we need to divide by the same to get the actual time. 
  
    - Timing:  \\[46.4ns \equiv 46.4 \cdot 10^{-8} =  \frac{464 \cdot 10^{-3}}{10 \cdot 10^6}  \leftarrow \frac{0.464000}{10000000}\\]

7. The graphic below illustrates how the sorting was performed: 

    ![](./figures/selection_sort.gif)

------------------

## Insertion Sort

Insertion sort works by building a sorted array one element at a time by repeatedly taking the next element from the unsorted part of the array and inserting it into its correct position in the sorted part. 

- How it works:
  - Start with the second element of the array (assuming the first element is already sorted).
  
  - Compare the current element with the elements before it in the sorted portion of the array.
  
  - Shift elements in the sorted portion to the right to make room for the current element, if necessary.
  
  - Insert the current element into its correct position in the sorted portion.
  
  - Move to the next element in the unsorted portion and repeat steps 2-4.
  
  - Repeat this process until the entire array is sorted.
  
- Insertion sort is like sorting a hand of cards: you pick up one card at a time and insert it into its correct position among the cards you're already holding.

1. To implement the bubble sort algorithm, revist the Sort.h and add the prototype `void insertionsort(int )`

6. If you have reproduce the above you should see the following output:

    ![](./figures/insertionsort.png)
    
    - You should see that the original array is sorted and the the time taken.
    
    - Time taken currentlty shows as milliseconds, however this 10^6 times larger than actual time. Remember we repeat the algorithm \\(10\cdot10^6\\) times, so we need to divide by the same to get the actual time. 
  
    - Timing:  \\[15.1ns \equiv 15.1 \cdot 10^{-8} =  \frac{151 \cdot 10^{-3}}{10 \cdot 10^6}  \leftarrow \frac{0.151000}{10000000}\\]

7. The graphic below illustrates how the sorting was performed: 

    ![](./figures/insertion_sort.gif)



----------------

## Investigation and exploration

1. Try running each algorithm to see if you get different results, record them and work out the average time, either in code or outside. 

2. Run each algorithm again using the following two arrays, and again compare the times:

    - Sorted
       - `int array1[] = {55, 60, 65, 70, 80, 90};`
    
    - Revesed Sorted
       - `int array1[] = {90, 80, 70, 65, 60, 55};`

3. Increase the size of the array and see if the current performance changes accross the each algorithm and rank them. 

