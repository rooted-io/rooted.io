# Buffer Overflow: ELI5

## What Is It?  
Imagine a cup designed to hold exactly 8 ounces of coffee.  
A buffer overflow is like pouring 12 ounces of coffee into that cup.  
The excess spills over, making a mess and potentially damaging the cup itself or the table.  

In programs, buffers are temporary storage areas for data.  
A buffer overflow happens when a program tries to stuff more data into a buffer than it can hold:  
this overflows the buffer and spills into neighboring memory locations, corrupting data or even crashing the program.  

## How Attackers Exploit It  
Attackers can craft malicious input that overflows a buffer.  
This can overwrite critical parts of a program's memory, like its instructions.  
The attacker can then replace those instructions with their own malicious code, giving them control of the program.  
This can be used to steal data, install malware, bypass authentication or take over the entire system.  

## Mitigating Buffer Overflow
There are several ways to prevent buffer overflows:  

1. **Input Validation**: Programs should check the size of any incoming data before putting it in a buffer.  
   If the data is too big, the program should reject it.  
2. **Safe Functions**: Programmers can use functions specifically designed to handle data of unknown size.  
   These functions often have built-in bounds checking to prevent overflows.  
3. **Memory Protection**: Operating systems can mark certain areas of memory as read-only.  
   This prevents programs from accidentally overwriting critical data structures.  
4. **Safer Programming Languages**: Some programming languages have features that make buffer overflows less likely. 
   For example, languages with garbage collection can automatically manage memory allocation and deallocation, reducing the risk of errors.
5. **Memory Randomization**: Modern operating systems employ techniques like *Address Space Layout Randomization (ASLR)* and *Data Execution Prevention (DEP)*.  
   ASLR randomizes the location of key program components like the stack and heap in memory.  
   DEP marks certain memory regions as non-executable, making it harder for attackers to inject and run malicious code even if a buffer overflow occurs.  


## Buffer Overflow in Action  

<video width="850" controls>
  <source src="media/bo.mp4" type="video/mp4">
</video>  
