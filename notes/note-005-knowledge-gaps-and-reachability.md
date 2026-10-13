# Note 005 — Knowledge Gaps and Reachability

*Evolving note*

What discoveries become possible through transformations we already possess? The earlier notes describe constructions and ways to check correspondences. Here I want to distinguish what is recorded from what could be reached by applying a recorded repertoire.

## 1. Known constructions and reachable constructions

Let $K$ be a collection of known constructions, representations, and established results. Let $\mathcal O$ be a repertoire of available operators. Provisionally, write

$$
\mathcal R_{\mathcal O}(K)
=\operatorname{Reach}_{\mathcal O}(K).
$$

This is the closure of $K$ under finite, well-typed applications and compositions of operators in $\mathcal O$, including zero-step reachability of the original material. It contains constructions that may not yet have been recorded as explicit applications. Reachability is a formal possibility under the selected model; it does not mean that someone has recognized, checked, or found a useful interpretation.

The notation is representation-relative. A concrete account has to specify:

- a representation language $\mathcal L$, including which objects, relations, operator contracts, and compositions it can express;
- the admissible interpretations of those representations in target domains;
- the conditions under which an operator may be applied and the observations its contract preserves;
- resource limits, such as a bound on derivation length, computation, memory, or source inspection.

For example, a resource-bounded envelope can be written $\mathcal R_{\mathcal O}^{B,\mathcal L}(K)$, where $B$ gives the chosen limits. An operator with a matching type but an unmet applicability condition does not extend the envelope. If a proposed transfer has not established its contract, it is a lead to check, not a verified member of the reachable set.

## 2. Uneven coverage and the convex-hull metaphor

Existing knowledge rarely covers a field evenly. It may contain many developed constructions in a few regions and sparse descriptions elsewhere. Structural transfer can expose a connection between those regions: a construction known in one setting may become interpretable in another, or a sequence of familiar operations may suggest an unrecorded method.

This is the intended role of the **convex-hull metaphor**. Imagine developed regions of knowledge as points or neighborhoods in a space of structural features. The repertoire and its compositions outline an envelope around what is already represented. A transfer may connect parts of that envelope that domain-by-domain organization leaves far apart.

The metaphor is not itself a geometric claim. A literal convex hull would require an embedding, a vector space, and a meaningful notion of interpolation. Operator reachability is one possible formal counterpart: it asks what can be derived by declared transformations from known material. It captures neither every kind of intellectual possibility nor the value of a discovery.

## 3. A collection gap is not yet an opportunity

Note 003's operator–domain table records which interpretations have been documented, checked, refuted, or left unresolved. An empty or “not found” cell means only that the current collection has not recorded a case. Sources may be missing; a construction may be known under different terminology; the representation may not express the relevant conditions.

It helps to separate three claims:

| Claim | Evidence needed |
| --- | --- |
| Collection gap | The current table has no recorded entry for this operator and domain pairing |
| Valid candidate | A target interpretation can be stated, applicability checked, and the operator contract justified |
| Discovery opportunity | The valid construction also serves a useful goal and is previously unexplored within a stated search scope |

Validity, usefulness, and novelty are distinct. A valid construction can be irrelevant to the target problem. A useful construction may already be well known. Absence from a notebook or a database search is not, by itself, evidence of novelty. Any novelty assessment needs a stated source collection, search strategy, and stopping point.

The table remains valuable as a map of attention. Its gaps suggest questions to investigate; they should not be presented as discoveries before those questions are answered.

## 4. From local cells to a global envelope

The operator–domain table from Note 003 gives a local view: it organizes candidate interpretations for selected operators and domains. $\mathcal R_{\mathcal O}(K)$ gives a broader view: it asks which constructions and compositions can be reached from the whole collection under the recorded repertoire.

The two views can inform one another. A gap in the table can suggest a reachable interpretation to test. A checked interpretation can add evidence to the table and reveal a missing condition, a useful composition, or a limitation in the representation. Conversely, a table full of documented examples does not show that the repertoire has been composed broadly or that the useful envelope has been explored.

One possible record for a reachability lead would include its derivation from $K$, the operators and parameters used, the target interpretation, the contract checks, the resource budget, and the unresolved usefulness or novelty questions. This keeps a derivation inspectable without equating derivability with discovery.

## 5. Questions for later notes

How should the representation language decide which derivations count as the same construction? Which resource limits make comparisons meaningful? How can an investigation estimate what has been explored beyond its own collection? What evidence would distinguish an unrecorded but routine application from a useful new connection?

Note 006 turns to the complementary question: how could the repertoire itself acquire a new transformation?

References: [shared reading list](../references.md).

Previous: [Note 004 — Categorical Semantics](note-004-categorical-semantics.md). Next: [Note 006 — Discovering Transformations](note-006-discovering-transformations.md).
