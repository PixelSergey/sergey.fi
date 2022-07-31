---
layout: post
category: [blog]
title: "On the definition of triviality"
author: PixelSergey
---

One can often hear the word "trivial" being thrown around when studying mathematics.
Unfortunately, no one quite seems to know what it means.

Various sources provide the following definitions:

> "A claim or a case which can be readily obtained from context" - Wikipedia

> "A solution or example that is ridiculously simple and of little interest" - Math StackExchange

> "Trust me bro" - Mathematics professors

None of these seem very satisfying to me.
They all seem to be lacking some sort of... concreteness, in a way?
They also seem to depend heavily on the context of where they're used.
In this post I will be trying to establish a more concrete and objective definition for this often misused word.

---

## What constitutes a good definition?

One thing to note: I want to define *triviality* for **problems and proofs** in mathematics.
This is not exactly the same as, say, trivial structures
(e.g. the "trivial" empty set `Ø` or the "trivial" Group containing only an identity element).

There are a few things that I want to encompass with my definition:

1. Objectivity

    Triviality should be an objective measure of a problem.
    It shouldn't really depend on your level of education or familiarity with the field.
    Anyone should be able to look at a problem
    and categorise it as trivial or non-trivial in the same way.

1. Universality

    The definition should apply to different fields of mathematics equally.
    That is, one should be able to categorise any arbitrary problem as either trivial or non-trivial
    regardless of the frame of reference.
    Note that this does not imply Uniqueness, as discussed next!

1. Non-uniqueness

    A problem can be categorised as *both* trivial and non-trivial
    depending on the field of mathematics or axiomatic system we are looking at it from.
    Therefore, triviality should be a measure of a problem
    *under a certain mathematical frame of reference*, and not in isolation.


That last point may deserve some motivation and elaboration.
Consider the following problem and solution:

$$\frac{d}{dx}\sin^2x=2\sin x\cos x=\sin\left(2x\right)$$

This is certainly trivial for someone on a high-school level acquainted with
standard results, such as the derivative of the sine function and the chain rule.
However, to actually prove this from first principles requires quite a bit of effort
(knowledge and geometric proof of the limit of sin x / x,
proof of the chain rule, maybe even inventing the definition of the derivative!),
which is most definitely a non-trivial task.

