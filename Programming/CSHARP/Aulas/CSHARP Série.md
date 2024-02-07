#classes
# O que é C#?
C# é uma linguagem de programação, desenvolvida pela Microsoft como parte da plataforma .NET.
## Ferramentas necessárias
- [Visual Studio Code](https://code.visualstudio.com/)
- [.NET Core SDK](https://dotnet.microsoft.com/download)
- [C# Dev Kit](https://marketplace.visualstudio.com/items?itemName=ms-dotnettools.csdevkit
- [Visual Studio](https://visualstudio.microsoft.com/pt-br/)
- [Rider](https://www.jetbrains.com/pt-br/rider/)
## Verificar instalação
```bash

dotnet --info

```
## Hello world
```bash

dotnet new console

```
#### Estrutura de diretórios
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
### Sintaxe
C-family: C, C++, C#, Java, JavaScript, etc.
{} blocos de código
() funções e métodos
[] arrays
; fim de instrução
"" strings
// comentários de linha
/* */ comentários de bloco
'' char
# Tipos de dados
Variáveis de [tipos de referência](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/reference-types) armazenam referências a seus dados (objetos), enquanto variáveis de [tipos de valor](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/builtin-types/value-types) contêm diretamente seus dados.

## Tipos de valores

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

## Tipos de referência
|C# type keyword|.NET type|
|---|---|
|[`object`](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/builtin-types/reference-types#the-object-type)|[System.Object](https://learn.microsoft.com/en-us/dotnet/api/system.object)|
|[`string`](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/builtin-types/reference-types#the-string-type)|[System.String](https://learn.microsoft.com/en-us/dotnet/api/system.string)|
|[`dynamic`](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/builtin-types/reference-types#the-dynamic-type)|[System.Object](https://learn.microsoft.com/en-us/dotnet/api/system.object)|

___

## Como usar:
### Var
```cs

//Var: tipo implícito

var v1 = 1;

var v2 = "string";

var v3 = true;

var v4 = 1.5f;

Console.WriteLine($"var1: {v1} var2: {v2} var3: {v3} var4: {v4}");

```

```cs

### Booleanos

//Boolean: 1 bit (True or False)

bool b1 = true;

bool b2 = false;

Console.WriteLine($"bool1: {b1} bool2: {b2}");

```

## Tipos de dados numéricos
### Inteiros
```cs
//Byte: 8 bits (256 valores)
byte b1 = 0;
byte b2 = 255;
Console.WriteLine($"byte1: {b1} byte2: {b2}");

//Sbyte: 8 bits (256 valores)
sbyte sb1 = -128;
sbyte sb2 = 127;
Console.WriteLine($"sbyte1: {sb1} sbyte2: {sb2}");

//Short: 16 bits (65.536 valores)
short s1 = -32768;
short s2 = 32767;
Console.WriteLine($"short1: {s1} short2: {s2}");

//Ushort: 16 bits (65.536 valores)
ushort us1 = 0;
ushort us2 = 65535;
Console.WriteLine($"ushort1: {us1} ushort2: {us2}");

//Int: 32 bits (4.294.967.296 valores)
int i1 = -2147483648;
int i2 = 2147483647;
Console.WriteLine($"int1: {i1} int2: {i2}");

//Uint: 32 bits (4.294.967.296 valores)
uint ui1 = 0;
uint ui2 = 4294967295;
Console.WriteLine($"uint1: {ui1} uint2: {ui2}");
```

### Ponto flutuante
```cs
//Long: 64 bits (18.446.744.073.709.551.616 valores)
long l1 = -9223372036854775808;
long l2 = 9223372036854775807;
Console.WriteLine($"long1: {l1} long2: {l2}");

//Ulong: 64 bits (18.446.744.073.709.551.616 valores)
ulong ul1 = 0;
ulong ul2 = 18446744073709551615;
Console.WriteLine($"ulong1: {ul1} ulong2: {ul2}");

//Float: 32 bits (1.5 x 10^-45 a 3.4 x 10^38)
float f1 = -3.402823e38f;
float f2 = 3.402823e38f;
Console.WriteLine($"float1: {f1} float2: {f2}");

Console.WriteLine($"The range of float is {float.MinValue} to {float.MaxValue}");
Console.WriteLine($"The range of double is {double.MinValue} to {double.MaxValue}");
Console.WriteLine($"The range of decimal is {decimal.MinValue} to {decimal.MaxValue}");
```

### Caracteres
```cs
//Char: 16 bits (0 a 65535)
char c1 = 'a';
char c2 = 'b';
Console.WriteLine($"char1: {c1} char2: {c2}");
```
### Strings
```cs
//String: sequência de caracteres
string s1 = "Hello";
string s2 = "World";
Console.WriteLine($"string1: {s1} string2: {s2}");
```
### Object
```cs
//Object: tipo base de todos os tipos
object o1 = 1;
object o2 = "string";
object o3 = true;
object o4 = 1.5f;
Console.WriteLine($"object1: {o1} object2: {o2} object3: {o3} object4: {o4}");
```
### Dynamic
```cs
//Dynamic: tipo dinâmico
dynamic d1 = 1;
dynamic d1 = "string";
dynamic d3 = true;
dynamic d4 = 1.5f;
Console.WriteLine($"dynamic1: {d1} dynamic2: {d2} dynamic3: {d3} dynamic4: {d4}");
```


