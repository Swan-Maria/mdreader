## Types

|                   | Value Types                                                                                                    | Reference Types                                                                                                                                                      |
| ----------------- | -------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Storage Location  | Stored directly in the stack.                                                                                  | A reference (memory address) is stored in the stack, while the actual data is stored in the heap.                                                                    |
| Assignment        | A new copy of the data is created. Changes to one variable do not affect the other.                            | The reference (memory address) is copied. Both variables point to the same data in the heap. Changes to one variable affect the other.                               |
| Memory Management | Automatic (handled by the stack).                                                                              | Handled by the garbage collector (GC).                                                                                                                               |
| Examples          | `int`, `double`, `char`, `bool`, `struct`, `enum`.                                                             | `class`, `record` `string`, `object`                                                                                                                                 |
| Performance       | Generally faster for small objects because there is no overhead of the heap allocation and garbage collection. | Can be slower due to the overhead of heap allocation and garbage collection. However, they are more efficient for large objects as you are only copying a reference. |
| **Default Value** | The default value is zero or `null` for the corresponding type (e.g., `0` for `int`, `false` for `bool`).      | The default value is `null`.                                                                                                                                         |

## Variables

Variable is a named storage location that holds a value. It acts as a container for data that can be referenced and manipulated throughout a program.
Structure: type variableName = value;
Example:
```csharp
int x = 5;
string name = "Bob";
string num = 4; // type error, can't assign int to string
var character = 'a'; // here in compile time var transforms to char
```

## Operators

### Arithmetic Operators
```csharp
int result; 
result = 10 + 5;  // 15
result = 10 - 5;  // 5
result = 10 * 5;  // 50
result = 10 / 5;  // 2
result = 10 % 5;  // 0

int a = 0;
a++;    // a = 1 post-increment
++a;    // a = 1 pre-increment
int b = a++; // b = 0
int b = ++a; // b = 1
a += 1; // a = 2
a *= 7; // a = 14
a--;    // a = 13
--a;    // a = 13
a %= 7; // a = 6
```

### Logical Operators

Logical operators receive boolean expressions as input and return a boolean value.
The `&&` operator takes two boolean expressions and returns `true` only if they both evaluate to `true`.
The `||` operator takes two boolean expressions and returns `true` if either one evaluates to `true`.
The `!` operator takes one boolean expression and returns the opposite value.

```csharp
// These variables equal true.
bool a = true && true;
bool b = false || true;
bool c = !false;

// These variables equal false.
bool d = true && false;
bool e = false || false;
bool f = !true;
```

![[Pasted image 20250904215949.png]]

### Conditionals
#### If Statements

In C#, an _if statement_ executes a block of code based on whether or not the _boolean expression_ provided in the parentheses is `true` or `false`.

If the expression is `true` then the block of code inside the braces, `{}`, is executed. Otherwise, the block is skipped over.
```csharp
if (true) {
  // This code is executed.
  Console.WriteLine("Hello User!");
}

if (false) {
  // This code is skipped.
  Console.WriteLine("This won't be seen :(");
}
```

#### Else Clause

An `else` followed by braces, `{}`, containing a code block, is called an `else` clause. `else` clauses must always be preceded by an `if` statement.

The block inside the braces will only run if the expression in the accompanying `if` condition is `false`. It is useful for writing code that runs _only if_ the code inside the `if` statement is not executed.
```csharp
if (true) {
  // This block will run.
  Console.WriteLine("Seen!");
} else {
  // This will not run.
  Console.WriteLine("Not seen!");
}

if (false) {
  // Conversely, this will not run.
  Console.WriteLine("Not seen!");
} else {
  // Instead, this will run.
  Console.WriteLine("Seen!");
}
```

#### If and Else If

A common pattern when writing multiple `if` and `else` statements is to have an `else` block that contains another nested `if` statement, which can contain another `else`, etc. A better way to express this pattern in C# is with `else if` statements. The first condition that evaluates to `true` will run its associated code block. If none are `true`, then the optional `else` block will run if it exists.
```csharp
int x = 100, y = 80;
 
if (x > y)
{
  Console.WriteLine("x is greater than y");
} 
else if (x < y) 
{
  Console.WriteLine("x is less than y");
} 
else
{
  Console.WriteLine("x is equal to y");
}
```

#### Switch Statements

