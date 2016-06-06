# Functional Refactorings

When writing programs with pure functions, it appears that there are some
refactorings which are more common in this paradigm. Some of these relate to
the [well know catalog of refactorings](http://refactoring.com/catalog/)
introduced by Martin Fowler, but others are not on that list.

In this catalog, I want to present the ones I have personally identified,
plus the additional ones propose in a session I ran at [SoCraTes
2016](http://socratesuk.org/) on this topic.

My hope is that others in the functional community will improve and extend this
catalog to create a useful resource. So please contribute thoughts (issues)
and (improvements) pull requests!

## Catalog

* [Rearrange Function Parameters](catalog/rearrange-function-parameters.md)
* Go Point Free
* Curry Function
* Recursion to Map
* Recursion to Filter
* Recursion to Reduce
* [Name Value](catalog/name-value.md)
* [Extract Function](catalog/extract-function.md)
* [Name Lambda](catalog/name-lambda.md)
* [Compose Nested Functions](catalog/compose-nested-functions.md)
* Reduce to Map and Filter
* Extract Parameter to Type
* Tail Call Optimise Recursion
* Replace Conditional with Polymorphism
* Chain of Consequences to Maybe (or Either) Monad

## Links

Links for further reading (not yet integrated into this document)

* http://refactoring.com/catalog/
* http://victorsavkin.com/post/63551894251/functional-refactoring-in-javascript
* https://www.cs.kent.ac.uk/projects/refactor-fp/publications/Huiqing-thesis.pdf
* http://thepugautomatic.com/2016/01/pattern-matching-complex-strings/
