# Weak Agreement

*Section 4.2.1 of the paper.*

## Informal definition

An agent $A$ has a weak agreement with another agent $B$ whenever $A$ completes a run of the protocol, believing they interacted with $B$. Nevertheless, the fact that $B$ was executing the protocol under the assumption of interacting with $A$ does not necessarily imply that $B$ assumed the role of peer.

## Formal definition

**Predicates** (shared by all authentication properties)

- $end(A, B, t, i)$: agent $A$ has completed a run of the protocol, apparently with agent $B$, with term $t$, at time (or trace step) $i$.
- $start(B, A, t, j)$: agent $B$ has started (or participated in) a protocol session with agent $A$, with term $t$, at time $j$.

$$
\forall A, B, t_1, i:\ end(A, B, t_1, i) \implies \exists t_2, j:\ start(B, A, t_2, j)
$$

## Files

| File | Content |
|---|---|
| `WeakAgreement.md` | Sequence diagram (Mermaid) of the example protocol, with event placement |
| `WeakAgreement.pv` | ProVerif model |
| `WeakAgreement.spthy` | Tamarin model |

## Running

```bash
proverif SecurityProperties/Authentication/WeakAgreement/WeakAgreement.pv
tamarin-prover --prove SecurityProperties/Authentication/WeakAgreement/WeakAgreement.spthy
```
