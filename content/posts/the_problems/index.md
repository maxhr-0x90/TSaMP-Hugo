---
title: "The Problems"
date: 2022-09-25T16:34:57+02:00
draft: false
weight: 2
summary: Where it all begins.
tags: ["lore"]
---

Let's waste no time ! We need to find a Millennium Problem.  
But to do so we must understand what each of them are. So here is a quick summary
of each one. Not to worry though, as I'm a layman myself it'll thus be in layman's terms.
If you are in a hurry to the point of not carring about the the accuracy of
the content you're consuming, those TL;DRs[^tldr] are made for you :sunglasses:.
Nonetheless, for the big brains amongst you, in time, there will be TS;WM[^tswm],
in the form of other entries.

Anyway here are those summaries :

[^tldr]: DEQ Ltd. is not responsable for the loss of any information during the
TL;DR compression process.
[^tswm]: Too Short; Want More

## Compression Level: Decent

Those summaries shouldn't be too detrimental to the understanding of the core
idea/principle of the problem.

### P versus NP

**Field**: Theoretical computer science

**Status**: {{< color fc="red" >}}Unsolved{{< /color >}}

Let's start with the easiest to explain. The goal here is to find out whether every
problem whose solution can be quickly verified can also be quickly solved.

**TS;WM**: Maybe later

### Riemann hypothesis

**Fields**: Number theory

**Status**: {{< color fc="red" >}}Unsolved{{< /color >}}

This will be swift. There is this zeta function
({{< math.inline >}}\(\zeta(s),~s\in\mathbb{C}\){{< /math.inline >}} [^sets])
that prime enjoyers really love, especially when it hits 0. Riemann though that,
except for the {{< math.inline >}}\(s=-2n,~n\in\N\){{< /math.inline >}} [^sets] inputs,
{{< math.inline >}}\(\zeta(s)=0,~then,~Re(s)=\frac{1}{2}\){{< /math.inline >}}
[^real]. Is he correct ?

**TS;WM**: Lost it :pensive:

[^real]: The real part of s. If you don't get it, don't worry it's complex.

## Compression Level: Dangerous

Sorry. We are in TL;DR realm, sacrifices had to be made.

### Navier–Stokes existence and smoothness

**Field**: Partial differential equations

**Status**: {{< color fc="red" >}}Unsolved{{< /color >}}

This one has many options accepted as a resolution of the problem. And thus offers
more ways to be wrong :smile:. Given equations that describe the motion of a fluid
in {{< math.inline >}}\(\R^3\){{< /math.inline >}}.
You need to either:

1. Prove the existence and smoothness of the solutions in {{< math.inline >}}\(\R^3\){{< /math.inline >}}[^3d]  
  Meaning the solutions are defined and have no abrupt change in value
2. Prove the breakdown of the solutions in {{< math.inline >}}\(\R^3\){{< /math.inline >}}[^3d]  
  Meaning there are some inputs that breaks the assumptions of the equations
3. Prove the existence and smoothness of the solutions in
{{< math.inline >}}\(\mathbb{T}^3\){{< /math.inline >}} [^torus]  
  Same thing as 1. but this time in a torus
4. Prove the breakdown of the solutions in {{< math.inline >}}\(\mathbb{T}^3\){{< /math.inline >}} [^torus]  
  Same thing as 2. but this time in a torus

**TS;WM**: My dog ate it

[^3d]: Good ol' 3D space :cowboy:
[^torus]: 3D Torus space; hyper-donut if you will

### Birch and Swinnerton-Dyer conjecture

**Field**: Number theory

**Status**: {{< color fc="red" >}}Unsolved{{< /color >}}

Some people cannot enjoy the fact reals ({{< math.inline >}}\(\R\){{< /math.inline >}} [^sets]) exist.  
For exemple: the Birch and Swinnerton-Dyer conjecture states that there is a way
to know if an elliptic curve of the form:

$$
y^2 = x^3+ax+b
$$
with {{< math.inline >}}\(a,~b \in \Z\){{</ math.inline >}} [^sets],
has solutions in the rationals, meaning:
{{< math.inline >}}\(x,~y \in \mathbb{Q}\){{</ math.inline >}} [^sets].  
And if there are finitely -- or infinitely -- many of them.

**TS;WM**: Last time I checked, you had it :unamused:

### Poincaré conjecture

**Field**: Geometric topology

**Status**: {{< color fc="green" >}}Solved{{< /color >}}

This one is solved. Why even bother. No money, no master plan. But in an act of
great magnanimity, a summary will be provided.  
If you don't know topology, we are on the same boat. But from what can be gathered
on the internet, it's mostly about this gif of a mug morphing into a donut:

{{< more "Topology (most of it)" >}}
![Mug to Donut](Mug_and_Torus_morph.gif)
{{< /more >}}

It's the art of finding geometric similarity between objects if you were allowed
to absolutely disfigure them. In this context of warping madness, the Poincaré conjecture
asserts that if an object has the same properties as the 3-sphere[^3spere] (simply connected,
closed) then it can be deformed to be the 3-sphere (or something that can be deformed
to the 3-sphere)[^morph].

**TS;WM**: It's solved, this would be a waste of time

[^3spere]: A sphere for laypersons is a 2-sphere for topologists. Thus a 3-sphere is
an hypersphere, which is -- as always -- a bit confusing to think about.
[^morph]: homeomorphic to the 3-sphere, as the cool kids say nowadays

## Compression Level: Dreadful

Why even bother :skull:

### Yang–Mills existence and mass gap

**Field**:  Mathematical physics

**Status**: {{< color fc="red" >}}Unsolved{{< /color >}}

If you like finishing games to 100%, this one is yours. In a nutshell, the task here
is to find equations that describe the bedrock of quantum field theories while being
in accordance with the mass gap observed in reality. And even though most physicists
aren't actively waiting for this one to be solved, as they already have their
experimental results. It would still be kinda cool -- for the sake of knowledge and
completism -- to find the underlying equations.

**TS;WM**: This part is left as an exercise to the reader

### Hodge conjecture

**Fields**: Algebraic geometry & complex geometry

**Status**: {{< color fc="red" >}}Unsolved{{< /color >}}

Ok, pretty sure this one was made to deter ignoramus like myself from even
attempting to think about it. The bare-bone idea is that some elements (Hodge
cycle) can always be expressed as a composition of other elements.  
That's as far as I can go without having to read a book :pensive:

**TS;WM**: Nope.

[^sets]: [Number sets](https://en.wikipedia.org/wiki/Set_(mathematics)#Special_sets_of_numbers_in_mathematics)

With all of this information I can easily finish step one of my master plan. Once
I've made up my mind on the matter, the [Progress](/posts/progress) entry will be updated.

---

Till we meet again, remember to always be less dense than your notation.  
Goodbye traveler :smile:
