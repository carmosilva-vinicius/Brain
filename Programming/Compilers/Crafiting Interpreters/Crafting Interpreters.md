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

## Single-pass compilers
Single-pass compilers are a type of compiler that combines parsing, analysis, and code generation into a single process, producing output code directly without creating any intermediate representations (IRs). This approach, however, limits the design of the programming language as there are no intermediate data structures to store global information about the program. Syntax-directed translation is a method used in these compilers, where an action, usually code generation, is associated with each piece of the grammar. This method was influenced by memory limitations of the time, leading to language design choices in Pascal and C to accommodate single-pass compilation. For instance, Pascal requires type declarations to appear first in a block and C requires explicit forward declarations for functions defined later in the code

## Tree-walk interpreters
Tree-walk interpreters are a type of implementation used in some programming languages where the code is executed immediately after parsing it into an Abstract Syntax Tree (AST). The interpreter traverses the syntax tree, evaluating each node as it progresses. While this implementation style is common for student projects and small languages, it's not widely used for general-purpose languages due to its slow performance. However, some developers use the term "interpreter" to refer to these kinds of implementations, while others use it more generally. To avoid confusion, the term "tree-walk interpreter" is used to refer to these specific implementations. Despite the slow performance, tree-walk interpreters are still used in various projects, mostly for educational purposes and small-scale tasks

## Transpilers
A transpiler, also known as a source-to-source compiler, is a type of compiler that translates code from one high-level language to another. This technique allows developers to write in a language they prefer and then convert the code into another language that can be executed more widely. For instance, a transpiler might convert TypeScript into JavaScript, which is more universally supported in web browsers.

The process of transpilation involves creating a front end for the source language and a back end that generates code in the target language. The front end of a transpiler, which includes a scanner and parser, is similar to other compilers. Depending on the semantic differences between the source and target languages, the back end might involve analysis and optimization phases typical of a full compiler. However, instead of outputting binary machine code, it produces a grammatically correct source code in the target language.

## Just-In-Time compilation
Just-in-time (JIT) compilation is a method of executing code that involves compiling the code to machine code on the end user's machine when the program is loaded. This is done to ensure that the code is compatible with the architecture of the user's computer. This method is used by the HotSpot Java Virtual Machine (JVM), Microsoft’s Common Language Runtime (CLR), and most JavaScript interpreters