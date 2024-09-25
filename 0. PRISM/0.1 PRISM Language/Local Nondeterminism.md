# Local Nondeterminism

PRISM models that support nondeterminism, such as are MDPs, can also exhibit *local nondeterminism*, which allows the modules themselves to make nondeterministic choices. In [[Example 1]], we can make the probabilistic choice in the first state of module M1 nondeterministic by replacing the command:

``` c
[] x=0 -> 0.8:(x'=0) + 0.2:(x'=1);
```

with the commands:

```c
[] x=0 -> (x'=0);  
[] x=0 -> (x'=1);
```

