0x19. C - Stacks, Queues - LIFO, FIFO
=====================================

CGroup projectAlgorithmData structure

*   Weight: 2
*   Project to be done in teams of 2 people (your team: Petrus TLHOMEDI)
*   Project over - took place from Dec 12, 2023 6:00 AM to Dec 15, 2023 6:00 AM
*   An auto review will be launched at the deadline

#### In a nutshell…

*   **Contribution:** 100.0%
    
*   **Auto QA review:** 0.0/43 mandatory & 0.0/87 optional
*   **Altogether:**  **0.0%**
    *   Mandatory: 0.0%
    *   Optional: 0.0%
    *   Contribution: 100.0%
    *   Calculation:  100.0% \* (0.0% + (0.0% \* 0.0%) )  == **0.0%**

![](https://pbs.twimg.com/media/CFYYWy6UEAE9Ow-.png)  
  

Resources
---------

**Read or watch**:

*   [Google](/rltoken/tn1X658KGumYYq_szFJI5w "Google")
*   [How do I use extern to share variables between source files in C?](/rltoken/0KVWTdE8xXy__jUfBfakCw "How do I use extern to share variables between source files in C?")
*   [Stacks and Queues in C](/rltoken/udmomL4F4mF630D2Z-ltqg "Stacks and Queues in C")
*   [Stack operations](/rltoken/fj_-SJXW-pWxgAnstsARoQ "Stack operations")
*   [Queue operations](/rltoken/6Y_GVoIH_rV45xd7w0a9FA "Queue operations")

Learning Objectives
-------------------

At the end of this project, you are expected to be able to [explain to anyone](/rltoken/_kxhiyVFey_mAGnzuHKL1w "explain to anyone"), **without the help of Google**:

### General

*   What do LIFO and FIFO mean
*   What is a stack, and when to use it
*   What is a queue, and when to use it
*   What are the common implementations of stacks and queues
*   What are the most common use cases of stacks and queues
*   What is the proper way to use global variables

### Copyright - Plagiarism

*   You are tasked to come up with solutions for the tasks below yourself to meet with the above learning objectives.
*   You will not be able to meet the objectives of this or any following project by copying and pasting someone else’s work.
*   You are not allowed to publish any content of this project.
*   Any form of plagiarism is strictly forbidden and will result in removal from the program.

Requirements
------------

### General

*   Allowed editors: `vi`, `vim`, `emacs`
*   All your files will be compiled on Ubuntu 20.04 LTS using gcc, using the options -Wall -Werror -Wextra -pedantic -std=c89
*   All your files should end with a new line
*   A `README.md` file, at the root of the folder of the project is mandatory
*   Your code should use the `Betty` style. It will be checked using [betty-style.pl](https://github.com/alx-tools/Betty/blob/master/betty-style.pl "betty-style.pl") and [betty-doc.pl](https://github.com/alx-tools/Betty/blob/master/betty-doc.pl "betty-doc.pl")
*   You allowed to use a maximum of one global variable
*   No more than 5 functions per file
*   You are allowed to use the C standard library
*   The prototypes of all your functions should be included in your header file called `monty.h`
*   Don’t forget to push your header file
*   All your header files should be include guarded
*   You are expected to do the tasks in the order shown in the project

### GitHub

**There should be one project repository per group. If you clone/fork/whatever a project repository with the same name before the second deadline, you risk a 0% score.**

More Info
---------

### Data structures

Please use the following data structures for this project. Don’t forget to include them in your header file.

    /**
     * struct stack_s - doubly linked list representation of a stack (or queue)
     * @n: integer
     * @prev: points to the previous element of the stack (or queue)
     * @next: points to the next element of the stack (or queue)
     *
     * Description: doubly linked list node structure
     * for stack, queues, LIFO, FIFO
     */
    typedef struct stack_s
    {
            int n;
            struct stack_s *prev;
            struct stack_s *next;
    } stack_t;
    

    /**
     * struct instruction_s - opcode and its function
     * @opcode: the opcode
     * @f: function to handle the opcode
     *
     * Description: opcode and its function
     * for stack, queues, LIFO, FIFO
     */
    typedef struct instruction_s
    {
            char *opcode;
            void (*f)(stack_t **stack, unsigned int line_number);
    } instruction_t;
    

### Compilation & Output

*   Your code will be compiled this way:

    $ gcc -Wall -Werror -Wextra -pedantic -std=c89 *.c -o monty
    

*   Any output must be printed on `stdout`
*   Any error message must be printed on `stderr`
    *   [Here is a link to a GitHub repository](/rltoken/NUGvCZqs609VjEHeutkICw "Here is a link to a GitHub repository") that could help you making sure your errors are printed on `stderr`

### Tests

We strongly encourage you to work all together on a set of tests

### The Monty language

Monty 0.98 is a scripting language that is first compiled into Monty byte codes (Just like Python). It relies on a unique stack, with specific instructions to manipulate it. The goal of this project is to create an interpreter for Monty ByteCodes files.

**Monty byte code files**

Files containing Monty byte codes usually have the `.m` extension. Most of the industry uses this standard but it is not required by the specification of the language. There is not more than one instruction per line. There can be any number of spaces before or after the opcode and its argument:

    julien@ubuntu:~/monty$ cat -e bytecodes/000.m
    push 0$
    push 1$
    push 2$
      push 3$
                       pall    $
    push 4$
        push 5    $
          push    6        $
    pall$
    julien@ubuntu:~/monty$
    

Monty byte code files can contain blank lines (empty or made of spaces only, and any additional text after the opcode or its required argument is not taken into account:

    julien@ubuntu:~/monty$ cat -e bytecodes/001.m
    push 0 Push 0 onto the stack$
    push 1 Push 1 onto the stack$
    $
    push 2$
      push 3$
                       pall    $
    $
    $
                               $
    push 4$
    $
        push 5    $
          push    6        $
    $
    pall This is the end of our program. Monty is awesome!$
    julien@ubuntu:~/monty$
    

**The monty program**

*   Usage: `monty file`
    *   where `file` is the path to the file containing Monty byte code
*   If the user does not give any file or more than one argument to your program, print the error message `USAGE: monty file`, followed by a new line, and exit with the status `EXIT_FAILURE`
*   If, for any reason, it’s not possible to open the file, print the error message `Error: Can't open file <file>`, followed by a new line, and exit with the status `EXIT_FAILURE`
    *   where `<file>` is the name of the file
*   If the file contains an invalid instruction, print the error message `L<line_number>: unknown instruction <opcode>`, followed by a new line, and exit with the status `EXIT_FAILURE`
    *   where is the line number where the instruction appears.
    *   Line numbers always start at 1
*   The monty program runs the bytecodes line by line and stop if either:
    *   it executed properly every line of the file
    *   it finds an error in the file
    *   an error occured
*   If you can’t malloc anymore, print the error message `Error: malloc failed`, followed by a new line, and exit with status `EXIT_FAILURE`.
*   You have to use `malloc` and `free` and are not allowed to use any other function from `man malloc` (realloc, calloc, …)

### Quiz questions

**Great!** You've completed the quiz successfully! Keep going! (Show quiz)

#### Question #0

Which of these stacks are keeping the order of insertion? (select all possible answers)

*   FILO
    
*   LILO
    
*   LIFO
    
*   FIFO
    

#### Question #1

What’s the command used to add a new element to a stack?

*   pop
    
*   push
    

#### Question #2

Which of these stacks are reversing the order of insertion? (select all possible answers)

*   FILO
    
*   LILO
    
*   LIFO
    
*   FIFO
    

#### Question #3

What’s the command used to remove a new element from a stack?

*   pop
    
*   push
    

Tasks
-----

### 0\. push, pall

mandatory

Score: 0.0% (Checks completed: 0.0%)

Implement the `push` and `pall` opcodes.

**The push opcode**

The opcode `push` pushes an element to the stack.

*   Usage: `push <int>`
    *   where `<int>` is an integer
*   if `<int>` is not an integer or if there is no argument given to `push`, print the error message `L<line_number>: usage: push integer`, followed by a new line, and exit with the status `EXIT_FAILURE`
    *   where is the line number in the file
*   You won’t have to deal with overflows. Use the `atoi` function

**The pall opcode**

The opcode `pall` prints all the values on the stack, starting from the top of the stack.

*   Usage `pall`
*   Format: see example
*   If the stack is empty, don’t print anything

    julien@ubuntu:~/monty$ cat -e bytecodes/00.m
    push 1$
    push 2$
    push 3$
    pall$
    julien@ubuntu:~/monty$ ./monty bytecodes/00.m
    3
    2
    1
    julien@ubuntu:~/monty$
    

**Repo:**

*   GitHub repository: `monty`

Done?! Check your code

×

#### Correction of "0. push, pall"

Start a new test Close

Requirement success

Requirement fail

Code success

Code fail

Efficiency success

Efficiency fail

Text answer success

Text answer fail

Skipped - Previous check failed

Ask for a new correction : in progress... : an error occurred Get a sandbox QA Review

×

#### 0\. push, pall

##### Commit used:

*   **User:** \---
*   **URL:** Click here
*   **ID:** `---`
*   **Author:** \---
*   **Subject:** _\---_
*   **Date:** \---

### 1\. pint

mandatory

Score: 0.0% (Checks completed: 0.0%)

Implement the `pint` opcode.

**The pint opcode**

The opcode `pint` prints the value at the top of the stack, followed by a new line.

*   Usage: `pint`
*   If the stack is empty, print the error message `L<line_number>: can't pint, stack empty`, followed by a new line, and exit with the status `EXIT_FAILURE`

    julien@ubuntu:~/monty$ cat bytecodes/06.m 
    push 1
    pint
    push 2
    pint
    push 3
    pint
    julien@ubuntu:~/monty$ ./monty bytecodes/06.m 
    1
    2
    3
    julien@ubuntu:~/monty$ 
    

**Repo:**

*   GitHub repository: `monty`

Done?! Check your code

×

#### Correction of "1. pint"

Start a new test Close

Requirement success

Requirement fail

Code success

Code fail

Efficiency success

Efficiency fail

Text answer success

Text answer fail

Skipped - Previous check failed

Ask for a new correction : in progress... : an error occurred Get a sandbox QA Review

×

#### 1\. pint

##### Commit used:

*   **User:** \---
*   **URL:** Click here
*   **ID:** `---`
*   **Author:** \---
*   **Subject:** _\---_
*   **Date:** \---

### 2\. pop

mandatory

Score: 0.0% (Checks completed: 0.0%)

Implement the `pop` opcode.

**The pop opcode**

The opcode `pop` removes the top element of the stack.

*   Usage: `pop`
*   If the stack is empty, print the error message `L<line_number>: can't pop an empty stack`, followed by a new line, and exit with the status `EXIT_FAILURE`

    julien@ubuntu:~/monty$ cat bytecodes/07.m 
    push 1
    push 2
    push 3
    pall
    pop
    pall
    pop
    pall
    pop
    pall
    julien@ubuntu:~/monty$ ./monty bytecodes/07.m 
    3
    2
    1
    2
    1
    1
    julien@ubuntu:~/monty$ 
    

**Repo:**

*   GitHub repository: `monty`

Done?! Check your code

×

#### Correction of "2. pop"

Start a new test Close

Requirement success

Requirement fail

Code success

Code fail

Efficiency success

Efficiency fail

Text answer success

Text answer fail

Skipped - Previous check failed

Ask for a new correction : in progress... : an error occurred Get a sandbox QA Review

×

#### 2\. pop

##### Commit used:

*   **User:** \---
*   **URL:** Click here
*   **ID:** `---`
*   **Author:** \---
*   **Subject:** _\---_
*   **Date:** \---

### 3\. swap

mandatory

Score: 0.0% (Checks completed: 0.0%)

Implement the `swap` opcode.

**The swap opcode**

The opcode `swap` swaps the top two elements of the stack.

*   Usage: `swap`
*   If the stack contains less than two elements, print the error message `L<line_number>: can't swap, stack too short`, followed by a new line, and exit with the status `EXIT_FAILURE`

    julien@ubuntu:~/monty$ cat bytecodes/09.m 
    push 1
    push 2
    push 3
    pall
    swap
    pall
    julien@ubuntu:~/monty$ ./monty bytecodes/09.m 
    3
    2
    1
    2
    3
    1
    julien@ubuntu:~/monty$ 
    

**Repo:**

*   GitHub repository: `monty`

Done?! Check your code

×

#### Correction of "3. swap"

Start a new test Close

Requirement success

Requirement fail

Code success

Code fail

Efficiency success

Efficiency fail

Text answer success

Text answer fail

Skipped - Previous check failed

Ask for a new correction : in progress... : an error occurred Get a sandbox QA Review

×

#### 3\. swap

##### Commit used:

*   **User:** \---
*   **URL:** Click here
*   **ID:** `---`
*   **Author:** \---
*   **Subject:** _\---_
*   **Date:** \---

### 4\. add

mandatory

Score: 0.0% (Checks completed: 0.0%)

Implement the `add` opcode.

**The add opcode**

The opcode `add` adds the top two elements of the stack.

*   Usage: `add`
*   If the stack contains less than two elements, print the error message `L<line_number>: can't add, stack too short`, followed by a new line, and exit with the status `EXIT_FAILURE`
*   The result is stored in the second top element of the stack, and the top element is removed, so that at the end:
    *   The top element of the stack contains the result
    *   The stack is one element shorter

    julien@ubuntu:~/monty$ cat bytecodes/12.m 
    push 1
    push 2
    push 3
    pall
    add
    pall
    
    julien@ubuntu:~/monty$ ./monty bytecodes/12.m 
    3
    2
    1
    5
    1
    julien@ubuntu:~/monty$
    

**Repo:**

*   GitHub repository: `monty`

Done?! Check your code

×

#### Correction of "4. add"

Start a new test Close

Requirement success

Requirement fail

Code success

Code fail

Efficiency success

Efficiency fail

Text answer success

Text answer fail

Skipped - Previous check failed

Ask for a new correction : in progress... : an error occurred Get a sandbox QA Review

×

#### 4\. add

##### Commit used:

*   **User:** \---
*   **URL:** Click here
*   **ID:** `---`
*   **Author:** \---
*   **Subject:** _\---_
*   **Date:** \---

### 5\. nop

mandatory

Score: 0.0% (Checks completed: 0.0%)

Implement the `nop` opcode.

**The nop opcode**

The opcode `nop` doesn’t do anything.

*   Usage: `nop`

**Repo:**

*   GitHub repository: `monty`

Done?! Check your code

×

#### Correction of "5. nop"

Start a new test Close

Requirement success

Requirement fail

Code success

Code fail

Efficiency success

Efficiency fail

Text answer success

Text answer fail

Skipped - Previous check failed

Ask for a new correction : in progress... : an error occurred Get a sandbox QA Review

×

#### 5\. nop

##### Commit used:

*   **User:** \---
*   **URL:** Click here
*   **ID:** `---`
*   **Author:** \---
*   **Subject:** _\---_
*   **Date:** \---

### 6\. sub

#advanced

Score: 0.0% (Checks completed: 0.0%)

Implement the `sub` opcode.

**The sub opcode**

The opcode `sub` subtracts the top element of the stack from the second top element of the stack.

*   Usage: `sub`
*   If the stack contains less than two elements, print the error message `L<line_number>: can't sub, stack too short`, followed by a new line, and exit with the status `EXIT_FAILURE`
*   The result is stored in the second top element of the stack, and the top element is removed, so that at the end:
    *   The top element of the stack contains the result
    *   The stack is one element shorter

    julien@ubuntu:~/monty$ cat bytecodes/19.m 
    push 1
    push 2
    push 10
    push 3
    sub
    pall
    julien@ubuntu:~/monty$ ./monty bytecodes/19.m 
    7
    2
    1
    julien@ubuntu:~/monty$
    

**Repo:**

*   GitHub repository: `monty`

Done?! Check your code

×

#### Correction of "6. sub"

Start a new test Close

Requirement success

Requirement fail

Code success

Code fail

Efficiency success

Efficiency fail

Text answer success

Text answer fail

Skipped - Previous check failed

Ask for a new correction : in progress... : an error occurred Get a sandbox QA Review

×

#### 6\. sub

##### Commit used:

*   **User:** \---
*   **URL:** Click here
*   **ID:** `---`
*   **Author:** \---
*   **Subject:** _\---_
*   **Date:** \---

### 7\. div

#advanced

Score: 0.0% (Checks completed: 0.0%)

Implement the `div` opcode.

**The div opcode**

The opcode `div` divides the second top element of the stack by the top element of the stack.

*   Usage: `div`
*   If the stack contains less than two elements, print the error message `L<line_number>: can't div, stack too short`, followed by a new line, and exit with the status `EXIT_FAILURE`
*   The result is stored in the second top element of the stack, and the top element is removed, so that at the end:
    *   The top element of the stack contains the result
    *   The stack is one element shorter
*   If the top element of the stack is `0`, print the error message `L<line_number>: division by zero`, followed by a new line, and exit with the status `EXIT_FAILURE`

**Repo:**

*   GitHub repository: `monty`

Done?! Check your code

×

#### Correction of "7. div"

Start a new test Close

Requirement success

Requirement fail

Code success

Code fail

Efficiency success

Efficiency fail

Text answer success

Text answer fail

Skipped - Previous check failed

Ask for a new correction : in progress... : an error occurred Get a sandbox QA Review

×

#### 7\. div

##### Commit used:

*   **User:** \---
*   **URL:** Click here
*   **ID:** `---`
*   **Author:** \---
*   **Subject:** _\---_
*   **Date:** \---

### 8\. mul

#advanced

Score: 0.0% (Checks completed: 0.0%)

Implement the `mul` opcode.

**The mul opcode**

The opcode `mul` multiplies the second top element of the stack with the top element of the stack.

*   Usage: `mul`
*   If the stack contains less than two elements, print the error message `L<line_number>: can't mul, stack too short`, followed by a new line, and exit with the status `EXIT_FAILURE`
*   The result is stored in the second top element of the stack, and the top element is removed, so that at the end:
    *   The top element of the stack contains the result
    *   The stack is one element shorter

**Repo:**

*   GitHub repository: `monty`

Done?! Check your code

×

#### Correction of "8. mul"

Start a new test Close

Requirement success

Requirement fail

Code success

Code fail

Efficiency success

Efficiency fail

Text answer success

Text answer fail

Skipped - Previous check failed

Ask for a new correction : in progress... : an error occurred Get a sandbox QA Review

×

#### 8\. mul

##### Commit used:

*   **User:** \---
*   **URL:** Click here
*   **ID:** `---`
*   **Author:** \---
*   **Subject:** _\---_
*   **Date:** \---

### 9\. mod

#advanced

Score: 0.0% (Checks completed: 0.0%)

Implement the `mod` opcode.

**The mod opcode**

The opcode `mod` computes the rest of the division of the second top element of the stack by the top element of the stack.

*   Usage: `mod`
*   If the stack contains less than two elements, print the error message `L<line_number>: can't mod, stack too short`, followed by a new line, and exit with the status `EXIT_FAILURE`
*   The result is stored in the second top element of the stack, and the top element is removed, so that at the end:
    *   The top element of the stack contains the result
    *   The stack is one element shorter
*   If the top element of the stack is `0`, print the error message `L<line_number>: division by zero`, followed by a new line, and exit with the status `EXIT_FAILURE`

**Repo:**

*   GitHub repository: `monty`

Done?! Check your code

×

#### Correction of "9. mod"

Start a new test Close

Requirement success

Requirement fail

Code success

Code fail

Efficiency success

Efficiency fail

Text answer success

Text answer fail

Skipped - Previous check failed

Ask for a new correction : in progress... : an error occurred Get a sandbox QA Review

×

#### 9\. mod

##### Commit used:

*   **User:** \---
*   **URL:** Click here
*   **ID:** `---`
*   **Author:** \---
*   **Subject:** _\---_
*   **Date:** \---

### 10\. comments

#advanced

Score: 0.0% (Checks completed: 0.0%)

Every good language comes with the capability of commenting. When the first non-space character of a line is `#`, treat this line as a comment (don’t do anything).

**Repo:**

*   GitHub repository: `monty`

Done?! Check your code

×

#### Correction of "10. comments"

Start a new test Close

Requirement success

Requirement fail

Code success

Code fail

Efficiency success

Efficiency fail

Text answer success

Text answer fail

Skipped - Previous check failed

Ask for a new correction : in progress... : an error occurred Get a sandbox QA Review

×

#### 10\. comments

##### Commit used:

*   **User:** \---
*   **URL:** Click here
*   **ID:** `---`
*   **Author:** \---
*   **Subject:** _\---_
*   **Date:** \---

### 11\. pchar

#advanced

Score: 0.0% (Checks completed: 0.0%)

Implement the `pchar` opcode.

**The pchar opcode**

The opcode `pchar` prints the char at the top of the stack, followed by a new line.

*   Usage: `pchar`
*   The integer stored at the top of the stack is treated as the ascii value of the character to be printed
*   If the value is not in the ascii table (man ascii) print the error message `L<line_number>: can't pchar, value out of range`, followed by a new line, and exit with the status `EXIT_FAILURE`
*   If the stack is empty, print the error message `L<line_number>: can't pchar, stack empty`, followed by a new line, and exit with the status `EXIT_FAILURE`

    julien@ubuntu:~/monty$ cat bytecodes/28.m 
    push 72
    pchar
    julien@ubuntu:~/monty$ ./monty bytecodes/28.m 
    H
    julien@ubuntu:~/monty$
    

**Repo:**

*   GitHub repository: `monty`

Done?! Check your code

×

#### Correction of "11. pchar"

Start a new test Close

Requirement success

Requirement fail

Code success

Code fail

Efficiency success

Efficiency fail

Text answer success

Text answer fail

Skipped - Previous check failed

Ask for a new correction : in progress... : an error occurred Get a sandbox QA Review

×

#### 11\. pchar

##### Commit used:

*   **User:** \---
*   **URL:** Click here
*   **ID:** `---`
*   **Author:** \---
*   **Subject:** _\---_
*   **Date:** \---

### 12\. pstr

#advanced

Score: 0.0% (Checks completed: 0.0%)

Implement the `pstr` opcode.

**The pstr opcode**

The opcode `pstr` prints the string starting at the top of the stack, followed by a new line.

*   Usage: `pstr`
*   The integer stored in each element of the stack is treated as the ascii value of the character to be printed
*   The string stops when either:
    *   the stack is over
    *   the value of the element is 0
    *   the value of the element is not in the ascii table
*   If the stack is empty, print only a new line

    julien@ubuntu:~/monty$ cat bytecodes/31.m 
    push 1
    push 2
    push 3
    push 4
    push 0
    push 110
    push 0
    push 108
    push 111
    push 111
    push 104
    push 99
    push 83
    pstr
    julien@ubuntu:~/monty$ ./monty bytecodes/31.m 
    School
    julien@ubuntu:~/monty$ 
    

**Repo:**

*   GitHub repository: `monty`

Done?! Check your code

×

#### Correction of "12. pstr"

Start a new test Close

Requirement success

Requirement fail

Code success

Code fail

Efficiency success

Efficiency fail

Text answer success

Text answer fail

Skipped - Previous check failed

Ask for a new correction : in progress... : an error occurred Get a sandbox QA Review

×

#### 12\. pstr

##### Commit used:

*   **User:** \---
*   **URL:** Click here
*   **ID:** `---`
*   **Author:** \---
*   **Subject:** _\---_
*   **Date:** \---

### 13\. rotl

#advanced

Score: 0.0% (Checks completed: 0.0%)

Implement the `rotl` opcode.

**The rotl opcode**

The opcode `rotl` rotates the stack to the top.

*   Usage: `rotl`
*   The top element of the stack becomes the last one, and the second top element of the stack becomes the first one
*   `rotl` never fails

    julien@ubuntu:~/monty$ cat bytecodes/35.m 
    push 1
    push 2
    push 3
    push 4
    push 5
    push 6
    push 7
    push 8
    push 9
    push 0
    pall
    rotl
    pall
    julien@ubuntu:~/monty$ ./monty bytecodes/35.m 
    0
    9
    8
    7
    6
    5
    4
    3
    2
    1
    9
    8
    7
    6
    5
    4
    3
    2
    1
    0
    julien@ubuntu:~/monty$ 
    

**Repo:**

*   GitHub repository: `monty`

Done?! Check your code

×

#### Correction of "13. rotl"

Start a new test Close

Requirement success

Requirement fail

Code success

Code fail

Efficiency success

Efficiency fail

Text answer success

Text answer fail

Skipped - Previous check failed

Ask for a new correction : in progress... : an error occurred Get a sandbox QA Review

×

#### 13\. rotl

##### Commit used:

*   **User:** \---
*   **URL:** Click here
*   **ID:** `---`
*   **Author:** \---
*   **Subject:** _\---_
*   **Date:** \---

### 14\. rotr

#advanced

Score: 0.0% (Checks completed: 0.0%)

Implement the `rotr` opcode.

**The rotr opcode**

The opcode `rotr` rotates the stack to the bottom.

*   Usage: `rotr`
*   The last element of the stack becomes the top element of the stack
*   `rotr` never fails

**Repo:**

*   GitHub repository: `monty`

Done?! Check your code

×

#### Correction of "14. rotr"

Start a new test Close

Requirement success

Requirement fail

Code success

Code fail

Efficiency success

Efficiency fail

Text answer success

Text answer fail

Skipped - Previous check failed

Ask for a new correction : in progress... : an error occurred Get a sandbox QA Review

×

#### 14\. rotr

##### Commit used:

*   **User:** \---
*   **URL:** Click here
*   **ID:** `---`
*   **Author:** \---
*   **Subject:** _\---_
*   **Date:** \---

### 15\. stack, queue

#advanced

Score: 0.0% (Checks completed: 0.0%)

Implement the `stack` and `queue` opcodes.

**The stack opcode**

The opcode `stack` sets the format of the data to a stack (LIFO). This is the default behavior of the program.

*   Usage: `stack`

**The queue opcode**

The opcode `queue` sets the format of the data to a queue (FIFO).

*   Usage: `queue`

When switching mode:

*   The top of the stack becomes the front of the queue
*   The front of the queue becomes the top of the stack

    julien@ubuntu:~/monty$ cat bytecodes/47.m
    queue
    push 1
    push 2
    push 3
    pall
    stack
    push 4
    push 5
    push 6
    pall
    add
    pall
    queue
    push 11111
    add
    pall
    julien@ubuntu:~/monty$ ./monty bytecodes/47.m
    1
    2
    3
    6
    5
    4
    1
    2
    3
    11
    4
    1
    2
    3
    15
    1
    2
    3
    11111
    julien@ubuntu:~/monty$ 
    

**Repo:**

*   GitHub repository: `monty`

Done?! Check your code

×

#### Correction of "15. stack, queue"

Start a new test Close

Requirement success

Requirement fail

Code success

Code fail

Efficiency success

Efficiency fail

Text answer success

Text answer fail

Skipped - Previous check failed

Ask for a new correction : in progress... : an error occurred Get a sandbox QA Review

×

#### 15\. stack, queue

##### Commit used:

*   **User:** \---
*   **URL:** Click here
*   **ID:** `---`
*   **Author:** \---
*   **Subject:** _\---_
*   **Date:** \---

### 16\. Brainf\*ck

#advanced

Score: 0.0% (Checks completed: 0.0%)

Write a Brainf\*ck script that prints `School`, followed by a new line.

*   All your Brainf\*ck files should be stored inside the `bf` sub directory
*   You can install the `bf` interpreter to test your code: `sudo apt-get install bf`
*   Read: [Brainf\*ck](/rltoken/x0I37o6PVmnT0M1RF0XXjg "Brainf*ck")

    julien@ubuntu:~/monty/bf$ bf 1000-school.bf 
    School
    julien@ubuntu:~/monty/bf$ 
    

**Repo:**

*   GitHub repository: `monty`
*   Directory: `bf`
*   File: `1000-school.bf`

Done?! Check your code

×

#### Correction of "16. Brainf\*ck"

Start a new test Close

Requirement success

Requirement fail

Code success

Code fail

Efficiency success

Efficiency fail

Text answer success

Text answer fail

Skipped - Previous check failed

Ask for a new correction : in progress... : an error occurred Get a sandbox QA Review

×

#### 16\. Brainf\*ck

##### Commit used:

*   **User:** \---
*   **URL:** Click here
*   **ID:** `---`
*   **Author:** \---
*   **Subject:** _\---_
*   **Date:** \---

### 17\. Add two digits

#advanced

Score: 0.0% (Checks completed: 0.0%)

Add two digits given by the user.

*   Read the two digits from stdin, add them, and print the result
*   The total of the two digits with be one digit-long (<10)

    julien@ubuntu:~/monty/bf$ bf ./1001-add.bf
    81
    9julien@ubuntu:~/monty/bf$
    

**Repo:**

*   GitHub repository: `monty`
*   Directory: `bf`
*   File: `1001-add.bf`

Done?! Check your code

×

#### Correction of "17. Add two digits"

Start a new test Close

Requirement success

Requirement fail

Code success

Code fail

Efficiency success

Efficiency fail

Text answer success

Text answer fail

Skipped - Previous check failed

Ask for a new correction : in progress... : an error occurred Get a sandbox QA Review

×

#### 17\. Add two digits

##### Commit used:

*   **User:** \---
*   **URL:** Click here
*   **ID:** `---`
*   **Author:** \---
*   **Subject:** _\---_
*   **Date:** \---

### 18\. Multiplication

#advanced

Score: 0.0% (Checks completed: 0.0%)

Multiply two digits given by the user.

*   Read the two digits from stdin, multiply them, and print the result
*   The result of the multiplication will be one digit-long (<10)

    julien@ubuntu:~/monty/bf$ bf 1002-mul.bf
    24
    8julien@ubuntu:~/monty/bf$
    

**Repo:**

*   GitHub repository: `monty`
*   Directory: `bf`
*   File: `1002-mul.bf`

Done?! Check your code

×

#### Correction of "18. Multiplication"

Start a new test Close

Requirement success

Requirement fail

Code success

Code fail

Efficiency success

Efficiency fail

Text answer success

Text answer fail

Skipped - Previous check failed

Ask for a new correction : in progress... : an error occurred Get a sandbox QA Review

×

#### 18\. Multiplication

##### Commit used:

*   **User:** \---
*   **URL:** Click here
*   **ID:** `---`
*   **Author:** \---
*   **Subject:** _\---_
*   **Date:** \---

### 19\. Multiplication level up

#advanced

Score: 0.0% (Checks completed: 0.0%)

Multiply two digits given by the user.  
  
![](http://mein-fun.com/data/media/5/brainfuck_bean.jpg)  
  

*   Read the two digits from stdin, multiply them, and print the result, followed by a new line

    julien@ubuntu:~/monty/bf$ bf 1003-mul.bf 
    77
    49
    julien@ubuntu:~/monty/bf$ 
    

**Repo:**

*   GitHub repository: `monty`
*   Directory: `bf`
*   File: `1003-mul.bf`

Done?! Check your code

×

#### Correction of "19. Multiplication level up"

Start a new test Close

Requirement success

Requirement fail

Code success

Code fail

Efficiency success

Efficiency fail

Text answer success

Text answer fail

Skipped - Previous check failed

Ask for a new correction : in progress... : an error occurred Get a sandbox QA Review

×

#### 19\. Multiplication level up

##### Commit used:

*   **User:** \---
*   **URL:** Click here
*   **ID:** `---`
*   **Author:** \---
*   **Subject:** _\---_
*   **Date:** \---

×

#### Recommended Sandbox

Running only

### 1 image(1/2 Sandboxes spawned)

### Ubuntu 20.04

Basic Ubuntu 20.04, with vim, emacs, curl, wget and all needed for Foundations

SSH

SFTP

[Webterm](/user_containers/653997/webterm)

RestartDestroy

#### Credentials

**Host**695d8fff081b.cea86b64.alx-cod.online

**Username**695d8fff081b

**Password**6d9ae01ce5775617e7cc

#### Web access

[HTTPS](https://695d8fff081b.cea86b64.alx-cod.online)[HTTP](http://695d8fff081b.cea86b64.alx-cod.online)[3000](http://695d8fff081b.cea86b64.alx-cod.online:3000)[4000](http://695d8fff081b.cea86b64.alx-cod.online:4000)[5000](http://695d8fff081b.cea86b64.alx-cod.online:5000)[5001](http://695d8fff081b.cea86b64.alx-cod.online:5001)[8000](http://695d8fff081b.cea86b64.alx-cod.online:8000)[8080](http://695d8fff081b.cea86b64.alx-cod.online:8080)

#### Port mapping

**SSH**55605

**HTTP**55604

**HTTPS**55603

**3000**55602

**MySQL**55601

**4000**55600

**5000**55599

**5001**55598

**8000**55597

**8080**55596
