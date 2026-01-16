# Understanding Hardcaml

In https://www.youtube.com/watch?v=X1cgRXhpQLY Andy Ray demonstrates Jane Street's use of OCaml for complete FPGA design stacks — from hardware description (Hardcaml DSL) to embedded software running on soft CPUs within the FPGA itself. 
​

## FPGA Fundamentals
FPGAs consist of programmable look-up tables (LUTs), abundant registers (effectively "free"), Block RAM (BRAM) for high-bandwidth memory, DSP blocks for math operations, and sophisticated clocking infrastructure. Effective designs exploit:

* Pipelining: New data every clock cycle across processing stages
* Parallelism: Multiple identical modules running simultaneously
* Bit-level custom logic: FPGAs excel at tailored bit manipulation
​

## Why Hardcaml Over Traditional Register Transfer Languages such as Verilog, VHDL?
- Higher abstraction and safety: OCaml's powerful features can be utilised, such as higher-order functions, strong typing and modules, very useful for hardware circuits and makes designs less error prone. OCaml's type safety catches width mismatches and semantic errors at elaboration time
- - Higher-order functions generate repetitive circuit structures (e.g., FIR filter taps, processing chains)
- Rapid testing and simulation: Hardcaml has built-in-cycle accurate simulation, directly in OCaml itself, allowing developers to test hardware designs directly within OCaml. Thus, you don't require a Verilog simulator!
- Formal verification: the hardware is represented as an OCaml data structure, it is easier to convert designs into mathematical formats for SAT solvers, or even formal prof tools.
- - AST (formal verification hardware) converts easily to SAT solver problems. 
- Efficient memory handling with FPGAs: registers are "free" in FPGA fabric, but for large datasets, you should use Block RAM (BRAM). Hardcaml provides macros to help the vendor tools infer these correctly so you don't run out of logic gates on the FPGA
- - An example of a self-adaptive design is Signal.width - Querying a signal's width at elaboration time using width.


## Architecture of a Hardcaml design

- Elaboration time (OCaml): Uses OCaml's high level features such as lists, recursion, modules to generate the circuit. FOr example, if you need a chain of 100 identical processing units for
- Hardware Execution with Signals: Once the circuit is drawn (elaborated) it runs as a graph of logic gates. Some standard OCaml statements cannot be used.





​

Hardcaml Architecture: Two Phases
