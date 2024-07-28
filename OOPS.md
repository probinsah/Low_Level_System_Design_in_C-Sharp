# Object Oriented Programming in C#
## Classes and Objects.
1. **Class-** A class is a blueprint for creating objects. It defines a type of object according to the properties and methods it should have.
2. **Object-** Objects are instances of a class. You use the new keyword followed by the class constructor to create an object.
> Program.cs
```
using OOPsDemo1;
using System;

public class Program
{
    public static void Main()
    {
        // Creating an object of Person class
        Person person = new Person();
        person.Name = "John";
        person.Age = 30;
        person.DisplayInfo();  // Output: Name: John, Age: 30
    }
}
```
> Person.cs
```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace OOPsDemo1
{
    public class Person
    {
        // Fields
        public string Name;
        public int Age;

        // Method
        public void DisplayInfo()
        {
            Console.WriteLine($"Name: {Name}, Age: {Age}");
        }
    }
}
```

3. **Instance Variable-** Instance variables are variables declared in a class that represent the state of an object. Each object has its own copy of these variables.
4. **Instance Methods-** Instance methods are functions defined in a class that can be called on objects of that class. They typically operate on instance variables.
```
public class Rectangle
{
    // Instance variables
    public double Length;
    public double Width;

    // Instance method
    public double GetArea()
    {
        return Length * Width;
    }
}

public class Program
{
    public static void Main()
    {
        // Creating an object of Rectangle class
        Rectangle rect = new Rectangle();
        rect.Length = 10.0;
        rect.Width = 5.0;

        double area = rect.GetArea();  // Output: 50.0
        Console.WriteLine($"Area: {area}");
    }
}
```

5. **Constructors and Destructors-** Constructors are special methods for instantiating objects. Destructors are called when an object is destroyed.
```
public class Book
{
    public string Title;
    public string Author;

    // Constructor
    public Book(string title, string author)
    {
        Title = title;
        Author = author;
    }

    // Destructor
    ~Book()
    {
        // Cleanup code here
    }
}

public class Program
{
    public static void Main()
    {
        // Creating an object using the constructor
        Book book = new Book("1984", "George Orwell");
        Console.WriteLine($"Title: {book.Title}, Author: {book.Author}");
    }
}
```

6. **Static Member-** Static members are shared among all instances of a class. This means there is only one copy of a static member, regardless of how many instances of the class are created. Static members can be variables, methods, properties, constructors, or even classes.
- **Static Variables** Static variables are useful for data that should be shared among all instances of a class.
- **Static Methods** Static methods are useful for utility functions that do not require any instance data.
- **Static Class** Static classes can only contain static members and cannot be instantiated.
```
public static class Logger
{
    // Static method for logging information
    public static void LogInfo(string message)
    {
        Console.WriteLine($"Info: {message}");
    }

    // Static method for logging errors
    public static void LogError(string message)
    {
        Console.WriteLine($"Error: {message}");
    }
}

public class Program
{
    public static void Main()
    {
        Logger.LogInfo("This is an informational message.");
        Logger.LogError("This is an error message.");
    }
}
```

