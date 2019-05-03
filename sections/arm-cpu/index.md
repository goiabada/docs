# ARM CPU

- The **ARM7TDMI** is a 32bit RISC (Reduced Instruction Set Computer) CPU, designed by ARM (Advanced RISC Machines) for both high performance and low power consumption.

## Detailed infomation

1. [ARM CPU Register Set](https://goiabada.github.io/docs/sections/arm-cpu/register-set)
2. [ARM CPU Flags](https://goiabada.github.io/docs/sections/arm-cpu/flags)
3. [ARM CPU Memory Interface](https://goiabada.github.io/docs/sections/arm-cpu/memory-interface)
4. [ARM CPU Exceptions](https://goiabada.github.io/docs/sections/arm-cpu/exceptions)
5. [ARM CPU Memory Alignments](https://goiabada.github.io/docs/sections/arm-cpu/memory-alignments)
6. [ARM 32bit Instruction Set (ARM Code)](https://goiabada.github.io/docs/sections/arm-cpu/arm-code)
7. [ARM 16bit Instruction Set (THUMB Code)](https://goiabada.github.io/docs/sections/arm-cpu/thumb-code)
8. [Extra info](https://goiabada.github.io/docs/sections/arm-cpu/extra)

## General information

### Data formats

- All opcodes are sized 32 ou 16 bits, with pipelining allowing the simultaneous **execution** of one instruction, **decodification** of the next one and **fetching** of yet another one.
- The CPU deals with **8**, **16** and **32 bit** data, called:
  - 8 bit: **byte**
  - 16 bit: **halfword**
  - 32 bit: **word**

### The Two CPU States

- Two CPU states exist:
  - **ARM State**: Uses the full 32bit instruction set (32bit opcodes)
  - **THUMB State**: Uses the full 32bit instruction set (32bit opcodes)

> Regardless of the opcode-width, both states are using 32bit registers, allowing 32bit memory addressing as well as 32bit arithmetic/logical operations.

#### ARM State

##### The good stuff

- Each single opcode provides more functionality, resulting in faster execution when using a 32bit bus memory system (such like opcodes stored in GBA Work RAM).
- All registers R0-R15 can be accessed directly.

##### The bad stuff

- Not so fast when using 16bit memory system (but it still works though).
- Program code occupies more memory space.

#### THUMB State

##### The happy stuff

- Faster execution up to approx 160% when using a 16bit bus memory system (such like opcodes stored in GBA GamePak ROM).
- Reduces code size, decreases memory overload down to approx 65%.

##### The sad stuff

- Not as multi-functional opcodes as in ARM state, so it will be sometimes required use more than one opcode to gain a similar result as for a single opcode in ARM state.
- Most opcodes allow only registers R0-R7 to be used directly.

#### Combining ARM with THUMB state

- Switching between ARM and THUMB states is done by a **normal branch (BX) instruction**, which takes some cycles to execute, allowing the shift to occur whith almost no overload.
- As both ARM and THUMB **are using the same register set**, it's possible to pass data between ARM and THUMB modes very easily.
- The **best** possible can be achieved by **combining both states**: THUMB for normal program code, and ARM for time critical subroutines (like interruption handlers).

> ARM and THUMB code cannot be executed simultaneously

#### Automatic mode change

- Beside for the above manual state switching by using BX instructions, the following situations involve automatic state changes:
  - CPU switches to ARM state when executing an exception
  - User switches back to old state when leaving an exception
