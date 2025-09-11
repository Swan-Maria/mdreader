
## Inheritance

In C#, _inheritance_ is the process by which one class inherits the members of another class. The class that inherits is called a _subclass_ or _derived_ class. The other class is called a _superclass_, or a _base_ class.

When you define a class that inherits from another class, the derived class implicitly gains all the members of the base class, except for its constructors. The derived class can thereby reuse the code in the base class without having to re-implement it. In the derived class, you can add more members. In this manner, the derived class extends the functionality of the base class.
```csharp
class Foo();  
class Bar : Foo;
```

### override/virtual Keywords

In C#, a derived class (subclass) can modify the behavior of an inherited method. The method in the derived class must be labeled `override` and the method in the base class (superclass) must be labeled `virtual`.

The `virtual` and `override` keywords are useful for two reasons:

1. Since the compiler treats “regular” and virtual methods differently, they must be marked as such.
2. This avoids the “hiding” of inherited methods, which helps developers understand the intention of the code.
```csharp
class BaseClass  
{  
    public virtual void Method1()  
    {
        
        Console.WriteLine("Base - Method1");  
    }
}  
  
class DerivedClass : BaseClass  
{  
    public override void Method1()  
    {
        base.Method1();  
        Console.WriteLine("Derived - Method1");  
    }
}
```

## Polymorphism

In C#, references are polymorphic, meaning a variable of a base type can refer to an object of a derived class. This allows for flexibility in code, enabling methods to operate on base class references, regardless of the specific subclass type.

### is Operator

The `is` operator in C# checks if a reference can be cast to a specified type. It returns `True` if the conversion is possible and `False` otherwise.
```csharp
public class Animal 
{
  public void MakeSound()
  {
    Console.WriteLine("Animal makes a sound");
  }
}

public class Dog : Animal 
{
  public void MakeSound()
  {
    Console.WriteLine("Dog barks");
  }
}

public class Program
{
  public static void Main(string[] args)
  {
    Dog myDog = new Dog();
    Console.WriteLine(myDog is Animal); // Outputs True
  }
}
```

### as Operator

The `as` operator in C# attempts to downcast a reference to a specified type. If the downcast fails, it returns `null` instead of throwing an exception.
```csharp
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
    
    public void Move()
    {
      Console.WriteLine("Dog walks");
    }
  }

public class Program
{
    public static void Main(string[] args)
    {
      Animal myAnimal = new Dog();
      // myAnimal.Move(); // Not available
      Dog myDog = myAnimal as Dog;
      if (myDog != null) 
      {
        myDog.MakeSound(); // Output: Dog barks
        myDog.Move(); // Output: Dog walks
      }
    }
}
```

### Abstract Classes

An abstract class in C# cannot be instantiated and is meant to be a base class for other classes. It can contain both abstract methods (without implementation) and concrete methods (with implementation).
```csharp
abstract class Employee {
    public abstract void MakeHRRequest(); // Must be implemented by the derived class
    public void ClockIn() {
        Console.WriteLine("Employee clocks in.");
    }
}
```

### Abstract Methods

An abstract method in C# is declared within an abstract class and does not have an implementation. It must be overridden in any derived class that inherits from the abstract class.
```csharp
abstract class Employee {
    public abstract void MakeHRRequest();
}

class Manager : Employee {
    public override void MakeHRRequest() {
        Console.WriteLine("Manager makes an HR request.");
    }
}
```

## Interface

In C#, an _interface_ contains definitions for a group of related functionalities that a class can implement.

Interfaces are useful because they guarantee how a class behaves. This, along with the fact that a class can implement multiple interfaces, helps organize and modularize components of software.

It is best practice to start the name of an interface with “I”.
```csharp
interface IAwesomeService
{
    public int Value { get; }

    void DoWork();
}

class AwesomeService : IAwesomeService
{
    public int Value { get; set; }

    public void DoWork()
    {
        Console.WriteLine("Working...");
    }
}
```

## Generics

In C#, generics enable the creation of classes, methods, and interfaces that can operate with any data type. They are defined with a type parameter and are instantiated with a specific data type.
Generic type parameters are specified using angle brackets (`<...>`). The type parameter goes after the name of the generic class, interface, or method.

### Generic Classes

