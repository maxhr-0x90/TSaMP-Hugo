---
title: "Turing's Keynote"
date: 2022-10-24T20:24:17+02:00
summary: Turing Machines 101
draft: false
---

I recently was at the S.A.M.S.A.R.A. [^meta], it was delightful ! There was a lot
of talks on various topics but the one that caught my attention was the keynote held by
that Alan Turing fella. Really exciting stuff about that new type of computer, more
abstract, simpler yet powerful, with a slick design. The minimalist dream.
Everyone most likely already heard of it: the A-Machine ! or Turing Machine as
everyone like to call it.  
Anyway let's see what's all that hype about.

[^meta]: S.A.M.S.A.R.A. Annual Mathematical Summit Against Recursive Annotation

## Turing Machine

Here is the main idea behind this machine. First no more hard drive, nor R.A.M.,
everything is on an tape with infinite cells. That means infinite memory, infite
possibilities :sunglasses:. On each cell there is a symbol from a predefined
alphabet with no limitations. So no more of that weak and flimsy binary, you can
now enjoy the new and improved {♛, ♫, ©, ඞ} alphabet, and more ! Though most
of the time binary is just fine.

Now onto the plat de résistance. Say goodbye to your obsolete CPU and hello to the
reading and writing apparatus of the machine, somberly called: the Head. The Head
of the machine can not only read and write symbols, it can also move along the tape.
In addition to its mobility, the Head also has multiple states that it can be in
to change its behaviour.

When all of this has been setup, the alphabet been chosen, the different states
defined with their according behaviours, we can run the machine. And as with
everything else the runtime execution is really intuive and simple. At the beginning
of each step the Head read the symbol on the tape then, according to the state it is
in, it can change the symbol, move on the tape and change its state. It will repeat
this process until there is no next step (i.e. no actions have been defined for the
symbol read and the current state), and at this point will stop/halt. If the state
the Head is in at that moment is an accepting state (defined before runtime as a
subset of all possible states) then the machine accepts the input (i.e. the initial
state of the tape before runtime) else it rejects it.

In short, more formally, and without the flamboyant sales pitch a Turing Machine is
a 7-tuple
{{< math.inline >}}
\(M = \langle Q, \Gamma, b, \Sigma, \delta, q_0, F \rangle\)
{{< /math.inline >}} where:

- {{< math.inline >}}\(\Gamma\){{< /math.inline >}} is a finite alphabet
  (e.g. {0, 1, □, ◿}, {♛, ♫, ©, ඞ} [^dream], or any other symbol set);
- {{< math.inline >}}\(b \in \Gamma\){{< /math.inline >}} is the blank symbol
  (e.g. □). It is the only one that can fill the tape infinitely;
- {{< math.inline >}}\(\Sigma \subseteq \Gamma\){{< /math.inline >}} is the input
  alphabet (e.g. {0, 1, ◿});
- {{< math.inline >}}\(Q\){{< /math.inline >}} is a finite set of all possible
  Head state;
- {{< math.inline >}}\(q_0 \in Q\){{< /math.inline >}} is the initial state;
- {{< math.inline >}}\(F \subseteq Q\){{< /math.inline >}} is the set of
  final/accepting states;
- {{< math.inline >}}
  \(\delta : (Q \setminus F) \times \Gamma \nrightarrow Q \times \Gamma \times \{L,R,S\}\)
  {{< /math.inline >}}
  is the transition function. That is, {{< math.inline >}}\(\delte\){{< /math.inline >}}
  is a partial function (i.e. we don't need to define all the transition from
  {{< math.inline >}}\((Q \setminus F)\){{< /math.inline >}}), that depending on
  the symbol read and the current state gives the symbol to write, the next state
  and the movement of the Head (e.i. L: left, R: right and S: stay)

