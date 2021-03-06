# Blixate Virtual Machine (Blixate VM / BVM)
## Design
  The Blixate virtual machine is currently not released or completed. It is a virtual-machine which interprets bytecode into instructions. The design is to be fast, and simple to develop programs for, aswell as having full control and not breaking your system in the process.
  
  ___REMEMBER:___ All of these are just ideas and hopes. Implementing all of this is a lot, but I want to make something that is useful and proper.
## Memory
  All program's memory is split up into 2 sections: Access memory, and Read-only memory.
### Access Memory
  The most obvious part of memory is the memory you can change. This memory can be written to, read from, and allocated. The programmer has full control over this memory, and can change it however they like. This is the place you would store variables, class instances, pointers, or anything else that will change during the course of your program.
### Stack and Heap
  There is a stack and heap system on BVM. The stack is used to store function returns, function parameters, local variables, and anything that is only required temporarily. Since **Registers** don't exist, this might not seem that necessary, but it's just nice to have. The heap is used to store anything that might be used in multiple different methods, or just to store stuff that shouldn't be placed on the stack. There are different opcodes depending if you want to store to the stack, the heap, or anywhere in memory.
### Read-only Memory
  This memory cannot be changed by the program, sort of. The program can move *Access Memory* to *Read-only Memory*, but the memory cannot be overwritten, as a new spot in *Read-only Memory* will be allocated. This is where you would store class definitions (not instances), your code, read-only variables, and other important memory that should never change.
  An address to ROM has it's first bit set to 1. If 32-bit addresses are used, instead of 4 billion addresses in RAM, 2 billion addresses are put in RAM and 2 billion in ROM. **This currently model for addresses is not final and is subject to change**
### Pointers
  Memory can store pointers to different parts of memory. These pointers can then be incremented, decremented, or offset to different parts of memory. These different parts can then be used to point to an element in an array, a variable in a class or structure, or just a normal variable. Typically when allocating onto the heap, a pointer will be stored. Which can then be used to access that memory indirectly. Pointers to ROM can also be stored.
### Registers
  There are no registers in BVM. I experimented with the idea of virtual registers, but since the registers were just stored in RAM, it didn't seem necessary.
## Performance
  Blixate VM is programmed in the C programming-language. Here is BVM compared to 3 other languages:
  - Python and JavaScript are entirely interpreted, and the source code is read everytime the code is run.
  - Java still uses class-names, which adds more bytes to be read at runtime.
  - C# must compile the code at runtime, which negatively impacts performance.

  Blixate VM is not as good as programs that are compiled to machine code. But since the BVM code is similar to machine code, the conversion from a BVM executable to a OS executable isn't too difficult if you know what you're doing.
## Security
  Running programs inside the VM doesn't mean they are more secure if BVM has a security issue. You should always have some level of caution when running code that you haven't wrote, and don't trust the individual that wrote the code.
  
  But, hackers and malicous programmers will have a much harder time writing viruses and malicous software. The security of a VM means that none of the code the bad people write will be executed directly to the machine, instead, it can be filtered. The VM can be locked down, so that certain operations are completely impossible.
  This only applies to exploits and security on BlixateVM, and not exploits generated by poorly written executables for BVM.
### Sandbox and Tools
  In order to make sure that malicous code or exploits cannot slip through the cracks, simple anti-malware tools can be developed to log system calls and dangerous methods. This could also help with debugging and patching security exploits.
### Anti-Malware
  Implementing anti-malware into a Blixate VM program is difficult, but this is a requirement to prevent malware from infecting machines. Since the anti-malware will never be perfect. If malware is developed, patching the exploit is ever-more easy than installing an OS update.
### Decompiling
  Although, decompilation tools might be made, there will be a way to make the bytecode more and more cluttered and obfuscated. I'm thinking a
  licensed instruction set, which will have different types of obfuscation and instructions, and be much harder to decompile. Since the code shouldn't contain method names and just instructions, this should make decompilation hard, but compilation is a bit more difficult.
## Control
  The code you write is the code that gets executed, and you can have full control over the executable, excluding for malicious purposes.
  
  The heavy-lifting like class implementation, functions, variables, and other programming features should be done by the programmer, but writing a compiler for these features is a better solution than writing an assembler and doing it by hand everytime you need to make a class. Blixate VM will have features to help with these abstract concepts, such as a way to copy an amount of bytes to a different address.
