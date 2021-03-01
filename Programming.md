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
