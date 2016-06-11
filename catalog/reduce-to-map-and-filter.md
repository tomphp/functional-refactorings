# Reduce to Map/Filter/Reduce

## Relates To

* [Recursion to Filter](recursion-to-filter.md)
* [Recursion to Map](recursion-to-map.md)
* [Recursion to Reduce](recursion-to-reduce.md)

## Languages

All

## Motivation

Both `map` and `filter` can be implemented using `reduce`. As a result, complex
reductions are like to contain some `map` and/or `filter` like behaviour. By
extracting these out into separate steps, we can create code which clearly
documents each transformation step as a pipeline of single responsibilities,
rather that creating one complex action.

## Description

Study the body reduction function and identify parts which can are either
translating all values or skipping values. Extract these parts into separate
functions and use the with `map` or `filter` to create a pipeline of
transformations.

## Examples

### Clojure

#### Given

```clojure
(defn tax-multiplier [rate] (+ 1 (/ rate 100)))
(defn with-tax [rate amount] (* amount (tax-multiplier rate)))
```

#### Before

```clojure
(defn order-total
  [items]
  (reduce
   (fn [total item]
    (if (:free-gift? item)
        total
        (+ total (with-tax (:amount item)))))
   0
   items))
```

#### After

```clojure
(defn order-total
  [items]
  (->> items
       (filter (compliment :free-gift?))
       (map :amount)
       (map with-tax)
       (reduce + 0)))
```
