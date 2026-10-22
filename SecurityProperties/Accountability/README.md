# Accountability

_Section 4.2.5 of the paper._

## Informal definition

Accountability is a property of a system or protocol that ensures that if a security goal is violated, the responsible parties can be identified. The verification of this property usually requires a trusted third-party judge.

## Formal definition

Following the definition introduced by Künnemann et al., we capture the intuition in the following way:

- $\phi$: protocol-specific property that holds.
- $blame(A, j)$: agent $A$ is responsible for failure at trace point $j$.
- $compromised(A)$: agent $A$ is compromised.

$$
\lnot\phi \iff \exists A, j:\ blame(A, j) \lor compromised(A)
$$

This formulation is a simplification. In the definition of Künnemann et al., the blamed parties must additionally be a sufficient and minimal cause of the violation, i.e., they alone could have caused it, and no proper subset of them could. Expressing this requires quantifying over counterfactual traces, so accountability is not a single trace property. The authors also consider coalitions of colluding parties, which they handle with a case-based verdict function, and reduce accountability to a set of verification conditions: trace properties, some over all traces and some over a single (existential) trace. They prove these conditions sound and complete. For details, we refer the reader to the original paper.

## Sub-properties

| Property        | Folder                                 |
| --------------- | -------------------------------------- |
| Traceability    | [`Traceability/`](Traceability/)       |
| Non-repudiation | [`Non-repudiation/`](Non-repudiation/) |

## Files

| File                   | Content                                                                  |
| ---------------------- | ------------------------------------------------------------------------ |
| `Accountability.md`    | Sequence diagram (Mermaid) of the example protocol, with event placement |
| `Accountability.pv`    | ProVerif model                                                           |
| `Accountability.spthy` | Tamarin model                                                            |

## Running

```bash
proverif SecurityProperties/Accountability/Accountability.pv
tamarin-prover --prove SecurityProperties/Accountability/Accountability.spthy
```
