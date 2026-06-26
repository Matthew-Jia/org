# Intro

OS development notes

# Booting and Startup

## Global Descriptor Table

The Global Descriptor Table is a binary data structure specific to IA-32 and x86-64 architectures. It contains entries telling the CPU about memory segments.\\

The GDT is a system that isn't really used anymore. It use to be used to define segments to isolate kernel memory and user memory, but nowadays its usually only used to define what protection mode the processor is currently in. This is why you will normally see the kernel data/code segments and user data/code segments all with base 0 and limit $\infty$, the only difference being the protection mode each one has. You don't really use the GDT anymore for isolating code (you rely on the page table to do this), you just rely on it filling a register on mode switch that defines what protection mode you are in. You might wonder, "Why can't I just set a 'Privilege' register directly?" The answer is Legacy. Intel maintains "backward compatibility" above almost all else. To avoid breaking the way computers boot, they kept the GDT mechanism but stripped it of its power. You still have to build the table, and you still have to point the CPU to it using the lgdt instruction, even if the "Base" and "Limit" columns in that table are now filled with zeros and ignored.

# TODOs:

- Understand why my GDT would fail with a useful output every so often.

- Understand how programs with external linkage look in assembly. I understand how functions use the global keyword, but what about other symbols like variables?

- Add way more documentation to the code. Perhaps make the entries data table more explicit by defining macros or constexpr helper functions.
