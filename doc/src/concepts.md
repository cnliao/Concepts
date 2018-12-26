## Draft of concepts

### SetLike
An object `x` is `SetLike` iff `in(x, i)` is defined for any object `i`.

### Indexable
An object `x` is `Indexable` iff:
1. `indices(x)` is defined and returns a `SetLike` object `I`;
2. `x[i]` is defined for all `i` in `I`.

#### Integral
An `Indexable` object `x` is `Integral` iff x[i] is defined for a subset of `ℤⁿ`.

##### Linear
An `Integral Indexable` object `x` is `Linear` iff x[i] is defined on a subset of `ℤ`.

##### Cartesian
An `Integral Indexable` object `x` is `Cartesian` iff x[i] is defined on a subset of `(ℤ,ℤ,ℤ,...)`.

##### Natural
An `Integral Indexable` object `x` is `Natural` iff x[i] is defined on `[1,N1]×[1,N2]×...`.

### BroadcastStyle
An object `S` is a BroadcastStyle iff:
* `broadcast_combine(S, args)` is defined and returns an object `bc` that satisfies:
    1. `bc` is `Indexable`;
    2. `indices_map(bc, arg)` is defined and returns a `Map` from `indices(bc)`
        to `indices(arg)` for all `arg` in `args`;
    3. `bc[i] = (args[1][indices_map(bc, args[1])(i)], args[2][indices_map(bc, args[2])(i)]), ...)`
* `broadcast_apply(f, bc, kws)` is defined and returns an object `bcf` that satisfies:
    1. `bcf` is `indexable`;
    2. `indices(bcf) === indices(bc)`;
    3. `bcf[i] == f(bc[i]...; kws)` for all `i` in `indices(bc)`;
* `broadcast_assign!(bc)` is defined iff `args` has exactly two elements, and has the following side effect:

    `args[1][indices_map(bc, args[1])(i)] == args[2][indices_map(bc, args[2])(i)])` for all `i` in `indices(bc)`.
