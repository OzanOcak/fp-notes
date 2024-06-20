### Intro to C#

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



### Reading and Writing to Console

```csharp
Console.WriteLine("What's your name?");
string name = Console.ReadLine();
Console.WriteLine($"Hello, {name}!");

int num = 42;
double pi = 3.14159;
Console.WriteLine($"Number: {num:D4}, Pi: {pi:F2}");
```