A `switch` statement is a control flow structure that evaluates one expression and decides which code block to run by trying to match the result of the expression to each `case`. In general, a code block is executed when the value given for a `case` equals the evaluated expression, i.e, when `==` between the two values returns `true`. `switch` statements are often used to replace `if else` structures when all conditions test for equality on one value.
```csharp
// The expression to match goes in parentheses.
switch (fruit) {
  case "Banana":
    // If fruit == "Banana", this block will run.
    Console.WriteLine("Peel first.");
    break;
  case "Durian":
    Console.WriteLine("Strong smell.");
    break;
  default:
    // The default block will catch expressions that did not match any above.
    Console.WriteLine("Nothing to say.");
    break;
}

// The switch statement above is equivalent to this:
if (fruit == "Banana") {
  Console.WriteLine("Peel first.");
} else if (fruit == "Durian") {
  Console.WriteLine("Strong smell.");  
} else {
  Console.WriteLine("Nothing to say.");
}
```

#### Ternary Operator

In C#, the _ternary operator_ is a special syntax of the form: `condition ? expression1 : expression2`.

It takes one boolean condition and two expressions as inputs. Unlike an `if` statement, the _ternary operator_ is an expression itself. It evaluates to either its first input expression or its second input expression depending on whether the condition is `true` or `false`, respectively.
```csharp
bool isRaining = true;
// This sets umbrellaOrNot to "Umbrella" if isRaining is true,
// and "No Umbrella" if isRaining is false.
string umbrellaOrNot = isRaining ? "Umbrella" : "No Umbrella";

// "Umbrella"
Console.WriteLine(umbrellaOrNot);
```

## C# Arrays

In C#, an _array_ is a structure representing a fixed length ordered collection of values or objects with the same type.

Arrays make it easier to organize and operate on large amounts of data. For example, rather than creating 100 integer variables, you can just create one array that stores all those integers!
```csharp
// `numbers` array that stores integers
int[] numbers = { 3, 14, 59 };

// 'characters' array that stores strings
string[] characters = new string[] { "Huey", "Dewey", "Louie" };
```

#### Declaring Arrays

A C# array variable is declared similarly to a non-array variable, with the addition of square brackets (`[]`) after the type specifier to denote it as an array.

The `new` keyword is needed when instantiating a new array to assign to the variable, as well as the array length in the square brackets. The array can also be instantiated with values using curly braces (`{}`). In this case the array length is not necessary.
```csharp
// Declare an array of length 8 without setting the values.
string[] stringArray = new string[8];

// Declare array and set its values to 3, 4, 5.
int[] intArray = new int[] { 3, 4, 5 };
```

#### Declare and Initialize array

In C#, one way an array can be declared and initialized at the same time is by assigning the newly declared array to a comma separated list of the values surrounded by curly braces (`{}`). Note how we can omit the type signature and `new` keyword on the right side of the assignment using this syntax. This is only possible during the array’s declaration.
```csharp
// `numbers` and `animals` are both declared and initialized with values.
int[] numbers = { 1, 3, -10, 5, 8 };
string[] animals = { "shark", "bear", "dog", "raccoon" };

// since .NET 8 also possible this
int[] numbers = [ 1, 3, -10, 5, 8 ];
string[] animals = ["shark", "bear", "dog", "raccoon"];
```

#### Array Element Access

In C#, the elements of an array are labeled incrementally, starting at 0 for the first element. For example, the 3rd element of an array would be indexed at 2, and the 6th element of an array would be indexed at 5.

A specific element can be accessed by using the square bracket operator, surrounding the index with square brackets. Once accessed, the element can be used in an expression, or modified like a regular variable.
```csharp
// Initialize an array with 6 values.
int[] numbers = { 3, 14, 59, 26, 53, 0 };

// Assign the last element, the 6th number in the array (currently 0), to 58.
numbers[5] = 58;

// Store the first element, 3, in the variable `first`.
int first = numbers[0];
```

#### C# Array Length

The _Length_ property of a C# array can be used to get the number of elements in a particular array.
```csharp
int[] someArray = { 3, 4, 1, 6 };
Console.WriteLine(someArray.Length); // Prints 4

string[] otherArray = { "foo", "bar", "baz" };
Console.WriteLine(otherArray.Length); // Prints 3
```

## Loops

### For Loop

A C# _for loop_ executes a set of instructions for a specified number of times, based on three provided expressions. The three expressions are separated by semicolons, and in order they are:

