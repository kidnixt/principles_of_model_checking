# The P Operator

One of the most important operators in the PRISM property specification language is the **P operator**, which is used to reason about the probability of an event's occurrence. This operator was originally proposed in the logic *PCTL* but also features in the other logics supported by PRISM, such as *CSL*. The **P operator** is applicable to all types of models supported by PRISM.

Informally, the property:


``` c
P bound [ pathprop ]
```

Is *true* in a state **s** of a model if "the probability that path property `pathprop`is satisfied by the paths from state **s** meets the bound `bound`". A typical example of a bound would be:


``` c
P>0.98 [ pathprop ]
```

which means: "the probability that `pathprop`is satisfied by the paths from state **s** is great than 0.98". More precisely, `bound`can be any of this:
- >=p
- >p
- <=p
- < p

where `p` is a PRISM language expression evaluating to a double in the range [0,1].

## Nondeterminism

For models that can exhibit nondeterministic behaviour, such as MDPs or PTAs, some additional clarifications are necessary. Whereas for fully probabilistic models such as DTMCs and CTMCs, **probability measures over paths are well defined** (see e.g. [KSK76]((https://www.prismmodelchecker.org/manual/Main/References#KSK76)and [BKH99](https://www.prismmodelchecker.org/manual/Main/References#BKH99), respectively).








