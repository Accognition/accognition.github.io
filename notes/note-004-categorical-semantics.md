# Note 004 — Categorical Semantics

*Evolving note*

The earlier notes use structures, transformations, interpretations, and composition. Category theory may help organize selected parts of that vocabulary. I want to introduce it through the job it could perform: describing how an interpretation relates constructions and their compositions.

This note sketches possible formal settings. Each setting still needs to be chosen and justified for the operator family under consideration.

## 1. Choosing objects and arrows

A category specifies objects, morphisms between objects, identity morphisms, and associative composition.

For a chosen fragment of the notebook, objects might represent admissible structured spaces or specifications. Arrows might represent constructions between them. The representation must state what counts as an arrow and when two arrows are equal.

An abstract category $\mathcal A$ could organize selected structural constructions. A domain category $\mathcal D$ could organize their chosen domain realizations.

The phrase “domain category” refers to this model of a selected fragment. It is not a claim that an entire scientific field comes with one canonical category.

Conditional applicability also needs a place in the model. Refined input objects can incorporate conditions, or an operator can be represented as a parameterized family of admissible arrows. A full schema record from Note 001 is not automatically a single morphism.

Several-input constructions can sometimes use product objects. Partial, relational, or probabilistic constructions need an appropriate choice of arrows and composition.

## 2. Interpretations as functors

An interpretation that respects the chosen categorical structure can be described by a functor

$$
F_D:\mathcal A\longrightarrow\mathcal D.
$$

It assigns an object $X$ to $F_D(X)$ and a morphism $f:X\to Y$ to

$$
F_D(f):F_D(X)\to F_D(Y).
$$

Functoriality requires

$$
F_D(\mathrm{id}_X)=\mathrm{id}_{F_D(X)},
\qquad
F_D(g\circ f)=F_D(g)\circ F_D(f).
$$

For an abstract construction $f$, its realized arrow is $F_D(f)$. A functor acts on that arrow; the expression $F_D\circ f$ would mix different kinds of objects in this notation.

Several functors can give the same abstract construction different domain realizations. This is one possible precise setting for the provisional idea of semantic polymorphism.

An introduction to this compositional viewpoint is [R21].

## 3. What composition preservation contributes

Suppose $f:X\to Y$ and $g:Y\to Z$ are valid abstract constructions. A functor sends their composite to the composite of their domain realizations.

For a longer admissible sequence,

$$
F_D(f_n\circ\cdots\circ f_1)
=F_D(f_n)\circ\cdots\circ F_D(f_1).
$$

This makes a particular compatibility requirement explicit: interpreting the composite agrees with composing the interpretations.

One possible abstract model starts with generating constructions and imposes equations between their compositions. A proposed interpretation must respect those equations to define a functor out of that model.

For example, if nondomination is represented as an endomorphism $n$ and the model includes $n\circ n=n$, a functorial interpretation must satisfy the corresponding idempotence equation.

The practical question is which objects, arrows, and equations retain the information needed for the intended transfer.

## 4. Preservation laws must be represented

An ordinary functor preserves identities, composition, and equations already expressed in its source category. Other desired properties require additional structure and conditions.

An optimality statement depends on an objective and feasible set. A probabilistic statement depends on a probability model. A complexity claim depends on an implementation and cost model.

If those requirements are absent from the representation, the word “functor” does not supply them.

The projection counterexample in Note 002 illustrates the issue. A well-defined map of representations can fail to preserve nondominated outputs. The correspondence must retain the particular relation and observations needed by that operation.

I would therefore record the operator contract alongside the proposed categorical setting and identify where each obligation is expressed.

## 5. Interpreting and extracting are different tasks

A functor $F_D:\mathcal A\to\mathcal D$ describes a chosen interpretation. It does not provide an algorithm for extracting $\mathcal A$ or its operator schemas from domain examples.

Extraction still needs a representation language, a generalization procedure, and a way to judge candidate abstractions. Interpretation needs concrete objects, constructions, and checked correspondence conditions.

The equation

$$
a_Y\circ p_D=p_A\circ a_X
$$

from Note 002 can express one such condition when the maps are represented in a suitable common setting, for example as functions.

Its meaning is determined by the observations retained by $a_X$ and $a_Y$. Reversibility, reconstruction, and target usefulness remain separate requirements.

Category theory can describe some relationships between representations without automatically finding the representations or making them useful.

## 6. Interpreting assumptions and theories

For some schemas, the most useful starting point may be an abstract vocabulary together with axioms.

