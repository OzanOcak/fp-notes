###  - Intro to C#

System username for calling Console, static main because its lifetime will be same as the thread
and it will be internal linked which means cant accessable outside files, and it is stored in static area(not stack or heap)

```csharp
using System;

public class HelloWorld
{
    public static void Main(string[] args)
    {
        Console.WriteLine("Hello, World!");
    }
}
```



### - Reading and Writing to Console

```csharp
Console.WriteLine("What's your name?");
string name = Console.ReadLine();
Console.WriteLine($"Hello, {name}!");

int num = 42;
double pi = 3.14159;
Console.WriteLine($"Number: {num:D4}, Pi: {pi:F2}");
```
### - Data type conversion

```csharp
int i = 42;
long l = i; // Implicit conversion from int to long
float f = i; // Implicit conversion from int to float
```

```csharp
double d = 3.14;
int i = (int)d; // Explicit conversion from double to int

int i = 42;
long l = (long)i; // Explicit conversion from int to long
float f = (float)i; // Explicit conversion from int to float
double d = (double)i; // Explicit conversion from int to double

char c = 'A';
int i = (int)c; // Explicit conversion from char to int (ASCII value of 'A' is 65)
char c2 = (char)65; // Explicit conversion from int to char ('A')
```

String Conversion

```csharp
char c = 'A';
int i = (int)c; // Explicit conversion from char to int (ASCII value of 'A' is 65)
char c2 = (char)65; // Explicit conversion from int to char ('A')
```

### - Arrays 

```csharp
int[] numbers;
string[] names;

int[] numbers = { 1, 2, 3, 4, 5 };
string[] names = { "John", "Jane", "Bob" };

int[] numbers = new int[5];
string[] names = new string[3];


Console.WriteLine(numbers[2]); // Output: 3
```
Arrays in C# have several useful properties and methods:

Length: Returns the number of elements in the array.
Array.Sort(): Sorts the elements of the array in ascending order.
Array.Reverse(): Reverses the order of the elements in the array.
Array.Copy(): Creates a new array by copying the elements of an existing array.

### - Methods

```csharp
// calling a regular method needed to creat a new obj outta its class

Program p = new Program();
p.function();

// calling static method doesnt need to create an obj

Program.static_function(); // if it is i the same class static_function() is enough to call
```

```csharp

int sum= add(10,20);

//argument pass by value unless use a ref keyword

Calculate(10, 20, out total, out product);

public static void Calculate(int a,int b,out sum,int out product){
  sum=a+b;
  product= a* b;
}

// params keyword

Calculate(){params int[] Numbers}{
  int sum=0;
  foreach(int i in Numbers){
    sum+=i;
  }
  Console.Writeline(sum);
}

```
 
