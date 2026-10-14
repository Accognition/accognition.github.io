# Note 009 — Transfer Through Preserved Structure

*Evolving note — 14 October 2026*

Topological combinatorics offers a concrete model for an idea behind Accognition: a construction or result can become useful in another setting when a change of representation preserves the structure on which that result depends.

I want to investigate this principle across different mathematical representations, and make the resulting transfers searchable and composable. The common question is which parts of a solved problem remain usable under another interpretation, what justifies their reuse, and which further questions become accessible through that correspondence.

This note develops the connection through an established example: spaces built from disconnected graphs and spaces built from set partitions can have the same homotopy type. It then uses that example to clarify the proposed generalization in Accognition.

## 1. Preservation is relative to the intended result

A useful correspondence need not retain every feature of the original object. It needs to retain enough information to justify the intended construction or conclusion.

For a topological question, that may mean preserving homotopy type or homology. For an automaton, the relevant observation may be its accepted language. For an optimization construction, the objective, feasible set, and comparison relation may determine what must survive.

Consequently, a transfer should name the property it supports. Two representations can agree for one purpose and differ for another.

This gives a working principle:

> Identify the structure required by a construction or result, establish how that structure is represented in a target setting, and transport only the conclusions justified by the checked correspondence.

The structural core therefore includes the assumptions and preservation conditions. They help explain both why a transfer works and where it fails.

## 2. An example: graphs and partitions

Fix a labelled vertex set $[n]=\{1,\ldots,n\}$, with $n\geq 4$. Consider:

- $P_n$: nonempty edge sets of disconnected simple graphs on $[n]$, ordered by edge inclusion;
- $Q_n$: set partitions of $[n]$, excluding the all-singleton partition and the one-block partition, ordered by refinement.

“Nonempty” concerns the edge set: every graph still has all $n$ labelled vertices. In the refinement order, $\pi\leq\rho$ means that every block of $\pi$ lies in a block of $\rho$.

Sending a graph to its connected components gives a monotone map

$$
f:P_n\longrightarrow Q_n.
$$

For four vertices:

| Edge set | Component partition |
| --- | --- |
| $\{12,23\}$ | $\{1,2,3\}\mid\{4\}$ |
| $\{12,23,13\}$ | $\{1,2,3\}\mid\{4\}$ |
| $\{12,34\}$ | $\{1,2\}\mid\{3,4\}$ |

The map forgets internal edges. To relate the spaces built from these orders, complete each component to a clique:

$$
c(G)=\text{the union of the complete graphs on the components of }G.
$$

This is an extensive, monotone, idempotent map on $P_n$. Its fixed points correspond exactly to $Q_n$. The construction and its topological consequence are standard [1, Example 5.2.8].

## 3. The reusable operator

For a finite poset $P$, its order complex $\Delta(P)$ has elements of $P$ as vertices and nonempty chains as simplices. Write $|\Delta(P)|$ for its geometric realization.

Suppose $c:P\to P$ satisfies

$$
x\leq c(x),\qquad
x\leq y\Longrightarrow c(x)\leq c(y),\qquad
c(c(x))=c(x).
$$

Define

$$
F=\operatorname{Fix}(c)=\{x\in P:c(x)=x\}.
$$

The restriction $r:P\to F$ of $c$ and inclusion $i:F\to P$ satisfy

$$
r\circ i=\mathrm{id}_F,
\qquad
\mathrm{id}_P\leq i\circ r.
$$

Pointwise comparable monotone maps induce homotopic maps on order complexes. Hence

$$
\boxed{|\Delta(P)|\simeq|\Delta(F)|.}
$$

This is the closure-operator principle [1, Exercise 5.2.6].

As an Accognition schema, the transformation is

$$
O_{\mathrm{cl}}:(P,c)\longmapsto(F,i,r).
$$

Its input conditions are the finite-poset structure and the three closure laws. Its output includes the reduced order and correspondence maps. Its contract guarantees homotopy equivalence of the realizations.

Completing graph components is one realization of this schema. Other finite orders with checked closure operators admit the same general argument. The interpretation supplies the concrete objects and map; the schema carries the reusable reasoning.

## 4. A result that actually transfers

For $n=4$, the two order complexes have different combinatorial descriptions. Counting their chains gives:

| Complex | Vertices | Edges | Filled triangles |
| --- | ---: | ---: | ---: |
| $\Delta(P_4)$ | 25 | 54 | 24 |
| $\Delta(Q_4)$ | 13 | 18 | 0 |

The second complex is a connected graph. There are six three-block partitions and seven two-block partitions. Each three-block partition has one two-element block. It lies below two partitions obtained by attaching a singleton to that block and one obtained by merging the two singletons. Thus there are $6\cdot3=18$ edges.

Its number of independent cycles is

$$
\beta_1=18-13+1=6.
$$

It has the homotopy type of six circles joined at a common point. The closure correspondence transfers that result to $|\Delta(P_4)|$, despite its additional vertices, edges, and triangular faces.

More generally, both realizations have the homotopy type

$$
|\Delta(P_n)|\simeq|\Delta(Q_n)|
\simeq\bigvee_{j=1}^{(n-1)!}S^{n-3}.
$$

Here $\bigvee$ means that one point from each sphere is identified. This established result is reviewed in [2, Proposition 2.1].

The cycles in this example belong to spaces of graph configurations and partitions. The transferred invariant describes how those configurations fit together.

## 5. A nearby abstraction that fails

Consider retaining only the number of connected components:

$$
\kappa:P_4\longrightarrow C,
\qquad
C=\{3\prec2\}.
$$

A nonempty disconnected graph on four vertices has either three or two components. Adding edges can only merge components, so $\kappa$ is monotone under the displayed order.

However, $\Delta(C)$ is one filled interval. It is contractible and has