## Constructors and Destructors in C#
### Constructors
**Constructors** are special methods that are called when an object is instantiated. They are used to initialize the object's state. Constructors have the same name as the class and do not have a return type.
1. **Default Constructor** - A default constructor is a constructor with no parameters. If no constructor is provided, the compiler automatically creates a default constructor.
```
public class Person
{
    public string Name;
    public int Age;

    // Default constructor
    public Person()
    {
        Name = "Unknown";
        Age = 0;
    }
}

public class Program
{
    public static void Main()
    {
        Person person = new Person();
        Console.WriteLine($"Name: {person.Name}, Age: {person.Age}");
    }
}
```
2. **Parameterized Constructor** - A parameterized constructor allows you to pass arguments when creating an object, enabling the initialization of the object with specific values.
```
public class Person
{
    public string Name;
    public int Age;

    // Parameterized constructor
    public Person(string name, int age)
    {
        Name = name;
        Age = age;
    }
}

public class Program
{
    public static void Main()
    {
        Person person = new Person("John", 30);
        Console.WriteLine($"Name: {person.Name}, Age: {person.Age}");
    }
}
```
3. **Copy Constructor** - A copy constructor creates a new object as a copy of an existing object.
```
public class Person
{
    public string Name;
    public int Age;

    // Parameterized constructor
    public Person(string name, int age)
    {
        Name = name;
        Age = age;
    }

    // Copy constructor
    public Person(Person person)
    {
        Name = person.Name;
        Age = person.Age;
    }
}

public class Program
{
    public static void Main()
    {
        Person person1 = new Person("John", 30);
        Person person2 = new Person(person1);
        Console.WriteLine($"Name: {person2.Name}, Age: {person2.Age}");
    }
}
```
4. **Static Constructor** - A static constructor is used to initialize static members of a class. It is called automatically before the first instance is created or any static members are referenced.
```
public class Configuration
{
    public static string Setting;

    // Static constructor
    static Configuration()
    {
        Setting = "Default Configuration";
    }
}

public class Program
{
    public static void Main()
    {
        Console.WriteLine(Configuration.Setting);
    }
}
```
5. **Private Constructor** - A private constructor prevents the instantiation of a class from outside the class. It is commonly used in singleton patterns.
> The **Singleton Pattern** is a design pattern that restricts the instantiation of a class to one single instance. This is useful when exactly one object is needed to coordinate actions across the system. The Singleton Pattern ensures that a class has only one instance and provides a global point of access to it.

```
public class Singleton
{
    private static Singleton instance = null;

    // Private constructor
    private Singleton() { }

    public static Singleton Instance
    {
        get
        {
            if (instance == null)
            {
                instance = new Singleton();
            }
            return instance;
        }
    }
}

public class Program
{
    public static void Main()
    {
        Singleton singleton1 = Singleton.Instance;
        Singleton singleton2 = Singleton.Instance;

        Console.WriteLine(object.ReferenceEquals(singleton1, singleton2));  // Output: True
    }
}
```

### Destructors
Destructors are special methods used to clean up resources before an object is destroyed. They have the same name as the class, preceded by a tilde (~), and do not take any parameters or have a return type. Destructors are called automatically by the garbage collector and cannot be called explicitly.
```
public class Resource
{
    // Destructor
    ~Resource()
    {
        // Cleanup code here
        Console.WriteLine("Destructor called, resource cleaned up.");
    }
}

public class Program
{
    public static void Main()
    {
        Resource res = new Resource();
    }
}
```

## Inheritance in C#
Inheritance is a fundamental concept in object-oriented programming (OOP) that allows a class to inherit properties and methods from another class. The class that inherits is called the derived class (or child class), and the class being inherited from is called the base class (or parent class).

