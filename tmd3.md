# lang.bash.type.special_characters

Some characters are evaluated to have **non-literal**

## Overview

- `$`: **Expansion**, introduces various types of expansions

- `[[ ]]`: **Test**, an evaluation of a expression

  - You can use this to **evaluate an expressionn** (true or false)

  - This version of test **may be preferred** over the old `[ ]` since:
    - **Easier** to use
    - **Less error** prone
    - Shares **similar functionalities**

- `!`: **Negate**, used to negate or reverse a test or exit status

- `>, >>, <`: **Redirection**, redirect a command's output or input to a file

  - Use `>>` to **append** something to a file

- `;`: **Command separator**, used to separate multiple commands

- `(( ))`: **Arithmetic expression**, use with characters such as `+,-,*,/`

  - Used for [variable](./y2lh.md) assignments: `(( a = 1 + 4 ))`
  - Used for tests: `(( a < b ))`

- `$(( ))`: **Arithmetic expansion**, the expression is replaced with the result

  - Ex: `echo "The average is $(( (a+b)/2 ))"`

- `$()`: **Command expansion**, the expression is replaced with the result

- `&`: **Background**, when used at the end of a command, run the command in
  the background

- `&&`: **And operator**, for conditional expressions

  - Ex: `(( 5 > 0 )) && echo "Five is greater than zero."`

- `||`: **Or operator**, for conditional expression
  - It can be **used as** an **else statement**
  - Ex: `(( 5 > 0 )) || echo "Five is greater than zero."`

- `{ }`: **Grouping statement**, group logical statements or commands together

## Cookbook

### Make an conditional statement without if and else

You can use the `&&` and `||` as `if` and `else` operators **respectively**

The following will **return** the **right hand expression if no argument** is
**passed** to the function

```sh
  main() {
    [ "$1" ] && echo "One for $1, one for me." || echo "One for you, one for me."
  }

  main "$@"
```

### Append lines to the end of a file

Here the `PATH="$HOME/bin:$PATH"` line will be appended to the **end of** the
`$HOME/.bashrc` file

```sh
  echo 'PATH="$HOME/bin:$PATH"' >> "$HOME/.bashrc"
```
