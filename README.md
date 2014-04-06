libfun
======

Crazy Eddie's functional C++ library

This is mostly serving as a basis for my own experimentation with
functional programming in C++.  Use at your own risk.


#concepts

I'm following much of the Haskell language version of functional programming
with a few twists to make it more C++ like--for example overloading and 
functions with an undefined arity.

## function

* operator()
* operator(...)
* operator(tuple)
* eval(...)
* value()

### variadic function

Variadic functions ALWAYS return functions.  When you're at a terminal evaluation point
using `operator()` you must call `value()` to retrieve the result.  The `eval()` member
can be used to evaluate with `operator()` and retrieve the value.  This may additionally
avoid creating copies when the function parameters are `const&`.

## data variables

All data variables are also functions.

* operator() - returns *this
* value() - returns *this

## type constructors

* naming - start with capital letters.  Example: List

# operators

## Fundational

* add
* sub
* mul
* div
* eq