- _Initializer_: This is run exactly once at the start of the loop, usually used to initialize the loop’s iterator variable.
- _Conditional expression_: This boolean expression is checked before each iteration to see if it should run.
- _Iteration expression_: This is executed after each iteration of the loop and is usually used to update the iterator variable.
```csharp
// This loop initializes i to 1, stops looping once i is greater than 10, and increases i by 1 after each iteration of the loop
for (int i = 1; i <= 10; i++) {
  Console.WriteLine(i); 
}

Console.WriteLine("Ready or not, here I come!");
```

### For Each Loop

A C# `foreach` loop runs a set of instructions once for each element in a given collection. For example, if an array has 200 elements, then the `foreach` loop’s body will execute 200 times. At the start of each iteration, a variable is initialized to the current element being processed.

A _for each_ loop is declared with the `foreach` keyword. Next, in parentheses, a _variable type_ and _variable name_ are followed by the `in` keyword and the collection to iterate over.
```csharp
string[] states = { "Alabama", "Alaska", "Arizona", "Arkansas", "California", "Colorado" };

foreach (string state in states) {
  // The `state` variable takes on the value of an element in `states` and updates every iteration.
  Console.WriteLine(state);
}
// Will print each element of `states` in the order they appear in the array. 
```

### While Loop

In C#, a _while loop_ executes a set of instructions continuously, as long as the given Boolean expression evaluates to `true`.

Note that the loop body might not run at all — since the Boolean condition is evaluated before every iteration of the _while loop_, including the very first, the loop will not execute if the conditional expression evaluates to `false` on the first pass.

The syntax to declare a while loop is simply the `while` keyword followed by a Boolean condition in parentheses.
```csharp
string guess = "";
Console.WriteLine("What animal am I thinking of?");

// This loop will keep prompting the user, until they type in "dog".
while (guess != "dog") {
  Console.WriteLine("Make a guess: ");
  guess = Console.ReadLine().ToLower();
}

Console.WriteLine("That's right!");
```

### Do While Loop

In C#, a _do…while_ loop runs a set of instructions once and then continues running as long as the given boolean condition is `true`. Notice how this behavior is nearly identical to a _while_ loop, with the distinction that a _do while_ runs one or more times, whereas a _while_ loop runs zero or more times.

The syntax to declare a _do while_ is the `do` keyword, followed by the code block, then the `while` keyword with the Boolean condition in parentheses. Note that a semi-colon is required to end a _do…while_ loop.
```csharp
do
{
  Console.WriteLine("This will always run at least once, even if boolCondition is false to begin with.");
} while(boolCondition);

// whereas the do...while loop will always run at least once, a while loop may not run at all if its conditional expression is false to begin with
while(boolCondition)
{
  Console.WriteLine("If boolCondition is false to begin with, this code will not run at all.");
}
```

### Jump Statements

_Jump statements_ are tools used to give the programmer additional control over the program’s control flow. They are very commonly used in the context of loops to exit from the loop early or skip parts of the loop’s body.

Common control flow keywords include `break` and `continue`. The given code snippets provide examples of their usage.
```csharp
while (true) {
  Console.WriteLine("This prints once.");
  // A `break` statement immediately terminates the loop that contains it.
  break;
}

for (int i = 1; i <= 10; i++) {
  // This prints every number from 1 through 10, except for 7.
  if (i == 7) {
    // A `continue` statement skips the rest of the loop and starts another iteration from the start.
    continue;
  }
  Console.WriteLine(i);
}
```

## Lists in C\#

In C#, a _list_ is a generic data structure that can hold any type. Use the `new` operator and declare the element type in the angle brackets `< >`.

In the example code, `names` is a list containing `string` values. `someObjects` is a list containing `Object` instances.
```csharp
List<string> names = new List<string>();
List<Object> someObjects = new List<Object>();
```

### Object Initialization

Values can be provided to a `List` when it is constructed in a process called _object initialization_.
Instead of parentheses, use curly braces after the list’s type.
Note that this can ONLY be used at the time of construction.
```csharp
List<string> cities = new List<string> { "Los Angeles", "New York City", "Dubai" };
```

### Limitless Lists

Unlike a C# array, a C# list does not have a limited number of elements. You can add as many items as you like.
```csharp
// Initialize array with length 2
string[] citiesArray = new string[2];
citiesArray[0] = "Los Angeles";
citiesArray[1] = "New York City";
citiesArray[2] = "Dubai"; // Error!

// Initialize list; no length needed
List<string> citiesList = new List<string>();
citiesList.Add("Los Angeles");
citiesList.Add("New York City");
citiesList.Add("Dubai");
```

