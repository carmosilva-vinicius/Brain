To use .NET, we will need SDK and Runtimes installed. To verify .NET installation, execute:
`dotnet --version` 
or
`dotnet --info`
and
`dotnet --list-sdks`: List installed SDKs;
`dotnet --list-runtimes`: List installed runtimes.

# First C# Code 
With CLI installation checked, create a folder to our project and create a console project with: `dotnet new console` (or use Visual Studio IDE):

This is the result content opened in VSCode:

├── bin
├── obj
├── console-test.csproj
├── console-test.sln
└── Program.cs

- `bin`: Contains the binaries (DLLs) and other output files.
- `obj`: Stores temporary object files and other files used to compiling.
- `console-test.csproj`: Contains information about the project and its dependencies, and is used by MSBuild to compile your project. A XML that includes information such as the target framework, package references, project references, etc.
- `console-test.sln`: In Visual Studio, a solution is a structure for organizing projects. It contains the state information for projects in .NET.
- `Program.cs`: The main file of the application. Is the entry-point of app:
```cs
Console.WriteLine("Hello, World!");
```

Finally, we can see the result with: `dotnet run`.

### Syntax 
C# is one of C family syntax. Is similar to C, c++, Java and JavaScript.
- Every statement needs to end with `;`
- Functions and methods has `()`
- Blocks of codes uses `{}`

# Variables

This is used to store data in memory. Example:
```cs
var nome = "Vinícius";
var idade = 28;
```

## Types
But, and if I wish to input the value after the creation of variable. We will need to declare the type of the variables, because the `var`, don't allow it.

|C# type keyword|.NET type|
|---|---|
|[`bool`](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/builtin-types/bool)|[System.Boolean](https://learn.microsoft.com/en-us/dotnet/api/system.boolean)|
|[`byte`](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/builtin-types/integral-numeric-types)|[System.Byte](https://learn.microsoft.com/en-us/dotnet/api/system.byte)|
|[`sbyte`](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/builtin-types/integral-numeric-types)|[System.SByte](https://learn.microsoft.com/en-us/dotnet/api/system.sbyte)|
|[`char`](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/builtin-types/char)|[System.Char](https://learn.microsoft.com/en-us/dotnet/api/system.char)|
|[`decimal`](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/builtin-types/floating-point-numeric-types)|[System.Decimal](https://learn.microsoft.com/en-us/dotnet/api/system.decimal)|
|[`double`](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/builtin-types/floating-point-numeric-types)|[System.Double](https://learn.microsoft.com/en-us/dotnet/api/system.double)|
|[`float`](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/builtin-types/floating-point-numeric-types)|[System.Single](https://learn.microsoft.com/en-us/dotnet/api/system.single)|
|[`int`](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/builtin-types/integral-numeric-types)|[System.Int32](https://learn.microsoft.com/en-us/dotnet/api/system.int32)|
|[`uint`](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/builtin-types/integral-numeric-types)|[System.UInt32](https://learn.microsoft.com/en-us/dotnet/api/system.uint32)|
|[`nint`](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/builtin-types/integral-numeric-types)|[System.IntPtr](https://learn.microsoft.com/en-us/dotnet/api/system.intptr)|
|[`nuint`](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/builtin-types/integral-numeric-types)|[System.UIntPtr](https://learn.microsoft.com/en-us/dotnet/api/system.uintptr)|
|[`long`](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/builtin-types/integral-numeric-types)|[System.Int64](https://learn.microsoft.com/en-us/dotnet/api/system.int64)|
|[`ulong`](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/builtin-types/integral-numeric-types)|[System.UInt64](https://learn.microsoft.com/en-us/dotnet/api/system.uint64)|
|[`short`](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/builtin-types/integral-numeric-types)|[System.Int16](https://learn.microsoft.com/en-us/dotnet/api/system.int16)|
|[`ushort`](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/builtin-types/integral-numeric-types)|[System.UInt16](https://learn.microsoft.com/en-us/dotnet/api/system.uint16)|

### Boolean
Like binary (0 or 1), booleans can be `true` or `false`. Use to store things tha can have just two states:
```cs
bool programador;

programador = true;
```