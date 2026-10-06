# Note 003 — Automating Research

*Evolving note*

The first two notes describe a possible unit of transfer and ways to examine a correspondence. Here I ask whether those descriptions could guide the search for further constructions.

The title names a direction to explore. At this stage, the notebook contains ideas for an inspectable research assistant, examples, and possible experiments.

## 1. Moving between examples and structures

A domain construction can suggest an operator schema. That schema can suggest a new interpretation, a composition, or a change of representation. Investigating the resulting construction can then revise the schema.

There are two connected search spaces:

- a **structural space** of typed schemas, relations, conditions, compositions, and refinements;
- a **semantic space** of domain problems, constructions, observations, and goals.

An interpretation connects a structural description to a domain realization. The connection can support exploration in either direction, but the searches need not undo one another.

This is the intuition I want to investigate: knowledge of a construction's input and output structures might change which questions become visible in another domain.

## 2. Extracting a candidate schema

Given solved examples, extraction asks which structural roles and steps are reusable, which parameters vary, and which conditions explain the result.

A skyline example can suggest nondomination. Comparing several state constructions might suggest a narrower state-expansion family, or show that a proposed family is too broad.

The original construction and the extracted schema should have separate records. The extraction may omit an assumption, select an unhelpful abstraction level, or encode too much domain detail.

Symbolic generalization and program-library learning provide relevant reading directions [R7, R8]. They offer concrete ways to think about reusable descriptions; their existence does not settle which description is useful here.

I would start with a small manually checked collection. Learning schemas from unrestricted scientific literature can be explored later, after the representation itself has been exercised.

## 3. A prospective interpretation

For a proposed target domain, an operator entry could guide the following questions:

1. Which target objects realize its input roles?
2. Which target relations and parameters realize its requirements?
3. Are the applicability conditions satisfied?
4. How is the target construction actually carried out?
5. Which property connects its input and output?
6. Does that property help with the target problem?

A proposal can remain unresolved when a condition has not been checked. A refutation should identify the failed condition or give a counterexample.

For example, the age-expansion idea from Note 002 suggests checking duration dependence in a regime model. The proposal must specify a transition law and its modeling assumptions. Merely adding an elapsed-time variable does not establish that the resulting empirical model is Markov.

A useful record would contain the source, the proposed schema, the target interpretation, the concrete construction, the intended benefit, and the next check that could clarify it.

## 4. Gaps in a collection

An operator–domain table can help organize exploration. This is a schematic example:

| Operator | Domain $D_1$ | Domain $D_2$ | Domain $D_3$ |
| --- | --- | --- | --- |
| $O_1$ | Documented | Candidate | Not found in collection |
| $O_2$ | Checked under stated contract | Refuted interpretation | Candidate |
| $O_3$ | Unresolved applicability | Documented | Checked under stated contract |

“Documented” records a source. “Checked” records a particular check and its scope. “Refuted” concerns a specified interpretation or contract; another interpretation may still work.

“Not found” describes the current collection. The construction might be known elsewhere or under another name. It is a reason to search, not evidence of novelty.

The table should retain sources, assumptions, and failures behind each status. Otherwise an apparently empty cell may conceal a missing source or an incompatible representation.

## 5. Choosing where to look

A close structural match with a distant domain interpretation can be an interesting search lead. Semantic distance is only a way to prioritize attention.

Applicability, target relevance, likely checking effort, and computational cost also matter. A structurally valid construction may be impractical or solve a problem nobody needs solved.

Domain language remains useful for finding sources and describing goals. Structural matching adds another index for comparing the roles and transformations those sources describe.

I would like to compare semantic retrieval, structural matching, and their combination before assuming that the structural index adds value.

## 6. Exploring an operator's neighborhood

Recognizing an operator also exposes possible incoming and outgoing constructions. For an instance $p_O:X\to Y$, write informally

$$
\begin{aligned}
\operatorname{In}(O)&=\{H\mid p_H:W\to X\},\\
\operatorname{Out}(O)&=\{K\mid p_K:Y\to Z\}.
\end{aligned}
$$

The spaces $W$ and $Z$ vary. Membership is provisional until the contracts, parameters, and observations are compatible.

Suitable instances suggest

$$
p_K\circ p_O\circ p_H.
$$

Other directions include alternative constructions with the same interface, decompositions into smaller steps, weakened assumptions, and operations that consume both the original input and its result.

This is where the earlier idea of **operator-guided abstraction** belongs. An identified core provides questions for the next search and may make additional reusable steps easier to notice.

## 7. Nondomination: restriction and layering

Let all sets below be finite subsets of one strict partial order, with the inherited relation. A restriction operation gives

$$
\operatorname{Restrict}_C(S)=S\cap C.
$$

