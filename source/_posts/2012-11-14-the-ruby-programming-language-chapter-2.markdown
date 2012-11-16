---
layout: post
title: "The Ruby Programming Language - Chapter 2"
date: 2012-11-14 20:39
comments: true
categories: [Reading]
tags: [Ruby]
---


## Identifiers

Identifiers that begin with a captial letter A-Z are constants, and the Ruby interpreter will issue a warning (but not an error) if you alter the value of such an identifier.

### Punctuation in identifiers

``` ruby
$files        # A global variable
@data         # An instance variable
@@counter     # A class variable
empty?        # A boolean-valued method or predicate
sort!         # A mutator method that alter the object
timeout=      # A method invoked by assignment
```


## Whitespaces


### Newlines as statement terminators

Semicolons are not required to terminate statements. It can be omitted.

Without explicit semicolons, Ruby interpreter figure out on its own where statements end:

1. For a syntactically complete statement, Ruby uses the newline as the terminator;
2. If the statement is not complete, Ruby continues parsing the statement on the next line.
3. (For Ruby 1.9) If the first character on a line is a period(.), then the line is considered a continuation line.

Be careful about the "newline terminator" when your statement doesn't fit on a single line. 
For example:
```
total = x +    # Incomplete expression, parsing continues
  y            # Adds x and y and assigns the sum to total
```
While in another case:

```
total = x    # This is a complete expression
  + y        # A useless but complete expression
```

Escaping a line break with a blackslash can safely prevent unexpected terminating:

```
total = x \
  + y
```
