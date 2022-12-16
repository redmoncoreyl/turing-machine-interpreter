# Turing Machine Interpreter
This project implements an interpreter which can read a [turing machine](https://wikipedia.org/wiki/Turing_machine) program file and display the tape contents at each step of processing.

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

## Writing your own turing machine
To write your own turing machine program, open up a text editor and start by writing the four sections you need:

```
transitions:

accepting:

rejecting:

input:

```

To learn more about what these sections refer to, see the __Formal definition__ section.

### Transitions:
Format your transitions like so:

```
q[start_state]:[start_character]/[output_character],[r_or_l]-q[end_state]
```
For example,  `q0:a/b,r-q2` would mean that if the execution is instate `q0` and the tape head points to  `a`, replace it with a `b`, move the head right, and move to state `q2`.

State identifiers can be any number. Read and write characters can be any ASCII character.

### Accepting:
This section is the list of accepting states. For example:

```
accepting:
q5
q8
```

The above example would mean that if the execution ever reaches state `q5` or `q8`, it would terminate and print `Accepted` to the terminal.

### Rejecting:
This section is the list of rejecting states. For example:

```
rejecting:
q9
q11
```

The above example would mean that if the execution ever reaches state `q9` or `q11`, it would terminate and print `Rejected` to the terminal.

### Input:
This section is how the tape will be initialized. For example:

```
input:
abbc
```

The above example would initialize the tape to the following value:

```
|abbc|||||||||||||||||||||||||||||||||||||||||||||
```

The decision was made to place the input in the second position, because some programs benefit from having a little space to the left of input.

The rest of the spaces are filled with `|` which can be read and manipulated by the turing machine like any other character

## Formal definition
A turing machine follows a set of rules to manipulate the contents of a *tape*. It is possible to construct a turing machine which implements any computer algorithm.

### The tape
Think of the *tape* as both the input and the memory of the program. With the interpreter included here, the *tape* is 50 characters long, though a true turing machine can have an infinitely long *tape*. Below is an example of how the *tape* is displayed by the interpreter:

```
|ababbabbaba||||||||||||||||||||||||||||||||||||||
```

The `|` symbol represents undefined data, though it is just like any other character: it can be manipulated the same as letter characters.

### The head
At any step of the execution, their is a *head* which points to one of the loctions on the tape. With the interpreter included here, the *head* points to the first character in the tape, which is always a `|` character. (More on that in the Input section below.)

### The states
At any step of the execution, the program is in one *state*. The *states* are numbered. The *state* is not visable during execution. With the interpreter included here, the initial *state* is `q0`.

### The transitions
At any step of the execution, the program will use a *transition* rule.

Which rule is used depends on:
1. the current *state* 
2. the character at the location pointed to by the *head*

When executing a rule:
1. the character at the *head* will be overwritten
2. the *head* will move one position to the right or left
3. the *state* may change.

### Special states: accepting and rejecting
Some *states* are *accepting* - if the execution arrives at any such *state*, the program is terminated, and the acceptance is returned.

Some *states* are *rejecting* - if the execution arrives at any such *state*, the program is terminated, and the rejection is returned.

### The input
The *input* is the initial value of the *tape*. With the interpreter included here, the *input* is placed in the second position of the *tape*. All other *tape* locations are initialized to `|`.