Types of Inheritance:
1. **Single Inheritance** - Single inheritance involves a single derived class inheriting from a single base class.
```
public class Animal
{
    public void Eat()
    {
        Console.WriteLine("Eating...");
    }
}

public class Dog : Animal
{
    public void Bark()
    {
        Console.WriteLine("Barking...");
    }
}

public class Program
{
    public static void Main()
    {
        Dog dog = new Dog();
        dog.Eat();  // Inherited method
        dog.Bark(); // Derived class method
    }
}
```
2. **Multilevel Inheritance** - Multilevel inheritance involves a derived class inheriting from another derived class.
```
public class Animal
{
    public void Eat()
    {
        Console.WriteLine("Eating...");
    }
}

public class Dog : Animal
{
    public void Bark()
    {
        Console.WriteLine("Barking...");
    }
}

public class Puppy : Dog
{
    public void Weep()
    {
        Console.WriteLine("Weeping...");
    }
}

public class Program
{
    public static void Main()
    {
        Puppy puppy = new Puppy();
        puppy.Eat();  // Inherited from Animal
        puppy.Bark(); // Inherited from Dog
        puppy.Weep(); // Method of Puppy
    }
}
```
3. **Hierarchical Inheritance** - Hierarchical inheritance involves multiple derived classes inheriting from a single base class.
```
public class Animal
{
    public void Eat()
    {
        Console.WriteLine("Eating...");
    }
}

public class Dog : Animal
{
    public void Bark()
    {
        Console.WriteLine("Barking...");
    }
}

public class Cat : Animal
{
    public void Meow()
    {
        Console.WriteLine("Meowing...");
    }
}

public class Program
{
    public static void Main()
    {
        Dog dog = new Dog();
        Cat cat = new Cat();

        dog.Eat();  // Inherited from Animal
        dog.Bark(); // Method of Dog

        cat.Eat();  // Inherited from Animal
        cat.Meow(); // Method of Cat
    }
}
```
4. **Multiple Inheritance (through Interfaces)** - C# does not support multiple inheritance directly to avoid complexity and ambiguity. However, it supports multiple inheritance through interfaces.
```
public interface IMovable
{
    void Move();
}

public interface IFlyable
{
    void Fly();
}

public class Bird : IMovable, IFlyable
{
    public void Move()
    {
        Console.WriteLine("Moving...");
    }

    public void Fly()
    {
        Console.WriteLine("Flying...");
    }
}

public class Program
{
    public static void Main()
    {
        Bird bird = new Bird();
        bird.Move(); // Method from IMovable
        bird.Fly();  // Method from IFlyable
    }
}
```
### Access Modifiers in Inheritance.
Access modifiers control the visibility of class members in derived classes.
- **public:** Accessible from anywhere.
- **private:** Accessible only within the same class (not inherited).
- **protected:** Accessible within the same class and derived classes.
- **internal:** Accessible within the same assembly.
- **protected internal:** Accessible within the same assembly and derived classes.
- **private protected:** Accessible within the same class and derived classes within the same assembly.
```
public class BaseClass
{
    public string PublicProperty = "Public";
    private string PrivateProperty = "Private";
    protected string ProtectedProperty = "Protected";
    internal string InternalProperty = "Internal";
    protected internal string ProtectedInternalProperty = "Protected Internal";
    private protected string PrivateProtectedProperty = "Private Protected";

    public void ShowProperties()
    {
        Console.WriteLine(PublicProperty);
        Console.WriteLine(PrivateProperty);
        Console.WriteLine(ProtectedProperty);
        Console.WriteLine(InternalProperty);
        Console.WriteLine(ProtectedInternalProperty);
        Console.WriteLine(PrivateProtectedProperty);
    }
}

public class DerivedClass : BaseClass
{
    public void ShowAccessibleProperties()
    {
        Console.WriteLine(PublicProperty);
        // Console.WriteLine(PrivateProperty); // Not accessible
        Console.WriteLine(ProtectedProperty);
        Console.WriteLine(InternalProperty);
        Console.WriteLine(ProtectedInternalProperty);
        Console.WriteLine(PrivateProtectedProperty);
    }
}

public class Program
{
    public static void Main()
    {
        DerivedClass derived = new DerivedClass();
        derived.ShowAccessibleProperties();
    }
}
```
Note- In C#, an assembly is a compiled code library used for deployment, versioning, and security. An assembly can be a .dll or .exe file. When we say that a member is "accessible within the same assembly," it means that the member can be accessed from any class or method within the same compiled code library (assembly), but not from another assembly.

