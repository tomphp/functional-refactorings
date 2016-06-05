# Compose Nested Functions

## Relevant To

* Extract Method
* Composed Method Pattern
* Single Responsibility Principal

## Relates To

* [Compose Nested Functions](compose-nested-functions.md)

## Languages

Languages with higher-order functions

## Motivation

As a function gains complexity, its parts may get extracted out into named
functions creating a deep stack of function calls. In these situations, it
becomes the responsibility of the functions calling inner functions, to push
data down the call stack.

This has 2 negative properties:

1. Function have multiple responsibilities:
   * To perform their intended calculation.
   * To push data not intended for them down to the next function.
2. When the call stack gets deep, it is harder to comprehend.

## Description

Remove the unwanted responsibility from the functions, then compose them to
create a pipeline which transforms the data one step at a time.

## Examples

### Clojure

#### Before

```clojure
(defn tax-multiplier [rate] (+ 1 (/ rate 100)))
(defn with-tax [rate amount] (* amount (tax-multiplier rate)))

; item-amounts has the single responsibility of extracting the amount properties
; from the items.
(defn item-amounts [items] (map :amount items))

; item-amounts-with-tax passes the items down to item-amounts and then adds
; the tax to exact of the amounts in the result.
(defn item-amounts-with-tax
  [tax-rate item]
  (map (partial with-tax tax-rate) (item-amounts items)))

(defn order-total
  [tax-rate items]
  (sum (item-amounts-with-tax tax-rate items)))
```

#### After

```clojure
(defn tax-multiplier [rate] (+ 1 (/ rate 100)))
(defn with-tax [rate amount] (* amount (tax-multiplier rate)))

; This function is fine
(defn item-amounts [items] (map :amount items))

; item-amounts-with-tax had two responsibilies. We've now replaced with this
; function which solely adds tax to a list of amounts
(defn amounts-with-tax
  [tax-rate amounts]
  (map (partial with-tax tax-rate) amounts))

; Now order-total simply composes all the steps to be applied to the items in
; in the order - one at a time
(defn order-total
  [tax-rate items]
  (->> items item-amounts amounts-with-tax sum))
```
