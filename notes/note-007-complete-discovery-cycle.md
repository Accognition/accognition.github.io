# Note 007 — A Complete Discovery Cycle

*Evolving note*

How do transfer and transformation invention interact in one investigation? This worked example connects a familiar state expansion, a second interpretation, a failed reduction, and a refinement of the operator record.

The labels below distinguish **established constructions**, **illustrative gaps** in this notebook's coverage, and **speculative proposals**. An illustrative gap is not a claim that the construction is unknown in the literature. The example demonstrates a workflow, not a new scientific discovery.

## 1. Start with a solved domain problem

**[Established construction]** Let a nondeterministic finite automaton have finite state set $Q$, alphabet $\Sigma$, transition function $\delta_N:Q\times\Sigma\to 2^Q$, initial state $q_0$, and accepting states $F$. The subset construction produces a deterministic automaton whose states are subsets $U\subseteq Q$ and whose transition is

$$
\delta_D(U,a)=\bigcup_{q\in U}\delta_N(q,a).
$$

The initial state is $\{q_0\}$, and a subset is accepting if it intersects $F$. With epsilon transitions, epsilon closure must also be included. This deterministic automaton recognizes the same language [R12].

The original problem is solved: construct a deterministic recognizer with the same accepted language as the given NFA.

## 2. Extract its structural transformation

**[Established construction, abstracted]** The automaton construction suggests a broader state-completion schema: augment a representation with the context needed to make its next-step rule well-defined, then update that context as the system evolves. For the NFA, the expanded state is the set of possible current states after a prefix. Its contract includes:

- finite input state structure and a defined transition rule;
- an expanded state space of subsets (and epsilon closure when needed);
- an update rule that depends only on the expanded state and next input symbol;
- an observation mapping from expanded states to the represented original possibilities;
- preservation of the accepted language.

This description is intentionally close to the automaton construction. A broader schema such as “store relevant context in the state” would need further parameters and a more specific contract.

## 3. Identify another interpretation

**[Established example, reframed]** Consider the discrete semi-Markov age model from Note 002, with visible state $i$ and sojourn duration

$$
\Pr(D_i=1)=\tfrac14,\qquad
\Pr(D_i=2)=\tfrac12,\qquad
\Pr(D_i=3)=\tfrac14,
$$

followed by a transition to an absorbing state $j$. The visible state alone does not determine the next-step probability: it depends on how long the process has remained at $i$.

The possible structural correspondence is that the representation stores the context needed for its next-step rule. Here the context is elapsed age, not a set of possible automaton states. This tests the broader state-completion schema, not an identification of the two domain constructions; the respective context updates and preservation contracts remain domain-specific.

## 4. Construct and check the transferred solution

**[Established construction]** Let the expanded states be $(i,a)$ for ages $a=0,1,2$, together with $(j,0)$. At an age with positive survival probability, define

$$
h_i(a)=\Pr(D_i=a+1\mid D_i>a).
$$

The age expansion stays at the visible state with age increment when the process does not exit, and enters $(j,0)$ when it exits:

$$
\begin{aligned}
\Pr((i,0)\to(i,1))&=\tfrac34,&\Pr((i,0)\to(j,0))&=\tfrac14,\\
\Pr((i,1)\to(i,2))&=\tfrac13,&\Pr((i,1)\to(j,0))&=\tfrac23,\\
\Pr((i,2)\to(j,0))&=1.
\end{aligned}
$$

The exit probabilities at ages zero, one, and two are $1/4$, $2/3$, and $1$. The expanded process is Markov: its next-step probabilities depend on $(i,a)$. Starting from $(i,0)$, its visible sojourn probabilities are $1/4$, $(3/4)(2/3)=1/2$, and $(3/4)(1/3)=1/4$, as required.

The observation map sends every $(i,a)$ to $i$ and $(j,0)$ to $j$. Under the declared duration law and renewal assumptions, this map recovers the modeled visible process. The transfer check concerns this concrete contract; merely adding an age field to arbitrary time-series data would not establish the Markov property.

## 5. Explore compatible operations

**[Established operations, with conditions]** On an expanded state system one can ask about reachability pruning, aggregation, or other reductions. Pruning states unreachable from the declared initial state preserves behavior from that initial state. Aggregation needs a separate condition: for a finite Markov chain, a partition must be strongly lumpable if the quotient is to have one Markov transition law valid for all initial distributions [R25].

For the toy model, try merging the three age states into the visible state $i$. This would erase the age context that made the expanded chain Markov. The reduction needs to be checked rather than assumed safe.

## 6. Encounter a preservation failure

**[Established counterexample]** Use the partition with one block $I=\{(i,0),(i,1),(i,2)\}$ and a second block $J=\{(j,0)\}$. The probabilities of moving from each state in $I$ to $J$ are respectively

$$
\tfrac14,\qquad \tfrac23,\qquad 1.
$$

They are unequal, so the partition is not strongly lumpable. The visible projection is meaningful, but it does not turn the age-dependent process into a first-order Markov chain on $\{i,j\}$. The attempted reduction fails the selected preservation condition.

## 7. Propose a refinement

**[Speculative proposal]** Refine the operator record from “expand, then reduce” to a contract-aware sequence:

1. Expand the state with the context needed for the next-step rule.
2. Prune only states unreachable under the declared initial conditions.
3. Aggregate states only when the chosen preservation condition holds, such as strong lumpability for a Markov quotient.

The refined reduction operator should state its partition, the observations to preserve, the initial-state scope, and the condition that makes the quotient valid. If the condition fails, the merge is refuted for that contract; the expanded representation remains available. Whether this sequence is useful or novel in a particular application still needs investigation.

## 8. Investigate another application with the revised repertoire

**[Established application; illustrative for this workflow]** Return to the automaton. After the subset construction, remove unreachable subsets from the initial subset. This pruning preserves the accepted language because no run from the initial state can visit a removed subset. Any further state merging would require its own equivalence and language-preservation argument.

This second application exercises the refined repertoire: expansion makes a desired local rule available, and reduction is admitted only with a stated preservation check. In the automaton case the relevant contract is language preservation; in the stochastic case it is a projected process law or Markov quotient. The same abstract question leads to domain-specific conditions.

The **illustrative gap in this notebook** is an integrated case record: Notes 002 and 003 discuss state expansion, the attempted reduction, and its preservation failure, but do not yet trace those pieces through an explicit contract revision and a second application. This note assembles that workflow. It is a gap in this account, not a claim about what is known elsewhere.

## 9. Questions for the next investigation

Which observations should a reduction preserve: a language, a process law, a set of reachable outputs, or only an approximation? Can a common operator schema express the condition without hiding domain-specific obligations? What source search would be needed before making any novelty claim?

The intended feedback process is: **applications produce evidence; evidence suggests abstractions; abstractions revise the repertoire; the revised repertoire enables further applications.**

References: [shared reading list](../references.md).

Previous: [Note 006 — Discovering Transformations](note-006-discovering-transformations.md).
