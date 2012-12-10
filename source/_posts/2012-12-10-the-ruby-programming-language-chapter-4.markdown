---
layout: post
title: "The Ruby Programming Language Chapter 4"
date: 2012-12-10 15:59
comments: true
external-url: 
categories: Reading
tags: Ruby
---

### Keyword Literals

* `__FILE__`: string that names the file that the Ruby interpreter is executing.

* `__LINE__`: integer that specifies the line number within `__FILE__` of the current line of code.

* `__ENCODING__`: encoding of the current file. (Ruby 1.9)

### Uninitialized Variables

* Class variables: Error

* Instance variables: Returns `nil`

* Global variables: Returns `nil`

* Local variables: Error, usually.

### Constants

* Like global variables, constants can be used anywhere in a Ruby program without regard to scope.
``` ruby
CM_PER_INCH = 2.54  # Define a global constant.
CM_PER_INCH         # Refer to the constant.
::CM_PER_INCH       # A better way to refer to a global constant.
```

* UNLIKE global variables, constants can be defined by classes and modules and therefore have qualified names, e.g. `Math::PI`


### Method Invocations

* The value of a method invocation expression is the value of the last evaluated expression in the body of the method.

* Ruby objects encapsulate instance variables but expose only methods to the outside world.


### Assignments

* Assignment to a constant that already exists causes warning, but it actually **WILL** be executed. That means, *Constants are not really constant*.

* Ruby do not create a constant until the assignment is executed; however, Ruby *admit* the existance of a variable even if its assignment is not executed but only seen by Ruby interpreter.


