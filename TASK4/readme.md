# SPIKE SIMULATION
Spike is a RISC-V ISA simulator written in C++ that models a RISC-V core and cache system. It can be used to run a Linux Kernel and non-I/O related programs. Spike is a starting point for running software on a RISC-V target. Some of Spike's main features include:
* Multiple ISAs
* Multiple memory models
* Privileged Spec
* Machine, Supervisor, User modes
* Hypervisor extension
* Svnapot extension
* Svpbmt extension

## SPIKE SIMULATION WITH -Ofast:
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
<img src= "https://github.com/ridhikapila27/vsdsquadron-mini-internship/blob/main/TASK4/Ofast_main.JPG?raw=true"/>;

## SPIKE SIMULATION WITH -O1:
This optimization flag specifies a lower level of optimization compared to -Ofast. It enables basic optimizations aimed at improving code performance without overly sacrificing compilation time or code clarity. -O1 optimizations typically include basic operations like constant folding, dead code elimination, and simple loop optimizations.

1. Create a C program using text editor
2. Run the code using gcc and display output
   ```
   gcc sum1ton.c
   ./a.out
   riscv64-unknown-elf-gcc O1 -mabi=lp64 -march=rv64i -o sum1ton.o sum1ton.c
   spike -d pk sum1ton.o
   until pc 0 100b0
   spike -d pk sum1ton.o
   ```
 <img src= "https://github.com/ridhikapila27/vsdsquadron-mini-internship/blob/main/TASK4/O1.JPG?raw=true"/>

3. Open another terminal window
   ```
   riscv64-unknown-elf-objdump -d  sum1ton.o | less
   main
   ```
   <img src = "https://github.com/ridhikapila27/vsdsquadron-mini-internship/blob/main/TASK4/O1_main.JPG?raw=true"/>

When using Spike for simulation, these optimization flags affect the performance characteristics of the compiled code running within the simulated RISC-V environment. The choice between -Ofast and -O1 depends on the specific requirements of the software being compiled, balancing between code execution speed and adherence to language standards or code clarity.
