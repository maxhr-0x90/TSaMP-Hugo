---
title: "The journey begins"
date: 2022-10-28T11:11:39+02:00
draft: false
summary: P vs. NP enters its formal form
---

I think we're ready for this :muscle::sunglasses::muscle:.

This is the basis of my quest. The million dollar problem itself:
{{< math.inline >}}\(\bold{P}~vs.~\bold{NP}\), also called
\(\bold{P} \stackrel{?}{=} \bold{NP}\). But what are
those elusive \(\bf P\) and \(\bf NP\) things ? Because if this is some kind of equation
it's pretty easy to see that \(P = NP \iff P = 0,~or~N = 1\). Which is pretty
underwhelming.{{< /math.inline >}}

But of course if it were that easy there would be any problem to begin with. No,
here we are dealing with a problem of the utmost importance. A core problem in
the field of computational complexity, that some say will not be solved for the
next millennia (they're obviously wrong). A problem that could change our vision
of problem solving as a whole.

Let's dig in and see what's all fuss about.

## Decidability

We are on formal ground here, so no more of those approximative statements (lie).

The first thing to understand when dealing with computational complexity is
decidability. The ability for a Turing machine to recognize a language. That is,
{{< math.inline >}}given an alphabet \(\Gamma\), and language \(L \subseteq \Gamma\),
we say that a Turing machine \(M\) decides \(L\) if \(x \in L \iff M(x)~accepted\).
{{< /math.inline >}} In other words, if it's possible to create a TM that accepts
only inputs if they're in a given language then that language is decidable.

A language that is famously undecidable is the `HALT` language, part of the Halting
problem. `HALT` contains the set of all TM descriptions that halt (i.e. don't loop
infinitely). Proving this requires explaining what a Universal Turing Machine
and diagonalization are. So, for now, we'll stop here, but, not to worry,
a future entry shall touch on that subject.

## Complexity classes

Now that we know what decidable languages are, we can attempt to classify them
(i.e. create sets of languages with similar properties).
There are a lot of way to consider such classification (e.g. finite or infinite
languages, alphabet used, cool or cringe, etc.), but one of the most relevant to
our [Need for Speed](/posts/quest/0x0001-complexity) is of course the runtime
classification.

### DTIME and P

The {{< math.inline >}} \(\bf DTIME\) is really straight forward:{{< /math.inline >}}  
{{< math.inline >}}\(L \in \bold{DTIME}(T(n)) \iff \exists M\), a deterministic TM,
\(\forall x \in L\), \(M\) runs in \(O(T(n)))\) and \(M\) decides \(L\)
{{< /math.inline >}}. This definition imposes no explicit limitations on runtime,
just limitations on the type of machine.