### Count Property

The number of elements in a list is stored in the `Count` property.
In the example code, the `Count` of `citiesList` changes as we add and remove values.
```csharp
List<string> citiesList = new List<string>();
citiesList.Add("Los Angeles");
Console.WriteLine(citiesList.Count);
// Output: 1

citiesList.Add("New York City");
Console.WriteLine(citiesList.Count);
// Output: 2

citiesList.Remove("Los Angeles");
Console.WriteLine(citiesList.Count);
// Output: 1
```

### Remove()

Elements of a list can be removed with the `Remove()` method. The method returns `true` if the item is successfully removed; otherwise, `false`.

In the example code, attempting to remove `"Cairo"` returns `false` because that element is not in the `citiesList`.
```csharp
List<string> citiesList = new List<string>();
citiesList.Add("Los Angeles");
citiesList.Add("New York City");
citiesList.Add("Dubai");

result1 = citiesList.Remove("New York City");
// result1 is true

result2 = citiesList.Remove("Cairo");
// result2 is false
```

### Clear()

All elements of a list can be removed with the `Clear()` method. It returns nothing.

In the example code, the list is initialized with three items. After calling `Clear()`, there are zero items in the list.
```csharp
List<string> citiesList = new List<string> { "Delhi", "Los Angeles", "Kiev" };
citiesList.Clear();

Console.WriteLine(citiesList.Count);
// Output: 0
```

### Contains()

In C#, the list method `Contains()` returns `true` if its argument exists in the list; otherwise, `false`

In the example code, the first call to `Contains()` returns `true` because “New York City” is in the list. The second call returns `false` because “Cairo” is not in the list.
```csharp
List<string> citiesList = new List<string> { "Los Angeles", "New York City", "Dubai" };

result1 = citiesList.Contains("New York City");
// result1 is true

result2 = citiesList.Contains("Cairo");
// result2 is false
```

### List Ranges

Unlike elements in a C# array, multiple elements of a C# list can be accessed, added, or removed simultaneously. A group of multiple, sequential elements within a list is called a range.

Some common range-related methods are:
- `AddRange()`
- `InsertRange()`
- `RemoveRange()`

```csharp
string[] african = new string[] { "Cairo", "Johannesburg" };
string[] asian = new string[] { "Delhi", "Seoul" };
List<string> citiesList = new List<string>();

// Add two cities to the list
citiesList.AddRange(african);
// List: "Cairo", "Johannesburg"

// Add two cities to the front of the list
citiesList.InsertRange(0, asian);
// List: "Delhi", "Seoul", "Cairo", "Johannesburg"

// Remove the second and third cities from the list
citiesList.RemoveRange(1, 2);
// List: "Delhi", "Johannesburg"
```

### List Indexing

In C#, elements in a list can be accessed and modified using zero-based indexing, similar to arrays. The indexer syntax, `list[index]` is used to get or set the value at a specific position in the list.
```csharp

List<string> citiesList = new List<string>();
citiesList.Add("Delhi");

// indexing can be used to access and reassign elements
string city = citiesList[0];
citiesList[0] = "New Delhi";
```

## Methods

### What is a Method?

In C#, a **method** is a reusable set of instructions that performs a specific task. Methods can be passed one or more values as _inputs_ and can _output_ one or more values at the end of their execution.

### Method Declaration

In C#, a _method declaration_, also known as a _method header_, includes everything about the method other than the method’s body. The method declaration includes:

- modifiers
- return type
- method name
- input parameters

### Return Keyword

In C#, the `return` statement can be used to return a value from a method back to the method’s caller.

When `return` is invoked, the current method terminates and control is returned to where the method was originally called. The value that is returned by the method must match the method’s _return type_, which is specified in the _method declaration_.
```csharp
static int ReturnAValue(int x)
{
  // We return the result of computing x * 10 back to the caller.
  // Notice how we are returning an int, which matches the method's return type.
  return x * 10;
}

static void Main()
{
  // We can use the returned value any way we want, such as storing it in a variable.
  int num = ReturnAValue(5);
  // Prints 50 to the console.
  Console.WriteLine(num);
}
```

### `Main()` method

In C#, the `Main()` method is the application’s entry point. When the application is run, execution begins at the start of the `Main()` method.

### Method Overloading

