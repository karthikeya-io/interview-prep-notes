**Exception Handling in Java**

An exception is an event that disrupts the normal flow of the program's instructions. Exception handling is the process of responding to the occurrence of exceptions that may happen during the execution of our program. It provides a way to transfer control from one part of a program to another.

In Java, exceptions are handled using five keywords: `try`, `catch`, `finally`, `throw`, and `throws`.

1. **try-catch**

   The `try` block contains a block of code where an exception can occur. The `catch` block contains the exception handler that handles the exception if one occurs in the `try` block.

   ```java
   try {
       int[] myNumbers = {1, 2, 3};
       System.out.println(myNumbers[10]); // This will throw an exception
   } catch (ArrayIndexOutOfBoundsException e) {
       System.out.println("Array Index is Out Of Bounds");
   }
   ```

2. **Multiple catch blocks**

   You can have multiple `catch` blocks to catch different types of exceptions.

   ```java
   try {
       int[] myNumbers = {1, 2, 3};
       System.out.println(myNumbers[10]); // This will throw an exception
   } catch (ArrayIndexOutOfBoundsException e) {
       System.out.println("Array Index is Out Of Bounds");
   } catch (Exception e) {
       System.out.println("Something went wrong");
   }
   ```

3. **finally**

   The `finally` block always executes when the `try` block exits, regardless of whether an exception occurred. This is useful for closing resources like files or network connections.

   ```java
   try {
       int[] myNumbers = {1, 2, 3};
       System.out.println(myNumbers[10]); // This will throw an exception
   } catch (Exception e) {
       System.out.println("Something went wrong");
   } finally {
       System.out.println("The 'try catch' is finished.");
   }
   ```

4. **throw**

   The `throw` keyword allows you to create a custom error. The `throw` statement requires a single argument which must be an instance of `Throwable` or a subclass of `Throwable`.

   ```java
   public static void checkAge(int age) {
       if (age < 18) {
           throw new ArithmeticException("Access denied - You must be at least 18 years old.");
       } else {
           System.out.println("Access granted - You are old enough!");
       }
   }

   public static void main(String[] args) {
       checkAge(15); // This will throw an ArithmeticException
   }
   ```

5. **throws**

   The `throws` keyword is used to declare an exception. It gives information to the programmer that there may occur an exception so it is better for the programmer to provide the exception handling code.

   ```java
   public static void findFile() throws IOException {
       File newFile = new File("test.txt");
       FileInputStream stream = new FileInputStream(newFile);
   }

   public static void main(String[] args) {
       try {
           findFile();
       } catch (IOException e) {
           System.out.println("An error occurred");
       }
   }
   ```

Remember, exception handling is all about maintaining the normal flow of the application even after an exception occurs. Understanding and properly using these constructs will help you to write robust and error-resistant code.
