# Non-injective Agreement

*Section 4.2.1 of the paper.*

## Informal definition

An agent $A$ has a non-injective agreement with an agent $B$ if, whenever $A$ finishes the protocol believing they communicated with $B$, $B$ has been running the protocol before, believing they were interacting with $A$, and both used the same data. However, several completed runs of $A$ may be justified by the same run of $B$. Thus, it does not guarantee a one-to-one relationship.

## Formal definition

**Predicates** (shared by all authentication properties)

- $end(A, B, t, i)$: agent $A$ has completed a run of the protocol, apparently with agent $B$, with term $t$, at time (or trace step) $i$.
- $start(B, A, t, j)$: agent $B$ has started (or participated in) a protocol session with agent $A$, with term $t$, at time $j$.

$$
\forall A, B, t, i:\ end(A, B, t, i) \implies \exists j:\ start(B, A, t, j)
$$

## Files

| File | Content |
|---|---|
| `Non-injectiveAgreement.md` | Sequence diagram (Mermaid) of the example protocol, with event placement |
| `Non-injectiveAgreement.pv` | ProVerif model |
| `Non-injectiveAgreement.spthy` | Tamarin model |

## Running

```bash
proverif SecurityProperties/Authentication/Non-injectiveAgreement/Non-injectiveAgreement.pv
tamarin-prover --prove SecurityProperties/Authentication/Non-injectiveAgreement/Non-injectiveAgreement.spthy
```
