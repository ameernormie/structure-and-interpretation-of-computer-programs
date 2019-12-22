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

A powerful programming language must have these elements in it.

- Numbers and arithmetic operations are primitive data and procedures.
- Nesting of combinations provides a means of combining operations.
- Definitions that associate names with values provide a limited means of abstraction.

Now we will learn about procedure definitions, a much more powerful abstraction technique by which a compound operation can be given a name and then referred to as a unit.
The general form of a procedure definition is
`(define (<name> <formal parameters>) <body>)`

### The Substitution Model for Procedure Application

To evaluate a combination whose operator names a compound procedure, the interpreter follows much the same process as for combinations whose operators name primitive procedures. That is, the interpreter evaluates the elements of the combination and applies the procedure (which is the value of the operator of the combination) to the arguments (which are the values of the operands of the combination).

We can assume that the mechanism for applying primitive procedures to arguments is built into the interpreter. For compound procedures, the application process is as follows:

- To apply a compound procedure to arguments, evaluate the body of the procedure with each formal parameter replaced by the corresponding argument.

To illustrate this process, let's evaluate the combination
`(f 5)`
where f is the procedure `(define (square x) (* x x))`. We begin by retrieving the body of f:

`(sum-of-squares (+ a 1) (* a 2))`
Then we replace the formal parameter a by the argument 5:
`(sum-of-squares (+ 5 1) (* 5 2))`
Thus the problem reduces to the evaluation of a combination with two operands and an operator sum-of-squares.Evaluating this combination involves three subproblems. We must evaluate the operator to get the procedure to be applied, and we must evaluate the operands to get the arguments. Now `(+ 5 1)` produces `6` and `(* 5 2)` produces `10`, so we must apply the sum-of-squares procedure to `6` and `10`. These values are substituted for the formal parameters x and y in the body of sum-of-squares, reducing the expression to
`(+ (square 6) (square 10))`
If we use the definition of square, this reduces to
`(+ (* 6 6) (* 10 10))`
which reduces by multiplication to
`(+ 36 100)`
and finally to
`136`

The process we have just described is called the **substitution model** for procedure application.

### Conditional Expressions and Predicates

### Example: Square Roots by Newton's Method

### Procedures as Black Box Abstractions
