# Injective Agreement

_Section 4.2.1 of the paper._

## Informal definition

This is the strongest level of authentication, where there is a non-injective agreement between agent $A$ and agent $B$ with a strict one-to-one relationship. Agent $A$ has an injective agreement with agent $B$ if, whenever $A$ finishes the protocol believing they communicated with $B$, $B$ has been running the protocol before, believing they were interacting with $A$, and both used the same data. Additionally, distinct executions of agent $A$ correspond to distinct executions of agent $B$, i.e., there is a one-to-one correspondence between $A$'s completed runs and $B$'s corresponding runs. Thus, no single run of $B$ is used to justify more than one completed run of $A$.

## Formal definition

**Predicates** (shared by all authentication properties)

- $end(A, B, t, i)$: agent $A$ has completed a run of the protocol, apparently with agent $B$, with term $t$, at time (or trace step) $i$.
- $start(B, A, t, j)$: agent $B$ has started (or participated in) a protocol session with agent $A$, with term $t$, at time $j$.

$$
\forall A, B, t, i:\ end(A, B, t, i) \implies \exists j:\ start(B, A, t, j) \land j < i \land \lnot \exists A_2, B_2, i_2:\ end(A_2, B_2, t, i_2) \land i_2 \neq i
$$

This definition means that a term can be used exactly once. It can be relaxed by allowing a term to be used multiple times still requiring injectivity:

$$
\forall A, B, t, i:\ end(A, B, t, i) \implies start(B, A, t, f(i)) \land f(i) < i,
$$

where $f$ is injective:

$$
\forall i, i':\ f(i) = f(i') \implies i = i'
$$

## Files

| File                       | Content                                                                  |
| -------------------------- | ------------------------------------------------------------------------ |
| `InjectiveAgreement.md`    | Sequence diagram (Mermaid) of the example protocol, with event placement |
| `InjectiveAgreement.pv`    | ProVerif model                                                           |
| `InjectiveAgreement.spthy` | Tamarin model                                                            |

## Running

```bash
proverif SecurityProperties/Authentication/InjectiveAgreement/InjectiveAgreement.pv
tamarin-prover --prove SecurityProperties/Authentication/InjectiveAgreement/InjectiveAgreement.spthy
```