A similar effect can be seen when considering the slightly simpler problem \(1+1=2\),
which is trivial for anyone over the age of three but takes about
[362 pages to prove from axioms in the Principia Mathematica](https://en.wikipedia.org/wiki/Principia_Mathematica).


---

## Definitions

The following section will consist of me gradually developing a definition
to suit my above requirements.

### 1: A problem is considered *trivial* if it can be easily solved.

Nope. This is no good.
This definition is a popular one, and misses the point.
After all, trivial problems are not necessarily easy!
They are just, in a way... straightforward.

Perhaps the existence of a method of solving a problem would be good.
In a way, if you can memorise a certain algorithm to solve a problem
then it becomes rather trivial.

### 2: A problem is considered *trivial* if there exists an algorithm for its solution.

This is better, but is also incomplete.
This is probably the definition that Feynman was thinking of when he said:

> "Mathematicians can prove only trivial theorems, because every theorem that’s proved is trivial."

Sure, okay, it's funny, but also misses the point.
The *existence* of an algorithm or proof shouldn't itself classify problems as trivial,
or we would end up with the notion that everything is either trivial or unsolved!
(Which seems to be [another quote](https://shreevatsa.wordpress.com/2010/04/03/on-trivial-in-mathematics/))

I think adding some sort of qualification specifying what *kind* of algorithm must exist would fix the problem.

### 3: A problem is considered *trivial* if there exists a trivial algorithm for its solution.

Oops, recursive definition!
That's not very helpful.
Let's try again.

### 4: A problem is considered *trivial* if there exists a straightforward algorithm for its solution.

The word "straightforward" I added here is better but is still very hand-wavy.
What do I mean by it? An algorithm with few steps? An algorithm which can be easily memorised?
With computers performing billions of operations per second and memorising giga-tera-exa-...-bytes of data,
I don't think this either of these constitutes a good definition.

Ideally, I would like something objective about the nature of the algorithm.
Perhaps the class of problems an algorithm can be applied to would be better.

### 5: A problem is considered *trivial* if there exists an algorithm for its solution, which can also be applied to solve other, similar problems.

Now my problem is reduced to defining what the criterion to be a "similar" problem is.

I am trying to get at an idea I had while doing repetitive homework problems at school.
While repeatedly counting up circles in first grade
or solving first-order linear differential equations in my final year of high school,
I always got the feeling that I was performing the same operations
on different but similar problems (and felt dread as a result).
These problems were the pinnacle of "triviality" for me: despite sometimes being long and compliated,
they only required me to apply the same standard set of steps to solve them.

An idea from Group theory comes to mind: what if there was a notion of
isomorphism (an extended notion of equality) between problems?
Two problems that require an identical (or almost identical) algorithm to solve,
could be considered isomorphic.

After a quick search on the internet, in found that apparently someone has had this idea before!
In the article titled
[How to Create Isomorphic Example-Problem Pairsfor Facilitating Analogical Thinking](https://iopscience.iop.org/article/10.1088/1742-6596/1397/1/012083/pdf) (F M Pastoriko and E Retnowati 2019 J. Phys.: Conf. Ser. 1397 012083),
the authors discuss how to construct isomorphic problems
and how to teach students to recognise such problems and think through them logically.

In my opinion, this is great pedagogical advice!
On a more related note, I will use this notion of isomorphic problems to construct a definition for triviality.

### 6: A problem is considered *trivial* if there exists an algorithm which can be used to solve it and its isomorphic problems.

The problem with this definition is that
isomorphic problems are solvable by the original problem's algorithm by definition.
Also, if one cannot derive isomorphic problems from a certain problem,
we are back to definition 2, which only required an algorithm for solution.
In my opinion, if the problem is *unique* (i.e. it doesn't have problems isomorphic to it),
it is more likely (or could it even be guaranteed?) for it to be non-trivial.

### 7: A problem is considered *trivial* if there exists an algorithm for its solution and a sufficient number of isomorphic problems can be derived from it.

This definition guarantees that a unique problem is non-trivial.
I am not 100% happy with this, but I also cannot think of a trivial, unique problem at the moment.

I could also specify that the algorithm has to be in polynomial time (or otherwise be by a non-bruteforce method).

Otherwise, I am quite content with this definition.
One thing I also forgot to specify was that the definition is specific to a certain (mathematical) frame of reference.

### 8: A problem is considered *trivial* under a certain frame of reference if there exists a non-exhaustive algorithm for its solution and a sufficient number of isomorphic problems can be derived from it.

This is all I can muster at the moment. The definition seems to cover all of the cases I can think of...

Here are some problems and their classifications under this final version thereof:

| Problem | Frame of reference | Trivial? |
| -- | -- | -- |
| $$\int e^x\sin x\ dx$$ | High school calculus | Yes |
| [Travelling salesman problem](https://www.youtube.com/watch?v=GiDsjIBOVoA) | Competitive programming / discrete mathematics | No (existence of non-exhaustive algorithm violated) |
| Fermat's last theorem | All of modern mathematics | No (cannot derive isomorphic problems) |

Does this seem reasonable?

---

## Implications

The final definition provided can be applied to a few real-world scenarios to see its implications.

Firstly, this definition could be used to show that almost the entirety of my high school maths syllabus,
IB Higher Level Mathematics (Analysis and Approaches), was trivial.
Despite some problems being hard, in general, there existed an algorithm to solve almost every problem
on the final exam. Our teaching consisted of learning these algorithms and our revision period
consisted of doing isomorphic problems for each topic until we were comfortable with the syllabus material.
The real "challenge" of my high school education was, therefore, learning these algorithms and keeping
up my skills for the duration of three years.

Would I be happy in considering high school maths to be trivial? Yes, I'd say so.
I could even extend this notion to all of my IB high school sciences.
The physics and chemistry exams I took required exactly the same revision strategy as maths:
identify the questions, remember some things, and recall the algorithm used to solve the problems.
Funnily enough, attempting to classify the humanities (such as Psychology) as trivial fails:
there is no one "algorithm" that one can learn to solve the questions there; rather, a thorough
understanding of the topics and good writing skills to pander to the examiners is required.
Note that this finding makes no comment about the relative difficulty of the subjects:
**triviality is not equal to ease**.

Another implication of this definition of triviality is that software development is trivial.
Though this claim might raise a few eyebrows, this is something that I've intuitively felt for ages.
In my opinion, the "algorithm" used to develop software is rather straightforward:
Identify the problem you want to solve, split it up into parts, and search up how to solve each part on StackOverflow.
Although creative thought is required when developing software,
the thought is quite a lot more linear and "trivial" than that of, for example, competitive or algorithmic programming.

This would also explain why many modern companies,
in particular the [FAANG group](https://en.wikipedia.org/wiki/Big_Tech),
use algorithmic problems to test candidates during a software development interview.
I often hear complaints stating things like
"These problems have nothing in common with what you do at work!",
"These problems don't test my ability at all!", or
"When will I ever need this in the real world?".
The reasons, in my opinion, stem back to triviality.
Companies are really not interested in how you solve the trivial problem of developing some code,
since that only requires reciting the three basic steps I outlined above.
Instead, they want to see you approach a non-trivial problem and develop a solution
for something that might be outside your comfort zone.
Looking at it this way, it would seem that this approach is really quite logical
and effective at filtering out only the best possible candidates!

---

## Conclusion

Disagree with the implications I presented?
Found a clear counter-example to my final definition and feel like it deserves an improvement?
Got any other comments on this?

**[Contact me!](https://sergey.fi/contact/)**


<script src="https://polyfill.io/v3/polyfill.min.js?features=es6"></script>
<script id="MathJax-script" async src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js"></script>
