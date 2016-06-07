# Recursion to Filter

## Relevant To


* Replace Loop with Collection Closure Method
* Replace Temp with Chain

## Relates To

* Recursion to Map
* Recursion to Reduce
* Tail Call Optimise Recursion

## Languages

All

## Motivation

Selectively filter a list of items into a new, smaller list of items, based
on defined criteria, in the form of a boolean statement or function. The main benefit
of this approach is it separates the predicate logic from the filtering code, providing
more opportunity for function reuse and composability. It describes the action rather
than the implementation of the action, improving legibility. Also it is not restricted
by stack size in languages where tail call recursion is not supported.

## Description

The filter takes a function (called a predicate) that is passed each element from
the original list. If the function returns `true` then that item is included in
the new list. If it returns false then that item is not included.
This refactoring can be identified when you have a recursive function that does some
form of inline filtering, possibly along with other manipulation. Once identified,
the filtering logic can be extracted out to an anonymous function or another function.
This is an immutable operation, returning a new list and not affecting the original.

## Examples

### Haskell

#### Given

```haskell
numbers = [1, 6, 3, 5, 8, 67, 43, 4, 6, 8]
```

#### Before

```haskell
-- tail recursion
evenNumbersOnly :: Integral a => [a] -> [a]
evenNumbersOnly [] = []
evenNumbersOnly (x:xs) = if even x
                         then x : evenNumbersOnly xs
                         else     evenNumbersOnly xs

evenNumbers = evenNumbersOnly numbers
```

#### After

```haskell

evenNumbers = filter even numbers
```
