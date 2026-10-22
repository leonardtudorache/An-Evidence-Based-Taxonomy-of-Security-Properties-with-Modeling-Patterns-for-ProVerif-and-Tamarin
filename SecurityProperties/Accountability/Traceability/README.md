# Traceability

*Section 4.2.5 of the paper.*

## Informal definition

Traceability is defined as the ability for a trusted entity to trace a message back to the sender to avoid malicious behaviors.

## Formal definition

- $send(A, m)$: agent $A$ sends message $m$.
- $computeId(m)$: a function that returns the identity of the agent who actually sent message $m$.

$$
\forall A, m:\ send(A, m) \implies computeId(m) = A
$$

## Notes

- The models in this folder (`Untraceability.*`) are an RFID tag-reader protocol that checks the correspondence $ReaderEnd(id) \implies TagStart(id)$. They do not instantiate $computeId$; see the header comments of the model files.

## Files

| File | Content |
|---|---|
| `Untraceability.md` | Sequence diagram (Mermaid) of the example protocol, with event placement |
| `Untraceability.pv` | ProVerif model |
| `Untraceability.spthy` | Tamarin model |

## Running

```bash
proverif SecurityProperties/Accountability/Traceability/Untraceability.pv
tamarin-prover --prove SecurityProperties/Accountability/Traceability/Untraceability.spthy
```
