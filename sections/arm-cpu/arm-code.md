# ARM 32bit Instruction Set (ARM Code)

## ARM Instruction Summary

### Logical ALU Operations

| Instruction             | Cycles | Flags | Explanation         |
| ----------------------- | ------ | ----- | ------------------- |
| MOV{cond}{S}  Rd,Op2    | 1S+x+y | NZc-  | Rd = Op2            |
| MVN{cond}{S}  Rd,Op2    | 1S+x+y | NZc-  | Rd = NOT Op2        |
| ORR{cond}{S}  Rd,Rn,Op2 | 1S+x+y | NZc-  | Rd = Rn OR Op2      |
| EOR{cond}{S}  Rd,Rn,Op2 | 1S+x+y | NZc-  | Rd = Rn XOR Op2     |
| AND{cond}{S}  Rd,Rn,Op2 | 1S+x+y | NZc-  | Rd = Rn AND Op2     |
| BIC{cond}{S}  Rd,Rn,Op2 | 1S+x+y | NZc-  | Rd = Rn AND NOT Op2 |
| TST{cond}{P}  Rn,Op2    | 1S+x   | NZc-  | Void = Rn AND Op2   |
| TEQ{cond}{P}  Rn,Op2    | 1S+x   | NZc-  | Void = Rn XOR Op2   |

### Arithmetic ALU Operations

| Instruction             | Cycles | Flags | Explanation      |
| ----------------------- | ------ | ----- | ---------------- |
| ADD{cond}{S}  Rd,Rn,Op2 | 1S+x+y | NZCV  | Rd = Rn+Op2      |
| ADC{cond}{S}  Rd,Rn,Op2 | 1S+x+y | NZCV  | Rd = Rn+Op2+Cy   |
| SUB{cond}{S}  Rd,Rn,Op2 | 1S+x+y | NZCV  | Rd = Rn-Op2      |
| SBC{cond}{S}  Rd,Rn,Op2 | 1S+x+y | NZCV  | Rd = Rn-Op2+Cy-1 |
| RSB{cond}{S}  Rd,Rn,Op2 | 1S+x+y | NZCV  | Rd = Op2-Rn      |
| RSC{cond}{S}  Rd,Rn,Op2 | 1S+x+y | NZCV  | Rd = Op2-Rn+Cy-1 |
| CMP{cond}{P}  Rn,Op2    | 1S+x   | NZCV  | Void = Rn-Op2    |
| CMN{cond}{P}  Rn,Op2    | 1S+x   | NZCV  | Void = Rn+Op2    |

### Multiply

| Instruction                     | Cycles      | Flags | Explanation                 |
| ------------------------------- | ----------- | ----- | --------------------------- |
| MUL{cond}{S}    Rd,Rm,Rs        | 1S+mI       | NZx-  | Rd = Rm*Rs                  |
| MLA{cond}{S}    Rd,Rm,Rs,Rn     | 1S+mI+1I    | NZx-  | Rd = Rm*Rs+Rn               |
| UMULL{cond}{S}  RdLo,RdHi,Rm,Rs | 1S+mI+1I    | NZx-  | RdHiLo = Rm*Rs              |
| UMLAL{cond}{S}  RdLo,RdHi,Rm,Rs | 1S+mI+2I    | NZx-  | RdHiLo = Rm*Rs+RdHiLo       |
| SMULL{cond}{S}  RdLo,RdHi,Rm,Rs | 1S+mI+1I    | NZx-  | RdHiLo = Rm*Rs              |
| SMLAL{cond}{S}  RdLo,RdHi,Rm,Rs | 1S+mI+2I    | NZx-  | RdHiLo = Rm*Rs+RdHiLo       |
| SMLAxy{cond}    Rd,Rm,Rs,Rn     | ARMv5TE(xP) | ----q | Rd=HalfRm*HalfRs+Rn         |
| SMLAWy{cond}    Rd,Rm,Rs,Rn     | ARMv5TE(xP) | ----q | Rd=(Rm*HalfRs)/10000h+Rn    |
| SMULWy{cond}    Rd,Rm,Rs        | ARMv5TE(xP) | ----  | Rd=(Rm*HalfRs)/10000h       |
| SMLALxy{cond}   RdLo,RdHi,Rm,Rs | ARMv5TE(xP) | ----  | RdHiLo=RdHiLo+HalfRm*HalfRs |
| SMULxy{cond}    Rd,Rm,Rs        | ARMv5TE(xP) | ----  | Rd=HalfRm*HalfRs            |

