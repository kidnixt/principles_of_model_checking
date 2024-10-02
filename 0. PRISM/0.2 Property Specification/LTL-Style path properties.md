# LTL-Style path properties

PRISM also supports probabilistic model checking of the temporal logic LTL (and, in fact PCTL*). LTL provides a richer set of path properties for use with the **P operator**, by permitting temporal operator to be combined. Here are a few examples of properties expressible using this functionality:


```
P>0.99 [F ("request" & (X "))]
```