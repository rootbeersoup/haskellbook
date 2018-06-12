# Chapter 5: Types

## 5.2 What are types for?
* Haskell is essentially a syntactically sweet implementation of a pure lambda calculus.
* Type systems are designed to impose constraints which enfore correctness.
* Static typing means typechecking occurs at compile time.

## 5.3 How to read type signatures
When numeric values are typechecked, GHCi displays typeclass info instead of a concrete type. This is because the compiler doesn't know which numeric type a value is until it is declared or the compiler infers one. Declaring a concrete type for a numeric value beforehand will display the type properly.
```haskell
Prelude> :type 13
13:: Num p => p

-- Declare the concrete type:
Prelude> :type 13 :: Integer
13 :: Integer :: Integer

Prelude> let x = 13 :: Integer
Prelude> :type x
x :: Integer
```

### Understanding the function type

`->` is the type constructor for functions in Haskell. It's similar to other type constructors, except it takes arguments and has no data constructors. `->` contains an `infixr` prioirty of 0.

A function must have two arguments - one input and one result - in order to be valid function. *Functions are values*.

Reading the `fst` type signature:
```haskell
fst :: (a, b) ->   a
       [ 1  ] [2]  [3]
```

1. First parameter has the type `(a, b)` (tuple), which itself contains two arguments coinjoined by an infix operator.
1. The function type `->` has two parameters; `(a, b)` (input) and `a` (result).
1. The result; The same `a` from the input tuple, `(a, b)`.

We *know* `a` is the same type from `(a, b)` because the type signature of `fst` shows that nothing else happens between the input and output.

### Typeclass-constrained type variables

A typeclass-constrained variable is named for when we don't fully know the concrete type of a function e.g. `(+) :: Num a => a -> a -> a`. See: Polymorphic. Typeclass-constraints represent the maximum ambiguity a function could have.

To turn the number 15 into a conrete type of `Int`:
```haskell
Prelude> let fifteen = 15
Prelude> let fifteenInt = fifteen :: Int
Prelude> :type fifteenInt
fifteenInt :: Int

-- or

Prelude> let fifteen = 15 :: Int
Prelude> :type fifteen
fifteen :: Int
```
