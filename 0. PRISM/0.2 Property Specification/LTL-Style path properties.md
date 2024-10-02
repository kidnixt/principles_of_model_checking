# LTL-Style path properties

PRISM also supports probabilistic model checking of the temporal logic LTL (and, in fact PCTL*). LTL provides a richer set of path properties for use with the **P operator**, by permitting temporal operator to be combined. Here are a few examples of properties expressible using this functionality:


```c
P>0.99 [F ("request" & (X "ack"))]
```

"with probability greater than 0.99, a request is eventually received, followed immediately by an acknowledgement"

```c
P>=1 [G F "send"]
```

"a message is sent **infinitely often** with probability 1"

```c
P=? [F G ("error" & !"repair")]
```

"the probability of and error occurring that is never repaired"

Note that logical operators have precedence over temporal ones, so you will often need to include parentheses when using logical operators, e.g.:

```c
P=? [(F "error1) & (F "error2")]
```

For temporal operators, unary operators (such as **F, G** and **X**) have precedence over binary ones (such as **U**). Unary operator can be nested, without parentheses, but binary ones cannot. 

So, these are allowed:

```c
P=? [ F X X X "a" ]  
P=? [ "a" U X X X "error" ]  
P=? [ ("a" U "b") U "c" "error" ]
```

but this is not:

```c
P=? [ "a" U "b" U "c" "error" ]
```

and to make the above property correct, you would need to add parentheses around the nested "U" operators, as follows:

```c
P=? [ ("a" U "b") U ("b" U "c") U "error" ]
```


