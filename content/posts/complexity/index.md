---
title: "The Complexity"
date: 2022-10-04T15:40:06+02:00
draft: true
summary: Understand and evaluate time complexity
tags: ["Exposition", "P vs. NP"]
---

If you've ever interacted with the programming community, you may have heard something
along those lines:

> `ProgSwagg64: I like the programming language X.`  
> `FastBoi1337: Yeah but Y is faster than X. X is lame >:)`  
> `ProgSwagg64: That may be but are you even worthy of such speed ?`

`ProgSwagg64` raises a great concern. Even though `FastBoi1337` language is fast
and cool, how much their programming skills can influence the velocity of the execution ?  
It all depends on how many times each operation[^sametime] in an algorithm is executed
depending on the input size. This measurement is called time complexity.

And as time complexity is at the core of the P vs. NP problem, it surely would be nice
to be able to understand and evaluate it.

[^sametime]: Supposing that each operation takes a fixed amount of time to perform.

## Asymptotic notation

First of all, we need to order our time complexities. Considering times complexities are
just functions giving the "time" of execution depending on the input size, we just
have to find a way to order functions. Which is what asymptotic notation does best.

Here's a quick summary of the different notations:

### o (Small O)

**Formal definition**:

$$
f(n) = o(g(n)) \iff \forall k > 0,~\exist n_0 : \forall n > n_0,~|f(n)| < k \cdot g(n)
$$

**Interpretation**:  
No matter how small k can be, there will always be a point where *g* surpass *f*.

Asymptotically, it can be viewed as
{{< math.inline >}}\(f(n) < g(n)\){{< /math.inline >}}.  
We say that "*f* is dominated by *g* asymptotically".

### O (Big O)

**Formal definition**:

$$
f(n) = O(g(n)) \iff \exist k > 0,~\exist n_0 : \forall n > n_0,~|f(n)| \le k \cdot g(n)
$$

**Interpretation**:  
For a certain k, passed a point, *g* is an upper bound of *f*, up to k.

Asymptotically, it can be viewed as
{{< math.inline >}}\(f(n) \le g(n)\){{< /math.inline >}}.  
We say that "*f* is bounded above by *g* asymptotically".

### Ω (Big Omega)

**Formal definition**:

$$
f(n) = Ω(g(n)) \iff \exist k > 0,~\exist n_0 : \forall n > n_0,~|f(n)| \ge k \cdot g(n)
$$

**Interpretation**:  
For a certain k, passed a point, *g* is an lower bound of *f*, up to k.

Asymptotically, it can be viewed as
{{< math.inline >}}\(f(n) \ge g(n)\){{< /math.inline >}}.  
We say that "*f* is bounded below by *g* asymptotically".

### ω (Small Omega)

**Formal definition**:

$$
f(n) = ω(g(n)) \iff \forall k > 0,~\exist n_0 : \forall n > n_0,~|f(n)| > k \cdot g(n)
$$

**Interpretation**:  
No matter how big k can be, there will always be a point where *f* surpass *g*.

Asymptotically, it can be viewed as
{{< math.inline >}}\(f(n) > g(n)\){{< /math.inline >}}.  
We say that "*f* dominates *g* asymptotically".

### Θ (Big Theta)

**Formal definition**:

$$
f(n) = Θ(g(n)) \iff \exist k_1,~k_2 > 0,~\exist n_0 :
\forall n > n_0,~k_1 \cdot g(n) \le |f(n)| \le k_2 \cdot g(n)
$$

We say that "*f* is bounded both above and below by *g* asymptotically".

NB: {{< math.inline >}}\(f(n) = Θ(g(n)) \iff f(n) = Ω(g(n))~and~f(n) = O(g(n)) \){{< /math.inline >}}.

### Use in time complexity

