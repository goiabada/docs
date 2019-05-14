# ARM CPU Exceptions

## Exception vectors

- When an exception arises, CPU is switched into ARM state, and the program counter (PC) is loaded by the respective address.

| Address  | Priority | Exception                | Mode on entry | Interrupt flags          |
| -------- | -------- | ------------------------ | ------------- | ------------------------ |
| BASE+00h | 1        | Reset                    | Supervisor    | (_svc)  I=1, F=1         |
| BASE+04h | 7        | Undefined Instruction    | Undefined     | (_und)  I=1, F=unchanged |
| BASE+08h | 6        | Software Interrupt (SWI) | Supervisor    | (_svc)  I=1, F=unchanged |
| BASE+0Ch | 5        | Prefetch Abort           | Abort         | (_abt)  I=1, F=unchanged |
| BASE+10h | 2        | Data Abort               | Abort         | (_abt)  I=1, F=unchanged |
| BASE+14h | ??       | Address Exceeds 26bit    | Supervisor    | (_svc)  I=1, F=unchanged |
| BASE+18h | 4        | Normal Interrupt (IRQ)   | IRQ           | (_irq)  I=1, F=unchanged |
| BASE+1Ch | 3        | Fast Interrupt (FIQ)     | FIQ           | (_fiq)  I=1, F=1         |

## Actions performed by CPU when entering an exception

- R14_(new mode)=PC+nn   ;save old PC, ie. return address
- SPSR_(new mode)=CPSR   ;save old flags
- CPSR new T,M bits      ;set to T=0 (ARM state), and M4-0=new mode
- CPSR new I bit         ;IRQs disabled (I=1), done by ALL exceptions
- CPSR new F bit         ;FIQs disabled (F=1), done by Reset and FIQ only
- PC=exception_vector    ;see table above

[Go back](https://goiabada.github.io/docs/sections/arm-cpu/index)