## The Central Processor
- The GBA processor is an **ARM7TDMI** chip. A 32-bit RISC processor with a three-stage pipeline, a hardware multiplier and quite a few registers.


### Two Instruction Sets
- The ARM is a RISC processor design. It's instrution set is very regular, so it's possible to encode an instrucion in quite a few ways.
- A second and denser instruction set was created by the ARM designers, the so-called **Thumb** instruction set
  - It allows two instruction sets to work together
  - The CPU converts Thumb instructions into equivalent ARM instructions on the fly
  - Each Thumb instruction is 16-bits, whereas the ARM ones are 32-bits

### CPU Registers
- The ARM has 16 registers accessible at any time, all of them can hold up to 32-bits

| Registers | Usage                                                                                                                                                                  |
| --------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| R0-R3     | Used for passing parameters to functions. Any parameter that don't fit here gets passed on the stack                                                                   |
| R4-R10    | Used for register variables. Registers 9 and 10 are also used for stack manipulation                                                                                   |
| R11       | Called the frame pointer. It's tipically set and restored during the prologue or epilogue code, since it's the pointer through all local variables are accessed        |
| R12       | Called the interlink pointer. A scratch register for most GBA code.                                                                                                    |
| R13       | The Stack pointer, points to the last item pushed on the stack.                                                                                                        |
| R14       | The link register. It holds the return address for the subroutine. Normally it's pushed to the stack and then popped directly into the program counter for the return. |
| R15       | The program counter. We can directly change it to execute a jump                                                                                                       |


[Go back](https://goiabada.github.io/docs/sections/overview/index)