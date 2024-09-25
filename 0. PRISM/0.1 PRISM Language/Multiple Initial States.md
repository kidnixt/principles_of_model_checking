# Multiple Initial States

Typically, a variable declaration specifies the initial value for that variable. The *initial state* for the model is then defined by the initial value for all variables. It is possible, however, to specify that a model has **multiple** initial states. This is done using the `init...endinit` construct, which can be placed anywhere in the file except within a module definition, and removing any initial values from variable declarations.