A nondomination schema can require a finite collection and an irreflexive, transitive relation. A domain interpretation supplies objects and a relation and establishes those requirements. The construction can then be interpreted under its stated contract.

This is close to the idea of a theory interpretation: abstract symbols are assigned meanings while the required axioms remain valid.

A fully formal treatment would choose a logic and define the relevant notion of theory morphism. At the notebook stage, the immediate use is simpler: make the vocabulary mapping and the assumptions visible.

An interpretation that matches the names but fails an axiom is a concrete failed transfer to retain.

## 7. Lossy abstraction and Galois connections

Some useful representations deliberately lose information. Abstract interpretation provides a way to study sound approximations of computations [R13].

For posets $(C,\le_C)$ and $(A,\le_A)$, monotone maps

$$
\alpha:C\to A,\qquad \gamma:A\to C
$$

form a Galois connection when

$$
\alpha(c)\le_A a
\quad\Longleftrightarrow\quad
c\le_C\gamma(a).
$$

Here the orders can express inclusion of represented possibilities. The maps relate an abstract description to the concrete possibilities it includes.

For example, take concrete sets of integers and abstract intervals, both ordered by inclusion. Include the empty interval and unbounded intervals so the abstraction is defined for every set. The abstraction takes the interval hull; the concretization takes the integers in an interval.

Then

$$
\alpha(\{1,3\})=[1,3],
\qquad
\gamma([1,3])=\{1,2,3\}.
$$

The abstract description contains an extra possibility. It can still support a sound statement about where the concrete values lie.

For a concrete transformer $T:C\to C$ and an abstract transformer $T^\#:A\to A$, one soundness condition is

$$
\alpha(T(c))\le_A T^\#(\alpha(c)).
$$

Under the Galois connection, this implies

$$
T(c)\le_C\gamma(T^\#(\alpha(c))).
$$

This gives a precise directional requirement for a chosen abstraction. It does not guarantee precision, efficiency, or a procedure for finding useful $\alpha$ and $\gamma$.

## 8. State and behavior: a coalgebraic direction

For transition and observation systems, a coalgebraic description may be useful [R22]. Given an endofunctor $B$, a coalgebra has the form

$$
c_X:X\to B(X).
$$

The choice of $B$ determines the kind of one-step behavior represented. For a deterministic automaton, one choice is

$$
B(X)=\{0,1\}\times X^\Sigma,
$$

recording acceptance and one next state for each symbol. For a finite Markov chain, a distribution-valued behavior can describe the next-state probabilities.

A structure-preserving map $h:X\to Y$ between two $B$-coalgebras satisfies

$$
B(h)\circ c_X=c_Y\circ h.
$$

For finite Markov chains and a map sending states to partition blocks, this requirement becomes equality of the transition probabilities aggregated into each block. It connects to the lumpability condition in Note 003.

The behavioral relationship must be chosen for the system. Accepted-language equivalence, state-by-state correspondence, and equality of projected probability laws have different meanings. A common state vocabulary cannot replace those distinctions.

This direction may help formalize particular state-expansion and reduction families. Its suitability for those families remains a question to work through.

## 9. Keeping the formal language proportional

A categorical description is useful here if it clarifies a concrete ambiguity: which compositions are admissible, which equations an interpretation must respect, or which observations a representation change retains.

More elaborate machinery can wait until a worked example requires it. The immediate task is to specify a small setting well enough to check its laws and connect it back to a domain construction.

I want to avoid choosing a broad formal language before knowing what distinction it needs to express.

## 10. Questions for later notes

Which operator families can be represented cleanly by a small category of constructions? Where is a typed schema with explicit assumptions sufficient? When does a sound approximation help more than an exact correspondence? How should the categorical model and its interpretations evolve when constructions are learned, composed, or invented? A new generator needs an interpretation, while a newly imposed equation must hold under every interpretation of the revised model. [Note 006 — Discovering Transformations](note-006-discovering-transformations.md) considers this change to the repertoire.

How should an abstraction learner propose a structural core, and how should a separate interpretation procedure test its domain realizations? Can observations and failed compositions help revise the core?

These questions continue the same notebook project. The formal examples provide tools for thinking about it; they do not establish a general theory of scientific discovery.

References: [shared reading list](../references.md).

Previous: [Note 003 — Automating Research](note-003-automating-research.md). Next: [Note 005 — Knowledge Gaps and Reachability](note-005-knowledge-gaps-and-reachability.md).
