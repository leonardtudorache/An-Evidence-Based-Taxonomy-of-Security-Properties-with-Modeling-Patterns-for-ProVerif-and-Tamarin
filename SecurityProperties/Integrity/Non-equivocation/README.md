# Non-equivocation

*Section 4.2.2 of the paper.*

## Informal definition

Equivocation happens when an actor of the protocol sends different messages to different actors in the same instance of the protocol while the protocol instructs that the same message must be sent. Non-equivocation has been formalized in the literature in (at least) two distinct ways, which are not interchangeable. A *signer-side* notion defines it as the assurance that an actor cannot use the same key to validate two conflicting messages (Clement et al.). A *channel-side* notion instead defines it as the guarantee that the stream of messages accepted by a receiver faithfully, uniquely, and in-order reflects the stream of messages actually sent (Giantsidi et al.). The taxonomy uses both definitions since they have a different viewpoint on the verification.

## Formal definition: signer-side

- $valid_{sig}(k, m)$: message $m$ is valid under public key $k$: $m$ was signed with the private key corresponding to $k$, and the signature verification succeeded.

$$
\forall k, m_1, m_2:\ valid_{sig}(k, m_1) \land valid_{sig}(k, m_2) \implies m_1 = m_2
$$

Models: `Non-equivocation.pv`, `Non-equivocation.spthy`, diagram `Non-Equivocation.md`.

## Formal definition: channel-side

- $send(e, m, i)$: actor $e$ sent message $m$ at time $i$.
- $accepted(e, m, i)$: actor $e$ accepted message $m$ at time $i$.

In the models, an actor $e$ is an endpoint, i.e., an agent together with a channel identifier.

**Faithfulness.** No message accepted by a receiver skips over an earlier message sent to it on the same channel:

$$
\forall e_1, e_2, m_j, i, j:\ accepted(e_1, m_j, i) \land send(e_2, m_j, j) \implies \forall m_k, k:\ \big(k < j \land send(e_2, m_k, k)\big) \implies \exists l:\ l < i \land accepted(e_1, m_k, l)
$$

**In-order delivery.** The order in which messages are accepted respects the order in which they were sent:

$$
\forall e_1, m_i, m_j, i, j:\ i < j \land accepted(e_1, m_i, i) \land accepted(e_1, m_j, j) \implies \exists e_2, k, l:\ k < l \land send(e_2, m_i, k) \land send(e_2, m_j, l)
$$

**Uniqueness.** A message is accepted at most once:

$$
\forall e_1, m, i, j:\ accepted(e_1, m, i) \land accepted(e_1, m, j) \implies i = j
$$

Models: `Non-equivocation_lower_bound.pv`, `Non-equivocation_lower_bound.spthy`, diagram `Non-Equivocation_lower_bound.md`.

## Files

| File | Content |
|---|---|
| `Non-Equivocation.md` | Sequence diagram, signer-side |
| `Non-equivocation.pv` / `.spthy` | ProVerif / Tamarin model, signer-side |
| `Non-Equivocation_lower_bound.md` | Sequence diagram, channel-side |
| `Non-equivocation_lower_bound.pv` / `.spthy` | ProVerif / Tamarin model, channel-side |

## Running

```bash
proverif SecurityProperties/Integrity/Non-equivocation/Non-equivocation.pv
tamarin-prover --prove SecurityProperties/Integrity/Non-equivocation/Non-equivocation.spthy
proverif SecurityProperties/Integrity/Non-equivocation/Non-equivocation_lower_bound.pv
tamarin-prover --prove SecurityProperties/Integrity/Non-equivocation/Non-equivocation_lower_bound.spthy
```
