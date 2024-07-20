## **C# Programming Cheat Sheet**

### **1. Basics**

- **Hello World**
  ```csharp
  using System;

  class Program
  {
      static void Main()
      {
          Console.WriteLine("Hello, World!");
      }
  }
  ```

- **Data Types**
  ```csharp
  int a = 10;             // Integer
  double b = 5.5;         // Double precision floating point
  char c = 'A';           // Character
  string d = "Hello";    // String
  bool e = true;         // Boolean
  ```

- **Variables and Constants**
  ```csharp
  const int MaxValue = 100;
  int x = 5;
  ```

- **Operators**
  ```csharp
  int sum = a + b;        // Addition
  int diff = a - b;       // Subtraction
  int product = a * b;    // Multiplication
  int quotient = a / b;   // Division
  int remainder = a % b;  // Modulus
  ```

- **Control Flow**
  - **If-Else**
    ```csharp
    if (x > 0)
    {
        Console.WriteLine("Positive");
    }
    else if (x < 0)
    {
        Console.WriteLine("Negative");
    }
    else
    {
        Console.WriteLine("Zero");
    }
    ```

  - **Switch-Case**
    ```csharp
    switch (x)
    {
        case 1:
            Console.WriteLine("One");
            break;
        case 2:
            Console.WriteLine("Two");
            break;
        default:
            Console.WriteLine("Other");
            break;
    }
    ```

  - **Loops**
    - **For Loop**
      ```csharp
      for (int i = 0; i < 10; i++)
      {
          Console.WriteLine(i);
      }
      ```

    - **While Loop**
      ```csharp
      int i = 0;
      while (i < 10)
      {
          Console.WriteLine(i);
          i++;
      }
      ```

    - **Do-While Loop**
      ```csharp
      int i = 0;
      do
      {
          Console.WriteLine(i);
          i++;
      } while (i < 10);
      ```

### **2. Functions**

- **Method Definition**
  ```csharp
  int Add(int a, int b)
  {
      return a + b;
  }
  ```

- **Method Call**
  ```csharp
  int result = Add(5, 3);
  ```

- **Overloading**
  ```csharp
  int Add(int a, int b) { return a + b; }
  double Add(double a, double b) { return a + b; }
  ```

### **3. Object-Oriented Programming**

- **Classes and Objects**
  ```csharp
  class Person
  {
      public string Name { get; set; }
      public int Age { get; set; }
      
      public void Greet()
      {
          Console.WriteLine($"Hello, my name is {Name}.");
      }
  }

  Person p = new Person();
  p.Name = "John";
  p.Age = 30;
  p.Greet();
  ```

- **Inheritance**
  ```csharp
  class Employee : Person
  {
      public int EmployeeId { get; set; }
  }

  Employee e = new Employee();
  e.Name = "Jane";
  e.EmployeeId = 123;
  ```

- **Polymorphism**
  ```csharp
  class Animal
  {
      public virtual void Speak() { Console.WriteLine("Animal speaks"); }
  }

  class Dog : Animal
  {
      public override void Speak() { Console.WriteLine("Woof"); }
  }

  Animal a = new Dog();
  a.Speak();  // Output: Woof
  ```

- **Interfaces**
  ```csharp
  interface IReadable
  {
      void Read();
  }

  class Book : IReadable
  {
      public void Read() { Console.WriteLine("Reading a book"); }
  }

  IReadable r = new Book();
  r.Read();
  ```

### **4. Collections**

- **Arrays**
  ```csharp
  int[] numbers = { 1, 2, 3, 4, 5 };
  ```

- **List**
  ```csharp
  using System.Collections.Generic;

  List<int> list = new List<int> { 1, 2, 3, 4, 5 };
  list.Add(6);
  list.Remove(3);
  ```

- **Dictionary**
  ```csharp
  Dictionary<string, int> dict = new Dictionary<string, int>();
  dict["Alice"] = 25;
  dict["Bob"] = 30;
  ```

### **5. Exception Handling**

- **Try-Catch**
  ```csharp
  try
  {
      int result = 10 / 0;
  }
  catch (DivideByZeroException ex)
  {
      Console.WriteLine($"Error: {ex.Message}");
  }
  ```

- **Finally**
  ```csharp
  try
  {
      // Code that may throw an exception
  }
  finally
  {
      // Code that will always execute
  }
  ```

### **6. File I/O**

- **Reading from a File**
  ```csharp
  using System.IO;

  string content = File.ReadAllText("file.txt");
  ```

- **Writing to a File**
  ```csharp
  File.WriteAllText("file.txt", "Hello, World!");
  ```

### **7. Advanced Features**

- **LINQ (Language Integrated Query)**
  ```csharp
  using System.Linq;

  int[] numbers = { 1, 2, 3, 4, 5 };
  var evenNumbers = numbers.Where(n => n % 2 == 0);
  ```

- **Delegates**
  ```csharp
  delegate void PrintDelegate(string message);

  void PrintMessage(string message)
  {
      Console.WriteLine(message);
  }

  PrintDelegate del = PrintMessage;
  del("Hello, Delegate!");
  ```

- **Events**
  ```csharp
  class Publisher
  {
      public event EventHandler OnChange;

      protected virtual void RaiseEvent()
      {
          OnChange?.Invoke(this, EventArgs.Empty);
      }
  }
  ```

- **Async and Await**
  ```csharp
  async Task<int> FetchDataAsync()
  {
      await Task.Delay(1000); // Simulate async operation
      return 42;
  }

  async void Main()
  {
      int result = await FetchDataAsync();
      Console.WriteLine(result);
  }
  ```

### **8. Attributes and Reflection**

- **Custom Attribute**
  ```csharp
  [AttributeUsage(AttributeTargets.Class | AttributeTargets.Method)]
  public class CustomAttribute : Attribute
  {
      public string Description { get; }
      public CustomAttribute(string description) => Description = description;
  }
  ```

- **Reflection**
  ```csharp
  using System.Reflection;

  Type type = typeof(Person);
  PropertyInfo[] properties = type.GetProperties();
  ```

### **9. Dependency Injection**

- **Basic Dependency Injection**
  ```csharp
  public interface IService
  {
      void Execute();
  }

  public class Service : IService
  {
      public void Execute() { Console.WriteLine("Service Executed"); }
  }

  public class Consumer
  {
      private readonly IService _service;

      public Consumer(IService service) => _service = service;

      public void Run() => _service.Execute();
  }
  ```

- **Using .NET Core Dependency Injection**
  ```csharp
  // In Startup.cs
  public void ConfigureServices(IServiceCollection services)
  {
      services.AddTransient<IService, Service>();
  }
  ```

### **10. Best Practices**

- **Code Formatting and Conventions**
  - Use PascalCase for class names and method names.
  - Use camelCase for method parameters and local variables.
  - Place each class in its own file.

- **Documentation**
  ```csharp
  /// <summary>
  /// Represents a person.
  /// </summary>
  public class Person
  {
      /// <summary>
      /// Gets or sets the name of the person.
      /// </summary>
      public string Name { get; set; }
  }
  ```

- **Error Handling**
  ```csharp
  // Always handle exceptions gracefully
  try
  {
      // Code that may throw exceptions
  }
  catch (Exception ex)
  {
      // Log the exception
      Console.WriteLine(ex.Message);
  }
  ```

---

This cheat sheet provides an extensive overview of C# programming, including both basic and advanced topics. Use it as a reference to strengthen your C# skills!