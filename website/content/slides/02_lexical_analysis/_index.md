---
title: "Lexical Analysis"
date: 2018-09-30T13:45:53+03:00
draft: false
outputs: ["Reveal"]
---

# Lexical Analysis

> Converting the sequence of characters into a sequence of tokens for the
> language grammar.

---

## Theory

Programming languages have a finite set of keywords and rules for defining
numbers and identifiers.

These are most easily modeled as a regular language, so you can use regex and
DFA to recognize the tokens.

---
## Token

> A token is a single terminal symbol for the language grammar.

Tokens have type and value - i.e. `3.14` is a *number* and has value *3.14*

---
## Lexer

The lexer is the component of the compiler that does lexical analysis.

---
### How a lexer works

Reads the source character by character and tries to match that against the
regexes that define the language.

- Generally the longest match is preferred, so that `>=` is preferred over `>`.

---
### How to write a lexer

- generate it with a tool
- write one by hand

---
#### Generate a lexer

Tools use finite automata to recognize the tokens. When a token is recognized,
an user action code is executed, so that the type and the value of the token can
be stored.

---
#### Tools

- *flex* - uses tables for the states of the automaton
- *re2c* - generates code for the automaton in *C*
    - claims easier debuggability, but still the generated code is pretty
      complex

---
### Flex

    definitions
    %%
    rules
    %%
    user code

---

    %{
    /* include verbatim code */
    #include <math.h>
    %}

    DIGIT    [0-9]
    ID       [a-z][a-z0-9]*

    %%

---

    {DIGIT}+    {
                printf("An int:%s:%d\n", yytext, atoi(yytext));
                }

    {DIGIT}+"."{DIGIT}*        {
                printf("A float:%s:%g\n", yytext, atof(yytext));
                }

    if|then|while|do|for|function        {
                printf("A keyword:%s\n", yytext);
                }

    {ID}        printf("An identifier:%s\n", yytext);

---
# TODO: Sample input and output

---
## Writing a lexer by hand

# TODO: EXPAND

---
### Note

Some languages do not have/need grammar for compilation

- most assembler languages
- Languages based on reverse or prefix notation
- Forth

---
# ?

