# Introduction

In order to analyse a probabilistic model which has been specified and constructed in PRISM, it is necessary to identify one or more *properties* of the model which can be evaluated by the tool. 


PRISM's *property specification language* subsumes several well-known probabilistic temporal logics, including PCTL, CSL, probabilistic LTL, and PCTL*. PRISM also supports most of the (non-probabilistic) temporal logic CTL.

---
Before discussing property specifications in more detail, it is perhaps instructive to first illustrate some typical examples of properties which PRISM can handle. The following are a selection of such properties. In each case, we give both the PRISM syntax and a natural language translation:


```c
P>=1 [F "terminate"]
```
***the algorithm eventually terminates succes***