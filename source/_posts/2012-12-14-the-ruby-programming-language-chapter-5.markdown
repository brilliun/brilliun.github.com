---
layout: post
title: "The Ruby Programming Language Chapter 5"
date: 2012-12-14 17:03
comments: true
external-url: 
categories: Reading
tags: Ruby
---

## Conditionals

In conditional expressions

* `nil` are equivalent to `false`

* Any other value are equivalent to `true`

### if

#### Return Value

The return value of an `if` statement is the value of the last expression in the code that was executed, or `nil` if no code was executed. Eg.:
``` ruby
name = if    x == 1 then "one"
       elsif x == 2 then "two"
	     elsif x == 3 then "three"
       elsif x == 4 then "four"
       else              "many"
       end
```


#### if As a Modifier

Instead of writing:
``` ruby
if message then puts message    # Output message, if it is defined
```
we can simply write:
``` ruby
puts message if message
```

However, we have to pay attention to the low precedence of `if` modifier.
The following two expressions have different behaviours:
``` ruby
y = x.invert if x.respond_to? :invert   # Equivalent to (y = x.invert) if x.respond_to? :invert)
y = (x.invert if x.respond_to? :invert)
```

### unless

`unless` is the opposite of `if`: it executes code only if an associated expression evaluateds to `false` or `nil`. Their syntaxs are just the same, except for the `elsif` clause.


### case

``` ruby
name = case x
       when 1 then "one"
	     when 2 then "two"
	     when 3 then "three"
	     else "many"
	     end
```

**The comarisons are done using** `===` **operator.** (*see p.125*)

The main differences `case` statement in Ruby and `swith` statement in C-derived language are:

* No "fall-through" behaviour in `case` statement, multiple conditions are separated by comma.

* Don't have to be compile-time constants, arbitrary runtime expressions are acceptable in Ruby's `case` statement.



## Loops

### while and until

* `while`: Body code are executed if the conditional expression is anything other than `false` or `nil`.

* `until`: Body code are executed if the conditional expression is `false` or `nil`.

### while and until As Modifiers

``` ruby
x = 0
puts x = x + 1 while x < 10
```

``` ruby
a = [1, 2, 3]
puts a.pop until a.empty?
```

**The loop condition is evaluated first even though it is writtern after the loop body.**


