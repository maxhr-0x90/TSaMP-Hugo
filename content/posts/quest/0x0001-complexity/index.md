---
title: "Need for Speed"
date: 2022-10-11T15:40:06+02:00
draft: false
summary: Understand and evaluate time complexity
---

If you've ever interacted with the programming community, you may have heard something
along those lines:

> `ProgSwagg64: I like the programming language X.`  
> `FastBoi1337: Yeah but Y is faster than X. X is lame >:)`  
> `ProgSwagg64: That may be but are you even worthy of such speed ?`

`ProgSwagg64` raises a great concern. Even though `FastBoi1337` language is fast
and cool, how much their programming skills can influence the velocity of the execution ?  
It all depends on how many times each elementary operation[^sametime] in an algorithm is
executed depending on the input size. This measurement is called time complexity.

And as time complexity is at the core of the P vs. NP problem, it surely would be nice
to be able to understand and evaluate it.

[^sametime]: Supposing that each operation takes a fixed amount of time to perform.

## Asymptotic notation

First of all, we need to order our time complexities. Considering times complexities are
just functions giving the "time" of execution depending on the input size, we just
have to find a way to order functions. Which is what asymptotic notation does best.

Here's a quick summary of the different notations:

For all definitions: {{< math.inline >}} \(k\in\R^+\) and \(n_0\in\N\) {{< /math.inline >}}

### o (Small O)

**Formal definition**:

$$
f(n) = o(g(n)) \iff \forall k,~\exist n_0 : \forall n > n_0,~|f(n)| < k \cdot g(n)
$$

**Interpretation**:  
No matter how small k can be, there will always be a point where *g* surpass *f*.

Asymptotically, it can be viewed as
{{< math.inline >}}\(f(n) < g(n)\){{< /math.inline >}}.  
We say that "*f* is dominated by *g* asymptotically".

### O (Big O)

**Formal definition**:

$$
f(n) = O(g(n)) \iff \exist k,~\exist n_0 : \forall n > n_0,~|f(n)| \le k \cdot g(n)
$$

**Interpretation**:  
For a certain k, passed a point, *g* is an upper bound of *f*, up to k.

Asymptotically, it can be viewed as
{{< math.inline >}}\(f(n) \le g(n)\){{< /math.inline >}}.  
We say that "*f* is bounded above by *g* asymptotically".

### Ω (Big Omega)

**Formal definition**:

$$
f(n) = Ω(g(n)) \iff \exist k,~\exist n_0 : \forall n > n_0,~|f(n)| \ge k \cdot g(n)
$$

**Interpretation**:  
For a certain k, passed a point, *g* is an lower bound of *f*, up to k.

Asymptotically, it can be viewed as
{{< math.inline >}}\(f(n) \ge g(n)\){{< /math.inline >}}.  
We say that "*f* is bounded below by *g* asymptotically".

### ω (Small Omega)

**Formal definition**:

$$
f(n) = ω(g(n)) \iff \forall k,~\exist n_0 : \forall n > n_0,~|f(n)| > k \cdot g(n)
$$

**Interpretation**:  
No matter how big k can be, there will always be a point where *f* surpass *g*.

Asymptotically, it can be viewed as
{{< math.inline >}}\(f(n) > g(n)\){{< /math.inline >}}.  
We say that "*f* dominates *g* asymptotically".

### Θ (Big Theta)

**Formal definition**:

$$
f(n) = Θ(g(n)) \iff f(n) = Ω(g(n))~and~f(n) = O(g(n))
$$

We say that "*f* is bounded both above and below by *g* asymptotically".

### Use in time complexity

Even though --almost-- all the notations were included for the sake of exhaustivity,
generally the ones often used are the Big O and the Big Omega. That's because **1.**
the "Small" notations aren't very informative about the behaviour of our algorithm.
And **2.**, when evaluating said algorithm we mostly consider the worst case in term
of input. Thus in order to be prepared for every eventuality, an upper bound is an
almost necessary information to have.  
In short the asymptotic notation is a way to know how easily an algorithm can become
unruly. We want to know how much "damage" it can cause.

Asymptotic notations are great because they allows us to not care about constants.
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

### Time complexities hierarchy[^tm]

You may have noticied in the previous example that the functions in the Big
Theta notation are really simple. Even if technically any function can be used,
In most cases, we use the functions in the following table:

