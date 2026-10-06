# Note 001 — Foundations

*Evolving note*

The question behind Accognition is whether a solved problem can suggest a structural transformation that becomes useful under another domain interpretation. I want to explore how to describe that transformation, how to separate it from its original context, and how to use its input and output structures to ask further questions.

This note introduces working vocabulary. The definitions may change as the examples become more precise.

## 1. Problems and constructions

A problem describes what counts as an acceptable result. A construction describes how a result is obtained.

For a simple deterministic setting, write a problem specification as

$$
P=(X,Y,\mathrm{Adm},R),
\qquad R\subseteq X\times Y,
$$

where $X$ is the input space, $Y$ is the output space, and $\mathrm{Adm}(x)$ identifies admissible inputs. The relation $R$ records acceptable input–output pairs.

A candidate implementation

$$
p:X\longrightarrow Y
$$

solves the specification if it is defined on every admissible input and

$$
\forall x\in X,\qquad
\mathrm{Adm}(x)\Longrightarrow (x,p(x))\in R.
$$

Several different outputs may be acceptable for the same input. An optimization problem, for example, may admit several minimizers. Several algorithms may also satisfy the same specification.

Probabilistic procedures, interactive tasks, and partial computations require richer descriptions. The simple notation is a starting point for the examples in these notes.

The object I would like to transfer is often a construction, a representation change, or a reusable part of a solution.

## 2. What remains when domain meaning is removed

A construction can be described through structural roles: objects, relations, types, parameters, rules, and conditions.

For nondomination, the domain objects might be investment alternatives, engineering designs, or database rows. An abstraction can retain a collection, a dominance relation, and the operation selecting its nondominated elements.

Removing domain meaning still leaves the formal information needed to define the operation. An order, a probability distribution, or a transition rule may be essential to the structural description.

I use **structural core** for such a description. “Independent of domain semantics” means that its roles can be interpreted in different domains. The chosen mathematical language still determines what the core can express.

The level of abstraction also matters. The powerset construction for automata is a specific construction. “Represent relevant context explicitly in the state” is a broader pattern that needs further specification.

## 3. Operators as typed schemas

A possible working record for an operator is

$$
O=(T_{\mathrm{in}},T_{\mathrm{out}},\Theta,\Gamma,p,Q).
$$

| Entry | Role |
| --- | --- |
| $T_{\mathrm{in}}$ | Required input structure |
| $T_{\mathrm{out}}$ | Resulting output structure |
| $\Theta$ | Formal parameters |
| $\Gamma$ | Applicability conditions |
| $p$ | Construction, rewrite, or program schema |
| $Q$ | Property expected to hold between input and output |

Together, $\Gamma$ and $Q$ form a **contract**: under these conditions, the construction is intended to have this property. Writing down $Q$ creates an obligation to justify it. It does not establish the property.

For example, a quotient schema needs an equivalence relation compatible with the structure being quotiented. A state-expansion schema needs an update rule and a precise account of the behavior to retain.

An operator schema may admit many parameter choices. A fixed, interpreted instance may realize an ordinary function. Keeping the schema and its instances distinct should make the vocabulary more useful.

The output can contain correspondence maps as well as a new object. Subset selection can return an inclusion; quotienting can return a quotient map; state expansion can return an observation map. Later constructions may need those maps.

Operators on data, transition systems, specifications, or proof states have different interfaces. A procedure that extracts operator schemas acts at another level again.

## 4. A representation-relative abstraction

There is generally more than one useful way to abstract a construction. The choice depends on a representation language $\mathcal L$, the intended transfer, and the observations that matter.

As informal bookkeeping, write

$$
(P_D,p_D)\rightsquigarrow_{\mathcal L}(O,h_D),
$$

where $(P_D,p_D)$ is a domain problem and a construction for it, $O$ is a proposed structural schema, and $h_D$ records its domain interpretation.

This notation describes a modeling choice. It does not assert a unique decomposition of a problem into structure and meaning.

To make that choice informative, I would need to say what $\mathcal L$ expresses, what the interpretation is allowed to supply, and which steps must remain explicit in $O$. An unrestricted interpretation could hide the entire solution and leave an uninformative core.

A useful abstraction should expose enough of the construction to guide a later interpretation.

## 5. Semantic interpretation

A **semantic interpretation** assigns domain objects and meanings to the schema's structural roles. It specifies how the required relations and parameters are realized, how the construction is carried out, and what its output means for the target problem.

Write provisionally

$$
O_D=\operatorname{Inst}(O,h_D).
$$

This is working notation for instantiation. Note 004 considers when a more precise, composition-preserving interpretation can be expressed using a functor.

The mapping can be explored in both directions. A known domain construction can suggest a core; a core can suggest domain constructions. These searches need different procedures. The maps involved need not be invertible.

Several constructions may support one core, and one construction may support several cores.

I use **semantic polymorphism** as a provisional label for a schema with several domain interpretations. The label helps describe the notebook's question; no claim of a new mathematical notion is intended.

## 6. A first example

Selecting nondominated elements can describe both a finite Pareto-front calculation and a database skyline query. The domain objects and the use of the result differ, while the selection rule can be expressed through the same dominance relation.

The comparison becomes useful when the correspondence is explicit: which objects are matched, which preferences define dominance, and which result is retained? Note 002 develops this example and a projection that breaks the correspondence.

State expansion offers a broader comparison. An automaton may represent a set of possible states; a duration-dependent stochastic model may represent a state together with elapsed age. Both make additional information available to a next-step rule. Their constructions and preservation requirements differ, so a common schema remains something to investigate.

## 7. Composition

Suppose two operator instances have compatible interfaces:

$$
p_1:X\to Y,\qquad p_2:Y\to Z.
$$

They suggest the composite

$$
p_2\circ p_1:X\to Z.
$$

Applicability also needs to be checked. The first construction must produce an input satisfying the second construction's conditions. For the declared parameter choices, one required condition is

$$
\Gamma_1(x)\Longrightarrow\Gamma_2(p_1(x)).
$$

Properties recorded in $Q_1$ may help establish this implication. Merely giving the intermediate objects the same broad type name does not settle it.

A composed construction also needs to satisfy the target problem's acceptable-result relation. A defined transformation, a useful solution, and an interesting research question are separate things to assess.

## 8. Questions to carry forward

I want to understand which parts of a construction remain reusable when its domain interpretation changes, and how much information a structural core must retain to guide that change.

The phrase **cognitive operator** is another provisional idea. These schemas might help describe some reasoning steps. Whether they describe human cognition would require its own investigation.

For now, Accognition is an evolving collection of representations, examples, counterexamples, and questions. These notes can make an idea precise without presenting it as an established scientific result.

Next: [Note 002 — Structural Correspondence](note-002-structural-correspondence.md).
