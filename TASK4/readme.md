# SPIKE SIMULATION
Spike is a RISC-V ISA simulator written in C++ that models a RISC-V core and cache system. It can be used to run a Linux Kernel and non-I/O related programs. Spike is a starting point for running software on a RISC-V target. Some of Spike's main features include:
* Multiple ISAs
* Multiple memory models
* Privileged Spec
* Machine, Supervisor, User modes
* Hypervisor extension
* Svnapot extension
* Svpbmt extension

## SPIKE SIMULATION WITH Ofast:
This optimization flag is typically used to enable aggressive optimization settings, often sacrificing strict compliance with language standards or precision in favor of maximizing performance.The resulting code may execute faster but might not strictly adhere to the original source code semantics, especially in cases involving floating-point arithmetic.

1. Create a C program using text editor
2. Run the code using gcc and display output
   ```
   gcc sum1ton.c
   ./a.out
   riscv64-unknown-elf-gcc Ofast -mabi=lp64 -march=rv64i -o sum1ton.o sum1ton.c
   spike -d pk sum1ton.o
   until pc 0 100b0
   spike -d pk sum1ton.o
   ```
<img src= "https://github.com/ridhikapila27/vsdsquadron-mini-internship/blob/main/TASK4/Ofast.JPG?raw=true"/>;

3. Open another terminal window
   ```
   riscv64-unknown-elf-objdump -d  sum1ton.o | less
   main
   ```
<img src= "https://github.com/ridhikapila27/vsdsquadron-mini-internship/blob/main/TASK4/Ofast.JPG?raw=true"/>;
