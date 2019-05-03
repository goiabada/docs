## Game Pak Memory Wait Control

- Although the 32 MB Game Pak memory space is mapped from **08000000h** onward, the 32 MB spaces beggining from **0A000000h** and **0C000000h** **are images** of the 32 MB space that starts at **08000000h**

- These images enable memory to be used **according the access speed of the Game Pak memory** (1-4 wait cycles)

![Memory Wait Control Diagram](/images/gpk_wait_control.png)

- **WAITCNT [d15]** : Game Pak Type Flag
- **WAITCNT [d14]** : Prefetch Buffer Flag
  - When the Prefetch Buffer Flag is enabled and there is some free space,
    the Prefetch Buffer takes control of the Game Pak Bus during the time
    when the CPU is not using it, and reads Game Pak ROM data repeatedly.
  - When the CPU tries to read instructions from the Game Pak and if it hits
    the Prefetch Buffer, the fetch is completed with no wait in respect to the
    CPU.
  - If there is no hit, the fetch is done from the Game Pak ROM and
    there is a wait based on the set wait state.
  - If the Prefetch Buffer Flag is disabled, the fetch is done from the Game Pak
    ROM.
  - There is a wait based on the wait state associated with the fetch
    instruction to the Game Pak ROM in respect to the CPU.
- **WAITCNT [d12 - 11]** : PHI Terminal Output Control
  - Controls the output from the PHI terminal. This should always be set to
    00(No Output).
- **WAITCNT [d10 - 08],[d07 - 05],[d04 - 02]** : Wait State Wait Control
  - Individual wait cycles for each of the three areas(Wait States 0-2) that
    occur in Game Pak ROM can be set.
  - The relation between the wait control settings and wait cycles is as follows:
  
![Wait State Wait Control](/images/wait_state_control.png)

- **WAITCNT [d01 - 00]** - Game Pak RAM Wait Control
  - Wait cycles for the Game Pak RAM can be set
  - The relation between the wait control settings and wait cycles is as follows:

![Game Pack RAM Wait Control](/images/gpk_ram_wait_control.png)

[Go back](https://goiabada.github.io/docs/sections/memory/index)
