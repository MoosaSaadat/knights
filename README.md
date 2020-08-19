![build-passing](https://img.shields.io/badge/Build-passing-success?style=flat-square)
![test-passing](https://img.shields.io/badge/Tests-passing-success?style=flat-square)
[![made-with-python](https://img.shields.io/badge/Made%20with-Python-informational?style=flat-square)](https://www.python.org/)


# Knights
### Harvard CS50's Introduction to Artificial Intelligence with Python (Project 1)
This program infers using propositional rule on the given knowledge base

## Description
In this project, we're required to build knowledge bases that can be used to infer missing information. Specifically, **Knights & Knaves** problems are used in this project. Such as, *A* says "I am both a knight and a knave" our program will output that *A* is a *knave*. We provide the available information using propositional logics: `OR`, `AND`, `NOT`, `IMPLICATION`, `BICONDITIONAL` in a single knowledge base. Then, our program performs **model_checking** algorithm which goes through all the possibilities to find if the given knowledge base entails the conclusion.

## Example
Let's say we have a single piece of information:
```
A says "I am both a knight and a knave."
```
We will encode it using propositional logic in the following knowledge base.
**Knowledge base:**
```
AKnight = Symbol("A is a Knight")
AKnave = Symbol("A is a Knave")

knowledge = And(
    And(Or(AKnight, AKnave), Not(And(AKnight, AKnave))),
    Biconditional(And(AKnight, AKnave), AKnight),
)
```
**Output:**
```
A is a Knave
```
**Explanation:**

First of all, we encode the possible outputs into *Symbols* which can be used in propositional logic:
```
AKnight = Symbol("A is a Knight")
AKnave = Symbol("A is a Knave")
```
Then, we encode the general rule of *Knights & Knaves* problem which is that a person can be either a *knight* or a *knave* but *not* both. This can be represented by an Exclusive OR (`XOR`) statement:
```
And(Or(AKnight, AKnave), Not(And(AKnight, AKnave)))
```
Then, we add the given information with a `BICONDITIONAL` statement that A is a knight if and only if what he says is true:
```
Biconditional(And(AKnight, AKnave), AKnight)
```
Finally, we encode these two together using an `AND` statement and assign it to our knowledge base:
```
knowledge = And(
    And(Or(AKnight, AKnave), Not(And(AKnight, AKnave))),
    Biconditional(And(AKnight, AKnave), AKnight),
)
```
We get the above mentioned output because we know that a person can be either a knave or a knight. So, if A says that he is both, it means he is lying and, therefore, he is a knave.