Generic classes in C# ensure type safety by allowing developers to define the specific data types they operate on. This approach minimizes runtime errors and enhances code reusability. Generics serve as powerful tools for creating flexible and type-safe code structures, accommodating various data types while reducing redundancy.
```csharp
// Defining a generic class
class GenericClass<T>
{
	public T GetValue(T input) => input;
}

// Instantiating a generic class
GenericClass<int> x = new();
```

### Generic Methods in Non-Generic Classes

In C#, generic methods can be declared within non-generic classes. Because the method declares its own type parameters, it can be defined within any class, not just a generic class.
```csharp
// A non-generic class with generic methods.
class SerializeMe {
    public static string GetJson<T> (T input) {  /* serialization code goes here */ }; 
    public static T ReadJson<T> (string input) {  /* deserialization code goes here */ }; 
}
```

### Constraints

In C#, constraints are used to restrict the types that can be used as arguments for a generic type parameter. They are declared with the `where` keyword after specifying the type parameter: `class myClass<T> where T : constraints.`

| Constraint | Description                                                                                                                                                                                                                                                | Usage            |
| ---------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------- |
| class      | In C#, the `class` constraint specifies that the type argument must be a reference type, such as a class, interface, delegate or array type. Trying to insatiate the generic class, interface, or method with some other type will throw an exception.     | where T : class  |
| struct     | In C#, the `struct` constraint specifies that the type argument must be a value type, such as `bool`, `int`, or a `struct`. Trying to instantiate the generic class, interface, or method with some other type will cause an exception.                    | where T : struct |
| new()      | In C#, the `new()` constraint specifies that the type argument must have a parameterless constructor. If you attempt to instantiate the generic class, interface, or method with a type whose constructor requires parameters, it will throw an exception. | where T : new()  |
| Base Class | In C#, a base class constraint ensures that the type argument inherits from a specific base class. If you attempt to instantiate the generic class, interface, or method with a type not derived from the base class, it will throw an exception.          | where T : List   |
| Interface  | In C#, an interface constraint ensures that the type argument implements a specific interface. If you try to instantiate the generic class, interface, or method with a type that is not derived from the interface, it will throw an exception.           | where T : IList  |

### Multiple Constraint Limitations

In C# when using multiple type constraints there are some limitations:

- `struct` and `class` constraints must be first.
- `new()` must be last.
- Only one base class constraint is allowed.
- The `struct` and `new()` constraints can’t be combined.

### Generic Interfaces

In C#, generic interfaces define methods and properties that can operate on different data types. They are defined just like generic classes and use the type parameter for method return types and parameters. They can be implemented in a generic class or implemented in a non-generic class when the type parameter is specified.
```csharp
// Define a generic interface.
interface IGenericInterface<T> { 
  T ReturnValue(T value);
} 

// Implemented in a generic class.
class MyGenericClass<T> :  IGenericInterface<T> { 
  T ReturnValue(T value) => value;
} 

// Implemented in a non-generic class
class MyNonGenericClass : IGenericInterface<int> { 
  int ReturnValue(int value) => value;
} 
```

## Exceptions

Exceptions are events that occur during the execution of a program, disrupting the normal flow of instructions.
```csharp
int a = 1;
int b = 0;
int c = a/b; // This line produces a System.DivideByZeroException.
int d = c;   // This line is never executed.
```


### Common Exceptions

In C#, some common system-defined exceptions include `NullReferenceException`, `IndexOutOfRangeException`, `InvalidOperationException`, `ArgumentException`, `IOException`, and `FormatException`.

- `NullReferenceException`: Occurs when trying to use a null object reference.
- `IndexOutOfRangeException`: Occurs when accessing an array element with an invalid index.
- `InvalidOperationException`: Occurs when a method call is invalid for the object’s current state.
- `ArgumentException`: Occurs when a method is called with an invalid argument.
- `IOException`: Occurs when there’s an error accessing a stream, file, or directory.
- `FormatException`: Occurs when the format of an argument is invalid.

### Custom Exceptions

In C#, system-defined exceptions are pre-defined by the .NET framework, while application-defined exceptions are custom exceptions created by developers.
```csharp
// Here we define a custom exception
public class InvalidAgeException : Exception
{
  public InvalidAgeException(string message) : base(message)
  {
  }
}
```

### Throwing Exceptions

In C#, the throw keyword allows developers to explicitly generate exceptions in their code, enabling them to signal specific error conditions and validate method arguments, thus contributing to more robust and maintainable applications.
```csharp
if (age < 0)
{
  throw new ArgumentException("Age cannot be negative.");
}
```

