# Blixate VM
## Design
  Blixate VM is currently not released or completed. It is a virtual-machine which interprets bytecode into instructions. The design is to be fast, and
  simple to develop programs for, aswell as having full control. 
  
  REMEMBER: All of these are just ideas and hopes. Implementing all of this is a lot, but I want to make something- if i'm making anything, it's got to be good.
## Performance
  Blixate VM is programmed in the C programming-language. This allows fast speed, whilst not giving me a headache.
  
  These programs are on the "third" level, which is based on a system of:
  0. The CPU: Pure machine code.
  1. The Operating System: Helps the CPU run executable files.
  2. Blixate VM: Helps the operating system run Executable Blixate Programs
  3. Bytecode: Where your program sits.
  
  This means it's reasonably high-level, but not too high-level. Unlike Python or C#, all code is run as bytecode; which means that reading each instruction and executing
  it takes smaller amounts of time.
## Security
  Running programs inside the VM means that they are more secure.
### Malware
  Implementing anti-malware into a Blixate VM program is difficult, but this is a requirement to prevent malware from infecting machines. Since the anti-malware will never
  be perfect, there should always be caution with running programs from people you don't trust. If malware is developed, 
  patching the exploit is ever-more easy than installing a windows update.
  
  Malware isn't easy to develop inside of Blixate VM, but server-security attacks are still possible.
### Decompiling
  Although, decompilation tools might be made, there will be a way to make the bytecode more and more cluttered and obfuscated. I'm thinking a
  licensed instruction set, which will have different types of obfuscation and instructions, and be much harder to decompile.
## Control
  The code you write is the code that gets executed, and you can have full control over the executable, excluding for malicious purposes.
  
  The heavy-lifting like class implementation, functions, variables, and other programming features should be done by the programmer, but writing a compiler
  for these features is a better solution. Blixate VM will have features to help with these.
