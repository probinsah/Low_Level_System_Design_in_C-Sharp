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
