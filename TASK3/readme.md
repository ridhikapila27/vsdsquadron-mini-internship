## COMPILED C CODE 
Steps to compile any C code in UBUNTU:
1. Open terminal and type the following instructions:

```
   cd
   sudo snap leafpad install
   leafpad sum1ton.c
```

2. The editor window will be opened where the C program needs to be written:
3. Type the following instructions in terminal:
   
```
   gcc sum1ton.c
   ./a.out
```

<img src = "https://github.com/ridhikapila27/vsdsquadron-mini-internship/blob/main/TASK3/c_program.JPG?raw=true" />


## RISC-V OBJDUMP:

1. Open terminal and type the following instructions:

   ```
   cat sum1ton.c
   ```
   The C code can be read in terminal using this command.
<img src = "https://github.com/ridhikapila27/vsdsquadron-mini-internship/blob/main/TASK3/cat.JPG?raw=true" />

   ```
   riscv32-unknown-elf-gcc -o sum1ton.o sum1ton.c
   ls -ltr sum1ton.o
   ```
2. Open another terminal window and type the following instructions:
   
   ```
   riscv32-unknown-elf-objdump -d sum1ton.o sum1ton.c
   riscv32-unknown-elf-objdump -d sum1ton.o sum1ton.c | less
   
   ```
   

