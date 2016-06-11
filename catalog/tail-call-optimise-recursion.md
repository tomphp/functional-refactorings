# Tail Call Optimise Recurssion

## Relates To

* [Recursion to Map](recursion-to-map.md)
* [Recursion to Filter](recursion-to-filter.md)
* [Recursion to Reduce](recursion-to-reduce.md)

## Languages

Languages which support tail call optimisation.

## Motivation

This refactoring is slightly different to all the others. Rather than doing
this for clarity, maintainability or extensibility, this is done to come over a
limitation of the language implementation - i.e. having a fixed stack size.

Often, the most obvious implementation of a recursive algorithm generates a
Stack Overflow error when the number of iterations exceeds the stack size. With
languages which support tail call optimisation, these recursive functions can
be re-written so that the stack size does not limit them.

## Description

For a function call to not use up an entry on the stack, it must be in the tail
call position. That is, no other operations must happen after it is called in
the calling function.

To achieve this, an accumulator value which stores all previous calculations
needs to be passed down the stack.

Performing this refactoring brings you one step closer to using a map or reduce
instead. Therefore, before performing this refactoring you should consider
using them instead.

## Examples

### Clojure

#### Before

```clojure
(defn factorial [n]
 (if (= n 1)
     1
     (* n (factorial (dec n))

```

When `n` != 1 in this example, the order of execution goes like this:
1. Get a decremented value of `n`
2. Call `factorial` with the decemented value of `n`
3. Multiple the result by `n`

Therefore, the call to factorial is not in the tail call position because the
multiplication happens afterwards.

#### After
```clojure
(defn factorial [n]
 (loop [current n
        accumulator 1]
  (if (= n 1)
      accumulator
      (recur (dec current) (* current accumulator)))))

```

Clojure has a [loop](https://clojuredocs.org/clojure.core/loop) macro and
[recur](https://clojuredocs.org/clojure.core/recur) special form which are used
specifically to perform tail call optimised recursions.