In C#, multiple methods can have the same name, as long as they each have a different method signature. A method’s **signature** comprises its name, parameter types, and parameter order. Defining multiple methods with the same name is called **method overloading**.
```csharp
// MultiplyValues has 2 overloads that accept different numbers of parameters
static int MultiplyValues(int a, int b)
{
  return a * b;
}

static int MultiplyValues(int a, int b, int c)
{
  return a * b * c;
}

static void Main(string[] args)
{
  MultiplyValues(2, 3); // Returns 6
  MultiplyValues(2, 3, 4); // Returns 24
}
```

### Variables Inside Methods

Parameters and variables declared inside of a method cannot be used outside of the method’s body. Attempting to do so will cause an error when compiling the program!
```csharp
static void DeclareAndPrintVars(int x)
{
  int y = 3;
  // Using x and y inside the method is fine.
  Console.WriteLine(x + y);
}

static void Main() 
{
  DeclareAndPrintVars(5);
  
  // x and y only exist inside the body of DeclareAndPrintVars, so we cannot use them here.
  Console.WriteLine(x * y);
}
```

### Optional Parameters

In C#, methods can be given _optional parameters_. A parameter is optional if its declaration specifies a _default argument_. Methods with an _optional parameter_ can be called with or without passing in an argument for that parameter. If a method is called without passing in an argument for the _optional parameter_, then the parameter is initialized with its default value.

To define an _optional parameter_, use an equals sign after the parameter declaration followed by its default value.
```csharp
// y and z are optional parameters.
static int AddSomeNumbers(int x, int y = 3, int z = 2)
{
  return x + y + z;
}

// Any of the following are valid method calls.
AddSomeNumbers(1); // Returns 6.
AddSomeNumbers(1, 1); // Returns 4.
AddSomeNumbers(3, 3, 3); // Returns 9.
```

### Positional vs Named Arguments

In C#, an argument passed to a method may be identified by position or name.

**Positional arguments** are values passed directly to the method call in the same order as the defined parameters. **Named arguments** are values passed to the method call along with the name of the parameter they should be assigned to, irrespective of the order in which the parameters are defined. An argument can be named by using the parameter name followed by a colon (:), and then the argument value.

Positional and named arguments may be used within the same method call, but all positional arguments must precede all named arguments.
```csharp
static void CalculateMean(double sumOfValues, double numberOfValues = 10)
{
  double result = sumOfValues / numberOfValues;
  Console.WriteLine(result);
}

static void Main(string[] args)
{
  // sumOfValues is passed positionally and numberOfValues is passed by name
  CalculateMean(50, numberOfValues: 20);
  // Prints 2.5

  // both arguments are passed by name
  CalculateMean(numberOfValues: 4, sumOfValues: 21);
  // Prints 5.25
}
```

### Void Return Type

In C#, methods that do not `return` a value have a `void` return type.
`void` is not an actual data type like `int` or `string`, as it represents the lack of an output or value.
```csharp
// This method has no return value
static void DoesNotReturn()
{
  Console.WriteLine("Hi, I don't return like a bad library borrower.");
}
// This method returns an int
static int ReturnsAnInt()
{
  return 2 + 3;
}
```

### Out Parameters

`return` can only return one value. When multiple values are needed, `out` parameters can be used.

`out` parameters are prefixed with `out` in the method header. When called, the argument for each `out` parameter must be a _variable_ prefixed with `out`.

The `out` parameters become aliases for the variables that were passed in. So, we can assign values to the parameters, and they will persist on the variables we passed in after the method terminates.
```csharp
// f1, f2, and f3 are out parameters, so they must be prefixed with `out`.
static void GetFavoriteFoods(out string f1, out string f2, out string f3)
{
  // Notice how we are assigning values to the parameters instead of using `return`.
  f1 = "Sushi";
  f2 = "Pizza";
  f3 = "Hamburgers";
}

static void Main()
{
  string food1;
  string food2;
  string food3;
  // Variables passed to out parameters must also be prefixed with `out`.
  GetFavoriteFoods(out food1, out food2, out food3);
  // After the method call, food1 = "Sushi", food2 = "Pizza", and food3 = "Hamburgers".
  Console.WriteLine($"My top 3 favorite foods are {food1}, {food2}, and {food3}");
}
```

## Classes

In C#, _classes_ are used to create custom types. The class defines the kinds of information and methods included in a custom type.

### C# Constructor

