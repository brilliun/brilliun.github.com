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

## Number literal

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

## Arithmetic in Ruby

Since Ruby automatically converts between `Fixnum` and `Bignum`, integer arithmetic in Ruby never overflows.  
Floating-point numbers overflow normally just like many other languages.

Ruby use `**` operator for exponentiation. Exponents need NOT be integers.  
When multiple exponentiations are combined into a single expression, they are evaluated from right to left. Thus, `4**3**2` is the same as `4**9`, not `64**2`.

Integers can be operated by bit-manipulation operators: `~, &, |, ^, <<, >>`.

Integers can be treated as arrays to query(but not set) individual bits:
``` ruby
even = (x[0] == 0)    # A number is even if the least-significant bit is 0
```

## String Literals

`String` in Ruby is mutable. Each time Ruby encounters a string literal, it creates a new object.  
Therefore, for efficiency, you should avoid using literals within loops.

### Single-quoted string literals

* The simplest  string literal.

* Backslash can only escape backslash and single-quote.

* To break a long single-quoted string literal across multiple lines without embedding newlines in it, use the following expression:

``` ruby
long_string = 
'These two literals are '\
'concatenated into one by the interpreter.'
```

### Double-quoted string literals

* More flexible than single-quoted literals.

* Support quite a few backslash escape sequences, including Unicode characters(`\u`).

* Arbitrary Ruby expressions can be included, beginning with the \# character and enclosed within curly braces:

``` ruby
"360 degrees = #{2*Math::PI} radians"
```

*When the expression to be included is simply a reference to a global($), instance(@), or class(@@) variable, the curly braces may be omitted:*

``` ruby
$my_var = 'hello'
"#$my_var world"
```
* Double-quoted string literals may span multiple lines with line terminators as part of them, unless escaped with a backslash:
``` ruby
"This string literal
has two lines \
but is written on three."
```

### Aribitrary delimiters for string literals

* `%q` represents the beginning of a string literal that follows single-quoted string rules.

* `%Q` represents the beginning of a string literal that follows double-quoted string rules.

* The first character following `q` or `Q` is the delimiter character.


### Backtick command execution

* When text is enclosed in backticks, that text is treated as a double-quoted string literal. Therefore, arbitrary Ruby expressions can be included into the string:
``` ruby
if windows
	listcmd = 'dir'
else
	listcmd = 'ls'
end
listing = `#{listcmd}`
```

* The content of that literal is executed as an shell command, and returns the output as a string.

* A generalized quote syntax in place of backticks will be `%x`



## String Operators

* The `+` operator concatenates two strings and returns the result as a new `String` object. However, not like in Java, the `+` operator doesn't  automatically convert its operand to a string:
``` ruby
"Hello, No." + number.to_s
```
In such cases, string interpolation is simpler:
``` ruby
"Hello, No.#{number}"
```

* Different from `+`, the `<<` operator appends its second operand to its first; it alters the first operand rather than creating and returning a new object.

* `==` and `!=` compare strings for equality and inequality. Two strings are equal if and only if they have the same length and all characters are equal.

## Accessing Characters and Substrings

* Access and alter the string literal using square-bracket array-index operator `[]`.

* Positive array-index specifies a 0-based position from the beginning of the string.

* Negative array-index specifies a 1-based position from the end of the string.

* Ruby does not throw an exception if you try to access a character beyond the range of the string; it simply returns `nil` instead.

* When altering the string at lefthand side, the righthand side of the assignment statement can be any string:
``` ruby
s = "hello"
s[-1] = ""      # s is now "hell"
s[-1] = "p!"    # s is now "help!"
```
* When dealing with substrings, use two comma-separated operands; the first one specifies an index and may be negative, the second one specifies a length and must be non-negative.
``` ruby
s = "hello"
s[0,2]          # "he"
s[-1,1]         # "o"
s[0,0]          # ""
s[0,10]         # "hello"
s[s.length,10]  # ""
s[s.length+1,1] # nil
s[1,-1]         # nil
```
* When altering a string using comma-separated operands:
``` ruby
s = "hello"
s[0,1] = "H"             # "Hello"
s[s.length,0] = " world" # "Hello world"
s[5,0] = ","             # "Hello, world"
s[5,6] = ""              # "Hellod"
```

* You can also index a string using `Range` object(`[a..b]`), with two integers specifies two indexes.

* It is also possible to index a string using a target string. The return value is the **first** substring that matches the target string:
``` ruby
s = "hello"
s["l"] = "L"    # "heLlo"
```

* You can index a string using regular expression. The result is the first substring that matches the pattern.

## Iterating Strings

* From Ruby 1.9, there are three clearly named string iterators: `each_byte`, `each_char`, and `each_line`. For example:

``` ruby
s = "hello"
s.each_char {|x| print "#{x} "}    # Prints "h e l l o".
```
