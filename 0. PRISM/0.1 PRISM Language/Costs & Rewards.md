# Costs & Rewards

PRISM supports the specification and analysis of properties based on _costs_ and _rewards_. This means that it can be used to reason, not just about the probability that a model behaves in a certain fashion, **but about a wider range of quantitative measures relating to model behaviour.**

For example, PRISM can be used to compute properties such as "expected time", "expected number of lost messages" or "expected power consumption". The implementation of cost- and reward-based techniques in the tool is only partially completed and is still ongoing.

The basic idea is that probabilistic models (of all types) developed in PRISM can be augmented with costs or rewards: real values associated with certain states or transitions of the model. *In fact, since there is no practical distinction between costs and rewards (except that costs are generally perceived to be "bad" and rewards to be "good")*, PRISM only supports rewards. The user is, however, free to interpret the values however they choose.

---

In this section, we describe how models described in the PRISM language can be augmented with rewards. Later, we will discuss how to express properties that relate to these rewards. Rewards are associated with models using `rewards ... endrewards` constructs, which can appear anywhere in a model file except within a module definition. These constructs contains one or more _reward items_. Consider the following simple example:


```c
rewards  
    true : 1;  
endrewards
```

This assigns a reward of 1 to every state of the model. It comprises a single reward item, the left part of which (`true`) is a guard and the right part of which (`1`) is a reward. **States of the model which satisfy the predicate in the guard are assigned the corresponding reward. More generally, state rewards can be specified using multiple reward items**, each of the form `guard : reward;`, where `guard`is a predicate (over all the variables of the model) and `reward` is an expression (containing any variables, constants, etc. from the model). For example:


```c
rewards  
    x=0 : 100;  
    x>0 & x<10 : 2*x;  
    x=10 : 100;  
endrewards
```

assigns a reward of 100 to states satisfying `x=0` or `x=10` and a reward of `2*x` to states satisfying `x>0 & x<10`. Note that a single reward item can assign different rewards to different states, depending on the values of model variables in each one. Any states which do not satisfy the guard of any reward item will have no reward assigned to them. **For states which satisfy multiple guards, the reward assigned to the state is the sum of the rewards for all the corresponding reward items.**

---
Rewards can also be assigned to transitions of a model. These are specified in a similar fashion to state rewards, within the `rewards ... endrewards` construct. Reward items describing transition rewards are of the form `[action] guard : reward;`, the interpretation being that transitions from states which satisfy the guard `guard` and are labelled with the action `action` acquire the reward `reward`. For example:


```c
rewards  
    [] true : 1;  
    [a] true : x;  
    [b] true : 2*x;  
endrewards
```

assigns a reward of 1 to all transitions in the model with no action label, and rewards of `x` and `2*x` to all transitions labelled with actions `a` and `b`, respectively.