### Memory load/store

| Instruction                      | Cycles     | Flags | Explanation            |
| -------------------------------- | ---------- | ----- | ---------------------- |
| LDR{cond}{B}{T} Rd,<Address>     | 1S+1N+1I+y | ----  | Rd=[Rn+/-<offset>]     |
| LDR{cond}H      Rd,<Address>     | 1S+1N+1I+y | ----  | Load Unsigned halfword |
| LDR{cond}D      Rd,<Address>     |            | ----  | Load Dword ARMv5TE     |
| LDR{cond}SB     Rd,<Address>     | 1S+1N+1I+y | ----  | Load Signed byte       |
| LDR{cond}SH     Rd,<Address>     | 1S+1N+1I+y | ----  | Load Signed halfword   |
| LDM{cond}{amod} Rn{!},<Rlist>{^} | nS+1N+1I+y | ----  | Load Multiple          |
| STR{cond}{B}{T} Rd,<Address>     | 2N         | ----  | [Rn+/-<offset>]=Rd     |
| STR{cond}H      Rd,<Address>     | 2N         | ----  | Store halfword         |
| STR{cond}D      Rd,<Address>     |            | ----  | Store Dword ARMv5TE    |
| STM{cond}{amod} Rn{!},<Rlist>{^} | (n-1)S+2N  | ----  | Store Multiple         |
| SWP{cond}{B}    Rd,Rm,[Rn]       | 1S+2N+1I   | ----  | Rd=[Rn], [Rn]=Rm       |
| PLD             <Address>        | 1S         | ----  | Prepare Cache ARMv5TE  |

### Jumps, Calls, CPSR Mode, and others

| Instruction               | Cycles   | Flags | Explanation                      |
| ------------------------- | -------- | ----- | -------------------------------- |
| B{cond}   label           | 2S+1N    | ----  | PC=$+8+/-32M                     |
| BL{cond}  label           | 2S+1N    | ----  | PC=$+8+/-32M, LR=$+4             |
| BX{cond}  Rn              | 2S+1N    | ----  | PC=Rn, T=Rn.0 (THUMB/ARM)        |
| BLX{cond} Rn              | 2S+1N    | ----  | PC=Rn, T=Rn.0, LR=PC+4, ARM9     |
| BLX       label           | 2S+1N    | ----  | PC=PC+$+/-32M, LR=$+4, T=1, ARM9 |
| MRS{cond} Rd,Psr          | 1S       | ----  | Rd=Psr                           |
| MSR{cond} Psr{_field},Op  | 1S       | (psr) | Psr[field]=Op                    |
| SWI{cond} Imm24bit        | 2S+1N    | ----  | PC=8, ARM Svc mode, LR=$+4       |
| BKPT      Imm16bit        | ???      | ----  | PC=C, ARM Abt mode, LR=$+4 ARM9  |
| The Undefined Instruction | 2S+1I+1N | ----  | PC=4, ARM Und mode, LR=$+4       |
| cond=false                | 1S       | ----  | Any opcode with condition=false  |
| NOP                       | 1S       | ----  | R0=R0                            |
| CLZ{cond} Rd,Rm           | ???      | ----  | Count Leading Zeros ARMv5        |
| QADD{cond} Rd,Rm,Rn       |          | ----q | Rd=Rm+Rn       ARMv5TE(xP)       |
| QSUB{cond} Rd,Rm,Rn       |          | ----q | Rd=Rm-Rn       ARMv5TE(xP)       |
| QDADD{cond} Rd,Rm,Rn      |          | ----q | Rd=Rm+Rn*2     ARMv5TE(xP)       |
| QDSUB{cond} Rd,Rm,Rn      |          | ----q | Rd=Rm-Rn*2     ARMv5TE(xP)       |


[Go back](https://goiabada.github.io/docs/sections/arm-cpu/index)