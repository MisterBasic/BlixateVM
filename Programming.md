# BCS: Blixate Compiled Script
## Grammar
  All lines of code should end with a semi-colon (";").
### Defining a module
  Every script file should be defined as a *Module*. The first line of the file should contain this:
  ```
  module MyModule;
  ```
  This defines the *Module* as "MyModule". An optional **Entry Point** can be specified:
  ```
  module MyModule start;
  ```
  This will set the **Entry Point** function to *start()*, which is *main()* by default.
### Import modules
  When using a function from a different module, the `using` keyword should be present before the name of the *Module*:
  ```
  using System;
  ```
  This will take the **System Module**, and allow all functions for the current module. A linker will take the name "System" and link it to a script file, which will be compiled along with the executable.
  If a specific function should be imported, like:
  ```javascript
  using System:output; // System is the module, output is the function
  ```
  Then the function can be used without specifying the *Module*, in this case `System.output("Hello, world!")` should be `output("Hello, world!")`
  A star can also be used to import all functions:
  ```
  using System:*;
  ```
  This is the same with sub-modules, which can be imported with a `.`
  ```
  using System.SubModule;
  ```
  When referencing a function or variable inside this sub-module, the name of the submodule should be used. In this case, `SubModule.someFunction()`
### Entry point
  The **Entry Point** is the point at which the program will start. This is symbolised with the *main()* function.
  ```javascript
  function main() {
    System.output("Hello, world!");
  }
  ```
### Functions
  The `function` keyword can be used to define a function.
  ```
  function add(a: int, b: int) int {
    return a + b;
  }
  ```
  The `main` function cannot be called, since an **Entry Point** is not a function.
### Variables
  Defining a variable is very simple:
  ```javascript
  var helloWorld = "Hello, world!";
  var hey: string = "Hey";
  var number: int = 42;
  ```
  The `var` keyword is used to create a variable. The name of the variable should always follow after `var`. Next, either a type or the value can be specified.
  Types should always be `var name: type;`, or `var name: type = "some value"`. If a type is not specified, then the type is `variant`.
  Types can also be classes, like:
  ```
  var myClass: MyObject();
  ```
  When creating a variable of a Object, then a type ***MUST*** be specified. The type becomes a constructor if there are brackets at the end of the type.
### Restricted variables, classes and functions
  Functions, variables, and classes can have a flag called "restricted" applied to them.
  ```
  module RestrictedExample;

  // This makes it so other files cannot use this variable, since they are out-of-scope
  restricted var someVariable: string;

  restricted class MyClass {
    restricted var someVar: int // Can only be edited inside this scope and lower, pretty much just this class.

    constructor(i: int) {
      this.someVar = i; // Allowed
    }
    
    function setSomeVar(i: int) int { // This function isn't restricted
      this.someVar = i; // Allowed
    }
  }

  restricted function myFunc() bool {
    return someVariable; // Allowed
  }

  // Main cannot have restricted applied to it, since it's technically not a function.
  function main() {
    myFunc(); // Allowed
    var classInstance: MyClass(10);
    classInstance.someVar = 15; // NOT ALLOWED
    classInstance.setSomeVar(15); // Allowed since setSomeVar() isn't restricted
    /* 
    If a module defines a global-variable as "restricted," i cannot be used.
    
    For example:
     */
    System.stdout.write("Hello, world!"); // stdout is restricted, therefore cannot be accessed.
  }
  ```
  What this means for each type:
  - Function: The function can only be called in the local **Class** or **Module**
  - Variable: The variable can only be read or changed in the local **Class** or **Module**
    - **THIS IS NOT TO BE CONFUSED WITH LOCAL VARIABLES**
  - Class: The class can only be constructed in the local **Module**.
    - I'm not sure if accessing an object that is an instance of that class from a different module should count. Up for discussion :)
### Example
  ```
  module ExampleModule;
  
  using System;
  
  class ExampleClass {
    var classVariable: int;
    constructor(i: int) { // function constructor() is also valid.
      this.classVariable = i; // "this" is a references to the current object instance.
    }
  }
  
  function main() void {
    var myString: string = "Hello, world!";
    var example: ExampleClass(15);
    System.output(myString);
    System.output(example.classVariable); // System.output can also output numbers and stuff.
  }
  ```
# Blixate Virtual Machine vague details
## Function calls
  Function arguments are placed onto the stack prior to the call, but first the return address has to be put onto the stack. When calling a function, a seperate call-stack is used to push the return address. This fixes the problem of the return address being the top of the stack. When returning from a function, an address from this call stack is retrieved and then returned to. Parameters to a function call are pushed onto the stack prior, and placed into a temporary area in memory (local variable storage). These can then be accessed when needed.
  If this function is to call another function, and the called function returns, the previous temporary variable storage should still be fine. This can be done a variety of ways, but this is to make sure that nothing gets lost when calling functions inside functions.
## Entry Point
  The entry point is simply a ROM address. This is normally zero, since the first method is the first thing that should be run, but can change depending on if the method changes.
## Exiting a program
  Blixate VM always exits if the program returns while the call stack is empty.
# Why?
  BCS is a way of programming the BlixateVM using human-readable syntax. This style of language is familar to web-developers, who may want to do low-level operations with a language that isn't too low-level.
## Why is it similar to JavaScript?
  Most people are familar with JavaScript, since it's one of the most important programming languages in web development. But, JavaScript is an interpreted language, which leaves little room for speed. Any language that is compiled typically requires strict-typing, but since BCS runs in BlixateVM, all variables are just black boxes, and no type is stored with the variable. It's the compilers job to figure out what to do with the memory, and how to modify it.
## Is BCS the only language?
  No, more are planned. Here are a few that I plan to make:
- BLS (Stands for nothing): A high-level object-oriented programming language, with strict-typing and classes. Similar to Java instead of JavaScript.
- BLX (Stands for nothing): A lower-level modification tool for BLS.
- CMP (Compiled (Blixate) Machine Program): An assembly-like language that is directly-translated to BVM machine code.
## Why wouldn't I just use Java or JavaScript?
  **You can just use Java or JavaScript**: In fact, those languages are great for what they are used for! This isn't saying that "Java is terrible and you should never use it!" or the same with JavaScript. This isn't a replacement, I'm only using similar syntax because most developers and programmers are familar with them, and therefore makes writing programs much easier since new concepts are easier to learn if you already know the basics. Blixate Languages don't work in the browser, although the syntaxes are similar and can be converted, so they aren't replacements.
## Why would I use BCS over any other language?
  BCS is for programming Blixate VM, which can do a range of tasks inside of a sandbox environment. If you want to learn more about Blixate VM, [click here](https://github.com/MisterBasic/BlixateVM/blob/main/BlixateVM.md)
