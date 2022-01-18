# Write Me Some Erlang

> This repository is for notes and code while reading [Learn You Some Erlang](https://learnyousomeerlang.com).

## Getting Help

```sh
erl -man lists
```

## Shell Commands

| Mapping | Function |
| --- | --- |
| `^A` | Move cursor to beginning of line |
| `^E` | Move cursor to end of line |
| `^G` | Abort (`h` for help) |
| `<TAB>` | Tab completion and suggestions |
| `help().` | Run the help |

## Basics

### Numbers

```erl
2 + 15.
49 * 100.
1892 - 1472.
5 / 2.
5 div 2.
5 rem 2.
(50 * 100) - 4999.
-(50 * 100 - 4999).
-50 * (100 - 4999).
2#101010.
8#0677.
16#AE.
```

### Invariable Variables

```erl
One.
One = 1.
Un = Uno = One = 1.
Two = One + One.
Two = 2.
Two = Two + 1.

47 = 45 + 2.
47 = 45 + 3.

_ = 14+3.
_.

f(One).
One.
f().
Two.
```

### Atoms

```erl
atom.
atoms_rule.
atoms_rule@erlang.
'Atoms can be cheated!'.
atom = 'atom'.
```

Atoms are really nice and a great way to send messages or represent constants. However there are pitfalls to using atoms for too many things: an atom is referred to in an "atom table" which consumes memory (4 bytes/atom in a 32-bit system, 8 bytes/atom in a 64-bit system). The atom table is not garbage collected, and so atoms will accumulate until the system tips over, either from memory usage or because 1048577 atoms were declared.

This means atoms should not be generated dynamically for whatever reason; if your system has to be reliable and user input lets someone crash it at will by telling it to create atoms, you're in serious trouble. Atoms should be seen as tools for the developer because honestly, it's what they are.

Some atoms are reserved words and can not be used except for what the language designers wanted them to be: function names, operators, expressions, etc. These are: `after and andalso band begin bnot bor bsl bsr bxor case catch cond div end fun if let not of or orelse query receive rem try when xor`

### Boolean Algebra

```erl
true and false.
false or true.
true xor false.
not false.
not (true and true).
```

The boolean operators `and` and `or` will always evaluate arguments on both sides of the operator. If you want to have the short-circuit operators (which will only evaluate the right-side argument if it needs to), use `andalso` and `orelse`.

### Comparison Operators

```erl
5 =:= 5.
```