{{< math.inline >}} \(\bf P\) on the other hand adds limitations for an "efficient"
runtime. That is, \(L \in \bold{P} \iff L \in \bigcup_{c \ge 1}\bold{DTIME}(n^c)\).
Thus \(\bf P\) is the set of all languages decidable in polynomial time on a
deterministic TM. Of course this notion that polynomial time is efficient is
questionable; e.g. what if the runtime is \(O(n^{10^{100}}\) ? It would be ludicrous
to consider that efficient even if it is asymptotically better than any exponential
runtime. Anyway, this is why we say that{{< /math.inline >}} problems [^prob]
{{< math.inline >}}in \(P\) are efficiently solvable.{{< /math.inline >}}

[^prob]: Most problems can be reformulated to be a language (e.g. encode every
  solution to the problem in a given alphabet).

### NTIME and NP

The definitions of {{< math.inline >}} \(\bf NTIME\) and \(NP\) are identical to
those of \(\bf DTIME\) and \(P\) except for the fact that \(\bf NTIME\) is running
on an NDTM, thus \(\bold{NP} = \bigcup_{c \ge 1} \bold{NTIME}(n^c)\).{{< /math.inline >}}

This definition, as informative as it is on the naming convention of classes, is
a bit lacklustre on the intuition side. To circumvent this shortcoming we can use
an alternative definition with certificates. It goes as follows:  
{{< math.inline >}}
\(L \subseteq \Gamma^*\in \bold{NP} \implies \exists p : \N \rarr \N\), a polynomial,
and a polynomial-time TM \(M\) (called the verifier for \(L\)) such that \(\forall x
\in \Gamma^*,\)
{{< /math.inline >}}
$$
x \in L \iff \exists u \in \Gamma^{p(|x|)}~s.t.~M(x,u)=accept
$$
{{< math.inline >}} where \(|x|\) denotes the length of \(x\). \(u\) is what we
call a certificate, it "helps" \(M\) to find a solution.
{{< /math.inline >}}

Because a solution/certificate for an {{< math.inline >}}\(\bf NP\) problem can
be verified in polynomial time we say that \(\bf NP\) is the class of efficiently
verifiable problems. Thus it is clear that \(\bold{P} \subseteq \bold{NP}\), from the fact
that any language in \(\bf P\) fits the 2nd definition of \(\bf NP\) with a trivial
certificate (i.e. the empty certificate).{{< /math.inline >}}

### Problem examples

#### **P** problems

{{< math.inline >}}To find a problem in \(\bf P\) is really easy. Just find a problem
solvable in polynomial time. For example, finding the max in a list of \(n\) elements
(\(O(n)\)), sorting a list of \(n\) elements (\(O(n \cdot log(n))\)), multipling 2
matrices (\(O(n^3)\), for the naive algorithm){{< /math.inline >}}, etc.

{{< math.inline >}}The resulting language \(L\) of those problem will be the set
of all input and answer, encoded and concatenated, that are correct. It may seem
dull but it is in accordance to the definition. Still, it's possible to create a
machine that produces the answer to a given input and then feed the input and answer
to a machine \(M\) capable of deciding \(L\){{< /math.inline >}}.

#### **NP** problems

Based on the 2nd definition, we can check that a {{< math.inline >}} problem is in
\(\bf NP\) if once we have the solution it is possible to verify in polynomial time.
We can see the example of the Travelling Salesperson Problem (TSP). The TSP consist
in checking the existance of a cycle a most \(\ell\) long in a \(n\)-vertex graph,
like a salesperson trying to find a tour a most \(\ell\) long between all the cities
they have to go to. This problem is clearly \(\bf NP\) as given a cycle that should
be at most \(\ell\) it is easy to verify that information. But it doesn't seem to
be in \(\bf P\) as the way to find a solution seems to involve checking every
permutation of the city visit order (\(O(n!)\)).{{< /math.inline >}}[^better]

[^better]: There are better algorithms like the [Held–Karp algorithm](https://en.wikipedia.org/wiki/Held%E2%80%93Karp_algorithm)
  but it's still in {{< math.inline >}}\(\Theta(n^2 2^n)\){{< /math.inline >}}

To point out the fact that --at least for now-- we have problems that cannot be solved
in polynomial time but can be verified in such time we use the notion of
{{< math.inline >}}\(\bf NP\) hardness. A \(\bf NP\)-Hard problem is a problem at
least as hard as any \(\bf NP\) problem. This notion gives us the definition of
\(\bf NP\)-Complete. That is, a problem in \(\bf NP\) which is \(\bf NP\)-Hard is therefore
\(\bf NP\)-Complete. Those kinds of problem can be seen as the quintecential NP problem,
the hardest amongst them defining the limits of this class.
We'll come back to that notion on the entry tackling the topic of reduction.
{{< /math.inline >}}

## Philosophy of P vs. NP

It is now clearer. The goal of {{< math.inline >}}\(\bold{P}~vs.~\bold{NP}\) is
to know if \(\bf P\) is the same set as \(\bf NP\) or not. More informally it's
asking whether every efficiently verifiable problem as an efficient solution.
Most expert on the domain are on the \(\bold{P} \ne \bold{NP}\) side. This is
because the implication of the contrary would be tremendous for the field of
computational complexity but also mathematics as a whole. Without getting into
too much details we observe one of those consequences in the following fact.
{{< /math.inline >}}

To know if a [boolean formula](https://en.wikipedia.org/wiki/Boolean_algebra)
{{< math.inline >}} is satisfiable (i.e. an assignment to all its variable
that returns \(True\)) is an \(\bf NP\)-Complete problem. One can clearly verify
in polynomial time that, given the assignment of every variable, a solution is
correct. But to find said solution it seems that bruteforce may be the only way.
We know that a lot of proof in mathematics can be expressed as a boolean formula.
This would explain why it is often harder to find a proof than to verify it.
That's pretty close to the world as we know it, and that's why most believe that
some problem do not have efficient solutions. But then, if \(\bold{P} = \bold{NP}\)
this would have unpresented impact on the way we consider problem solving. That
is to one exception. That is if to get a problem from \(\bf NP\) to \(\bf P\)
the resulting algorithm ends up with a monstruous polynomial complexity.
{{< /math.inline >}}
Algorithms so massive that they would only make sense to an eternal being, also
called [galactic algoritms](https://en.wikipedia.org/wiki/Galactic_algorithm).
This would explain why we haven't stumbled on this way of solving before.
