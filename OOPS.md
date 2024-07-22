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
