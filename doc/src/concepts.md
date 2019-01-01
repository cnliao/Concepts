## Draft of concepts

### Set
An object `x` is a `Set` iff `in(x, i)` is defined for any object `i`.

### Indexable
An object `x` is `Indexable` iff `x[i]` is defined for some object `i`.

Outside this section `DomainKnown Indexable` is abbreviated as `Indexable`.

#### DomainKnown
An `Indexable` object `x` is `DomainKnown` iff:
1. `indices(x)` is defined and returns a `Set` `I`;
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
An object `S` is a BroadcastStyle iff, given a function `f` and a tuple of `Indexable`s `args`,
 the following apply:
* `broadcast_plan(S, f, args)` is defined and returns an object `bc` that satisfies:
    1. `bc` is `Indexable`;
    2. `indices_map(bc, arg)` is defined and returns a `Function` from `indices(bc)`
        to `indices(arg)` for all `arg` in `args`;
    3. `bc[i] == f(args[1][indices_map(bc, args[1])(i)], args[2][indices_map(bc, args[2])(i)]), ...)`
* `broadcast_assign!(bc)` is defined if `args` has exactly two elements. It has the following side effect:

    `args[1][indices_map(bc, args[1])(i)] == args[2][indices_map(bc, args[2])(i)])` for all `i` in `indices(bc)`.
