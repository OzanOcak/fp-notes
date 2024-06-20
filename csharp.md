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

