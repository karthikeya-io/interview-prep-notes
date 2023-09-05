**Java I/O (Input/Output)**

Java I/O (Input and Output) is used to process the input and produce the output. Java uses the concept of streams to make I/O operations fast. The java.io package contains all the classes required for input and output operations.

1. **Byte Streams**: Java byte streams are used to perform input and output of 8-bit bytes.

   - **FileInputStream**: Used to read data from a file.
   - **FileOutputStream**: Used to write data to a file.

   ```java
   import java.io.*;

   // Write to a file using FileOutputStream
   try {
       FileOutputStream fout = new FileOutputStream("test.txt");
       String s = "Hello, world!";
       byte[] b = s.getBytes();  // Converting string into byte array
       fout.write(b);
       fout.close();
       System.out.println("Success...");
   } catch (Exception e) {
       System.out.println(e);
   }

   // Read from a file using FileInputStream
   try {
       FileInputStream fin = new FileInputStream("test.txt");
       int i;
       while ((i = fin.read()) != -1) {
           System.out.print((char) i);
       }
       fin.close();
   } catch (Exception e) {
       System.out.println(e);
   }
   ```

2. **Character Streams**: Java byte streams are used to perform input and output for 16-bit unicode.

   - **FileReader**: Used for reading streams of characters from a file.
   - **FileWriter**: Used for writing streams of characters to a file.

   ```java
   // Write to a file using FileWriter
   try {
       FileWriter fw = new FileWriter("test.txt");
       fw.write("Hello, world!");
       fw.close();
   } catch (IOException e) {
       System.out.println(e);
   }

   // Read from a file using FileReader
   try {
       FileReader fr = new FileReader("test.txt");
       int i;
       while ((i = fr.read()) != -1)
           System.out.print((char) i);
       fr.close();
   } catch (IOException e) {
       System.out.println(e);
   }
   ```

3. **Buffered Streams**: Java BufferedInputStream class is used to read information from stream. It internally uses buffer mechanism to make the performance fast.

   - **BufferedReader**: Reads text from a character-input stream, buffering characters so as to provide for the efficient reading of characters, arrays, and lines.
   - **BufferedWriter**: Writes text to a character-output stream, buffering characters so as to provide for the efficient writing of single characters, arrays, and strings.

   ```java
   // Write to a file using BufferedWriter
   try {
       FileWriter writer = new FileWriter("test.txt");
       BufferedWriter buffer = new BufferedWriter(writer);
       buffer.write("Hello, world!");
       buffer.close();
       System.out.println("Success...");
   } catch (IOException e) {
       System.out.println(e);
   }

   // Read from a file using BufferedReader
   try {
       FileReader reader = new FileReader("test.txt");
       BufferedReader buffer = new BufferedReader(reader);
       String line;
       while ((line = buffer.readLine()) != null) {
           System.out.println(line);
       }
       buffer.close();
   } catch (IOException e) {
       System.out.println(e);
   }
   ```

4. **Standard Streams**: All the programming languages provide support for standard I/O where the user's program can take input from a keyboard and then produce an output on the computer screen. If you are aware of C or C++ programming languages, then you must be aware of three standard devices STDIN, STDOUT and STDERR. Similarly, Java provides the following three standard streams −

- **Standard Input**: This is used to feed the data to user's program and usually a keyboard is used as a standard input stream and represented as `System.in`.

  - **Standard Output**: This is used to output the data produced by the user's program and usually a computer screen is used for standard output stream and represented as `System.out`.
  - **Standard Error**: This is used to output the error data produced by the user's program and usually a computer screen is used for standard error stream and represented as `System.err`.

  ```java
  System.out.println("Output message");
  System.err.println("Error message");

  Scanner scanner = new Scanner(System.in);
  System.out.println("Enter your name: ");
  String name = scanner.next();
  System.out.println("Your name is " + name);
  ```

  ```java
  import java.util.Scanner;

  public class NextExample {
      public static void main(String[] args) {
          Scanner scanner = new Scanner(System.in);

          System.out.print("Enter your first name: ");
          String firstName = scanner.next();

          System.out.print("Enter your last name: ");
          String lastName = scanner.next();

          System.out.println("Hello, " + firstName + " " + lastName + "!");

          scanner.close();
      }
  }
  ```

These are some of the common classes and methods used in Java I/O. There are many more classes in the `java.io` package that you can explore to perform various other I/O operations.
