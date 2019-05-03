# ARM CPU Register Set

- The following table shows the **ARM7TDMI** register set, which is available for both CPU modes.
- There is a total of 37 registers (32 bits each), being **31** of them **general purpose registers** (RXX) plus **6 status registers** (xPSR)
- Only some registers are "banked", like each mode having it's own R14 register (R14, R14_fiq, R15_svc) and such. They are not shared between modes.
- However, other registers are not "banked", meaning for example that every mode shares the same R0 register and such. Writing at those registers will always affect the respective ones in other modes, as they are the same.

| System/User | FIQ      | Supervisor | Abort    | IRQ      | Undefined |
| ----------- | -------- | ---------- | -------- | -------- | --------- |
| R0          | R0       | R0         | R0       | R0       | R0        |
| R1          | R1       | R1         | R1       | R1       | R1        |
| R2          | R2       | R2         | R2       | R2       | R2        |
| R3          | R3       | R3         | R3       | R3       | R3        |
| R4          | R4       | R4         | R4       | R4       | R4        |
| R5          | R5       | R5         | R5       | R5       | R5        |
| R6          | R6       | R6         | R6       | R6       | R6        |
| R7          | R7       | R7         | R7       | R7       | R7        |
| R8          | R8_fiq   | R8         | R8       | R8       | R8        |
| R9          | R9_fiq   | R9         | R9       | R9       | R9        |
| R10         | R10_fiq  | R10        | R10      | R10      | R10       |
| R11         | R11_fiq  | R11        | R11      | R11      | R11       |
| R12         | R12_fiq  | R12        | R12      | R12      | R12       |
| R13 (SP)    | R13_fiq  | R13_svc    | R13_abt  | R13_irq  | R13_und   |
| R14 (LR)    | R14_fiq  | R14_svc    | R14_abt  | R14_irq  | R14_und   |
| R15 (PC)    | R15      | R15        | R15      | R15      | R15       |
| CPSR        | CPSR     | CPSR       | CPSR     | CPSR     | CPSR      |
| --          | SPSR_fiq | SPSR_svc   | SPSR_abt | SPSR_irq | SPSR_und  |

- Some things in this table must be explained for better understanding:
  - "**System**" refers to the **System Mode**. You can find more about it [here](https://www.heyrick.co.uk/armwiki/Processor_modes#System_mode).
  - "**User**" refers to the **User Mode**, which is the mode in which user application tasks should run. It has access to the base register set, and no privileges.
  - "**FIQ**" refers to the **FIQ Mode**, which provides a large number of shadow registers (R8 to R14, CPSR) and is useful for things that must complete extremely quickly or else data loss is a possibility.
  - "**IRQ**" refers to the **IRQ Mode**, which is the other regular interrupt mode. Only R13, R14, and CPSR are shadowed. All interrupts that don't require extreme speed (clock ticks, screen VSync, keyboard,etc...) will use IRQ mode.
  - "**Supervisor**" refers to the **Supervisor Mode**, which is the privileged mode reserved for the operating system. R13, R14, and CPSR are shadowed.
  - "**Abort**" refers to the **Abort Mode**. You can find more about it [here](https://www.heyrick.co.uk/armwiki/Processor_modes#Abort_mode)
  - "**Undefined**" refers to the **Undefined Mode**. You can find more about it [here](https://www.heyrick.co.uk/armwiki/Processor_modes#Undefined_mode)

> IRQ's (Interrupt Requests) are "normal" types of interrupts. FIQ's (Fast Interrupt Requests) are an feature that software can optionally use to increase the speed and/or priority of interrupts from a specific source.