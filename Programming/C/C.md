## Hellow World

1. Create a new file called `hello.c` using a text editor of your choice. You can use the `touch` editor in the terminal:
```c
#include <stdio.h>

int main() {
   printf("Hello, World!\n");
   return 0;
}
```

2. Compile the C program using the GCC compiler:
```
gcc -o hello hello.c
```

Or compile your C program with the `-S` flag to generate the assembly code:
```
gcc -S -o hello.s hello.c
```

```armasm
     .file   "hello.c"
     .text
     .section    .rodata
 .LC0:
     .string "Hello World!"
     .text
     .globl  main
     .type   main, @function
 main:
.LFB0:
   .cfi_startproc
   pushq   %rbp
   .cfi_def_cfa_offset 16
   .cfi_offset 6, -16
   movq    %rsp, %rbp
   .cfi_def_cfa_register 6
   leaq    .LC0(%rip), %rax
   movq    %rax, %rdi
   call    puts@PLT
   movl    $0, %eax
   popq    %rbp
   .cfi_def_cfa 7, 8
   ret
   .cfi_endproc
.LFE0:
   .size   main, .-main
   .ident  "GCC: (GNU) 13.2.1 20230801"
   .section    .note.GNU-stack,"",@progbits
```

To view the hex representation of the compiled binary, you can use the `xxd` command:
```
xxd hello
```

3. Finally to run the C compiled binary:
```
./hello
```
