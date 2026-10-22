# Mutual Authentication

*Section 4.2.1 of the paper.*

## Informal definition

Mutual authentication holds when two agents, $A$ and $B$, each independently authenticate the other's participation in the same protocol session. It is not a new primitive but the symmetric composition of Lowe's agreement in both directions: $A$ agrees with $B$ on the session, and $B$ agrees with $A$ on the same session. This is not a security property primitive but a mechanism employing authentication bi-directionally.

## Formal definition

**Predicates** (shared by all authentication properties)

- $end(A, B, t, i)$: agent $A$ has completed a run of the protocol, apparently with agent $B$, with term $t$, at time (or trace step) $i$.
- $start(B, A, t, j)$: agent $B$ has started (or participated in) a protocol session with agent $A$, with term $t$, at time $j$.

$$
\forall A, B, t_1, t_2, i, i':\ \big(end(A, B, t_1, i) \implies \exists j:\ start(B, A, t_1, j)\big) \land \big(end(B, A, t_2, i') \implies \exists j':\ start(A, B, t_2, j')\big)
$$

## Notes

- In the models, the start and end events are role-specific (`startI`/`endI` raised by the initiator and `startR`/`endR` raised by the responder in ProVerif; `StartI`/`EndI`/`StartR`/`EndR` in Tamarin), so that each query states which role obtains the guarantee and which role must have started.
- The Tamarin model is a bounded-session result: the responder is restricted to a single session (initiator sessions, certificate issuance and the adversary remain unbounded). See the comment in `MutualAuthentication.spthy`.

## Files

| File | Content |
|---|---|
| `MutualAuthentication.md` | Sequence diagram (Mermaid) of the example protocol, with event placement |
| `MutualAuthentication.pv` | ProVerif model |
| `MutualAuthentication.spthy` | Tamarin model |

## Running

```bash
proverif SecurityProperties/Authentication/MutualAuthentication/MutualAuthentication.pv
tamarin-prover --prove SecurityProperties/Authentication/MutualAuthentication/MutualAuthentication.spthy
```
