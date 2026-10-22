# Aliveness

*Section 4.2.1 of the paper.*

## Informal definition

This is the weakest form of authentication, which ensures that agent $B$ has been running the protocol at some point in the past, but it does not guarantee that agent $B$ interacted with agent $A$, or that the protocol has been running recently.

## Formal definition

**Predicates** (shared by all authentication properties)

- $end(A, B, t, i)$: agent $A$ has completed a run of the protocol, apparently with agent $B$, with term $t$, at time (or trace step) $i$.
- $start(B, A, t, j)$: agent $B$ has started (or participated in) a protocol session with agent $A$, with term $t$, at time $j$.

$$
\forall A, B, i, t_1:\ end(A, B, t_1, i) \implies \exists C, j, t_2:\ start(B, C, t_2, j)
$$

## Files

| File | Content |
|---|---|
| `Aliveness.md` | Sequence diagram (Mermaid) of the example protocol, with event placement |
| `Aliveness.pv` | ProVerif model |
| `Aliveness.spthy` | Tamarin model |

## Running

```bash
proverif SecurityProperties/Authentication/Aliveness/Aliveness.pv
tamarin-prover --prove SecurityProperties/Authentication/Aliveness/Aliveness.spthy
```
