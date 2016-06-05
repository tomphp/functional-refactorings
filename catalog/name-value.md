# Name Value

## Relevant To

* Extract Constant
* Extract Variable

## Relates To

* [Extract Function](extract-function.md)

## Languages

All

## Motivation

As a function's expression gains complexity, it is behaviour becomes harder to
comprehend. Giving names to intermediate steps of the expression can
significantly increase clarity.

## Description

Identify groups in the expression which perform a specific task, then store
them as values with meaningful names.

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
(defn order-total
  [items tax-rate]
  (let [tax-multiplier (+ 1 (/ tax-rate 100))
        total-amount (sum (map :amount items)))]
    (* tax-multiplier total-amount))
```
