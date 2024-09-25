# Example 1

System comprising two identical processes which must operator under mutual exclusion.  Each process can be in one of 3 states: {0,1,2}. From state 0, a process will move to state 1 with probability 0.2 and remain in the same state with probability 0.8. From state 1, it tries to move to the critical section: state 2. This can only occur if the other process is not in its critical section. Finally, from state 2, a process will either remain there or move back to state 0 with equal probability. The PRISM code to describe an MDP model of this system can be seen below. In the next sections, we explain each aspect of the code in turn.

```c
mdp 

module M1

	x : [0..2] init 0;
	[] x=0 -> 0.8:(x'=0) + 0.2:(x'=1)
	[] x=1 & y!=2 -> (x'=2);  
    [] x=2 -> 0.5:(x'=2) + 0.5:(x'=0);
endmodule

module M2  
  
    y : [0..2] init 0;  
  
    [] y=0 -> 0.8:(y'=0) + 0.2:(y'=1);  
    [] y=1 & x!=2 -> (y'=2);  
    [] y=2 -> 0.5:(y'=2) + 0.5:(y'=0);  
  
endmodule

```

## Model Type
PRISM language can be used to describe several types of probabilistic models. To indicate which type is being described, a PRISM model usually includes a model type keyword:

- **dtmc:** discrete-time Markov chain
- **ctmc:** continuous-time Markov chain
- **mdp:** Markov decision process (or probabilistic automaton)
- **pta**: probabilistic timed automaton
- **pomdp:** partially observable Markov decision procress
- **popta:** partially observable probabilistic timed automaton

## Modules and Variables

The definition of a module contains two parts: its *variables* and its *commands*. The variables describe the possible states that the module can be in; the commands describe its behaviour, i.e. the way in which the state changes over time.

In the example above, each module has one integer variable with range [0..2]

```c
x : [0..2] init 0;
```

Notice that the initial value of the variable is also specified. A Boolean variable is declared as follows:

```c
b : bool init false;
```

It is also possible to omit the initial value of a variable, in which case it is assumed to be the lowest value in the range (or *false* for a Boolean). Thus, the variable declarations shown below are equivalent to the ones above.

