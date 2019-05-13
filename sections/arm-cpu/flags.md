# ARM CPU Flags

- The opcode **{cond}** suffixes can be used for conditionally executed code based on the **C, N, Z and V flags** in the CPSR Register.
- In ARM Mode, **{cond}** can be used with all opcodes, whereas in THUMB mode only for branch opcodes.

| Code | Suffix | Flags       | Meaning                                       |
| ---- | ------ | ----------- | --------------------------------------------- |
| 0:   | EQ     | Z=1         | equal (zero) (same)                           |
| 1:   | NE     | Z=0         | not equal (nonzero) (not same)                |
| 2:   | CS/HS  | C=1         | unsigned higher or same (carry set)           |
| 3:   | CC/LO  | C=0         | unsigned lower (carry cleared)                |
| 4:   | MI     | N=1         | negative (minus)                              |
| 5:   | PL     | N=0         | positive or zero (plus)                       |
| 6:   | VS     | V=1         | overflow (V set)                              |
| 7:   | VC     | V=0         | no overflow (V cleared)                       |
| 8:   | HI     | C=1 and Z=0 | unsigned higher                               |
| 9:   | LS     | C=0 or Z=1  | unsigned lower or same                        |
| A:   | GE     | N=V         | greater or equal                              |
| B:   | LT     | N<>V        | less than                                     |
| C:   | GT     | Z=0 and N=V | greater than                                  |
| D:   | LE     | Z=1 or N<>V | less or equal                                 |
| E:   | AL     | -           | always (the "AL" suffix can be omitted)       |
| F:   | NV     | -           | never (ARMv1,v2 only) (Reserved ARMv3 and up) |

## Current Program Status Register (CPSR)

| Bit  | Explanation                                                    | Extra        |
| ---- | -------------------------------------------------------------- | ------------ |
| 31   | N - Sign Flag       (0=Not Signed, 1=Signed)                   | ;\           |
| 30   | Z - Zero Flag       (0=Not Zero, 1=Zero)                       | ; Condition  |
| 29   | C - Carry Flag      (0=Borrow/No Carry, 1=Carry/No Borrow)     | ; Code Flags |
| 28   | V - Overflow Flag   (0=No Overflow, 1=Overflow)                | ;/           |
| 27   | Q - Sticky Overflow (1=Sticky Overflow, ARMv5TE and up only)   |              |
| 26-8 | Reserved            (For future use) - Do not change manually! |              |
| 7    | I - IRQ disable     (0=Enable, 1=Disable)                      | ;\           |
| 6    | F - FIQ disable     (0=Enable, 1=Disable)                      | ; Control    |
| 5    | T - State Bit       (0=ARM, 1=THUMB) - Do not change manually! | ; Bits       |
| 4-0  | M4-M0 - Mode Bits   (See below)                                | ;/           |

### Bit 31-28: Condition Code Flags (N,Z,C,V)

- Reflect on results of logical arithmetic instructions.
- In ARM mode is often optional whether an instruction should modify flags or not. Making it possible, for example, to execute a SUB instruction that does NOT modify the condition flags.
- In ARM state, all instructions can be executed conditionally depending on the settings of the flags, such like MOVEQ (Move if Z=1).
- In THUMB state, only Branch instructions (jumps) can be made conditionally.

### Bit 27: Sticky Overflow Flag (Q) 

- Used by QADD, QSUB, QDADD, QDSUB, SMLAxy, and SMLAWy only.
- These opcodes set the Q-flag in case of overflows, but leave it unchanged otherwise.

### Bit 27-8: Reserved Bits 

- These bits are reserved for possible future implementations.
- For best forwards compatibility, the user should never change the state of these bits, and should not expect these bits to be set to a specific value.

### Bit 7-0: Control Bits (I,F,T,M4-M0)

- These bits may change when an exception occurs.
- In privileged modes (non-user modes) they may be also changed manually.
- The interrupt bits I and F are used to disable IRQ and FIQ interrupts respectively (a setting of "1" means disabled).
- The T Bit signalizes the current state of the CPU (0=ARM, 1=THUMB), this bit **should never be changed manually**.
  - Changing between ARM and THUMB state must be done by **BX instructions**.
- The **Mode Bits M4-M0** contain the current operating mode:

| Binary | Hex | Dec | Explanation                                      |
| ------ | --- | --- | ------------------------------------------------ |
| 0xx00b | 00h | 0   | - Old User                                       |
| 0xx01b | 01h | 1   | - Old FIQ                                        |
| 0xx10b | 02h | 2   | - Old IRQ                                        |
| 0xx11b | 03h | 3   | - Old Supervisor                                 |
| 10000b | 10h | 16  | - User (non-privileged)                          |
| 10001b | 11h | 17  | - FIQ                                            |
| 10010b | 12h | 18  | - IRQ                                            |
| 10011b | 13h | 19  | - Supervisor (SWI)                               |
| 10111b | 17h | 23  | - Abort                                          |
| 11011b | 1Bh | 27  | - Undefined                                      |
| 11111b | 1Fh | 31  | - System (privileged 'User' mode) (ARMv4 and up) |

> Writing any other values into the Mode bits is not allowed.

### Saved Program Status Registers

- Additionally to above CPSR, five Saved Program Status Registers exist: **SPSR_fiq, SPSR_svc, SPSR_abt, SPSR_irq, SPSR_und**
- Whenever the CPU enters an exception, the current status register (CPSR) is copied to the respective SPSR_(mode) register.
- For example, for an IRQ exception: IRQ-mode is entered, and CPSR is copied to SPSR_irq. If the interrupt handler wants to enable nested IRQs, then it must first push SPSR_irq before doing so.