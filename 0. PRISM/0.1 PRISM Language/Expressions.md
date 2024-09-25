# Expressions
We now define more precisely what types of expression are supported by PRISM. Expressions can contain literal values (12, 3.141592, `true`, `false`, etc.), identifiers (corresponding to variables, constants, etc.) and operators from the following list:

- `-` (unary minus)
- `*`, `/` (multiplication, division)
- `+`, `-` (addition, subtraction)
- `<`, `<=`, `>=`, `>` (relational operators)
- `=`, `!=` (equality operators)
- `!` (negation)
- `&` (conjunction)
- `|` (disjunction)
- `<=>` (if-and-only-if)
- `=>` (implication)
- `?` (condition evaluation: `condition ? a : b` means "if `condition` is true then `a` else `b`")
Al 