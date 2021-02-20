# Blixate Virtual Machine (Blixate VM / BVM)
## Design
  The Blixate virtual machine is currently not released or completed. It is a virtual-machine which interprets bytecode into instructions. The design is to be fast, and simple to develop programs for, aswell as having full control and not breaking your system in the process.
  
  REMEMBER: All of these are just ideas and hopes. Implementing all of this is a lot, but I want to make something- if i'm making anything, it's got to be good.
## Read-only memory and Access memory
  All program's memory is split up into 2 sections: Access memory, and Read-only memory.
### Access Memory
  The most obvious part of memory is the memory you can change. This memory can be written to, read from, and allocated. The programmer has full control over this memory, and can change it however they like. This is the place you would store variables, class instances, pointers, or anything else that will change during the course of your program.
### Read-only Memory
  This memory cannot be changed by the program, sort of. The program can move *Access Memory* to *Read-only Memory*, but the memory cannot be overwritten, as a new spot in *Read-only Memory* will be allocated. This is where you would store class definitions (not instances), your code, read-only variables, and other important memory that should never change.
## Performance
  Blixate VM is programmed in the C programming-language. This allows fast speed, whilst not giving me a headache.
  
  These programs are on the "third" level, which is based on a system of:
  
  0. The CPU: Pure machine code.
  1. The Operating System: Helps the CPU run executable files.
  2. Blixate VM: Helps the operating system run Executable Blixate Programs
  3. Bytecode: Where your program sits.
  
  This means it's reasonably high-level, but not too high-level. Unlike Python or C#, code must be compiled as bytecode; which means that reading each instruction and executing it takes smaller amounts of time.
## Security
  Running programs inside the VM means that they are more secure, if Blixate VM doesn't have a security issue. You should always have some level of caution when running code that you haven't wrote, and don't trust the individual that wrote the code.
### Exploits
  It is entirely possible that BlixateVM can contain an exploit that can be abused. Of course, these should be reported and promptly fixed. Although, if someone decides to discover an exploit and then doesn't report it, this could cause major issues. If you find an exploit, report it.
### Sandbox and Tools
  In order to make sure that malicous code or exploits cannot slip through the cracks, simple anti-malware tools can be developed to log system calls and dangerous methods. This could also help with debugging and patching security exploits.
### Anti-Malware
  Implementing anti-malware into a Blixate VM program is difficult, but this is a requirement to prevent malware from infecting machines. Since the anti-malware will never be perfect. If malware is developed, patching the exploit is ever-more easy than installing a windows update.
  
  Malware isn't easy to develop inside of Blixate VM, but external server attacks are still possible.
### Decompiling
  Although, decompilation tools might be made, there will be a way to make the bytecode more and more cluttered and obfuscated. I'm thinking a
  licensed instruction set, which will have different types of obfuscation and instructions, and be much harder to decompile. Since the code shouldn't contain method names and just instructions, this should make decompilation hard, but compilation is also harder.
## Control
  The code you write is the code that gets executed, and you can have full control over the executable, excluding for malicious purposes.
  
  The heavy-lifting like class implementation, functions, variables, and other programming features should be done by the programmer, but writing a compiler
  for these features is a better solution than writing an assembler and doing it by hand. Blixate VM will have features to help with these abstract concepts, such as a way to copy an amount of bytes to a different address.