Even though --almost-- all the notations were included for the sake of exhaustivity,
generally the ones often used are the Big O and the Big Omega. That's because **1.**
the "Small" notations aren't very informative about the behaviour of our algorithm.
And **2.**, when evaluating said algorithm we mostly consider the worst case in term
of input. That way we can be prepared for every eventuality. Thus an upper bound
encapsulate perfectly this search for the worst.

Asymptotic notation is great because it allows us to not care about constants.
Which is --considering we don't always know how many operations a single instruction
represents-- a really versatile tool.  
For example, considering 3 functions *f*, *g* and *h*:

$$
\begin{aligned}
f(n) = 4n^2 + 138n + 12 &= \Theta(n^2)\\\\
          g(n) = 823n^2 &= \Theta(n^2)\\\\
         h(n) = 2^{100} &= \Theta(1)
\end{aligned}
$$

It's clear that *f* and *g* have the same kind of evolution even though they don't have
the same factors. And that even if *h* has an horrendous cost, it would still be more
efficient than *f* or *g* given a sufficiently large input.  

### Typical time complexities

You may have noticied in the previous example that the functions in the Big
Theta notation are really simple. Even if technically any function can be used,
you will see in most cases something in the following table:

| Notation   | Growth       |
| ---------- | ------------ |
| Θ(1)       | Constant     |
| Θ(log n)   | Logarithmic  |
| Θ(n)       | Linear       |
| Θ(n log n) | Super Linear |
| Θ(n^x)     | Polynomial   |
| Θ(x^n)     | Exponential  |
| Θ(n!)      | Factorial    |

## Evaluate an algorithm

Now that we know the meaning of the asymptotic notations we can try to find it for
ourselves looking at an algorithm.  
Let's get our hands dirty.

### Non-recursive

As long as there are no recursive call and you are aware of each time complexity for
every function your program this technique is perfect and easy.

Initialise every line (considering that a line = an operation) to be either Θ(1)
if its elementary or Θ(f(n)) if its a call to a function (change f(n) accordingly).
Then the idea is that if you enter a loop that depends on the input size then **every** time
complexities inside is multiplied by n. Once you evaluated the time complexity of
every line, take the the one that's an upper bound to the other asymptotically. Done.

### Recursive (Ha shit here we go again)

Recursion has an additional challenge. The next method can be helpful in most cases
but the topic of recusion is quite a treaterous one. Still here it is:

1. valuate the time complexity of a function call with the previous method up
  until the recursive call.
2. Extract the recurrence relation.
    1. It shoul either be of the form:
        $$
        U(n) = U(n-a) + \Theta(f(n))
        $$
        Which is just a loop in disguise. Thus the resulting complexity is n×f(n)
    2. Or: [^gen]
        $$
        U(n) = aU(n/b) + \Theta(f(n)),~a>0,~b>1
        $$
        From here there's 3 possibilities:
        1. {{< math.inline >}} \(\exist\epsilon > 0 : f(n) = O(n^{log_ba-\epsilon})
            \implies T(n) = \Theta(n^{log_ba})\){{< /math.inline >}}
        2. {{< math.inline >}} \(\exist k \ge 0 : f(n) = \Theta(n^{log_ba}log_2^kn)
            \implies T(n) = \Theta(n^{log_ba}log_2^{k+1}n)\){{< /math.inline >}}
        3. {{< math.inline >}} \(\exist\epsilon > 0 : f(n) = \Omega(n^{log_ba+\epsilon})
            ~and~af(n/b) \le cf(n),~c < 1\\\\
            \implies T(n) = \Theta(f(n))\){{< /math.inline >}}
    3. Sorry but this form isn't disponible at the moment [^srry]

[^gen]: There is a more general method called the [Akra-Bazzi Method](https://en.wikipedia.org/wiki/Akra%E2%80%93Bazzi_metho)
[^srry]: That doesn't mean that it's unsolvable or even remotely complicated to solve.
  But if you wanna be unstoppable I'm sure there is a book or articles that can suit
  your desire for knowledge in the art of recurrence relation.
