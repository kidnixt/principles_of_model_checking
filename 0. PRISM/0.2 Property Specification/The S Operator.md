# The S Operator

The **S operator** is used to reason about the *steady-state* behaviour of a model, i.e. its behaviour in the *long-run* or *equilibrium*. PRISM currently only provides support for DTMCs and CTMCs. The definition of steady-state (long-run) probabilities for finite DTMCs and CTMCs is well defined (see e.g. [Ste94](https://www.prismmodelchecker.org/manual/Main/References#Ste94)). Informally, the property:

```c
S bound [prop]
```

is true in a state **s** of a DTMC or CTMC if "starting from *s*, the steady-state (long-run) probability of being in a state which satisfies the (Boolean-valued) PRISM property `prop`, meets the bound `bound`". A typical example of this type of property would be:

```c
S<0.05 [ queue_size / max_size > 0.75 ]
```

which means: "the long-run probability of the queue being more than 75% full is less than 0.05"

Like the [[The P Operator]], the **S operator** can be used in a *quantitative* form, which returns the actual probability value, e.g.:

