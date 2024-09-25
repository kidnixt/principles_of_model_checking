


## Commands

The behaviour of each module is described by *commands*, comprising a **guard** and one or more **updates**. The first command of module M1 in our example is:

``` c
[] x=0 -> 0.8:(x'=0) + 0.2:(x'=1);
```

The guard x=0 indicates that this describes the behaviour of the module when the variable **x** has value 0. The updates (x'=0) and (x'=1) and their associated probabilities state that the value of **x** will remaint at 0 with probability 0.8 and change to 1 with probability 0.2.

The second command:

``` c
[] x=1 & y!=2 -> (x'=2);
```

Illustrates that guards can contain constraints on any variable, not just the ones in that module, i.e. the behaviour of one module can depend on the state of another.

**Updates, however, can only specify values for variables belonging to the module.** In general a module *can read* the variables of any other module, but **only write to its own**. When a command comprises a single update with probability 1.0, the 1.0 can be omitted, as is done in the example above.

If a module has more than one variable, updates describe the new value for each of them. For example, if it had two variables $\large x_1$ and $\large x_2$, a possible command would be:

```c
[] x1=0 & x2>0 & x2<10 -> 0.5:(x1'=1)&(x2'=x2+1) + 0.5:(x1'=2)&(x2'=x2-1);
```

Notice that elements of the updates are concatenated with `&` and that each element must be bracketed individually. If an update does not give a new value for a local variable, it is assumed not to change. As a special case, the keyword **`true`** can be used to denote an update where no variable's value changes, i.e. the following are all equivalent:

``` c
[] x1>10 | x2>10 -> (x1'=x1)&(x2'=x2);  
[] x1>10 | x2>10 -> (x1'=x1);  
[] x1>10 | x2>10 -> true;
```

Finally, it is important to remember that the expressions on the right hand side of each update refer to the state of the model *before* the update occurs. So, for example, this command:

```c
[] x1=0 & x2=1 -> (x1'=2)&(x2'=x1)
```
updates variable $\large x_2$ to 0, not 2. 

## Parallel Composition
The probabilistic model corresponding to a PRISM language description is constructed as the *parallel composition* of its modules. In every state of the model, there is a set of commands (belonging to any of the modules) which are enabled, i.e. whose guardas are satisfied in that state. The choice between which command is performed (i.e. the *scheduling*) depends on the model type. 

For and MDP, as in Example 1, the choice is *nondeterministic*. By way of example, consider state (0, 0) (i.e x = 0 and y = 0). There are two commands enabled, one from each module:


``` c
[] x=0 -> 0.8:(x'=0) + 0.2:(x'=1);
```
``` c
[] y=0 -> 0.8:(y'=0) + 0.2:(y'=1);
```

In state (0, 0) of the MDP, there would be a nondeterministic choice between those two probability distributions:
- `0.8:(0,0) + 0.2:(1,0)` (module `M1` moves)
- `0.8:(0,0) + 0.2:(0,1)` (module `M2` moves)

For a DTMC, the choice is *probabilistic*, each enabled command is selected with **equal probability**. If Example 1 was a DTMC, then in state (0, 0) of the model the following probability distribution would result:

- `0.8:(0,0) + 0.1:(1,0) + 0.1:(0,1)`