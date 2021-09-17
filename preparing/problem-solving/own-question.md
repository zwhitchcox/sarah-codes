## Questions

In the following sections, I will discuss the process for answering a question you may have as well as the reasoning behind the process.

### Keywords

* `issue`: An error you encounter while programming or a concept you are unfamiliar with
* `solution`: A fix for the error you are having or an explanation of the concept you are unfamiliar with
* `dependency`: Any `issue` you encounter while searching for a `solution`
* `dependent`: The original `issue` you were trying to resolve when encountering a `dependency`
* `label`: a short hand for an `issue` or `solution` used in "Dependency Notation"
* `chain`: multiple layers of nested `dependency`s
* `root`: The original issue
* `peer`: Another `dependency` with the same `dependent`

### Dependency Notation

#### Labels

If an `issue` with the `label`, `A`,  is has a `solution` with the `label`, `B`, we would denote that `solution` as `A->B`.

However, `solution` `A->B` may have a `dependency` of its own, `label`ed `C`. We could denote that `dependency` `A->B->C`.

#### Multiple Dependencies

`A` could have `dependency`s `B` and `C`, which could be denoted

```
A
  ->B
  ->C
```

####  Nested Dependencies

If `A->B` had `dependency`s `D` and `E`, the could be denoted

```
A
  ->B
    ->D
    ->E
  ->C
```

#### Namespaces

Another `root`, `B` might have a `dependency` with a `B` in it too. That `B` is not necessarily the same `B` that was in `A`. That is, in

```
A->B
C->B
```

`A->B` is not `C->B`

#### References

If we want to use the same `B` in both `A` and `C`, we could reference `B` by surrounding it with parentheses:

```
B
A->(B)
C->(B)
```

Here, all references to `B` refer to the same `solution`.

#### Partial Dependencies

An `dependent` might not need *all* of a `dependency`s `dependent`s. In

```
B
  ->C
  ->D

C->(B->C)

D->(
  B
    ->C
    ->D
)
```

`C`'s `solution` depends on `B->C`, but not on `B->D`. `D`'s `solution` depends on `B->C` and `B->D`

#### Aliases

If we want to make use a shorthand to refer to `B`, we can give it an alias. An alias gives a different name to the same references.

We denote a reference with `:=`. In

```
B
  ->C
  ->D

A:=(
  B
    ->C
    ->D
)

X->(A)
```

`X->(A)` and is the same as saying

```
X->(
  B
    ->C
    ->D
)
```

#### Multiple Solutions

An `issue` can have multiple `solution`s. In

```
B->M
B->
  P
    ->J
    ->T
  N->X
```

`B` has two `solution`s, `B->M` being the far simpler one.



### Why Answering Your Own Question Is Important

Let's say you have a `issue`, `G`, with a technology `B`, with `dependency`s `B->C`, `B->D`, and `B->E`.

```
G:=(B->C)

B
  ->C
  ->D
  ->E
```

You could ask a bear for help, and they will explain `B->C` to you.

Then later, you need to understand `H`. You ask your bear, and he shows you that `H` is actually and alias of `B->D`.

```
H:=(B->D)
```

and explains `B->D` to you.

Next, you need to understand `I`. You ask your bear, but he has never seen `I` before. You are lost until you can find someone who can explain `I` to you. You scour the internet and eventually find that a `solution` for `I` is actually `B->D`. Thus

```
I:=(B->D)
```

But you don't know this, because you didn't actually look at the documentation for `B` and understand the whole scope. You may have spent hours/days tracking down the solution.

This is a simple example, but interdependencies and relations can be complex.

For instance, you could have a `chain`.

```
M
  -> J
  -> (B->C)
  -> B
X
  ->N
  ->L

H
  -> (B->N->P)
  -> J
  -> (M->J)

T:=(H
  -> (B->N->P)
  -> J
  -> (M->J)
)

H->X

B
  -> C
  -> N
    -> P
    -> (M->B)
  -> (H)
  -> E->(B->N->(M->B))

```

If you're looking for `B->E->(B->N->(M->B))`, you must look for each link in the `chain`, each of which may be difficult to find. The more context you have, the easier it will be to find each link.

Furthermore, understanding the full context of the technologies you are using can help you prevent `issue`s or find novel `solution`s. For example, maybe you can get `M->J` to work, but when you try to use `H->(M->J)`, you have an `issue`.

Someone to whom is explained `H->J` and now needs to solve `H` might not ever know about the shortcut `H->X` and have to solve all of `T`.