| Notation                                                          | Growth       |
| ----------------------------------------------------------------- | ------------ |
| {{< math.inline >}}\(\Theta(1)\){{< /math.inline >}}              | Constant     |
| {{< math.inline >}}\(\Theta(log(n))\){{< /math.inline >}}         | Logarithmic  |
| {{< math.inline >}}\(\Theta(n)\){{< /math.inline >}}              | Linear       |
| {{< math.inline >}}\(\Theta(n \cdot log(n))\){{< /math.inline >}} | Super Linear |
| {{< math.inline >}}\(\Theta(n^x)\){{< /math.inline >}}            | Polynomial   |
| {{< math.inline >}}\(\Theta(x^n)\){{< /math.inline >}}            | Exponential  |
| {{< math.inline >}}\(\Theta(!n)\){{< /math.inline >}}             | Factorial    |

The simple idea of this hierarchy is that the functions are all Small O of the
next one. Meaning that --even if the constants are way worse-- the lower in the
hierarchy the more efficient your algorithm is.

{{< more "Visual representation of the hierarchy" >}}
![Time complexity hierarchy](complexity.png)
{{< /more >}}

NB: For polynomial and exponential growth,
{{< math.inline >}}\(x < x_0 \implies f(n) = o(g(n))\)
for \(f(n) = n^x,~g(n) = n^{x_0}\)
or \(f(n) = x^n,~g(n) = {x_0}^n\)
{{< /math.inline >}}

[^tm]: There is a concept named the [Time hierarchy theorem](https://en.wikipedia.org/wiki/Time_hierarchy_theorem).
    Which is the same idea, but more formal.

## Evaluate an algorithm

With the idea of the asymptotic notations in mind we can extract the essence of
efficiency in algorithms. But to do so evaluation is needed. That being said to find
the complexity of an algorithm is not always a simple task or even a feasible one at
that. But there are some common cases. This next part covers the easy one among those.
One last thing, what we are trying to evaluate are the number of time an elementary
operation is executed. Depending on the context this notion of elementary operation
can change wildly. Here we assume that basic operation in common modern programming
languages (i.e. assignment, expression evaluation, etc.) are one elementary operation.
Anyway, enough preamble, let's get our hands dirty.

### Non-recursive case

As long as there are no recursive call and you are aware of each time complexity for
every function your program this technique is quite useful and easy.

Initialise every line to be either Θ(1) if it's an elementary operation or Θ(f(n))
if its a call to a function (change f(n) accordingly).
Then the idea is that if you enter a loop that depends on the input size then **every** time
complexities inside is multiplied by n. Once you evaluated the time complexity of
every line, take the the one that's an upper bound to the other asymptotically. Done.

Example:

``` C
input = getinput();                     // O(n)
n = size(input);                        // O(1) (depends on the type of input)

for (i = 0; i < n; i++){                // Depends on n
    for (j = 0; j < 5; j++){            // Does not depend on n
        for (k = 0; k < n; k += 2){     // Depends on n (even though it's only half of it)
            input[k] = input[k] / 2;    // O(n^2) (O(1) operation within 2 n depedent loop)
        }
        input[i] += 1;                  // O(n) (O(1) operation within 1 n depedent loop)
    }
    // sort has an O(n*log(n)) complexity
    sort(input);                        // O(n^2*log(n)) (O(n*log(n)) operation within 1 n depedent loop)
}

// => this --useless-- algorithm is O(n^2*log(n))
```

### Recursive case (Ha shit here we go again)

Recursion has an additional challenge. The next method can be helpful in most cases
but the topic of recusion is quite a treaterous one. Still here it is:

1. evaluate the time complexity of a function call with the previous method up
  until the recursive call.
2. Extract the recurrence relation.
    1. It should either be of the form:
        $$
        T(n) = T(n-i) + \Theta(f(n)),~i<n
        $$
        Which is just a loop in disguise. Thus the resulting complexity is
        {{< math.inline >}}\(\Theta(n \cdot f(n))\){{< /math.inline >}}
    2. Or: [^gen]
        $$
        T(n) = aT(n/b) + \Theta(f(n)),~a>0,~b>1
        $$
        From here there's 3 possibilities:
        1. {{< math.inline >}} \(\exist\epsilon > 0 : f(n) = O(n^{log_b a-\epsilon})
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

So to answer the initial question, the programming skills of `FastBoi1337` indeed
matter, and in a very significant way. At the end of the day, unless a programming
language introduces an gargantuan overhead, in term of speed, the choice of a language
is of little conquence. The concept of a solution is more important than it's
implementation (at least in theory). That's why we made an entire field of
mathematics about this idea of doing things efficiently.
