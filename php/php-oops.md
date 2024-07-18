### PHP Object-Oriented Programming (OOP)

Object-Oriented Programming (OOP) in PHP allows developers to create modular, reusable, and organized code. Below are explanations and examples of key OOP concepts in PHP.

### PHP What is OOP
OOP is a programming paradigm that uses "objects" to model real-world entities. Objects are instances of classes, which define their properties (attributes) and methods (functions).

### PHP Classes/Objects
A class is a blueprint for creating objects, which are instances of that class.

**Example:**
```php
<?php
class Car {
    // Properties
    public $make;
    public $model;

    // Methods
    public function setMake($make) {
        $this->make = $make;
    }

    public function getMake() {
        return $this->make;
    }
}

$myCar = new Car();
$myCar->setMake("Toyota");
echo $myCar->getMake(); // Outputs: Toyota
?>
```

### PHP Constructor
A constructor is a special method that is automatically called when an object is instantiated.

**Example:**
```php
<?php
class Car {
    public $make;
    public $model;

    // Constructor
    public function __construct($make, $model) {
        $this->make = $make;
        $this->model = $model;
    }

    public function getDetails() {
        return $this->make . " " . $this->model;
    }
}

$myCar = new Car("Toyota", "Corolla");
echo $myCar->getDetails(); // Outputs: Toyota Corolla
?>
```

### PHP Destructor
A destructor is a special method called when an object is destroyed. Runs at the end of script.
**Example:**
```php
<?php
class Car {
    public $make;
    public $model;

    public function __construct($make, $model) {
        $this->make = $make;
        $this->model = $model;
    }

    // Destructor
    public function __destruct() {
        echo "The car is being destroyed: " . $this->make . " " . $this->model;
    }
}

$myCar = new Car("Toyota", "Corolla");
?>
```

### PHP Access Modifiers
Access modifiers define the visibility of properties and methods. They are `public`, `protected`, and `private`.

**Example:**
```php
<?php
class Car {
    public $make; // Public property
    protected $model; // Protected property
    private $year; // Private property

    public function setModel($model) {
        $this->model = $model;
    }

    public function getModel() {
        return $this->model;
    }

    public function setYear($year) {
        $this->year = $year;
    }

    public function getYear() {
        return $this->year;
    }
}

$myCar = new Car();
$myCar->make = "Toyota"; // Accessible
$myCar->setModel("Corolla"); // Accessible through method
$myCar->setYear(2020); // Accessible through method
echo $myCar->getModel(); // Outputs: Corolla
echo $myCar->getYear(); // Outputs: 2020
?>
```

### PHP Inheritance
Inheritance allows a class to inherit properties and methods from another class.

**Example:**
```php
<?php
class Vehicle {
    public $make;
    public $model;

    public function getDetails() {
        return $this->make . " " . $this->model;
    }
}

class Car extends Vehicle {
    public function getCarDetails() {
        return "Car: " . $this->getDetails();
    }
}

$myCar = new Car();
$myCar->make = "Toyota";
$myCar->model = "Corolla";
echo $myCar->getCarDetails(); // Outputs: Car: Toyota Corolla
?>
```

### PHP Constants
Constants are defined using the `const` keyword and cannot be changed once set.

**Example:**
```php
<?php
class Car {
    const WHEELS = 4;

    public function getWheels() {
        return self::WHEELS;
    }
}

echo Car::WHEELS; // Outputs: 4
?>
```

### PHP Abstract Classes
Abstract classes cannot be instantiated and are meant to be extended by other classes. They can have abstract methods that must be implemented by derived classes.

**Example:**
```php
<?php
abstract class Vehicle {
    public $make;
    public $model;

    abstract public function getDetails();
}

class Car extends Vehicle {
    public function getDetails() {
        return $this->make . " " . $this->model;
    }
}

$myCar = new Car();
$myCar->make = "Toyota";
$myCar->model = "Corolla";
echo $myCar->getDetails(); // Outputs: Toyota Corolla
?>
```

### PHP Interfaces
Interfaces define a contract for classes without implementing any methods. Classes that implement an interface must define all its methods.

**Example:**
```php
<?php
interface VehicleInterface {
    public function getDetails();
}

class Car implements VehicleInterface {
    public $make;
    public $model;

    public function getDetails() {
        return $this->make . " " . $this->model;
    }
}

$myCar = new Car();
$myCar->make = "Toyota";
$myCar->model = "Corolla";
echo $myCar->getDetails(); // Outputs: Toyota Corolla
?>
```

### PHP Traits
Traits are used to include methods in a class. They are a mechanism for code reuse.

**Example:**
```php
<?php
trait ElectricVehicleTrait {
    public function charge() {
        return "Charging the electric vehicle.";
    }
}

class Car {
    use ElectricVehicleTrait;
}

$myCar = new Car();
echo $myCar->charge(); // Outputs: Charging the electric vehicle.
?>
```

### PHP Static Methods
Static methods belong to the class rather than any object instance and are called using the class name.

**Example:**
```php
<?php
class Car {
    public static function getDescription() {
        return "This is a car.";
    }
}

echo Car::getDescription(); // Outputs: This is a car.
?>
```

### PHP Static Properties
Static properties belong to the class rather than any object instance and are accessed using the class name.

**Example:**
```php
<?php
class Car {
    public static $type = "Sedan";

    public static function getType() {
        return self::$type;
    }
}

echo Car::$type; // Outputs: Sedan
echo Car::getType(); // Outputs: Sedan
?>
```

### PHP Namespaces
Namespaces are used to avoid name collisions between classes or functions.

**Example:**
```php
<?php
namespace Vehicles;

class Car {
    public function getDetails() {
        return "This is a car.";
    }
}

$myCar = new \Vehicles\Car();
echo $myCar->getDetails(); // Outputs: This is a car.
?>
```

### PHP Iterables
Iterables can be used with `foreach` loops and include arrays and objects implementing the `Traversable` interface.

**Example:**
```php
<?php
function printIterable(iterable $myIterable) {
    foreach ($myIterable as $item) {
        echo $item . "\n";
    }
}

$myArray = ["apple", "banana", "cherry"];
printIterable($myArray); // Outputs: apple, banana, cherry
?>
```

### Important points
1. What will you use, for calling the same function with different parameters within a class? Is there any way to have the same function within class but with different parameters?
- This is called Overloading but PHP does not support redefining a method multiple times. But in PHP we can achieve this by following ways.
  1. Default Parameters
     - We can pass default parameter so if the the parameter is not passed default value is take
     - `function(name, age=25)` so if age is not passed 25 is taken.
  2. Variadic Functions
     - `function name( ...$param ) ` `$param` stores any number of params as an array.
  3. Method Overloading with Magic Methods
     - `function __call(string $function_name, array $arguments) {}` the first argument is function name and the second argument takes any number of parameters and stores as array.

2. What is the difference between Global Variable and Class Variable?
- Global Variable:
Global Variable are declared at top level and can be used with `global` keyword or `$GLOBALS`
```php
<?php
$x = 1;

function test()
{
  echo $x; // warning undefined
  echo $GLOBALS['x']; // output 1
  global $x;
  echo $x; // output 1
}

test();
?>
```
- Class Variable:
  - Static Variables: Class Variables that are static variables can be accessed with class name or inside class with `self` or `parent` if declared in parent class.
    - `ClassName::$staticVar;` outside class
    - `self::staticVar ` inside the class
  - Non static variables:
    - `$this->var` accessed inside class
    - `object->var` outside class is accessed with instance of class (objects)
  - these variables also follow the access modifier rules based on the access modifier.
