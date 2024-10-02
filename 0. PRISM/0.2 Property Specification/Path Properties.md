# Path Properties

PRISM supports a wide range of path properties that can be used with the **P operator**. *A path property is a formula that evaluates to either true or false for a single path in a model.* Here, we review some of the simpler properties that feature a single *temporal operator*, as used for example in the logics PCTL and CSL. Later, we briefly describe how PRISM also supports more complex LTL-style path properties.

The basic different types of path property that can be used inside the **P operator** are:

- **X**: "next"
- **U**: "until"
- **F**: "eventually" (sometimes called "future")
- **G**: "always" (sometimes called "globally")
- **W**: "weak until"
- **R**: "release"

In the following sections, we describe each of these *temporal operators*. We then discuss the (optional) use of time bounds with 