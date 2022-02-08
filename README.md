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
1 =:= 0.
1 =/= 0.
5 =:= 5.0.
5 == 5.0.
5 /= 5.0.
1 < 2.
1 < 1.
1 >= 1.
1 =< 1.
```

Notice the `=<` operator.

``` erl
5 + llama.
5 =:= true.
0 == false.
1 < false.
```

**Note:** The correct ordering of each element in a comparison is the following:

`number < atom < reference < fun < port < pid < tuple < list < bit string`

### Tuples

A tuple is a way to organize data. It's a way to group together many terms when you know how many there are. In Erlang, a tuple is written in the form `{Element1, Element2, ..., ElementN}`. As an example, you'd give me the coordinates (x,y) if you wanted to tell me the position of a point in a Cartesian graph. We can represent this point as a tuple of two terms:

``` erl
X = 10, Y = 4.
Point = {X,Y}.

Point = {4,5}.
{X,Y} = Point.
X.
{X,_} = Point.
{_,_} = {4,5}.
{_,_} = {4,5,6}.
Temperature = 23.213.
PreciseTemperature = {celsius, 23.213}.
{kelvin, T} = PreciseTemperature.
{celsius, T} = PreciseTemperature.
{point, {X,Y}}.
```

### Lists

Lists are the bread and butter of many functional languages. They're used to solve all kinds of problems and are undoubtedly the most used data structure in Erlang. Lists can contain anything! Numbers, atoms, tuples, other lists; your wildest dreams in a single structure. The basic notation of a list is `[Element1, Element2, ..., ElementN]` and you can mix more than one type of data in it:

``` erl
[1, 2, 3, {numbers,[4,5,6]}, 5.34, atom].
[97, 98, 99].
[97,98,99,4,5,6].
[233].

[1,2,3] ++ [4,5].
[1,2,3,4,5] -- [1,2,3].
[2,4,2] -- [2,4].
[2,4,2] -- [2,4,2].
[1,2,3] -- [1,2] -- [3].
[1,2,3] -- [1,2] -- [2].

hd([1,2,3,4]).
tl([1,2,3,4]).

List = [2,3,4].
NewList = [1|List].
[Head|Tail] = NewList.
Head.
Tail.
[NewHead|NewTail] = Tail.
NewHead.

[1 | []].
[2 | [1 | []]].
[3 | [2 | [1 | []] ] ].

[a, b, c, d].
[a, b, c, d | []].
[a, b | [c, d]].
[a, b | [c | [d]]].
[a | [b | [c | [d]]]].
[a | [b | [c | [d | [] ]]]].

% Improper list
[1 | 2].

% Proper list
[1 | [2]].
```

### List Comprehensions

List comprehensions are ways to build or modify lists. They also make programs short and easy to understand compared to other ways of manipulating lists. It's based off the idea of set notation; if you've ever taken mathematics classes with set theory or if you've ever looked at mathematical notation, you probably know how that works. Set notation basically tells you how to build a set by specifying properties its members must satisfy. List comprehensions may be hard to grasp at first, but they're worth the effort. They make code cleaner and shorter, so don't hesitate to try and type in the examples until you understand them!

``` erl
[2*N || N <- [1,2,3,4]].
```