In C#, whenever an instance of a class is created, its _constructor_ is called. It must have the same name as the enclosing class. Like other methods, a constructor can be overloaded. This is useful when you may want to define an additional constructor that takes a different number of arguments.
```csharp
// Takes two arguments
public Forest(int area, string country)
{ 
  this.area = area;
  this.country = country;
}

// Takes one argument
public Forest(int area)
{ 
  this.area = area;
  this.country = "Unknown";
}


// Typically, a constructor is used to set initial values and run any code needed to “set up” an instance.

// A constructor looks like a method, but it does not include a return type and it must have the same name as the enclosing type.
```

### Parameterless Constructor

In C#, if no constructors are specified in a class, the compiler automatically creates a parameterless constructor.
```csharp
public class Freshman
{
  public string firstName;
}

public static void Main (string[] args)
{
  Freshman f = new Freshman();
  // name is null
  string name = f.firstName;
}

// In this example, no constructor is defined in Freshman, but a parameterless constructor is still available for use in Main(). All fields will be set to a default value according to their type and remain unchanged until updated manually.
```

### Static Constructor

In C#, a _static constructor_ is run once per type, not per instance. It cannot take any parameters or be defined with an access modifier. A static constructor cannot be invoked directly — it is invoked automatically exactly once, before one of the following happens for the first time:

- an instance of the type is instantiated
- a static member of the type is accessed
```csharp
class Forest
{
  static Forest()
  { 
    Console.WriteLine("Type Initialized"); 
  }

  public static void Define()
  {
    Console.WriteLine("A forest is a large area where trees are the primary life-form.")
  }
}

// For this class, either of the following two lines would trigger the static constructor, but only the first time one of them occurs:
Forest f  = new Forest();
Forest.Define();
```

### Static Class

In C#, a _static class_ can only contain static members and cannot be instantiated. All of its members are accessed by the class name.

This is useful when you want a class that provides a set of tools, but doesn’t need to maintain any internal data.

`Math` is a commonly used, built-in static class.\
```csharp
Math.Min(23, 97);

Console.WriteLine("Let's Go!");
```

### Field

In C#, a _field_ stores a piece of data within an object. It acts like a variable and may have a different value for each instance of a type.
```csharp
public class Person
{
   public string firstName;
   public string lastName;
}

// In this example, firstName and lastName are fields of the Person class.
```

### Property

In C#, a _property_ is a member of an object that controls how one field may be accessed and modified.

A property defines two _accessor methods_:

- a `get()` method, which defines how its associated field can be accessed
- a `set()` method, which defines how the same field can be modified

Accessor methods default to `public` when no access modifier is specified.
```csharp
public class Freshman
{
  // FIELD
  private string firstName;

  // PROPERTY
  public string FirstName
  {
    get { return firstName; }
    set { firstName = value; }
  }
  
  public string LastName { get; set; }
}

public static void Main (string[] args) {
  Freshman f = new Freshman();
  f.FirstName = "Louie";
  
  Console.WriteLine(f.FirstName);
  // Prints "Louie"
}


```

### **this** Keyword

In C#, the `this` keyword refers to the current instance of a class.
```csharp
// We can use the this keyword to refer to the current class's members hidden by similar names:
public NationalPark(int area, string state)
{
  this.area = area;
  this.state = state;
}

// The code below requires duplicate code, which can lead to extra work and errors when changes are needed:
public NationalPark(int area, string state)
{
  area = area;
  state = state;
}
public NationalPark(int area)
{
  area = area;
  state = "Unknown";
}

// When "this" is used as a method 
// it instructs one constructor to call another
// the following achieves the same as the preceding 2 constructors
public NationalPark(int area) : this(are, "Unknown")
{ }
```

## Access Modifiers

In C#, members of a class can be marked with an _access modifier_, such as `public` or `private`. A `public` member can be accessed by any class. A `private` member can only be accessed by code within the same class it is defined.

By default, fields, properties, and methods are private, and classes are public.
```csharp
public class Speech
{
  private string greeting = "Greetings";

  // FormalGreeting() can access greeting since they are part of the same class
  private string FormalGreeting()
  {
    return $"{greeting} and salutations";
  }

  // Scream() can access FormalGreeting() since they are part of the same class
  public string Scream()
  {
    return FormalGreeting().ToUpper();
  }

}

public static void Main (string[] args)
{
  Speech s = new Speech();

  // greeting and FormalGreeting() are private, so they cannot be accessed outside the Speech class
  // string sg = s.greeting; // Error!
  // string sfg = s.FormalGreeting(); // Error!

  // Scream is public, so it can be accessed anywhere
  Console.WriteLine(s.Scream());
}
```
