---
layout: post
title: "The Ruby Programming Language- Chapter 3"
date: 2012-11-26 21:34
comments: true
external-url: 
categories: Reading
tags: Ruby
---

# Datatypes and Objects


All Ruby values are objects.

The `Integer` class has two sub-classes: `Fixnum`(within 31 bits) and `Bignum`(arbitrary size).  
Operations on `Fixnum` or `Bignum` can have transparent conversion of results between the two classes.

`BigDecimal`(provided by Ruby standard library) represents real numbers with arbitrary precision, using a decimal representation rather than a binary representation.

### Number literal

Underscores may be inserted into literals, sometimes used as a thousands separator:

``` ruby
1_000_000_000    # One billion
```

Representations other than base 10:

``` ruby
0377        # Octal
Ob1111_1111 # Binary
0xFF        # Hexadecimal
```

For floating-point literals, digits must appear before AND after the decimal point.  
You CANNOT simply write `.1`; you must write `0.1` explicitly.

### Arithmetic in Ruby

Since Ruby automatically converts between `Fixnum` and `Bignum`, integer arithmetic in Ruby never overflows.  
Floating-point numbers overflow normally just like many other languages.

Ruby use `**` operator for exponentiation. Exponents need NOT be integers.  
When multiple exponentiations are combined into a single expression, they are evaluated from right to left. Thus, `4**3**2` is the same as `4**9`, not `64**2`.

Integers can be operated by bit-manipulation operators: `~, &, |, ^, <<, >>`.

Integers can be treated as arrays to query(but not set) individual bits:
``` ruby
even = (x[0] == 0)    # A number is even if the least-significant bit is 0
```

