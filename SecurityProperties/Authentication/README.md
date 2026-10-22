# Authentication

_Section 4.2.1 of the paper._

## Informal definition

A fairly common property that appears in some of the surveyed papers is authentication provided some compromise did not happen. This is not a new authentication primitive but a relaxation of the base authentication (agreement) definition: $A$'s agreement with $B$ on the session holds unless the relevant key was already compromised. This is a property that is actually provable and honest about the real guarantee, that there is no such thing as authentication surviving total key compromise for a symmetric or asymmetric identity check alone. Nevertheless, what counts as a compromise is protocol-specific, as it may be a long-term key reveal, a sequence-number leak, or a session-identifier disclosure, and is therefore left abstract in the definition below.

## Formal definition

**Predicates** (shared by all authentication properties)

- $end(A, B, t, i)$: agent $A$ has completed a run of the protocol, apparently with agent $B$, with term $t$, at time (or trace step) $i$.
- $start(B, A, t, j)$: agent $B$ has started (or participated in) a protocol session with agent $A$, with term $t$, at time $j$.
- $compromise(A, t, i)$: a relevant compromise involving agent $A$, with a leak of term $t$, occurred at time $i$. Its concrete definition depends on the considered protocol. An example of compromise is a leaked long-term key.

$$
\forall A, B, t, i:\ end(A, B, t, i) \implies \exists j, k, l:\ start(B, A, t, j) \lor compromise(A, t, k) \lor compromise(B, t, l)
$$

## Sub-properties

| Property                | Folder                                               |
| ----------------------- | ---------------------------------------------------- |
| Aliveness               | [`Aliveness/`](Aliveness/)                           |
| Weak agreement          | [`WeakAgreement/`](WeakAgreement/)                   |
| Non-injective agreement | [`Non-injectiveAgreement/`](Non-injectiveAgreement/) |
| Injective agreement     | [`InjectiveAgreement/`](InjectiveAgreement/)         |
| Mutual authentication   | [`MutualAuthentication/`](MutualAuthentication/)     |

## Files

| File                   | Content                                                                  |
| ---------------------- | ------------------------------------------------------------------------ |
| `authentication.md`    | Sequence diagram (Mermaid) of the example protocol, with event placement |
| `authentication.pv`    | ProVerif model                                                           |
| `authentication.spthy` | Tamarin model                                                            |

## Running

```bash
proverif SecurityProperties/Authentication/authentication.pv
tamarin-prover --prove SecurityProperties/Authentication/authentication.spthy
```
