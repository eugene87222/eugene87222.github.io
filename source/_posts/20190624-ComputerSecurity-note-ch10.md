---
title: '[Intro. to Computer Security Course Note] Ch 10'
tags:
  - NCTU
  - computer security
  - note
date: 2019-06-24 19:50:36
---

# Ch10. Buffer Overflow

__Buffer overrun__
__Buffer overwrite__

---

# Buffer overflow basics

- Programming error: a process attempts to store data __beyond the limits of a fixed sized buffer__

## Needs for the Attacker: Exploiting a Buffer Overflow

- To identify a buffer overflow vulnerability in some program
- To understand how that buffer will be stored in the process memory

## How to Identify Vulnerable Programs

- Inspecting the program source
- Tracing the execution of programs as they process oversized input
- Using tools to automatically identity potentially vulnerable programs

## Why Programs are not Necessarily Protected

- Basic machine level
   - Data's interpretation: entirely determined by the function of the instructions
   - Responsibility on the assembly language programmer: ensuring that the correct interpretation is placed on any saved value
- Assembly language programs
   - The greatest access to the resources
- Modern high-level programming languages (e.g., Java, Python)
   - Not vulnerable to buffer overflows: flexibility and safety
      - More data to be saved are not allowed
   - Costs in resource use
   - Limiting the usefulness in writing code
- Between these two extremes: C and related languages
   - Have many modern high-level control structures and data type abstractions
   - But, allow direct access to low-level resources

# Stack overflows

## Stack Buffer Overflows

- Also referred to as __stack smashing__

## Some Common Unsafe C Standard Library

```c
gets(char *str)
sprintf(char *str, char *format, ...)
strcat(char *dest, char *src)
strcpy(char *dest, char *src)
vsprintf(char *str, char *fmt, va_list ap)
```

## Shellcode

- Code supplied by the attacker
   - __Often save in buffer being overflowed__
   - Traditionally transferred control to a user command-line interpreter (shell)
- Simply machine code
   - Specific to processor and operating system
- Many sites and tools have been developed that automate this process

# Defending against buffer overflows

- Two broad defense approaches
   - Compile-time defenses
      - Aim to detect harden programs to resist attacks in __new__ programs
      - Choice of programming languages
         - Use modern high-level language
         - Pros: not vulnerable to buffer overflow ([上面](#Why-Programs-are-not-Necessarily-Protected)有提到)
         - Cons: Access to some low-level instructions and hardware resources is lost ([上面](#Why-Programs-are-not-Necessarily-Protected)有提到)
      - Safe coding techniques
         - C designers placed much more emphasis on space efficiency and performance considerations than on type safety
            - Assumed programmers would exercise due care in writing code
         - Programmers need to inspect the code and rewrite any unsafe coding
         - Codes not only for normal successful execution
            - __But, constantly aware of how things might go wrong__
      - Languages extensions and use of safe libraries
         - Handling dynamically allocated memory: __more problematic__
            - __The size of info. is not available at compile time__
         - Requiring an extension and the use of library routines
            - Cons:
               - Generally, there is a performance penalty
               - Programs and libraries __need to be recompiled with the modified compiler__
               - Feasible for new OSes, but likely to __have problems with third-party apps__
      - Stack protection mechanisms
         - Add function entry and exit code to check for signs of corruption
            - Stackguard: best known protection mechanism -> a GCC compiler extension
            - Function entry code: writing a __canary value__ below the old frame pointer address
            - Function exit code: checking that the __canary value__ has not changed
            - The __canary value__: unpredictable and different on different systems
            - Cons:
               - All programs needing protection __need to be recompiled__
               - The structure of the stack frame has changed: causing problems with programs, e.g., debuggers
            - Has been used to recompiled an entire Linux distribution
         - Another variants: Stackshield and Return Address Defender (RAD)
            - Also GCC extension: including additional function entry and exit code
            - __Do not alter__ the structure of the stack frame
            - Function entry code: __writing a copy of the return address to a safe region of memory__
            - Function exit code: __checking the return address in the stack frame against the save copy__
            - Compatible with unmodified debuggers __Why?__
            - __Programs must be recompiled__
   - Run-time defenses
      - Aim to detect and abort attacks in __existing__ programs
      - Can be deployed as OS updates to provide protection
         - Compile-time approaches: __usually requires recompilation of existing programs__
         - Involving changes to the memory management
      - Executable Address Space Protection
         - Block the execution of code on the stack
            - Against the attacks: copying machine code into the targeted buffer and then transferring execution to it
         - Tag pages of virtual memory as being nonexecutable
            - Requires support from memory management unit (MMU)
            - Long existed on SPARC used by Solaris
            - Recent addition of the no-execute bit in the x86 family
            - A standard feature in recent Oses
         - Cons:
            - Unable to support executable stack code
      - Address space randomization
         - Manipulate location of key data structure
            - Stack, heap, global data
            - Using random shift for each process
            - Large address range on modern systems: wasting some has negligible impact
         - Randomize location of heap buffers
         - Random location of standard library functions
      - Guard pages
         - Place guard pages between critical regions of memory
            - Flagged in MMU as illegal addresses
            - Any attempted access aborts process
         - Further extension places guard pages between stack frames and heap buffers
            - __Cost in execution time__ to support the large number of page mappings necessary

# Other forms of overflow attacks

## Replacement stack frame

## Return to system call

## Heap overflows

- Attack buffer located in heap
   - __Typically located above program code__
   - Memory is requested by programs to use in dynamic data structures (such as linked lists of records)
- No return address
   - Hence no easy transfer of control
   - May have function pointers to be exploited
   - Or manipulate management data structure
- __Defenses__
   - Making the heap non-executable
   - __Randomizing the allocation__

## Global data area overflows

- Attacks buffer located in global data
   - Aim to overwrite function pointer later called

- __Defenses__
   - __Non executable or random__ global data region
   - Move function pointers or use guard pages

## Other types of overflows