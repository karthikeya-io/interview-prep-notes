## Basic Concepts of Object-Oriented Programming (OOP)

The four basic pillars of Object-Oriented Programming (OOP) are:

1. **Encapsulation:** Encapsulation is the concept of bundling data (attributes) and methods (functions) that operate on the data into a single unit called a class. It restricts direct access to some of an object's components, allowing only the methods defined within the class to manipulate the internal state. Encapsulation helps to achieve data hiding and reduces the chances of unintended interference with the object's internal state.

2. **Abstraction:** Abstraction is the process of simplifying complex reality by modeling classes based on the essential properties and behaviors an object should have. It involves focusing on what an object does rather than how it does it. Abstract classes and interfaces are used to define the structure and contracts that concrete classes must adhere to.

3. **Inheritance:** Inheritance allows a new class (subclass or derived class) to inherit properties and behaviors (attributes and methods) from an existing class (superclass or base class). This promotes code reusability and allows for the creation of hierarchical relationships between classes. Subclasses can extend or override the behavior of their parent classes.

4. **Polymorphism:** Polymorphism means the ability of objects of different classes to be treated as objects of a common superclass. It allows objects to be manipulated using their common interface (methods), even if they belong to different classes. Polymorphism is achieved through method overriding (runtime polymorphism) and method overloading (compile-time polymorphism).

These pillars provide a foundation for creating well-structured, modular, and maintainable software using object-oriented principles. They enable better organization of code, separation of concerns, and the ability to model real-world entities more accurately within the programming paradigm.

## **Object-Oriented Programming (OOP) in Java**

1. **Classes and Objects**

   A class is a blueprint from which individual objects are created. An object is an instance of a class.

   ```java
   // Define a class
   class Dog {
       String name;
       int age;

       void bark() {
           System.out.println(name + " says: Woof!");
       }
   }

   // Create an object
   Dog myDog = new Dog();
   myDog.name = "Rex";
   myDog.age = 5;
   myDog.bark();  // Prints: Rex says: Woof!
   ```

2. **Constructors**

   A constructor is a special method used to initialize objects. The constructor is called when an object of a class is created.

   ```java
   class Dog {
       String name;
       int age;

       // Constructor
       Dog(String name, int age) {
           this.name = name;
           this.age = age;
       }

       void bark() {
           System.out.println(name + " says: Woof!");
       }
   }

   // Create an object using the constructor
   Dog myDog = new Dog("Rex", 5);
   myDog.bark();  // Prints: Rex says: Woof!
   ```

3. **Inheritance**

   Inheritance is a mechanism where you can derive a class from another class for a hierarchy of classes that share a set of attributes and methods.

   ```java
   // Parent class
   class Animal {
       void eat() {
           System.out.println("The animal eats");
       }
   }

   // Child class
   class Dog extends Animal {
       void bark() {
           System.out.println("The dog barks");
       }
   }

   // Use the child class
   Dog myDog = new Dog();
   myDog.eat();  // From the parent class
   myDog.bark(); // From the child class
   ```

4. **Polymorphism**

   Polymorphism allows us to perform a single action in different ways. In Java, we use method overloading and method overriding to achieve polymorphism.

   - **Method Overloading**: Occurs within the same class where two or more methods share the same name but have different parameters.

   - **Method Overriding**: Occurs in two classes that have IS-A (inheritance) relationship. The method in the child class has the same name, type, and parameters as the one in its parent class.

   ```java
   class Dog {
       // Method overloading
       void bark() {
           System.out.println("Woof!");
       }

       void bark(int times) {
           for (int i = 0; i < times; i++) {
               System.out.print("Woof! ");
           }
           System.out.println();
       }
   }

   class BigDog extends Dog {
       // Method overriding
       @Override
       void bark() {
           System.out.println("WOOF!");
       }
   }

   // Use polymorphism
   Dog myDog = new Dog();
   myDog.bark();
   myDog.bark(3);

   Dog myBigDog = new BigDog();
   myBigDog.bark();
   ```

5. **Encapsulation**

   Encapsulation is the technique of making the fields in a class private and providing access to the fields via public methods.

   ```java
   class Dog {
       private String name;  // Private field

       // Getter method
       public String getName() {
           return name;
       }

       // Setter method
       public void setName(String name) {
           this.name = name;
       }
   }

   // Use encapsulation


   Dog myDog = new Dog();
   myDog.setName("Rex");
   System.out.println(myDog.getName());
   ```

6. **Abstraction**

   Abstraction is a process of hiding the implementation details and showing only functionality to the user. In Java, we use abstract classes and interfaces to achieve abstraction.

   - **Abstract Class**: A class that cannot be instantiated. It can have abstract and non-abstract methods.

   - **Interface**: A completely abstract class that can only have abstract methods.

   ```java
   // Abstract class
   abstract class Animal {
       abstract void makeSound();
   }

   // Interface
   interface Pet {
       void beFriendly();
   }

   // A class can inherit from an abstract class and multiple interfaces
   class Dog extends Animal implements Pet {
       @Override
       void makeSound() {
           System.out.println("Woof!");
       }

       @Override
       public void beFriendly() {
           System.out.println("Wags tail");
       }
   }

   // Use abstraction
   Dog myDog = new Dog();
   myDog.makeSound();
   myDog.beFriendly();
   ```

7. **Interfaces**

   An interface is a completely abstract class that is used to group related methods with empty bodies. A class can implement any number of interfaces.

   ```java
   interface Animal {
       void eat();
       void sleep();
   }

   class Dog implements Animal {
       public void eat() {
           System.out.println("The dog eats");
       }

       public void sleep() {
           System.out.println("The dog sleeps");
       }
   }

   Dog myDog = new Dog();
   myDog.eat();
   myDog.sleep();
   ```

Each of these concepts plays a critical role in object-oriented programming in Java. Understanding them will provide a solid foundation for your Java programming skills.