**What is the use of base keyword in C#?**
- The base keyword in C# is used to access members of the base class from within a derived class. It is commonly used to call base class constructors, methods, and properties.
```
public class Animal
{
    public string Name;

    // Base class constructor
    public Animal(string name)
    {
        Name = name;
    }
}

public class Dog : Animal
{
    public string Breed;

    // Derived class constructor
    public Dog(string name, string breed) : base(name)  // Call to base class constructor
    {
        Breed = breed;
    }

    public void DisplayInfo()
    {
        Console.WriteLine($"Name: {Name}, Breed: {Breed}");
    }
}

public class Program
{
    public static void Main()
    {
        Dog dog = new Dog("Buddy", "Golden Retriever");
        dog.DisplayInfo();  // Output: Name: Buddy, Breed: Golden Retriever
    }
}
```
## Polymorphism in C#
Polymorphism is a fundamental concept in object-oriented programming that allows objects of different types to be treated as objects of a common super type. In C#, polymorphism is typically achieved through inheritance and interfaces, allowing methods to behave differently based on the object that invokes them.
### Types of Polymorphism.
1. **Compile-Time Polymorphism** - Compile-time polymorphism is achieved through method overloading and operator overloading. It is called static polymorphism because the method to be invoked is determined at compile time. Example-
```
public class Calculator
{
    // Method Overloading
    public int Add(int a, int b)
    {
        return a + b;
    }

    public double Add(double a, double b)
    {
        return a + b;
    }
}

public class Program
{
    public static void Main()
    {
        Calculator calculator = new Calculator();
        Console.WriteLine(calculator.Add(2, 3));       // Output: 5
        Console.WriteLine(calculator.Add(2.5, 3.5));   // Output: 6.0
    }
}
```
2. **Run-Time Polymorphism** - Run-time polymorphism is achieved through method overriding and interfaces. It is called dynamic polymorphism because the method to be invoked is determined at run time. Example -
```
public class Animal
{
    public virtual void MakeSound()
    {
        Console.WriteLine("Animal makes a sound");
    }
}

public class Dog : Animal
{
    public override void MakeSound()
    {
        Console.WriteLine("Dog barks");
    }
}

public class Cat : Animal
{
    public override void MakeSound()
    {
        Console.WriteLine("Cat meows");
    }
}

public class Program
{
    public static void Main()
    {
        Animal myAnimal = new Animal();
        Animal myDog = new Dog();
        Animal myCat = new Cat();

        myAnimal.MakeSound();  // Output: Animal makes a sound
        myDog.MakeSound();     // Output: Dog barks
        myCat.MakeSound();     // Output: Cat meows
    }
}
```
> **Compile-time** is the phase during which the source code is translated into executable code by a compiler. Syntax errors, type checking, and other compile-time errors are detected at this stage.
> **Run-time** is the phase during which the executable code is run on the machine. Run-time errors like exceptions and logic errors are detected at this stage.

#### Virtual Methods in C#
In C#, virtual methods allow a method in a base class to be overridden in a derived class. This enables polymorphism, where the method to be executed is determined at run-time based on the actual object type. Virtual methods support run-time polymorphism, allowing derived class methods to be called through a base class reference. Useful for designing extensible and flexible code where derived classes can provide specific implementations of base class methods. *Refer the example of Method Overriding above for better understanding of the working.*

### Abstract Classes and Methods in C#
Abstract Classes and Abstract Methods in C# are used to define a template for other classes. They provide a way to enforce that certain methods are implemented by derived classes while allowing the base class to provide common functionality.
- **Abstract Classes** - An abstract class is a class that cannot be instantiated on its own and is intended to be a base class for other classes. It can contain both abstract methods (methods without implementation) and concrete methods (methods with implementation).
- **Abstract Methods** - An abstract method is a method that is declared without any implementation. Derived classes must provide an implementation for all abstract methods inherited from the abstract class.
> Abstract classes provide a template for other classes, enforcing a contract for the derived classes while allowing common functionality to be shared.
Consider an abstract class Shape and its derived classes Circle and Rectangle.
```
// Abstract Class with Abstract and Concrete Methods:
public abstract class Shape
{
    // Abstract method (no implementation)
    public abstract double GetArea();

    // Concrete method
    public void DisplayArea()
    {
        Console.WriteLine("The area of the shape is: " + GetArea());
    }
}
// Derived Class Implementing Abstract Methods:
public class Circle : Shape
{
    public double Radius { get; set; }

    public Circle(double radius)
    {
        Radius = radius;
    }

    // Implementation of the abstract method
    public override double GetArea()
    {
        return Math.PI * Radius * Radius;
    }
}

public class Rectangle : Shape
{
    public double Width { get; set; }
    public double Height { get; set; }

    public Rectangle(double width, double height)
    {
        Width = width;
        Height = height;
    }

    // Implementation of the abstract method
    public override double GetArea()
    {
        return Width * Height;
    }
}
// Using the Abstract Class and Derived Classes:
public class Program
{
    public static void Main()
    {
        Shape myCircle = new Circle(5.0);
        Shape myRectangle = new Rectangle(4.0, 6.0);

        myCircle.DisplayArea();    // Output: The area of the shape is: 78.53981633974483
        myRectangle.DisplayArea(); // Output: The area of the shape is: 24
    }
}
```

