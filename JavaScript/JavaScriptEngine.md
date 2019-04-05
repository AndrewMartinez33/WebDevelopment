# What is a JavaScript engine?
A JavaScript engine takes JS code and communicates with the computer and tells it what we want it to do. Some popular JavaScript engines are V8 engine (Google Chrome), Spider Monkey (Mozilla), Chakra (Microsoft), and many more.

# Interpreters vs Compilers
In programming there are generally two ways of coverting code to machine code. With an interpreter we translate and read the files line by line on the fly. A compiler translates the code we write ahead of time and compiles it down to something that the machine can understand.

## Interpreter Pros and Cons
Pros
* No compilation step before the code runs

Cons
* When you run the same code more than once, it can get really slow
* Does not optimize the code.

## Compiler 
Pros
* When it sees code the repeats, the compiler optimizes the code.

# JIT Compilers
A Just In Time compiler gives you the best of both worlds. It combines an interpreter and a compiler. Here is how it works:
* First we feed the the V8 engine the JavaScript code.
* Then, the engine parses that code and creates an AST, Abstract Syntax Tree.
* Then, that code goes through the Interpreter, which produces Bytecode that can be understood by the machine.
* Meanwhile, a Profiler monitors the code and sees where optimizations can be made.
* Now, as the code is running through the Interpreter, the profiler hands off the pieces of code that can be optimized to the Compiler.
* Then, the compiler takes the code, makes the optimization and inserts the optimized machine code back into the Bytecode.

The term, Just in Time, comes from the fact that the engine makes optimizations just as the code is running.