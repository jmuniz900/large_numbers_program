# large_numbers_calculator_program


Objective
To solidify what we learned about pointers and addresses by implementing linked lists to perform mathematical operations.
Background
In the field of mathematics, there are many research areas that heavily rely on computer science applications. One such area involves discovering new large prime numbers. Currently, the largest known prime number is 2^(82,589,933) − 1 (which contains 24,862,048 digits). A number as large as this one could not be stored in a conventional C++ type. A different approach would need to be taken to handle special numbers; namely one that treats each digit separately. Let’s explore how we can use what we’ve learned thus far to cleverly store large numbers and perform basic computations.
Overview
NOTE: Addition is mandatory, subtraction is optional
Consider the idea of storing a large number in a linked list, one digit per node, where all the nodes together form the original large number. By choosing a linked list and treating each digit as an individual component of the whole, we are expanding the range of numbers we can handle in a program (where the max range is environment-dependent).
In this assignment you will read in various computations consisting of 2 numbers of an unknown length of digits, followed by an operator defining what math operation to perform (in order to simplify our program we will only implement addition and subtraction). Below is an example of the input file largeNumbers.txt containing 2 mathematical operations:
1234567
9876543
+
8888888
9999999
(minus)

The results for each calculation should be written to the output.txt as they’re computed. This means that output.txt should be opened only once and remain open until all results have been obtained and saved to the file. Below is an example of the output file output.txt:
11111110
-1111111

NOTE: The file only contains digits, newline characters, and the + and - operators. If you view either file in a standard text editor, the numbers may appear to wrap. Regardless of this, keep in mind that each number or operator is followed by a single newline character.
Implementation
Each large number will be stored in one linked list comprised of digit objects. In main, you will need 3 head pointers to store each number. Below is the class definition (NOTE: no changes must be made to the class - the members are already public and accessible from main):
class digit
{
    public:
    int data;
    digit *next = NULL;
};
There should only be one digit per object; the valid range is 0 to 9, inclusive. The only exception may occur in the result pointer after a subtraction where the first digit may be negative if the number is negative; the valid range is -9 to -1, inclusive.
When you add or subtract numbers, you normally start with the least significant digit (LSD), and work your way from right to left. We can employ that same mechanism here. When loading a number into a linked list, we can load it backwards so that number 12345 would produce the following linked list:
Doing so allows us to start with the LSD at the head pointer and align types that are alike (ones, tens, thousands place, etc.). This is purely a recommendation and design choice; you are able to store the number in either manner. However, keep in mind that when the result is output to the file, it must be in the natural, human-readable order.
If you have a negative number, only one digit will be negative (either the first or last):
If you store numbers in reverse order, then -12345 will produce (HINT: best to output with a recursive function):
head -> 5 -> 4 -> 3 -> 2 -> (-1) -> NULL
Otherwise, -12345 will produce (HINT: best to output with a while loop):
head -> (-1) -> 2 -> 3 -> 4 -> 5 -> NULL
The program calculator.cpp will contain the 6 functions in the table below. Any additional helper functions (such as recursive methods) are encouraged. The two text files should be opened in main and any required file handles can be passed to functions accordingly. Starter code has been provided. NOTE: compile with flag -std=c++11

Function & Description
digit * loadNumber(ifstream & file);
Is called twice for each computation (once for each large number in the file). Returns a pointer to the first element in the linked list. Uses the new operator to create each element in the list.

char getOperator(ifstream & file);
Returns the char version of the + or - operators to indicate the desired operation.

void writeNumber(digit * num, ofstream & file);
Writes the resulting number to the file. Should be passed the head pointer of that number.

void deleteNumber(digit * num);
Is called for each number created dynamically when no longer needed. Calls the delete operator on each node in the list to protect against a memory leak.
digit * addNumbers(digit * left, digit * right);
Adds the left and right operands. Returns a pointer to the first element of the result in a newly-created linked list. Creates each element in the list using the new operator. The right operand is the second number in the input file.

digit * subNumbers(digit * left, digit * right);
Subtracts the right operand from the left and returns a pointer to the first element of the result in a newly-created linked list. Creates each element in the list using the new operator. The right operand is the second number in the input file.

Additional Considerations
The functions addNumbers(...) and subNumbers(...) need to handle carrying properly.
Only the first digit will be negative if the result is negative. To do subtraction, you must determine which number is larger in the absolute sense, and subtract the smaller one. If the Right hand number is larger, the result will be negative. A function to test which number is larger has been provided.
In this example, you would need to determine that 3250 is larger than 183, so you subtract 183 from 3250, then go back and set your result to negative.



The input file will not contain negative numbers, however, the results of subtraction may be negative.
Your program will be tested on numbers that are hundreds of digits in length, therefore do not attempt to use a long C++ type as this will not work.
Submission
Upload your calculator.cpp file to Titanium and in the comments section paste your GitHub repository link.