And of course, it's possible to witness the power of this beast --at least partially--
on the [Turing Machine Simulator](https://turingmachinesimulator.com/).

[^dream]: I dream of the day where the copyrighted royal amongi musical will
  prevail :pensive:

## Upgrades

But that's not all, it's possible to get an upgrade !

We can divide them into 2 categories. First, the conceptual upgrades. They help to think
about a Turing machine without altering its inner workings. A simple example would
be that on some machines the transition function doesn't allow the Head to stay. Even
though it seems like a limitation, it's still possible for such a machine to simulate
the action of staying in place (going back and forth with some state shenanigans should
do the trick).

The second type of upgrade is fundamental. They are useful if ones wants to give
more --or less-- power to their machine. Playing with different power can allow for more
advanced operations but it can also be used to show that some power are in fact
overkill and can be simulated with less powerful machines for a reasonable cost.
A good example a more powerful machine compared to the initial definition is a
Random Access Turing Machine (RATM). Instead of gliding along the infinite tape,
a RATM can just seemingly teleport itself to a random position on the tape. This
offers obvious perks as it allows the machine to do in one step what the other
could only do in arbitrarily many.

During the keynote a LOT of upgrades were presented. So here is
a more in-depth presentation of some of the most common amongst them.

### Multi-tapes

The title is pretty self-explanatory. More often than not it's really handy to not
do everything on the same tape. Then just use a machine with multi-tapes. That way
it's possible to have a tape for the input, one for the output and many more for
the work in-between those 2. Multi-tapes also implies multi-heads that can each
move independently of each others. All of this seperate nicely every aspect of a
machine and can make it a lot clearer it term of its functionning.

It's interesting to note that because there can be an output tape we aren't obligated
to depend on the final state to know if an input can be accepted. We can simply define,
for example, a symbol that if present on that tape mean that the input has been accepted.
Both method of approval are used but the halting state one is often preferred.
It goes without saying that changing to a multi-tapes machine changes the definition
of the transition function to something like this (for k tapes):

$$
\delta : (Q \setminus F) \times \Gamma^k
\nrightarrow Q \times \Gamma^{k - 1} \times \lbrace L,R,S\rbrace ^{k}
$$

NB: the {{< math.inline >}}\(\Gamma^{k - 1}\){{< /math.inline >}} comes from the fact
that the input tape is usually a read-only tape in multi-tapes machine.

It's obvious that a multi-tape machine can simulate a single-tape one but the other
way around may seem like a bit of a stretch. I assure it's not. The main idea to simulate
multi-tapes on a single one is to first squash every tape down into one using a new
"squashed" alphabet (e.g. 3 cells containing a, b and c will become one cell
containing the symbol "a/b/c"). Next, to simulate the independant heads add to the
"squashed" alphabet a head indicator. So, for example, if we have 3 cells containing
a, b and c and the 2nd head is on b then the "squashed" cell will contain the symbol
"a/>b/c", assuming that ">" indicate the presence of the head.

Now that everything is squashed to one tape, we only need one more trick. We'll
go back and forth on the tape, stocking information on the state, moving heads
and changing symbols accordingly. Let's see an abbriviated idea of this concept
on an example.

At the start the squashed tape might look something like this:

```goat
       head
         v
----+---------+---------+---------+---------+---------+---------+---------+---------+---------+----
    |>◿,>◿,>◿ | 1, □, □ | 1, □, □ | 0, □, □ | 1, □, □ | 1, □, □ | 0, □, □ | 1, □, □ | □, □, □ |
----+---------+---------+---------+---------+---------+---------+---------+---------+---------+----
```

Initially we'll the head sweep along the tape until find a cell containing "□,□,□".
The next state just after {{< math.inline >}}\(q_0\){{< /math.inline >}} would be
one that indicate the direction we're sweeping. It could look something like this:
{{< math.inline >}}\(q_{ltr,(q_0),[?,?,?]}\){{< /math.inline >}}, with the state
of the multi-tape machine in parenthesis. The "?" indicate the fact that we haven't
encountered any head indicator yet.  
When we come across a cell containing a head indicator we "add" the symbol pointed to
the state. Here, the state at the end of the first sweep might look something like this:
{{< math.inline >}}\(q_{ltr,(q_0),[◿,◿,◿]}\){{< /math.inline >}} just before encountering the
"□,□,□" cell.

When the head is on the "□,□,□" cell it will do 2 things. First, it will change
its direction from left to right (ltr) to right to left (rtl). Then it will change
its state according to the multi-tapes machine's transition function. So now the
state looks like this
{{< math.inline >}}
\(q_{rtl,(q_1),[◿,◿,◿],([◿,◿],[R,R,\times])}\)
{{< /math.inline >}}.
Thus the head begins sweeping right to left. When it encounters a head indicator,
it replace its symbol with the new one.

Additionnaly, if it encounters a head
indicator that needs to move left it will "delete" it from the current cell
--keep that information-- and "place" it in the next cell. For example,
{{< math.inline >}}\(L\) becomes \(del\) indicating that the head has been deleted
and then \(\times\) when it's placed to avoid futher action{{< /math.inline >}}.

Finally, when the head arrive at the cell containing "◿,◿,◿" it can change direction
and move the heads moving to right whilst gathering the symbols pointed. With all
of that in mind, our example would look like this the 2nd it encounters the "□,□,□" cell.

```goat
                                                                                       head
                                                                                         v
----+---------+---------+---------+---------+---------+---------+---------+---------+---------+----
    | ◿, ◿,>◿ |>1,>□, □ | 1, □, □ | 0, □, □ | 1, □, □ | 1, □, □ | 0, □, □ | 1, □, □ | □, □, □ |
----+---------+---------+---------+---------+---------+---------+---------+---------+---------+----
```

with the state
{{< math.inline >}}
\(q_{ltr,(q_1),[1,□,◿],([?,?],[\times,\times,\times])}\)
{{< /math.inline >}} before the changes.

NB: The states name are quite cumbersome. That's why generally just describing the
idea without the specifics is often the go to. That being said seeing how states
can store information is still pretty insightful.

### Oblivious tech

In short, this upgrade makes it so that the movements of a machine heads only
depend on the size of the input. Thus it is oblivious to the content of the input;
i.e. at step `i` of the machine, for 2 inputs of identical length, the heads will
be at the same position, thus the heads positions are just a function of `i`.
It may seems useless at first glance but it actualy gets rid of a sizable problem:
inconsistencies.

To make a machine oblivious the idea is simple (this time it will be short, I swear).
If it takes a machine {{< math.inline >}}\(M\) at most \(T(n)\) steps to deal with
any input of length \(n\), where \(T(n)\) is a time constructible function
{{< /math.inline >}}[^reason]. Then on any tapes for those inputs there is at most
{{< math.inline >}}\(T(n)\) symbols. Thus if you transform \(M\) into a single tape
machine (with the method seen previously) and, instead of sweeping until there no
relevant information, go back and forth to the \(T(n)\)th cell no matter what.
With the head position function being in the in the ballpark of
\(f(i) = T(n) - |(i~mod~2 \cdot T(n)) - T(n)|\), it is clear that this machine is
oblivious.{{< /math.inline >}}

{{< math.inline >}}
It's to be noted that there exist a more efficient way to create an oblivious machine.
running in \(O(T(n) \cdot log(T(n)))\). Whereas the ones created with this method
run in \(O(T^2(n))\).
{{< /math.inline >}}

Anyway, onto the last upgrade.

[^reason]: A function that can be calculated in a reasonable time like
  {{< math.inline >}}\(n\), \(n^2\) or even \(n \cdot log(n)\){{< /math.inline >}}.
  Nothing too wacky.

### Determinism removal

The 2 previous upgrade are conceptual one contrary to this one which is --most
likely-- fundamental. Until now we have assumed that a Turing Machine is deterministic.
That is, for every possible state the machine can be in, there is at most one action
possible depending on the content of the tapes. But of course this limitation can
be bypassed. But to do so we have to renonce our determinism.

This gives us a new definition of the transition function, which becomes a transition
relation:

$$
\delta \subseteq (Q \setminus A \times \Sigma)
\times ( Q \times \Sigma \times \{L,S,R\} )
$$

{{< math.inline >}}
So, given the tuple \((q_0, s_r) \in (Q \setminus A \times \Sigma)\) the machine
can choose to use any instruction in \((q_1, s_w, m) \in ( Q \times \Sigma \times
\{L,S,R\} )\) as long as \(((q_0, s_r),(q_1, s_w, m)) \in \delta\).
{{< /math.inline >}}
We say that a non-deterministic Turing machine (NDTM) accept an input if at least
one of the sequence of choices leads to an accepting state.

One way to visualize deterministic vs. non-deterministic TM is to use a configuration
graph. Each node of such a graph represent the configuration (state, head, content
of the tapes) of a machine at a given step. A node is connected to another node
if and only if the machine can go from the configuration of the first node to the
configuration of the other in just one step. When the configuration contains an
accepting state then it is a leaf on the graph.

Thus, with this information, this is what a configuration graph looks like for
a deterministic machine:

```goat
 .-.          .-.          .-.    T(n) steps    .-.
| 0 +------->| 1 +------->| 2 +---- · · · ---->| * |
 '-'          '-'          '-'                  '-'
```

And here is the one for the non-deterministic case (assuming exactly 2 choices
possible for each configuration):

```goat
                                                                                .-.    --+
                                     ···                                       | * |     |
                                .-. /                                           '-'      |
                       +-------+ 2 +                                                     |
                      /         '-' \                                                    |
                 .-. /               ···                                                 |
          +-----+ 1 +                                                                    |
         /       '-' \               ···                                                 |
        /             \         .-. /                                                    |
       /               +-------+ 2 +                                                     |
      /                         '-' \                                                    |
 .-. /                               ···            run for T(n) steps           ·       |
| 0 +                                       ------------------------------>      ·       |  at most 2^(T(n)) leafs
 '-' \                               ···                                         ·       |
      \                         .-. /                                                    |
       \               +-------+ 2 +                                                     |
        \             /         '-' \                                                    |
         \       .-. /               ···                                                 |
          +-----+ 1 +                                                                    |
                 '-' \               ···                                                 |
                      \         .-. /                                                    |
                       +-------+ 2 +                                                     |
                                '-' \                                           .-.      |
                                     ···                                       | * |     |
                                                                                '-'    --+             
```

Clearly, the non-deterministic case has more power given that it can check exponantialy
more than a derministic machine configuration in the same amount of steps.

One other way to consider NDTMs in terms of deterministic TMs is with the use of a certificate.
A certificate is a string of symbols that gives informations on the choices of an NDTM
to an accepting state. Thus it's possible to produce a certificate if and only if
an NDTM accepts a given input. Additionally, given a well enough made certificate
a deterministic TM can accept the same input as an NDTM, running in
{{< math.inline >}}\(T(n)\), in \(O(T(n))\){{< /math.inline >}} [^hind].

[^hind]: Hindsight is quite the power indeed

Turing Machines are quite the tool. This entry is this a quick peak at the versatility
they can offer. They are the backbone of computational complexity theory. We didn't
get to use them in any kind of useful way but I assure you that they will come in handy later.
