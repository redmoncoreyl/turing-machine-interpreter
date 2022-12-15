# Turing Machine Interpreter
This project implements an interpreter which can read a [turing machine](https://wikipedia.org/wiki/Turing_machine) program file, and display the tape contents at each step of processing.

## Getting started
First, compile the interpreter using this command:

```
g++ TuringMachineInterpreter.cpp -o turing
```

Then, to run a turing machine program, use this command:

```
[executable] [turing_machine_program_file]
```

There are sample turing machine programs in `./sample-machines`. Try running them and inspecting their source to see the kind of programs you can make.