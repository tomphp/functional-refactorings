# Rearrange Function Parameters

## Relevant To

* Change Method Signature

## Relates To

* [Go Point Free](go-point-free.md)

## Languages

All

## Motivation

Rearranging function/method parameters is a common thing to do in most
programming languages. There are several reasons to do this, including:
Consistency, style and preference. However, when working with higher order
functions, which is a large aspect of functional programming, currying and
partial application of function arguments becomes a very common technique. To
increase the opportunity to partially apply arguments to functions, it often
makes sense to change the order of the parameters, so that the ones which might
more commonly want to be applied come first.

Partial application is not the only reason you might consider rearranging you
function parameters. For instance, the pipe mechanism in Elixir and the thread
first macro in Clojure, both inject the value in as the first argument to
functions.  Rearranging the order of the parameters the make your API more
pipeable could be a wise refactoring to make.

## Description

Rearranging function parameters is a simple refactoring. When you identify
situations where the order makes it hard to apply arguments to the function as
you would like, you simply change the order.

## Examples

### Clojure

#### Given

```clojure
(def messages [["hello" "world"]
               ["hello" "moon"]
               ["goodbye" "world"]
               ["goodbye" "moon"]])
```

#### Before

```clojure
(defn list-contains? [coll x] (boolean (some #(= % x) coll)))

(filter (fn [msg] (list-contains? msg "world")) messages)
; (["hello" "world"] ["goodbye" "world"])
```

#### After

```clojure
; Changing the order of x and coll...
(defn list-contains? [x coll] (boolean (some #(= % x) coll)))

(def messages [["hello" "world"]
               ["hello" "moon"]
               ["goodbye" "world"]
               ["goodbye" "moon"]])

; ...allows the use of partial application instead of an anonymous function
(filter (partial list-contains? "world") messages)
; (["hello" "world"] ["goodbye" "world"])
```

