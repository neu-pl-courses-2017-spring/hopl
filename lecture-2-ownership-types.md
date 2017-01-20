# From Encapsulation to Ownership (J. Vitek)

## Intro

OO-paradigm was viewed as a tool that would work as an electronics: you have a 
number of substitutable components (objects) which you can compose. This idea
did not work at all: objects has subobjects (it is what problem of aliasing all
about).

Software crises -- 1968-.. Mcilroy: the problem is in absence of a software 
components industry. (Accidentally, he is known for invention of Unix pipes: great
approach for composing components).

## Syntatic control of interference (J.C.Reynolds)

J.C.Reynolds, POPL 1978, Syntactic control of interference. A number of Algol-68 
examples where you have call-by-ref semantics and you usually have problems when
you pass the same thing in place of different parameters of a procedure
(`fact(n,f)` (input and output param), think about call: `fact(z,z)`; also the 
parallel computations: `x = x + 1 || y = 2*y` -- what if x and y are the same).

JCR suggests syntactic control. Introduce relation `P # Q` to handle interference:
If `P # Q`, then

1. P and Q don't interfere (whatever this means).
2. If `P=P'(A)` then it is true that `P' # Q` and `A # Q`.

We would like to have a PL which (syntactically) gives as this very relation. To 
develop such PL we should stick to some principles.

1. `P ∈ I`, `Q ∈ J`, `I#J` then `P#Q`.
2. `I` and `J` distinct, then `I#J`.
3. If `P` and `Q` passive then `P#Q`. (whatever passive means)

JCR developed such a language with quite primitive means of building structures 
(boxes with int's or bool's inside). Restrictions:

1. `P#Q` if `F(P) ∩ F(Q) = ∅`.
2. P(A) if P#A.

Second restriction rules out many useful things (e.g. recursion in terms of Y:
`Y(f) => f(Y(f))`). So he relax restrictions with tune of the notion of *passive
statements*: more or less it is equivalent to not having side effects. Now this 
passive statements could be called non-interfering and e.g. run in parallel.

## Side-effect Free Functions (J. Hogg)

John Hogg "Islands: ...'', OOPSLA 1991. Introduce `%read` annotations n Smalltalk.
A `%read`-annotation means:

1. Var cannot be assigned.

2. Var can be exported only in `%read`-mode.

3. Var cannot be RHS of the assignment (as it could be updated later through alias).

Very strong restriction (like `const` in C++, but no casts in a language). Introduce
`Copy` which can help escaping from `%read`'s.

Island is a subgraph of object graph in a program which have exactly one reference 
inside it (SCC?). You can run two island in parallel. Plus: `unique` and `free` annotations.
Together w/`%read` they build linear like system which guarantees strong encapsulation.

## Flexible Alias Protection (Nobble, Vitek, Potter)

Islands have problem. Consider usage of a hash table...

New set of modifiers: `rep` (representation -- some "private'' thing to an object), 
`arg` (thing that can change, but not in the way sensible for us; we can call only 
read-like methods), `free`, `val` (immutable value), `var` (thing that can change).

## Ownership Types for Flexible Alias Protection (D.G.Clarke, J.M. Potter, J. Nobble)

Still an academic paper: no implementation, treat subset of Java.
They drop `arg`. The can parametrize a type over `rep`/`norep`-annotations. 
Thing is `rep` if it does not escape the class in which it was declared.

## Encapsulating Objects with Confined Types (.. J.Vitek)

Prev. works put consider. burden on user. Can we do something lighter but still of
interest?

Confined types: object of such type can be accessed only by the contents of this
type's package.

