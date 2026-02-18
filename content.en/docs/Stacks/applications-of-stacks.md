---
title: Applications of Stacks
weight: 4
---

Stacks are often used in evaluation of arithmetic expression. An arithmetic expression consists of operands and operators. The operands can be constant or variables. The operators used in an arithmetic expression can be `+`, `-`, `*` and `/`.

While writing an arithmetic expression, the operator is placed between two operands as shown in the examples below.

```
A + B * C
A * B - C
A + B / C - D
A $ B + C
```

This way of representing arithmetic expressions is called **infix notation**. While evaluating an infix expression usually the following operator precedence is used:

| Priority | Operators |
|----------|-----------|
| Highest | Exponentiation ($) |
| Next highest | Multiplication (*) and Division (/) |
| Lowest | Addition (+) and Subtraction (-) |

If we wish to override these priorities we can do so by using a pair of parentheses as shown below.

```
(A + B) * C
A * (B - C)
(A + B) / (C - D)
```

The expressions within a pair of parentheses are always evaluated earlier than other operations.

To make evaluation of an arithmetic expression easy, a polish mathematician Jan Lukasiewicz suggested a notation called **Polish notation**. As per this notation, an expression in infix form can be converted to either **prefix** or **postfix** form and then evaluated. In **prefix notation** the operator comes before the operands. In **postfix notation**, the operator follows the two operands. These forms are shown below.

| Infix | Prefix | Postfix |
|-------|--------|---------|
| A + B | + A B | A B + |

The prefix and postfix expressions have three features:
- The operands maintain the same order as in the equivalent infix expression
- Parentheses are not needed to designate the expression unambiguously.
- While evaluating the expression the priority of the operators is irrelevant.

The stack data structure is used while carrying out the conversion of an expression given in one form to another.

---