### Try…Catch…Finally

In C#, `try`, `catch`, and `finally` blocks are used to test code for exceptions and handle them if necessary.
```csharp
int numerator = 10;
int denominator = 0;
int result = numerator / denominator;

try // We catch any exception in this block.
{
    int numerator = 10;
    int denominator = 0;
    int result = numerator / denominator;
}
catch (Exception ex) // This block runs if there is an exception.
{
    Console.WriteLine("An exception occurred.");
}
finally // This block always runs after the prior two blocks.
{
    Console.WriteLine("This message is always printed, even if an exception occurs.");
}
```

## C# Nullable Types

In C#, nullable value types are declared using the `?` syntax.
```csharp
// Define a nullable int value type
int? optionalValue = null;
```

### Null-Conditional Operators

In C#, null-conditional operators (`?.` and `?[]`) safely access members of objects that might be `null` for both nullable value types and reference types.
```csharp
// Using the ? null-conditional operator returns null if the refrence is null
string? message = null;
int? incorrectLength = message.Length; // Throws NullReferenceException

// Using ? null-conditional operator safely returns null
int? correctLength = message?.Length; // Returns null
```

### Null-Forgiving Operator

In C#, the null-forgiving operator (`!`) suppresses warnings when the developer knows a value is not `null` for both nullable value types and reference types.
```csharp
// The ! tells the compiler that we know the value is not going to be null, suppressing a warning
string? possiblyNull = GetResult();
Console.WriteLine(possiblyNull!.Length); // No warning will occur since ! is used
```

### Null-Coalescing Operator

In C#, the null-coalescing operator (`??`) provides default values for nullable types.
```csharp
int? a = null;

int? b = a ?? 3; // b is equal to 3 because a is null

a = 5;
b = a ?? 3; // b is now equal to 5
```

## Delegates

A delegate in C# is a type that references a method. Use `delegate` to encapsulate a method signature for a specific parameter list and return type. This allows methods to be passed as parameters.
```csharp
public delegate void MessageDelegate(string message);

public void ShowMessage(string msg) {
    Console.WriteLine(msg);
}

// Usage
MessageDelegate del = ShowMessage;
del("Hello, World!");
```

In C#, the `Action` and `Func` types are built-in delegates for defining common method signatures in a simplified manner. `Action` is used for methods without a return value, while `Func` is for methods with a return value.
```csharp
// Action delegate example
Action printHello = () => Console.WriteLine("Hello, World!");
printHello();

// Func delegate example
Func<int, int, int> add = (a, b) => a + b;
int result = add(5, 3);
Console.WriteLine(result);
```

Delegates can invoke multiple methods in sequence, known as multicast delegation. This feature is beneficial when you need several actions triggered by a single event, improving modular code design.
```csharp
// Define a delegate type
public delegate void Notify();

static void Main()
{
    // Instantiate the delegate
    Notify notifyAll = Alert1;
    notifyAll += Alert2;  // Multicast: Add another method
    // Invokes both Alert1 and Alert2
    notifyAll();
}
static void Alert1()
{
    Console.WriteLine("Alert 1 called!");
}
static void Alert2()
{
    Console.WriteLine("Alert 2 called!");
}
```

## Events

In C#, use the `event` keyword to declare events. An event is associated with a delegate type, allowing multiple methods to be called when the event is triggered. You can also specify access modifiers to control the event visibility, enhancing encapsulation.
```csharp
using System;

public class Car
{
    // Declare the event using a delegate type
    public event EventHandler EngineStarted;

    public void StartEngine()
    {
        Console.WriteLine("Engine started.");
        // Trigger the event
        EngineStarted?.Invoke(this, EventArgs.Empty);
    }
}

class Program
{
    static void Main()
    {
        Car car = new Car();
        car.EngineStarted += (sender, e) => Console.WriteLine("Listener: The engine has been started!");
        car.StartEngine();
    }
}
```

### EventHandler Pattern

The `EventHandler` delegate pattern in C# requires methods to include two specific parameters: `object sender` for the event source and `EventArgs e` for event data. This pattern standardizes how events are handled in applications, promoting consistency across event handling logic.

### Event Handlers

