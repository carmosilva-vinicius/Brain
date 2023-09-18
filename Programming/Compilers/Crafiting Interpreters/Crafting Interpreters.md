Here are some notes of the this book, as a beginner steps to start with [[Compilers]].
Source: [Crafting Interpreters](https://craftinginterpreters.com)

![[mountain.png]]

To start with the interpreters, we need to understand the topics presented in this mountain path. Here are some explanation of this steps with this piece of code: 

![[string.png]]

## Scanning
Also knowing as lixing or laxical analysis, this step is used to analyse a stream of text and chunks them in **_tokens_**. The scanner/lexer is also responsible to ignore discard insignificant parts, like comments and withe space. The result will be like:

![[Programming/Compilers/Crafiting Interpreters/assets/tokens.png]]

## Parsing
To detect the keyword and extract some meaning of the code, we use the parser. It are used to get the **_grammar_** of our code. To achieve it, the parser takes a flat sequence of tokens, scanned by lexer, and build a [[Tree]] that represents the grammar. This is called as **parse tree** or **abstract syntax tree** (AST):

![[Programming/Compilers/Crafiting Interpreters/assets/ast.png]]

## Static analysis
Different of the previous topics,  which is similar in all languages, the static language is commonly particular for each language. It is in this steps where we identify things like scope, types and variables particularity. Commonly, at first, the first process in these steps are binding or resolution.

This semantic insights needs to be stored. Store as attributes of on the syntax trees is one off the approach es. Other possibility is to create a symbol table, where identifiers like name of variables and declarations is stored with their respective values associated.

## Intermediate representation 
In the compilers we also have a middle end, a stage between the front-end and back-end in the pipeline that is responsible to make a interface between the two languages. 
There are a few styles of IRs like “control flow graph”, “static single-assignment”, “continuation-passing style”, and “three-address code”.

This allows us to transpire one language to several others. That is how GCC produce binaries for many processors architectures (back end) using just [[C]] language.

## Optimizatios
Is the process where the compiler change a piece of code for another with the same semantic, but with better performance. For example, we can do the evaluation at compile time and replace the code for the some expression that always result in the same value:
```csharp
pennyArea = 3.14159 * (0.75 / 2) * (0.75 / 2);

//Resulting code after optimazation:
pennyArea = 0.4417860938;
```

Some problems to deep in that are : “**constant propagation**”, “**common subexpression elimination**”, “**loop invariant code motion**”, “**global value numbering**”, “**strength reduction**”, “**scalar replacement of aggregates**”, “**dead code elimination**”, and “**loop unrolling**”.

## Code generation
The text discusses the process of code generation in programming, where a user's program is converted into a form executable by a machine. This involves choosing between generating instructions for a real CPU (native code) or a virtual one (bytecode). Generating native code is complex but fast, however, it lacks portability across different architectures. Bytecode, on the other hand, is a compact binary encoding of the language’s low-level operations, and is more portable but slower. Bytecode represents an idealized machine, mapping closely to the language's semantics and not tied to any specific computer architecture.

Generating native code ties the compiler to a specific architecture, resulting in faster execution but limited portability. In contrast, bytecode, generated for a hypothetical machine, offers better portability across different architectures but at the expense of execution speed. Bytecode is often used to enhance the portability of the program without the need for recompiling the code for each specific hardware.

## Virtual machine
Once we have **bytecode** we need to make another choice. One possibles is to use this **bytecode** as a intermediate language between the programming one and the binary that runs at the processor. In that case, a mini-compiler needs to be created, for each processor architecture that will run the code.

In the other hand, a virtual machine can be created. A software which emulates a chip and runs the byte code should be made, and to achieve this we need to implement it in a language (like [[C]]) that compiles to the real chip.

## Runtime
The process of running a user's program depends on whether it is compiled to machine code or to bytecode. If compiled to machine code, the operating system is instructed to load the executable. If compiled to bytecode, a virtual machine (VM) is started to load the program [freecodecamp.org](https://www.freecodecamp.org/news/compiled-versus-interpreted-languages/), [baeldung.com](https://www.baeldung.com/java-compiled-interpreted). Regardless of the compilation method, the program typically requires certain services provided by the language during runtime, such as memory management or type tracking. These services, collectively referred to as the runtime, are embedded directly into the resulting executable in fully compiled languages like Go. In languages run inside an interpreter or VM, like Java, Python, or JavaScript, the runtime is located within the interpreter or VM [en.wikipedia.org](https://en.wikipedia.org/wiki/Runtime_system), [stackoverflow.com](https://stackoverflow.com/questions/1326071/is-java-a-compiled-or-an-interpreted-programming-language).