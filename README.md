# Struture and interpretation of Computer Programs

### Table of Contents

- [1 The Elements of Programming](#the-elements-of-programming)
  - [1.1 Expressions](#expressions)
  - [1.2 Naming and the environment](#naming-and-the-environment)
  - [1.3 Evaluating combinations](#evaluating-combinations)
  - [1.4 Compound Procedures](#compound-procedures)
  - [1.5 The Substitution Model for Procedure Application](#the-substitution-model-for-procedure-application)
  - [1.6 Conditional Expressions and Predicates](#conditional-expressions-and-predicates)
  - [1.7 Example: Square Roots by Newton's Method](#expressions)
  - [1.8 Procedures as Black-Box Abstractions](#procedures-as-black-box-abstractions)

`primitive expressions, which represent the simplest entities the language is concerned with`
`means of combination, by which compound elements are built from simpler ones, and`
`means of abstraction, by which compound elements can be named and manipulated as units.`

## The Elements of Programming:

### Expressions

    (+ 2.7 10)

Expressions such as these, formed by delimiting a list of expressions within parentheses in order to denote procedure application, are called combinations.

### Naming and the environment

### Evaluating combinations

**To evaluate a combination, do the following**

1. Evaluate the subexpressions of the combination.
2. Apply the procedure that is the value of the leftmost subexpression (the operator) to the arguments that are the values of the other subexpressions (the operands).

`(* (+ 2 (* 4 6)) (+ 3 5 7))`
Requires that the evaluation rule be applied to four different combinations.

`We take care of the primitive cases by stipulating that:`

1. the values of numerals are the numbers that they name
2. the values of built-in operators are the machine instruction sequences that carry out the corresponding operations
3. the values of other names are the objects associated with those names in the environment

We may regard the second rule as a special case of the third one by stipulating that symbols such as + and \* are also included in the global environment, and are associated with the sequences of machine instructions that are their `values`.

### Compound Procedures

### The Substitution Model for Procedure Application

### Conditional Expressions and Predicates

### Example: Square Roots by Newton's Method

### Procedures as Black Box Abstractions
