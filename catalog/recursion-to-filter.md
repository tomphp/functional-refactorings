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
on defined criteria, in the form of a boolean statement or function.

## Description

The filter takes a function (called a predicate) that is passed each element from
the original list. If the function returns `true` then that item is included in
the new list. If it returns false then that item is not included.
This is an immutable operation, returning a new list and not affecting the original.

## Examples

### Haskell

#### Given

```haskell
numbers = [1, 6, 3, 5, 8, 67, 43, 4, 6, 8];
```

#### Before

```haskell
-- tail recursion
filter' :: (a -> Bool) -> [a] -> [a]
filter' _ [] = []
filter' f (x:xs) = if (f x)
                   then x : filter' f xs
                   else     filter' f xs

evenNumbers = filter' even numbers
```

#### After

```haskell

evenNumbers = filter even numbers
```

### PHP

#### Given

```php
$numbers = [1, 6, 3, 5, 8, 67, 43, 4, 6, 8];
```

#### Before

```php
$evenNumbers = [];

foreach ($numbers as $n) {
    if ($n % 2 == 0) {
        $evenNumbers [] = $n;
    }
}
```

#### After

```php
$evenNumbers = array_filter($numbers, function ($n) {
    return $n % 2 == 0;
});
```