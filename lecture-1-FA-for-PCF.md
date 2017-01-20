# Full Abstraction: From PCF to SPCF (M. Felleisen)

CS started at 1929 with Godel's incompletness theorems. Then lambda calculus
appeared. It wasn;t quite a programming languge. In 70-s we came up with a PL
inspired by LC, that is PCF. Let's describe it.

PCF has 

* Types 
        t = i | t -> t

* Exp
        e = x | \x:t.e | ee | ...

* Type Sys: standard

* Programs: `e` which is closed and has ground type `i`.

* Meaning function:
        m: Programs -> {\top. \bot}

    This can be given in various ways:
        
        * axiomatic,
        * reducing,
        * denotational,
        * Kahn,
        * SOS,
        * ...

Denotational semantics is a machinethat incrementally produces info about expr. 
and program. Bottom (\bot) means no information, top (\top) means you have any information
you want.

    [| i |] = Nat_{\bot}
    [| t -> t' |] = [| t |] -> [| t' |]
    
`->` on the left is just a symbol, and on the right -- math. space of function.
The latter space is a subject of some restirctions (aka properties).

### Properties of den. sem. for PCF 

* **Extensionality**: unique rep. for any function.

* **Monotonicity**: don't retract information (the machine does not backtrack,
    does not say: nevermind of what I said before).

* **Continuity**: 
        f(\lub e) = \lub f(e)
    Note: we mean set-theoretic lattice on a space of functions. We could say
    \lim instead of \lub.

* \omega-algebraicity: ...

* consistency-complete: ...


Example (Scott domains are wrong):

    ! = {(0,1), (1,1), (2,2), (3,6), ...}
        {_      (1,1), (2,2), (3,6), ...}
        {_,     _,     (2,2), (3,6), ...}

That is a bad thing we don't want to have, because this is a process not producing
information, but lesser it. Infinite descending chain. *Note*: none of students get it ;-)

Bottom line: the space should have more props than Scott-Strachey came up with.

## Observational equality (Morris, 1969)

Programmers must be able to reason *locally* because pragramms are large. Do not
think about context. 

We define a context (note: just like in IPPL class).

Def:

    e < e' <=> forall C, s.t. C[e], C[e'] are programms, m[| C[e] |] < m[| C[e'] |]

This induces equiv. relation ~.

Thm.: ~ is the max. relation on programms, s.t.:

    * is not trivial,
    * is a superset of basic PCF -- compatability,
    * respects `m`,
    * is congruence: `e ~ e'` => `C[| e |] ~ C[| e' |]`

... this leads to the question of FA (full abstraction), i.e. completeness w.r.t.
`~` (note: we know the soundness part).


## Milner

PCF has one denotational model that is fully abstract (and all others are isomorphic).

    |e| = {e' | e ~ e'}

## Plotkin

P. discovered junk in a SS-spaces. There is a functions which are computable, but not in a SS-space.

## Berry & Curien: Concrete Date Structures (CDS) + Algorithms

Use desicion trees as a model. It is not extensional! But this is sequential, 
denotational model (more over -- a CCC).

## Cartwright + Felleisen

"Sequentiality from errors'': take CDS and make them propagate errors automatically, 
this removes non-extensionality.

This leads to extended PCF -- SPCF. Programms can observe errors (exception handlers).

