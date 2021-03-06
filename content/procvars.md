---
title: First Class Functions
---

# First Class Functions

Nim supports closures as well as passing functions. Two different syntaxes available for closures, proc syntax, which is identical to regular procedure syntax, and "do notation", which is a bit shorter.

``` nimrod
import sequtils

let powersOfTwo = @[1, 2, 4, 8, 16, 32, 64, 128, 256]

echo powersOfTwo.filter do (x: int) -> bool : x > 32
echo powersOfTwo.filter(proc (x: int): bool = x > 32)
```
``` console
$ nim c -r filterclosure.nim
@[64, 128, 256]
@[64, 128, 256]
```

Existing procedures can also be passed as functions, but only if they are annotated with the `{.procvar.}` pragma. This is because there may be default parameters, which must be specially handled by the compiler.

``` nimrod
proc greaterThan32(x: int): bool {.procvar.} = x > 32

echo powersOfTwo.filter(greaterThan32)
```
