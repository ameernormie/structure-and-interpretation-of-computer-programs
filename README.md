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
- [2 Procedures and the processes they generate](#procedures-and-the-processes-they-generate)
  - [2.1 Linear Recursion and Iteration](#linear-recursion-and-iteration)

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

**Applicative order versus normal order**
Normally the interpreter first evaluates the operator and operands and then applies the resulting procedure to the resulting arguments. This is not the only way to perform evaluation. An alternative evaluation model would not evaluate the operands until their values were needed. Instead it would first substitute operand expressions for parameters until it obtained an expression involving only primitive operators, and would then perform the evaluation.
If we used this method, the evaluation of
`(f 5)`
would proceed according to the sequence of expansions
`(sum-of-squares (+ 5 1) (* 5 2))`
`(+ (square (+ 5 1)) (square (* 5 2)) )`
`(+ (* (+ 5 1) (+ 5 1)) (* (* 5 2) (* 5 2)))`
followed by the reductions
`(+ (* 6 6) (* 10 10))`
`(+ 36 100)`
`136`

This gives the same answer as our previous evaluation model, but the process is different. In particular, the evaluations of (+ 5 1) and (_ 5 2) are each performed twice here, corresponding to the reduction of the expression
`(_ x x)`with x replaced respectively by`(+ 5 1)`and`(\* 5 2)`.

This alternative `fully expand and then reduce` evaluation method is known as **`normal-order evaluation`**, in contrast to the `evaluate the arguments and then apply` method that the interpreter actually uses, which is called applicative-order **`evaluation`**.

### Conditional Expressions and Predicates

### Example: Square Roots by Newton's Method

There is an important difference between mathematical functions and computer procedures.
As a case in point, consider the problem of computing square roots. We can define the square-root function as
`sqrt(x) = the y such that y >= 0 and y(square) = x`
This describes a perfectly legitimate mathematical function. We could use it to recognize whether one number is the square root of another, or to derive facts about square roots in general. On the other hand, the definition does not describe a procedure. Indeed, it tells us almost nothing about how to actually find the square root of a given number
`The contrast between function and procedure is a reflection of the general distinction between describing properties of things and describing how to do things, or, as it is sometimes referred to, the distinction between declarative knowledge and imperative knowledge. In mathematics we are usually concerned with declarative (what is) descriptions, whereas in computer science we are usually concerned with imperative (how to) descriptions.`

### Procedures as Black Box Abstractions

## Procedures and the processes they generate

We know how to to write procedures and combine procedures to build compound procedures. But that is not enough to enable us to say that we know how to program. `Our situation is analogous to that of someone who has learned the rules for how the pieces move in chess but knows nothing of typical openings, tactics, or strategy.` We don't yet know the common patterns of usage in the domain. We lack the knowledge of which moves are worth making (which procedures are worth defining). We lack the experience to predict the consequences of making a move (executing a procedure).
**The ability to visualize the consequences of the actions under consideration is crucial to becoming an expert programmer, just as it is in any synthetic, creative activity.**

A procedure is a pattern for the local evolution of a computational process. It specifies how each stage of the process is built upon the previous stage. We would like to be able to make statements about the overall, or global, behavior of a process whose local evolution has been specified by a procedure. This is very difficult to do in general, but we can at least try to describe some typical patterns of process evolution.

In this section we will examine some common `shapes` for processes generated by simple procedures. We will also investigate the rates at which these processes consume the important computational resources of time and space.

### Linear Recursion and Iteration

#### Linear Recursive Process

```
Linear Recursive process for calculating 6!

(factorial 6)
(* 6 (factorial 5))
(* 6 (* 5 (factorial 4)))
(* 6 (* 5 (* 4 (factorial 3))))
(* 6 (* 5 (* 4 * (3 (factorial 2)))))
(* 6 (* 5 (* 4 * (3 * (2 (factorial 1))))))
(* 6 (* 5 (* 4 * (3 * (2 * 1)))))
(* 6 (* 5 (* 4 * (3 * 2))))
(* 6 (* 5 (* 4 * 6)))
(* 6 (* 5 * 24))
(* 6 * 120)
(720)

```

We begin by considering the factorial function, defined by

`n! = n.[(n-1).(n-2).(n-3)... 3.2.1] = n.(n-1)!`

There are many ways to compute factorials. One way is to make use of the observation that n! is equal to n times (n - 1)! for any positive integer n:

Thus, we can compute n! by computing (n - 1)! and multiplying the result by n. If we add the stipulation that 1! is equal to 1, this observation translates directly into a procedure:

```
(define (factorial n)
  (if (= n 1)
      1
      (* n (factorial (- n 1)))))
```

#### Linear Iterative Process

Now let's take a different perspective on computing factorials. We could describe a rule for computing n! by specifying that we first multiply 1 by 2, then multiply the result by 3, then by 4, and so on until we reach n. More formally, we maintain a running product, together with a counter that counts from 1 up to n. We can describe the computation by saying that the counter and the product simultaneously change from one step to the next according to the rule

**product ← counter · product
counter ← counter + product**

and stipulating that n! is the value of the product when the counter exceeds n.

```
Linear Iterative process for calculating 6!

(factorial 6)
(fact-iter 1 1 6)
(fact-iter 1 2 6)
(fact-iter 2 3 6)
(fact-iter 6 4 6)
(fact-iter 24 5 6)
(fact-iter 120 6 6)
(fact-iter 720 7 6)
(720)

```

```
(define (factorial n)
  (fact-iter 1 1 n))

(define (fact-iter product counter max-count)
  (if (> counter max-count)
      product
      (fact-iter (* counter product)
                 (+ counter 1)
                 max-count)))
```

#### Comparison (Iterative vs Recursive)
