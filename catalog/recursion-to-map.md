# Recursion to Map

## Relates To

* [Recursion to Filter](recursion-to-filter.md)
* [Recursion to Reduce](recursion-to-reduce.md)

## Languages

All

## Motivation

In functional programming `map`, `reduce` and `filter` (and their synonyms)
become fundamental building blocks for your programs.

`map` is used when you want create a one-to-one mapping values in a collection
to new values via a transformation function.

Using `map` instead of a loop or recursive function creates more declarative
code. It describes the process which you are performing on the data, rather
than how you are implementing it.

It also separates to the responsibility of iterating over the collection from
the per item transformation rules. This increases reusability and
composability.

## Description

Any time where you have a recursive function or a loop which iterates over a
list and peforms a calcuation on each indiviual item, you have a good case to
use `map` instead.

The in order to refactor you need to extract the transformation function and
then pass that to `map` instead.

## Examples

### Clojure

#### Given

```clojure
(defn tax-multiplier [rate] (+ 1 (/ rate 100)))
(defn with-tax [rate amount] (* amount (tax-multiplier rate)))
```

#### Before

```clojure
(defn amounts-with-tax
  [tax-rate amounts]
  (if (empty? amounts)
      []
      (cons (with-tax (head amounts)) (amounts-with-tax tax-rate (tail amounts)))))
```

#### After

```clojure
(defn amounts-with-tax
  [tax-rate amounts]
  (map (partial with-tax tax-rate) amounts))
```
