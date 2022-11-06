---
title: "One Machine to rule them all"
date: 2022-11-05T15:33:43+01:00
summary: Universal Turing Machines, or the abstraction of software
draft: true
---

Turing Machines have many tricks up their sleeves. So many in fact that it would
be quite tedious to just list them all. That's why in my recap' of
[Turing's Keynote](/posts/quest/0x0002-tm) I have kept things at surface level.
But even in this endeavour of sum up the conference I wasn't able to cram in one
very important matter: Universal Turing Machines.

So here it is. The follow up to my first entry on TMs.

## Encoding

First order of business, we need to adress this fact that was kind of glossed
over in the first entry on the topic:

> Though, I'll admit it, for all cases, with some encoding trickery, binary is just fine.

{{< math.inline >}}
This asserts that given a machine \(M\) using alphabet \(\Gamma = {s_1,...,s_n}\)
running in \(T(n)\) time. There exist a machine \(M'\) with the alphabet
\(\Gamma_b = \{0, 1, □, ◿\}\), running in \(4 \cdot log(|\Gamma|) \cdot T(n)\).
The proof goes something like this:
{{< /math.inline >}}

1. {{< math.inline >}}
  Use \(log_2 |\Gamma|\) steps to read from each tape the \(log_2 |\Gamma|\) bits
  encoding a symbol of \(\Gamma\)
  {{< /math.inline >}}
2. Use the head state to store the symbols read
3. {{< math.inline >}}
  Use \(M\)’s transition function to compute the symbols \(M\) writes and \(M\)’s
  new state given this information
  {{< /math.inline >}}
4. Store this information in the head state
5. {{< math.inline >}}
  Use \(log_2 |\Gamma|\) steps to write the encodings of these symbols on its tapes.
  {{< /math.inline >}}

{{< math.inline >}}
NB: It should take around \(3 \cdot log(|\Gamma|)\) steps to execute one step
of \(M\) (that includes moving the heads). That being said to be absolutely sure
we say that each step finishes within \(4 \cdot log(|\Gamma|)\)
{{< /math.inline >}}.

{{< math.inline >}}
It can seem like using \(\Gamma_b\) instead of a true binary alphabet
(i.e. \(\{0, 1\}\)) is a bit of let down. But \(\Gamma_b\) is more easy to use in
parctice with \(□\) marking empty cell and \(◿\) marking the start of the heads
(note: we're assuming that \(\Gamma\) uses a similar kind of symbols to do
the same things; i.e. filling the empty cells and marking the start).
{{< /math.inline >}}
And the principal idea is the same, with encoding it is possible to use an
arbitrarily small alphabet -- of size at least 2 -- and get the same results
as a bigger one, for a constant cost -- relative to the ito unarynput size -- at runtime
(thus asymptotically irrelevant).

This tangent allows us to comprehend the power of encoding. But of course, it's useful
for way more than alphabets. It is always possible to encode something as long as the
alphabet describing it is finite -- natural language and formal notation count :wink:.
That way it's possible to input numbers, lists and graphs in a TM no matter the alphabet.
And that also goes also for TMs themselves !

## UTMs

And so, what if we created a machine capable of taking a TM as an input (with its
input) and simulate said TM. Then we would have what we call a Universal TM (UTM).
In a sense, UTMs are programmable TMs. You write a program and then execute it
on a UTM.

Here is an examples of how one can create such a machine that runs efficiently
relative to the machine simulated without the specifics of encoding.

{{< math.inline >}}
A universal TM \(\cal U\) is given an input \(x, \alpha\), where \(\alpha\) represents
some TM \(M\). We thus need to compute \(M(x)\). First we modify \(M\) to fit our
needs{{< /math.inline >}}.

That means **1.** reducing the number of working tapes to one (the input and output)
tapes stay the same). To do so we'll use a similar method as the one for making a
multitape machine into a single tape one. This will introduce an additional cost
making the final machine run in {{< math.inline >}}\(O(T^2(n))\){{< /math.inline >}}.
**2.** {{< math.inline >}} change the alphabet of \(M\) to \(\{0, 1, □, ◿\}\){{< /math.inline >}}
with the encoding method.

{{< math.inline >}}
\(\cal U\) uses the same alphabet as \(M\) and three work tapes in addition to its input
and output tape. it uses its input tape, output tape, and one of the work
tapes in the same way \(M\) uses its three tapes{{< /math.inline >}}.

{{< math.inline >}}
In addition, \(\cal U\) will use its first extra work tape to store the table of values
of \(M\)’s transition function, and its other extra work tape to store the current state
of \(M\) {{< /math.inline >}}.

{{< math.inline >}}
To simulate one computational step of \(M\), \(\cal U\) scans the table of \(M\)’s
transition function and the current state to find out the new state, symbols to be
written and head movements, which it then executes. This only add a constant
depending on the size of \(M\) description to the final cost{{< /math.inline >}}.

This model can be improved efficiency wise. The most expensive part being the
*flattening* of the machine simulated if we can improve that then we can improve
the whole UTM. This is exactly what the *Theorem 3.1* does in this
[lecture](https://glennsun.com/docs/cs281-lec3.pdf).
{{< math.inline >}}
It allows to run a k-tapes machine on a 2-tapes one in \(O(T(n) \cdot log(T(n)))\),
if the k-tapes one runs in \(T(n)\).
{{< /math.inline >}}

## Turing Completeness

UTMs clearly expose why TMs are so versatile and powerful. They're one of the favorite
tool for computer science shenanigans. And that is mostly because of Turing Completeness.
Something is said to be Turing complete when it can simulate any Turing machine.
Of course, by definition, UTMs are Turing Complete. But they are also useful to
know if something is Turing Complete. Naturally, if a system of data-manipulation [^vague]
can simulate a UTM then it has this property. That's how most of the time Turing
Completeness is proven.

[^vague]: It is intentionally vague. Because of how simple TM definition is lots
  of things end up being akin to them.

And because our CPUs are basically uber-UTMs it means that anything Turing Complete
can simulate, albeit very inefficiently in practice, a CPU. This is why you can
often see CS scholars laughing maniacally at the fact that your uncle's pacemaker
is Turing Complete and could theoretically run DOOM. An entire
[webpage](https://beza1e1.tuxen.de/articles/accidentally_turing_complete.html) is
dedicated to this madness (your uncle's pacemaker not included). This also explain
why `HTML` is **NOT** a programming language. And why you should never ask a computer
nerd if he programs in `HTML`. It would be quite apathetic vis-à-vis your uncle's fate.