It can be followed by nondomination. The order of operations matters:

$$
\operatorname{ND}(S\cap C)\ne\operatorname{ND}(S)\cap C
$$

in general. If $S=\{a,b\}$, $b$ dominates $a$, and $C=\{a\}$, the left side is $\{a\}$ and the right side is empty.

In a domain interpretation, a feasibility filter applied after frontier selection can therefore discard the element needed for the feasible answer.

Nondomination is idempotent:

$$
\operatorname{ND}(\operatorname{ND}(S))=\operatorname{ND}(S).
$$

To obtain further layers, retain the original set and remove the extracted frontier:

$$
\begin{aligned}
R_0&=S,\\
L_t&=\operatorname{ND}(R_t),\\
R_{t+1}&=R_t\setminus L_t.
\end{aligned}
$$

Every nonempty finite strict partial order has a maximal element. The loop therefore terminates and partitions $S$ into layers. The example in Note 002 gives $\{A,B,D\}$ followed by $\{C\}$.

The next operation needs the remaining collection as well as the frontier. This illustrates why correspondence maps and access to the original input can matter.

## 8. Nondomination: merging summaries

For finite $U,V$ under the same strict partial order,

$$
\operatorname{ND}(U\cup V)
=\operatorname{ND}\bigl(\operatorname{ND}(U)\cup\operatorname{ND}(V)\bigr).
$$

A discarded element has a maximal dominator within its finite input set. By transitivity, that maximal element can replace it as a dominance witness. This yields the identity.

The identity suggests partitioning a collection, computing local frontiers, and merging those frontiers. It also supports insertion into an existing frontier summary under the same relation.

Deletion needs more information: removing a frontier element can expose an element previously discarded. Changing the dominance relation can also invalidate a summary.

These are elementary properties of the declared mathematical setting. Their role in the notebook is to show how one recognized construction leads to additional compositions and failure cases.

## 9. State expansion: what can follow it?

The output of state expansion suggests questions about reachability, reduction, aggregation, products, and approximation.

For an automaton, unreachable subset states can be removed. The resulting DFA also admits language-preserving minimization. Its representation suggests an expansion–pruning–reduction sequence.

For a stochastic model, state aggregation requires a different contract. In a finite Markov chain with transition matrix $P$, a partition $\mathcal B$ is strongly lumpable precisely when, for every $B,C\in\mathcal B$ and all $x,x'\in B$,

$$
\sum_{y\in C}P(x,y)
=\sum_{y\in C}P(x',y).
$$

The common block probabilities define one Markov transition law on blocks for every initial distribution [R25, Theorem 2.3].

In Note 002's toy age model with absorbing destination $j$, merging $(i,0),(i,1),(i,2)$ fails this condition: their exit probabilities to $j$ are $1/4$, $2/3$, and $1$.

State expansion therefore suggests a neighboring aggregation question, and the contract explains why erasing age is invalid in this example. A shared word such as “state” does not determine the correct reduction.

## 10. Revising the collection

Comparing related constructions may reveal a useful suboperator, a repeated composition, or a distinction between families previously grouped together.

Let $\mathcal L_t$ be the active operator collection, $\mathcal E_t$ newly examined evidence, and $\mathcal H_t$ the archive of investigations. A possible bookkeeping rule is

$$
\mathcal L_{t+1}
=\operatorname{Revise}(\mathcal L_t,\mathcal E_t),
\qquad
\mathcal H_t\subseteq\mathcal H_{t+1}.
$$

The active collection may gain, split, merge, correct, or retire entries. The archive retains why an interpretation was proposed or rejected.

More entries do not by themselves indicate progress. A useful revision should make later constructions easier to find, interpret, or check.

The recursive direction remains open: examples suggest cores; cores guide searches; examined constructions suggest revised cores.

## 11. Questions for a small experiment

A first experiment could use a fixed collection of schemas and target problems with independently checkable answers. It would ask whether the representation helps find a valid interpretation and reject a nearby invalid one.

Useful comparisons would give semantic retrieval, structural matching, and a combined approach the same sources and comparable search budgets. I would record valid useful proposals, missed opportunities, false proposals, checking effort, and construction cost.

A separate experiment could allow schema extraction and collection revision. Keeping those experiments separate would help identify what each layer contributes.

Holding out a domain presentation does not guarantee an unfamiliar example for a pretrained model. Related variants should be grouped, and any limits of the holdout should remain explicit.

The modest question is whether this organization helps with a selected set of tasks. Broader usefulness, new applications, and human cognitive interpretation remain questions for later notes.

References: [shared reading list](../references.md).

Previous: [Note 002 — Structural Correspondence](note-002-structural-correspondence.md). Next: [Note 004 — Categorical Semantics](note-004-categorical-semantics.md).