### Interfaces in C#
An interface in C# is a contract that defines a set of methods and properties that a class must implement. Interfaces are used to achieve abstraction and multiple inheritance, providing a way to enforce certain functionalities across different classes without dictating how those functionalities should be implemented. Interfaces cannot contain fields (variables). Interfaces can inherit from other interfaces, allowing the creation of more complex contracts.

```
public interface IAnimal
{
    // Method declaration
    void MakeSound();
    
    // Property declaration
    string Name { get; set; }
}
```
```
public class Dog : IAnimal
{
    // Implementing the property
    public string Name { get; set; }

    // Implementing the method
    public void MakeSound()
    {
        Console.WriteLine("Dog barks");
    }
}

public class Cat : IAnimal
{
    // Implementing the property
    public string Name { get; set; }

    // Implementing the method
    public void MakeSound()
    {
        Console.WriteLine("Cat meows");
    }
}
```
```
public class Program
{
    public static void Main()
    {
        IAnimal myDog = new Dog() { Name = "Buddy" };
        IAnimal myCat = new Cat() { Name = "Whiskers" };

        Console.WriteLine($"{myDog.Name}:");
        myDog.MakeSound();  // Output: Buddy: Dog barks

        Console.WriteLine($"{myCat.Name}:");
        myCat.MakeSound();  // Output: Whiskers: Cat meows
    }
}
```
#### Operator Overloading in C#
Operator Overloading allows you to redefine or "overload" the built-in operators for user-defined types. This means you can specify how operators like +, -, *, /, and others behave when applied to instances of your classes or structs. The return type can be of any type but is typically the same as the type of the operands. The parameters must include at least one operand of the type that defines the operator.
```
public class Complex
{
    public double Real { get; set; }
    public double Imaginary { get; set; }

    public Complex(double real, double imaginary)
    {
        Real = real;
        Imaginary = imaginary;
    }

    // Overloading the + operator
    public static Complex operator +(Complex c1, Complex c2)
    {
        return new Complex(c1.Real + c2.Real, c1.Imaginary + c2.Imaginary);
    }

    // Overloading the - operator
    public static Complex operator -(Complex c1, Complex c2)
    {
        return new Complex(c1.Real - c2.Real, c1.Imaginary - c2.Imaginary);
    }

    // Overriding ToString() for easy display
    public override string ToString()
    {
        return $"{Real} + {Imaginary}i";
    }
}
```
```
public class Program
{
    public static void Main()
    {
        Complex c1 = new Complex(2.0, 3.0);
        Complex c2 = new Complex(1.5, 2.5);

        Complex sum = c1 + c2;
        Complex difference = c1 - c2;

        Console.WriteLine("c1: " + c1);          // Output: c1: 2 + 3i
        Console.WriteLine("c2: " + c2);          // Output: c2: 1.5 + 2.5i
        Console.WriteLine("Sum: " + sum);        // Output: Sum: 3.5 + 5.5i
        Console.WriteLine("Difference: " + difference);  // Output: Difference: 0.5 + 0.5i
    }
}
```
> **Readonly** fields in C# are fields that can be assigned a value only during their declaration or in a constructor. Once assigned, their values cannot be changed. This ensures that the value of the field remains constant after object construction, providing a form of immutability.
