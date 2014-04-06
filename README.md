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

## data variables

All data variables are also functions.

* operator() - returns *this
* value() - returns *this

## type constructors

* naming - start with capital letters.  Example: List
