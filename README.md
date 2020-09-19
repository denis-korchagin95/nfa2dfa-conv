# FSMCONV
fsmconv is a command-line tool for converting FSA from one to another representation.

## Features

  1. Transform an NFA or an epsilon-NFA to a DFA
  2. **(in development)** Minimization of DFA
  3. **(in development)** Transform an epsilon-NFA to an NFA
  4. **(in development)** Unite many initial states of FSM to one in output FSM

## Installation

You can install it by the following commands:

```bash
git clone https://github.com/denis-korchagin95/fsmconv.git
cd fsmconv
sudo make install
```

You also can remove the program by the next command:

```bash
sudo make uninstall
```

If you don't want to install it to you user-space, you will use it locally by next command:

```bash
make build
./bin/fsmconv [arguments...]
```

## Language

It is a native language to be parsed by this program.

Each statement must be ends by semicolon character.

The rules of FSA have to be written by next format: `STATE to STATE by CHARACTERS` or `STATE -> STATE by CHARACTERS`. 
For example `q0 -> q1 by 'a'`.

To mark some states as initial or finished you can use directives 'start' or 'end':

`start q0;` or `end q1, q2;`

There is a special character that can be written by `@epsilon` to give the opportunity to write epsilon-NFA rules.

You can comment out some lines putting the `#` character at the beginning of the line.

Example:

```
# An nfa FSM example
start A;
end B;

A to A by 'a', 'b';
A to B by 'b';
A to B by 'c', 'a';
B to C by @epsilon;
```

[The full grammar in BNF](./lang-grammar.txt)

## Usage

```
Usage: file [options]

OPTIONS
        --print-only
                Print only the given FSM and exit.
        --format=[native|dot] (native by default)
                Print the FSM in a given format, where format can be one of 'native', or 'dot'.
```

## Example

This command will print out an FSM in dot format.

```
fsmconv nfa.txt --format=dot
```

The output of this command may be:

```dot
digraph dfa {
        s0 [label="State 0", shape=tripleoctagon];
        s0 -> s0 [label="1"];
        s0 -> s0 [label="0"];
}
```