C# leverages `EventHandler<T>` to handle events with specific data types, ensuring compile-time type safety. This method allows developers to prevent runtime errors by enforcing type consistency at compile time. In the snippet, note how `MyEventArgs` enforces type safety for our event data.
```csharp
// Define event data class
public class MyEventArgs : EventArgs {
   public string Message { get; set; }
}

// Define a class with an event
public class Publisher {
   public event EventHandler<MyEventArgs> OnDataReceived;

   public void RaiseEvent(string message) {
       OnDataReceived?.Invoke(this, new MyEventArgs { Message = message });
   }
}

// Subscriber class
public class Subscriber {
   public void OnDataReceived(object sender, MyEventArgs e) {
       Console.WriteLine($"Received message: {e.Message}");
   }
}

// Usage Example
var publisher = new Publisher();
var subscriber = new Subscriber();

publisher.OnDataReceived += subscriber.OnDataReceived;
publisher.RaiseEvent("Hello, EventHandling!");
```

You use the `+=` operator to subscribe and the `-=` operator to unsubscribe an event handler to an event. This allows your program to respond dynamically to events, like button clicks or data changes.
```csharp
using System;

public class EventExample
{
    public event EventHandler ButtonClicked;

    public void ClickButton()
    {
        if (ButtonClicked != null)
            ButtonClicked(this, EventArgs.Empty);
    }

    public static void Main(string[] args)
    {
        EventExample example = new EventExample();

        // Subscribe to the event
        example.ButtonClicked += Example_ButtonClicked;

        // Trigger the event
        example.ClickButton();

        // Unsubscribe from the event
        example.ButtonClicked -= Example_ButtonClicked;
    }

    private static void Example_ButtonClicked(object sender, EventArgs e)
    {
        Console.WriteLine("Button was clicked!");
    }
}
```

## Asynchronous Programming

Asynchronous programming in C# allows your application to execute tasks without blocking the main thread. This enhances responsiveness and optimizes resource usage. By using keywords like `async` and `await`, functions can run independently of the main execution flow, improving performance.

### Task

The `Task<T>` represents an asynchronous operation in C# that returns a value of type `T`. It allows you to run tasks concurrently, handle task results, and catch exceptions efficiently. This enhances application responsiveness.

### Await Keyword

The `await` keyword in C# allows you to work with asynchronous methods efficiently. This keyword supports non-blocking task completion, improving application performance by not holding the executing thread.

### Async Methods

Asynchronous methods in C# are defined using the `async` keyword, allowing non-blocking code execution. They return a `Task` or `Task<T>` for handling asynchronous operations.
```csharp
public async Task<string> FetchDataAsync()
{
    // Simulate an asynchronous operation
    await Task.Delay(1000);
    return "Data fetched successfully!";
}
```

### CancellationToken Usage

The `CancellationToken` in C# allows for cancelling asynchronous tasks gracefully. It is often passed to tasks or operations that support cancellation, enabling them to check for termination requests and return early if needed, ensuring resource efficiency and responsive applications.
```csharp
using System;
using System.Threading;
using System.Threading.Tasks;

class Program {
    static async Task Main(string[] args) {
        using var cts = new CancellationTokenSource();

        // Simulate user cancellation after 2 seconds
        Task.Run(() => {
            Thread.Sleep(2000);
            cts.Cancel();
        });

        Console.WriteLine("Task starting...");
        try {
            await RunTaskAsync(cts.Token);
        } catch (OperationCanceledException) {
            Console.WriteLine("Task cancelled.");
        }
    }

    static async Task RunTaskAsync(CancellationToken token) {
        for (int i = 0; i < 5; i++) {
            token.ThrowIfCancellationRequested();
            await Task.Delay(1000); // Simulate work
            Console.WriteLine($"Iteration {i+1} complete.");
        }
    }
}
```

### Async Coordination

In C#, manage concurrent operations using `Task.WhenAll()` and `Task.WhenAny()`. These methods allow running multiple operations parallelly and syncing their outcomes effectively.
```csharp
// Example of using Task.WhenAll
async Task PerformTasksConcurrentlyAsync() {
    var task1 = Task.Delay(2000);
    var task2 = Task.Delay(1000);

    await Task.WhenAll(task1, task2);
    Console.WriteLine("Both tasks have completed.");
}

// Example of using Task.WhenAny
async Task PerformAnyTaskCompletionAsync() {
    var task1 = Task.Delay(2000);
    var task2 = Task.Delay(1000);

    var firstCompletedTask = await Task.WhenAny(task1, task2);
    Console.WriteLine("A task has completed first.");
}
```