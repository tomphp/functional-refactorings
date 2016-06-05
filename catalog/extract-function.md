# Extract Function

## Relevant To

* Extract Method
* Single Responsibility Principal

## Relates To

* [Compose Nested Functions](compose-nested-functions.md)

## Languages

All

## Motivation

As a function's expression gains complexity, it is behaviour becomes harder to
comprehend. Extracting a new, well named, function for different parts of that
function can significantly increase clarity.

Creating smaller functions, with a single responsibility, promotes more
opportunities for code reuse via composition.

## Description

Identify groups in the expression which perform a specific task, then extract
it to a new, well-named function.

## Examples

### Clojure

#### Before
```clojure
(defn order-total
  [tax-rate items]
  (* (sum (map :amount items)) (+ 1 (/ tax-rate 100))))
```

#### After
```clojure
(defn tax-multiplier [rate] (+ 1 (/ rate 100)))
(defn with-tax [rate amount] (* amount (tax-multiplier rate)))
(defn total-amount [items] (sum (map :amount items)))

(defn order-total
  [tax-rate items]
  (with-tax tax-rate (total-amount items)))
```
