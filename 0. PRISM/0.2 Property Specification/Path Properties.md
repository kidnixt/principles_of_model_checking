# Path Properties

PRISM supports a wide range of path properties that can be used with the **P operator**. *A path property is a formula that evaluates to either true or false for a single path in a model.* Here, we review some of the simpler properties that feature a single *temporal operator*, as used for example in the logics PCTL and CSL. Later, we briefly describe how PRISM also supports more complex LTL-style path properties.

The basic different types of path property that can be used inside the **P operator** are:

- **X**: "next"
- **U**: "until"
- **F**: "eventually" (sometimes called "future")
- **G**: "always" (sometimes called "globally")
- **W**: "weak until"
- **R**: "release"

In the following sections, we describe each of these *temporal operators*. We then discuss the (optional) use of time bounds with these operators. Finally, we also discuss LTL-style path properties.


---
## "Next" path properties

The property **X** `prop`is true for a path if `prop`is true in its second state. An example of this type of property, used inside a **P operator**, is:


```c
P<0.01 [ X y = 1]
```

which is true in a state if "the probability of the expression y = 1 being true in the next state is less than 0.01"

## "Until" path properties

The property `prop1`**U** `prop2`is true for a path if `prop2`is true in some state of the path and `prop1`is true in all preceding states. A simple example of this would be:


```c
P>0.5 [z<2 U z=2]
```

which is true in a state if "the probability that `z`is eventually equal to 2, and that `z`remains less than 2 up until that point, is greater than 0.5"

## "Eventually" path properties

The property **F** `prop`is true for a path if `prop`eventually becomes true at some point along the path. The **F operator** is in fact a special case of the **U operator** (*you will often see **F** `prop`written as **true U `prop`***) A simple example is:


```c
P<0.1 [F z>2]
```

which is true in a state if "the probability that `z`is eventually greater than 2 is less than 0.1"

## "Globally" path properties

Whereas the **F operator** is used for ***reachability*** properties, **G operator** represents ***invariance***. The property **G** `prop`is true of a path if `prop`remains true at all states along the path. Thus, for example:


```c
P>=0.99 [G z<10]
```

states that, with probability at least 0.99, `z`never exceeds 10.

## "Weak until" & "release" path properties

Like **F and G**, the operators **W and R** are derivable from other temporal operators.

Weak until (`a` **W** `b`), which is equivalent to (`a`**U** `b`) | **G** `a`, requires that `a`remains true until `b`, becomes true, but does not require that `b`ever does become true (i.e. `a`remains true forever). For example a weak form of the until example used above is:

```c
P>0.5 [z<2 U z=2]
```

which states that, with probability greater than 0.5, either `z`is always less than 2, or it is less than 2 until the point where `z`is 2.

Release (`a` **R** `b`), which is equivalent to ! (`!a`**U** `!b`), informally means that `b`is true until`a`becomes true, or `b`is true forever.


## "Bounded" variants of path properties

All of the temporal operators given above, with the exception of **X**, have "bounded" variants, where an additional time bound is imposed on the property being satisfied. The most common case is to use an *upper time bound*, i.e. of the form "<=t" or "<t", where *t* is a PRISM expression evaluating to a constant, non-negative value.

For example, a bounded until property `prop1`**U<=t** `prop2`, is satisfied along a path if `prop2`becomes true within *t* steps and `prop1`is true in all states before that point. A typical example of this would be:


```c
P>=0.98 [y<4 U<=7 y=4]
```

which is true in a state if "the probability of `y`first exceeding 3 within 7 time units is greater than or equal to 0.98". Similarly:


```c
P>=0.98 [F<=7 y=4]
```

is true in a state if "the probability of `y`being equal to 4 within 7 time units is greater than or equal to 0.98" and:


```c
P>=0.98 [G<=7 y=4]
```

is true if the probability of `y`staying equal to 4 for 7 time units is t least 0.98

