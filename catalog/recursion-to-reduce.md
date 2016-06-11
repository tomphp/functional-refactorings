# Recursion to Reduce

## Relates To

* [Recursion to Filter](recursion-to-filter.md)
* [Recursion to Reduce](recursion-to-reduce.md)

## Languages

All

## Motivation

In functional programming `map`, `reduce` and `filter` (and their synonyms)
become fundamental building blocks for your programs.

`reduce` is used when you want reduce the values in a list down to a single
value via some calculation.

Using `reduce` instead of a loop or recursive function creates more declarative
code. It describes the process which you are performing on the data, rather
than how you are implementing it.

It also separates to the responsibility of iterating over the collection from
the calcuation rule. This increases reusability and composability.

## Description

Any time where you have a recursive function or a loop which iterates over a
list and to calculate a single value, you might have a good case to use
`reduce` instead.

The in order to refactor you need to extract the transformation function and
then pass that to `map` instead.

## Examples

### Clojure

#### Before

```clojure
(defn total-amount
  [item-amounts]
  (if (empty? item-amounts)
      0
      (+ (head item-amounts) (order-total (tail items)))))
```

#### After

```clojure
(defn total-amount [item-amounts] (reduce + 0 item-amounts))
```
