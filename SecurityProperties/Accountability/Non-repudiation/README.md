# Non-repudiation

*Section 4.2.5 of the paper.*

## Informal definition

Non-repudiation property for protocols ensures that its agents are able to provide evidence that another agent previously transmitted a message, which can be presented to a judge to prove its behavior.

## Formal definition

- $sent(A, m)$: agent $A$ genuinely sent/authorized message $m$.
- $evidence(e, A, m)$: $e$ is evidence (e.g., a signature) binding agent $A$ to message $m$.
- $verifies(J, e, A, m)$: judge $J$, given evidence $e$, confirms that $A$ is bound to $m$.

$$
\forall J, e, A, m:\ verifies(J, e, A, m) \land evidence(e, A, m) \implies sent(A, m)
$$

The notation expresses that whenever a judge $J$ verifies evidence $e$ as binding agent $a$ to message $m$, $a$ must have genuinely sent $m$. This makes explicit who the judge is (any independent third party checking the evidence, not just the original recipient), what the evidence is (an artifact cryptographically bound to both the agent and the message, e.g. a signature), and what is being proved (that $a$ cannot deny having sent $m$).

## Notes

- The models in this folder are an auction example checking $Won(p, id) \implies Bid(p, id)$; they have no separate judge role or evidence term (see the header comments of the model files).

## Files

| File | Content |
|---|---|
| `Non-Repudiation.md` | Sequence diagram (Mermaid) of the example protocol, with event placement |
| `Non-Repudiation.pv` | ProVerif model |
| `Non-repudiation.spthy` | Tamarin model |

## Running

```bash
proverif SecurityProperties/Accountability/Non-repudiation/Non-Repudiation.pv
tamarin-prover --prove SecurityProperties/Accountability/Non-repudiation/Non-repudiation.spthy
```
