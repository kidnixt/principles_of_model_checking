# Reward-based Properties

PRISM models can be augmented with information about [[Costs & Rewards | rewards]](or, equivalently, costs). The tool can analyse properties which relate to the *expected values* of these rewards. This is achieved using the **R operator**, which works in a similar fashion to the [[The P Operator | P]]and [[The S Operator | S]]operators, and can be used either in a Boolean-valued query, e.g.:

```c
R bound [ rewardprop ]
```

where `bound`takes the form `<r`, `<=r`, `>r` or `>=r` for an expression `r` evaluating to a non-negative double, or a real-valued query, e.g.:

```c
R query [ rewardprop ]
```

