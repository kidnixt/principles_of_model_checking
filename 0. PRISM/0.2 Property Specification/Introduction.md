# Introduction

In order to analyse a probabilistic model which has been specified and constructed in PRISM, it is necessary to identify one or more *properties* of the model which can be evaluated by the tool. 


PRISM's *property specification language* subsumes several well-known probabilistic temporal logics, including PCTL, CSL, probabilistic LTL, and PCTL*. PRISM also supports most of the (non-probabilistic) temporal logic CTL.

---
Before discussing property specifications in more detail, it is perhaps instructive to first illustrate some typical examples of properties which PRISM can handle. The following are a selection of such properties. In each case, we give both the PRISM syntax and a natural language translation:


```c
P>=1 [F "terminate"]
```
***"the algorithm eventually terminates successfully with probability 1"***


```c
P<0.1 [ F<=100 num_errors > 5 ]
```
***"the probability that more than 5 errors occur within the first 100 time unit is less than 0.1"***


```c
S<0.01 [ num_sensors < min_sensors ]
```

***"in the long-run, the probability that an inadequate number of sensors are operational is less than 0.01"***

---
Note that the above properties are all assertions,, i.e. ones to which we would expect a "yes" or "no" answer. This is because all references to probabilities are associated with an upper or lower bound which can be checked to be either true or false. In PRISM, we can also directly specify properties which evaluate to a numerical value, e.g.:


```c
P=? [ !proc2_terminate U proc1_terminate ]
```