## **Java Basics**

1. **Data Types**

   Java has two categories of data types: primitive and reference.

   **Primitive data types**:

   - byte: 8-bit integer (-128 to 127)
   - short: 16-bit integer (-32,768 to 32,767)
   - int: 32-bit integer (-2,147,483,648 to 2,147,483,647)
   - long: 64-bit integer (-9,223,372,036,854,775,808 to 9,223,372,036,854,775,807)
   - float: 32-bit floating-point number
   - double: 64-bit floating-point number
   - char: 16-bit Unicode character
   - boolean: true or false

   ```java
   int age = 25;
   double salary = 50000.50;
   char initial = 'A';
   boolean isStudent = false;
   ```

   **Reference data types**:

   - Classes
   - Interfaces
   - Arrays

   ```java
   String name = "John Doe";
   Integer[] numbers = {1, 2, 3};
   ```

2. **Variables**

   A variable is a named memory location that stores a value. In Java, variables must be declared with a data type before they can be used.

   ```java
   int count; // Declaration
   count = 10; // Initialization
   int sum = 20; // Declaration and Initialization
   ```

3. **Operators**

   Java provides a variety of operators for performing operations on variables and values.

   - Arithmetic: `+`, `-`, `*`, `/`, `%`
   - Comparison: `==`, `!=`, `<`, `>`, `<=`, `>=`
   - Logical: `&&`, `||`, `!`
   - Bitwise: `&`, `|`, `^`, `~`, `<<`, `>>`, `>>>`
   - Assignment: `=`, `+=`, `-=`, `*=`, `/=`, `%=`, `&=`, `|=`, `^=`, `<<=`, `>>=`, `>>>=`

   ```java
   int result = 10 + 20; // Arithmetic operator
   boolean isEqual = 5 == 5; // Comparison operator
   boolean isTrue = (5 > 3) && (2 < 4); // Logical operator
   int bitwiseResult = 5 & 3; // Bitwise operator
   ```

4. **Control Flow**

   Control flow statements enable you to execute different code branches based on conditions, and to repeat code execution with loops.

   - **If-Else Statement**:

     ```java
     int number = 10;

     if (number > 0) {
         System.out.println("Positive number");
     } else if (number < 0) {
         System.out.println("Negative number");
     } else {
         System.out.println("Zero");
     }
     ```

   - **Switch-Case Statement**:

     ```java
     int day = 3;

     switch (day) {
         case 1:
             System.out.println("Monday");
             break;
         case 2:
             System.out.println("Tuesday");
             break;
         case 3:
             System.out.println("Wednesday");
             break;
         // More cases...
         default:
             System.out.println("Invalid day");
     }
     ```

   - **Loops**:

     ```java
     // For loop
     for (int i = 0; i < 5; i++) {
         System.out.println("
     ```

Iteration: " + i);
}

     // While loop
     int i = 0;
     while (i < 5) {
         System.out.println("Iteration: " + i);
         i++;
     }

     // Do-while loop
     int j = 0;
     do {
         System.out.println("Iteration: " + j);
         j++;
     } while (j < 5);
     ```

5. **Arrays**

   An array is a container object that holds a fixed number of values of a single type.

   ```java
   // Declare and initialize an array
   int[] numbers = {1, 2, 3, 4, 5};

   // Access elements of an array
   int firstNumber = numbers[0]; // firstNumber = 1

   // Modify an element of the array
   numbers[0] = 10; // numbers = {10, 2, 3, 4, 5}

   // Iterate over an array
   for (int number : numbers) {
       System.out.println(number);
   }
   ```

Remember to experiment with these concepts and create your own examples to reinforce your understanding.