$$
H_1(|\Delta(C)|;\mathbb Z)=0.
$$

The source has

$$
H_1(|\Delta(P_4)|;\mathbb Z)\cong\mathbb Z^6.
$$

Thus an order-preserving summary can still lose the invariant of interest. The full component partition retains distinctions that the component count discards.

This supplies a useful pair for Accognition: a justified representation change and a nearby, explicitly rejected one. Matching broad input and output types would not distinguish them; their preservation contracts do.

## 6. What is generalized in Accognition?

The example suggests a broader organization of transfer:

| Setting | Intended preserved result | Relevant obligation |
| --- | --- | --- |
| Closure reduction of a finite poset | Homotopy type of its order complex | Extensivity, monotonicity, and idempotence |
| Pareto selection and a skyline query | Corresponding nondominated outputs | A correspondence preserving and reflecting dominance |
| Exact deterministic state reduction | Specified observations under admitted actions | Updates descend through the representation |
| Sound approximation | Inclusion of concrete outcomes in represented possibilities | An explicit soundness relation |

The later rows are discussed in [Note 002](note-002-structural-correspondence.md), [Note 004](note-004-categorical-semantics.md), and the reachability framing in [Note 005](note-005-knowledge-gaps-and-reachability.md).

Each row has its own mathematical conditions. A proposed common framework must represent those differences. Exact equivalence, a directional guarantee, and a bounded approximation can each support useful transfers.

I therefore see three dimensions of the proposed generalization:

1. **Representations:** allow different formal descriptions, including orders, transition systems, optimization specifications, and topological spaces.
2. **Contracts:** state which observations, constructions, or conclusions survive a correspondence.
3. **Search:** extract candidate schemas, find target interpretations, compose compatible transformations, and use failures to revise the collection.

Topological methods provide an established model for this architecture. Accognition's research question concerns how that organization could guide the discovery and development of further transfers.

## 7. From a correspondence to a search neighborhood

A successful transfer can expose additional operators that accept its output, produce its input, or act on the correspondence maps.

The closure example suggests investigating:

- other closure operators on the same order;
- smaller fixed-point descriptions;
- operations that preserve the chosen invariant after reduction;
- a richer representation when a later task requires information discarded by the reduction.

Such questions turn a correspondence into an entry point for further research. This is the operator-neighborhood search of [Note 003](note-003-automating-research.md).

For instances $p_1:X\to Y$ and $p_2:Y\to Z$, a candidate composition requires

$$
\Gamma_1(x)\Longrightarrow\Gamma_2(p_1(x))
$$

on the intended inputs. Compatible contracts can then justify an end-to-end result. If both steps preserve the same declared observation through their respective maps, that observation can be traced through the composite.

When a categorical model is appropriate, composition-preserving interpretations express part of this compatibility. The representation must also express the assumptions and result being transported, as discussed in Note 004.

## 8. Preservation can change with the next question

The graph completion discards distances and internal edge counts. Its topological contract does not provide those quantities for the original graphs.

A later task can therefore change what the structural core needs to retain. This connects the present idea to Note 005: a representation adequate for the current observation may become inadequate under an enlarged repertoire of operations, so reachability must be indexed by the intended observation and preservation contract.

There are several possible responses. An investigation might retain extra data, use a different representation, restrict the admitted operations, or adopt a weaker result with an explicit bound. A failure should identify the missing distinction or unmet condition so that it can guide one of those choices.

Representation choice, operator choice, and intended observation consequently belong in the same transfer record.

## 9. A record for an inspectable transfer

A useful entry would contain:

| Part | What should be recorded |
| --- | --- |
| Source | The construction or result and its original assumptions |
| Core | Formal roles, transformation, and applicability conditions |
| Target interpretation | Concrete objects, relations, parameters, and maps |
| Preservation | The exact, directional, or approximate contract |
| Transport | How a source conclusion yields the target conclusion |
| Boundary | A counterexample or known unsupported observation |
| Composition | Conditions required by incoming and outgoing operators |
| Evidence and cost | Proof or verification scope, implementation work, and checking effort |

For the worked example, this record includes component completion, the closure laws, the fixed-point correspondence with partitions, the transferred homotopy type, and the failed component-count summary.

A search system could retrieve that record when it encounters another ordered family with a candidate closure operation. It would still need to establish the target conditions and assess whether the resulting invariant helps answer the target question.

An initial experiment could ask whether access to such records helps find valid reductions and reject nearby invalid ones, compared with searching by domain language alone. A further experiment could investigate whether a discovered correspondence helps propose and check useful neighboring constructions.

## 10. The proposed position

Accognition investigates structural transfer as a research process: extract reusable transformations, interpret them under checked conditions, compose them, and let applications and failures improve the repertoire.

Topological combinatorics makes one part of this idea tangible. Different discrete structures can support the same conclusions through a carefully chosen representation and a preservation theorem. The proposed generalization extends the range of representations and contracts, and studies how to find and develop those correspondences.

The mathematical transfer above is established. A general Accognition framework would earn its scope through explicit operator families, worked transfers, failure cases, and evidence that their organization assists the search.

## References

1. Michelle L. Wachs. *Poset Topology: Tools and Applications*. See Section 1.1 and Section 5.2, particularly Exercise 5.2.6 and Example 5.2.8. [Author's lecture notes](https://www.math.miami.edu/~wachs/papers/toolnotes.pdf).
2. Eric Babson, Anders Björner, Svante Linusson, John Shareshian, and Volkmar Welker. *Complexes of not i-connected graphs*. Topology 38 (1999), 271–299. See Proposition 2.1. [Preprint](https://arxiv.org/pdf/math/9705219).

Previous: [Note 007 — A Complete Discovery Cycle](note-007-complete-discovery-cycle.md).
