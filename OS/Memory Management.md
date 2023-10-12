# Stack
The stack is used for **static memory allocation** and as the name suggests it is a last in first out(**LIFO**) stack (Think of it as a stack of boxes).

- Due to this nature, the process of storing and retrieving data from the stack is **very fast** as there is no lookup required, you just store and retrieve data from the topmost block on it.
- But this means any data that is stored on the stack has to be **finite and static**(The size of the data is known at compile-time).
- This is where the execution data of the functions are stored as **stack frames**(So, this is the actual execution stack). Each frame is a block of space where the data required for that function is stored. For example, every time a function declares a new variable, it is "pushed" onto the topmost block in the stack. Then every time a function exits, the topmost block is cleared, thus all of the variables pushed onto the stack by that function, are cleared. These can be determined at compile time due to the static nature of the data stored here.
- **Multi-threaded applications** can have a **stack per thread**.
- Memory management of the stack is **simple and straightforward** and is done by the [[OS]].
- Typical data that are stored on stack are **local variables**(value types or primitives, primitive constants), **pointers** and **function frames**.
- This is where you would encounter **stack overflow errors** as the size of the stack is limited compared to the Heap.
- There is a **limit on the size** of value that can be stored on the Stack for most languages.
[source](https://dev.to/deepu105/demystifying-memory-management-in-modern-programming-languages-ddd)
# Heap
Heap is used for **dynamic memory allocation** and unlike stack, the program needs to look up the data in heap using **pointers** (Think of it as a big multi-level library).

- It is **slower** than stack as the process of looking up data is more involved but it can store more data than the stack.
- This means data with **dynamic size** can be stored here.
- Heap is **shared** among threads of an application.
- Due to its dynamic nature heap is **trickier to manage** and this is where most of the memory management issues arise from and this is where the automatic memory management solutions from the language kick in.
- Typical data that are stored on the heap are **global variables**, **reference types** like objects, strings, maps, and other complex data structures.
- This is where you would encounter **out of memory errors** if your application tries to use more memory than the allocated heap(Though there are many other factors at play here like GC, compacting).
- Generally, there is **no limit** on the size of the value that can be stored on the heap. Of course, there is the upper limit of how much memory is allocated to the application.
