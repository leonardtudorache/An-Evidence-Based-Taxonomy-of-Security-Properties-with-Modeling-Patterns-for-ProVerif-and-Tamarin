# Post-compromise Security (PCS)

*Section 4.2.3 of the paper.*

## Informal definition

Post-compromise security, also known as backward secrecy, is defined as the property of a protocol where actor $A$ has a security guarantee about the communication with actor $B$, even if the attacker has $B$'s secrets. It has the ability to recover after the compromise, so leaking the partner's key does not imply that all future messages can be decrypted. The recovery process is often a protocol-specific function, so it differs from protocol to protocol.

## Formal definition

Adapted from Cremers et al.

- $sent(sid_A, A, B, sck, i)$: agent $A$ sends a message to $B$ using session key $sck$ during the session identified by $sid_A$, at time $i$.
- $K(x, j)$: value $x$ is known by the attacker at time $j$.
- $heal(sid_A, A, B, k)$: the session between $A$ and $B$ (session id $sid_A$) was healed at time $k$.
- $compromise(sid_A, A, B, l)$: the session between $A$ and $B$ is compromised at time $l$.

$$
\forall A, B, sck, sid_A, i, j, k:\ sent(sid_A, A, B, sck, i) \land K(sck, j) \land heal(sid_A, A, B, k) \land k < i \implies \exists l:\ compromise(sid_A, A, B, l) \land k < l
$$

## Files

| File | Content |
|---|---|
| `PostCompromiseSecurity.md` | Sequence diagram (Mermaid) of the example protocol, with event placement |
| `PostCompromiseSecurity.pv` | ProVerif model |
| `PostCompromiseSecurity.spthy` | Tamarin model |

## Running

```bash
proverif SecurityProperties/Confidentiality/Post-compromiseSecurity/PostCompromiseSecurity.pv
tamarin-prover --prove SecurityProperties/Confidentiality/Post-compromiseSecurity/PostCompromiseSecurity.spthy
```
