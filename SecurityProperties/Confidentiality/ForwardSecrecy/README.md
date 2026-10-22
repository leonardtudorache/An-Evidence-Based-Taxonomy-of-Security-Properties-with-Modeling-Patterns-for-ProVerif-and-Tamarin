# Forward Secrecy

*Section 4.2.3 of the paper.*

## Informal definition

Forward secrecy property, also known as perfect forward secrecy, is a property of key exchange protocols that ensures past session keys remain secure even if long-term secret keys (used for authentication or key negotiation) are later compromised.

## Formal definition

- $sessionKey(k, ltk, t)$: the session key $k$ was established at time $t$ using long-term key $ltk$.
- $K(x)$: value $x$ is known by the attacker.
- $leaked(ltk, t)$: key $ltk$ is leaked at time $t$.

$$
\forall ltk, k, t_1:\ sessionKey(k, ltk, t_1) \land K(k) \implies \exists t_2:\ leaked(ltk, t_2) \land t_2 < t_1
$$

## Files

| File | Content |
|---|---|
| `ForwardSecrecy.md` | Sequence diagram (Mermaid) of the example protocol, with event placement |
| `ForwardSecrecy.pv` | ProVerif model |
| `ForwardSecrecy.spthy` | Tamarin model |

## Running

```bash
proverif SecurityProperties/Confidentiality/ForwardSecrecy/ForwardSecrecy.pv
tamarin-prover --prove SecurityProperties/Confidentiality/ForwardSecrecy/ForwardSecrecy.spthy
```
