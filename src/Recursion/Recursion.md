# Lab n: Recursion

Recursion is a programming concept where a function calls itself in its own definition. In other words, a recursive function is a function that solves a problem by solving smaller instances of the same problem. This process continues until a **base case** is reached, at which point the function **returns** a result without making a recursive call.

Recursion consists of **two** main components:

1. **Base Case**: 
   - This is the terminating condition that prevents the function from calling itself indefinitely. When the base case is met, the recursion stops, and the function returns a specific value.

2. **Recursive Case**: 
   - This is the part of the function where it calls itself with a smaller or simpler input. Each recursive call should bring the problem closer to the base case.



-----------------------------------
-----------------------------------

## Task 1.

1. First recursive task is to perform a factorial, to do this we need a new project. Open VSCode and create a new C++ console project, and call it Factorial.

>**Note:**
>>
>>    As a reminder the factorial of a non-negative integer \\( n \\), denoted by \\( n! \\), is the product of all positive integers less than or equal to \\( n \\). It is defined as:
>>
>>    \\[ n! = n \times (n-1) \times (n-2) \times \ldots \times 2 \times 1 \\]
>>
>>For example:
>>
>>    \\[ 5! = 5 \times 4 \times 3 \times 2 \times 1 = 120 \\]
>>
>>The factorial function is often used in combinatorics and probability, where it represents the number of ways to arrange \\(n \\) distinct objects into a sequence.


1. Change the extension of the `Factorial.cpp` to `Factorial.c`

2. Reproduce the following:
    ```c
    #include <stdio.h>

    int main(){

        return 0;
    }
    ```

3. Underneath the line `#include <stdio.h>` add the defintion of a new function called factorial that returns an `int` and takes one argument which is also an `int`.
   <details>
   <summary>Solution</summary>

    ```c
    int factorial(int n);
    ```

   </details>

<p></p>

4. After the closing `}` of `main()` write the factorial function that has just been defined, write the head and leave the body empty. 

    <details>
    <summary>Solution</summary>

    ```c
    int main(){
        ...
    }

    int factorial(int n){

    }
    ```

    </details>

5. Inside the factorial function write an if statement that checks if `n` is `0` or `1`, and if true, it returns `1`. Add a comment to the top of the if block that says `\\base case`. 


    <details>
    <summary>Possible Solution</summary>

    ```c
    int factorial(int n) {
        // Base case
        if (n == 0 || n == 1) {
            return 1;
        }
    }
    ```

    </details>

6. Now add the recusive case which will be the `else` block. Write the `return` keyword after the inside the `else{}` block. Continuing on the same line multiply `n` to the result of the factorial function invocation (the recursion). The `factorial()`'s argument should be `n - 1`

    <details>
    <summary>Possible Solution</summary>

    ```c
    int factorial(int n) {
        // Base case
        if (n == 0 || n == 1) {
            return 1;
        }else {
            // Recursive case
            return n * factorial(n - 1);
        }
    }
    ```

    </details>


7. Now revist `main()` and create a variable called `result` which is of the data type `int` which stores the result of the `factorial(5)` as part of it's declaration and initilaisation. On the next line print the variable `result` the prepened string `"Factorial: "`


    <details>
    <summary>Possible Solution</summary>

    ```c
    int main() {
        // Example usage
        int result = factorial(5);
        printf("Factorial: %d\n", result);  // Output: 120

        return 0;
    }
    ```
    </details>

<details>
<summary>Possible Solution</summary>

```c
#include <stdio.h>

// Function prototype
int factorial(int n);

int main() {
    // Example usage
    int result = factorial(5);
    printf("Factorial: %d\n", result);  // Output: 120

    return 0;
}

// Function definition
int factorial(int n) {
    // Base case
    if (n == 0 || n == 1) {
        return 1;
    } else {
        // Recursive case
        return n * factorial(n - 1);
    }
}
```

</details>

## Task 2.

Create a recursive function to generate the *n*th term of the Fibonacci series.

C
<div align=center>

0,1,1,2,3,5,8,13,21,34,…

</div>

Here’s how the sequence progresses:

Start with 0 and 1.

The next number is 0 + 1 = 1.
The next number is 1 + 1 = 2.
The next number is 1 + 2 = 3.
The next number is 2 + 3 = 5. And so on...

𝐹(𝑛) = 𝐹(𝑛 − 1) + 𝐹(𝑛 − 2)





------------------------------
------------------------------

The **base case** checks if `n` is `0` or `1`, and `if` `true`, it returns `1`. Otherwise, it makes a recursive call with the argument `n - 1`. The main function demonstrates the usage of the factorial function by calculating the factorial of 5 and printing the result.

```c
#include <stdio.h>

int fibonacci(int c);

int main(){

    int n;

    printf("Enter the value of n: ");
    scanf_s("%d", &n);

    // check if the input is non-negative
    if(n < 0){
        printf("Fibonacci sequence is not defined for negative numbers.");
    }else{
        int fibVaule = fibonacci(n - 1);
        printf("Fibonacci number at position %d is: %llu\n", n, fibValue);
    }

    return 0;
}

int fibonacci(int n){
    if (n <=1 ){
        return n;
    }
    return fibonacci(n -1) + fibonacci(n -2);
}
```

## Conclusion

Recursion is a powerful and elegant technique, but it should be used with caution. Improper use of recursion can lead to **stack overflow** errors, and in some cases, it might be less efficient than iterative solutions. However, for certain problems, recursion can provide a clearer and more concise solution.