# Name Lambda

## Relevant To

* Extract Variable

## Relates To

* [Name Value](extract-function.md)
* [Extract Function](extract-function.md)

## Languages

Languages with lambdas

## Motivation

Lambdas/anonymous functions are very useful. However, if is not immediately
clear from it is code what one does, it is helpful to give it a name to
describe it.

## Description

Either store the lambda in a named value or extract it to a new, named
function.

## Examples

### Clojure

#### Before

```clojure
(defn tax-multiplier [rate] (+ 1 (/ rate 100)))
(defn with-tax [rate amount] (* amount (tax-multiplier rate)))

(defn order-total
  [items tax-rate]
  (sum (map (fn [item] (with-tax (:amount item))) items))
```

#### After

```clojure
(defn tax-multiplier [rate] (+ 1 (/ rate 100)))
(defn with-tax [rate amount] (* amount (tax-multiplier rate)))

(defn item-amount-with-tax [item] (with-tax (:amount item)))

(defn order-total [tax-rate items] (sum (map item-amount-with-tax items)))
```
