# Garbage Collection vs Manual Allocation (Will Clinger)

## Intro

GC -- about finding largest connected components. Started at LISP.

## Experiments

Let's try to allocate and deallocate large number of objects. In language with
manual A/D and with GC. C++ sucks over Java which sucks over Scheme.

Let's try Dijkstra. Results are quite similar. Java starts to eat lots of memory
if we don't tel it to limit itself.

These measurements are done on desktop computers. There are other contexts of course.

Ben Zorn made an effort with more comprehensive benchmarks (6 C programms) with similar 
results. He never managed to publish it (see TR references on the site).

## Present times

Generational GC -- dominating tech. Works well but no one knows why. One say: it
improves cache locality. Some possible principle:

> Most objects die young.

X noted that objects lives resembles radioactive nuclear particles with their half-live
conventionally described with exponential distribution. The problem is: sum
of exp. distrib. is not an exp. distrib. Turns out that objects behave as a
system of two nuclear particles: one with infinitely long half-live (long-live 
objects), one with fairly short (temporary objects).

This observations lead to a model: Linear combinations of radioactive decay models.

## References (besides the ones on the site)

1. Psychology of programming, 1970s.

