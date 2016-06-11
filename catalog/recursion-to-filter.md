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

In functional programming `map`, `reduce` and `filter` (and their synonyms)
become fundamental building blocks for your programs.

`filter` is used when you want to remove items from a list based on some
predicate test.

Using `filter` instead of a loop or recursive function creates more declarative
code. It describes the process which you are performing on the data, rather
than how you are implementing it.

It also separates to the responsibility of iterating over the collection from
the per item filtering rules. This increases reusability and composability.

## Description

This refactoring can be identified when you have a recursive function that does
some form of inline filtering, possibly along with other manipulation. Once
identified, the filtering logic can be extracted out to an anonymous or named
function.

The filter takes a function (called a predicate) that is passed each element
from the original list. If the function returns `true` then that item is
included in the new list. If it returns false, then that item is not included.


## Examples

### Haskell

#### Given

```haskell
numbers = [1, 6, 3, 5, 8, 67, 43, 4, 6, 8]
```

#### Before

```haskell
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
