# Anonymity

*Section 4.2.4 of the paper.*

## Informal definition

Anonymity is defined as the confidentiality of the identification of agents of a protocol. Only authorized parties have access to relevant identification elements.

## Formal definition

$$
P(id_1) \approx P(id_2)
$$

The notation expresses that the protocol process $P$, instantiated with identity $id_1$, is observationally equivalent to the same process instantiated with a different identity $id_2$. Thus, no external observer can determine which identity was actually used based on the observable outputs of the process.

In practice, many of the surveyed protocols verify a secrecy-based approximation of this property instead, treating the identifier itself as a value that must remain unknown to the attacker. This is more tractable to verify than full observational equivalence, and is expressed as a trace property in first-order logic:

- $actor(B, id)$: agent $B$ is a legitimate actor in the protocol with unique identifier $id$.
- $K(x)$: value $x$ is known by the attacker.

$$
\forall B, id:\ actor(B, id) \implies \lnot K(id)
$$

## Notes

- The models in this folder verify the secrecy-based approximation (`query attacker(p_id)` in ProVerif, lemma `Secret_ID` over `Actor` in Tamarin), not the equivalence $P(id_1) \approx P(id_2)$.

## Files

| File | Content |
|---|---|
| `Anonymity.md` | Sequence diagram (Mermaid) of the example protocol, with event placement |
| `Anonymity.pv` | ProVerif model |
| `Anonymity.spthy` | Tamarin model |

## Running

```bash
proverif SecurityProperties/Privacy/Anonymity/Anonymity.pv
tamarin-prover --prove SecurityProperties/Privacy/Anonymity/Anonymity.spthy
```
