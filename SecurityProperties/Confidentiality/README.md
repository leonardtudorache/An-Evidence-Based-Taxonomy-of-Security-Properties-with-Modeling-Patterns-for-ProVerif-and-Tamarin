# Confidentiality

*Section 4.2.3 of the paper.*

## Informal definition

Confidentiality, also referred to as secrecy in practice, is achieved when a protocol ensures the secrecy of data $M$ by never publishing $M$, or the means to compute $M$, even if there is an interaction with an attacker. This also holds when the protocol is using public channels for communication. We include stronger versions of confidentiality, such as forward secrecy and post-compromise security. Confidentiality is one of the most verified security properties using ProVerif or Tamarin. ProVerif supports it as a primitive query to check this property, while Tamarin provides clear instructions in the manual. Based on the lemma extracted from the Tamarin manual, we can express confidentiality as follows.

## Formal definition

- $K(x)$: value $x$ is known by the attacker.
- $secret(x)$: value $x$ is expected to remain confidential, i.e., not known to the adversary.

$$
\forall x:\ secret(x) \implies \lnot K(x)
$$

## Sub-properties

| Property | Folder |
|---|---|
| Forward secrecy | [`ForwardSecrecy/`](ForwardSecrecy/) |
| Post-compromise security | [`Post-compromiseSecurity/`](Post-compromiseSecurity/) |

## Files

| File | Content |
|---|---|
| `Secrecy.md` | Sequence diagram (Mermaid) of the example protocol, with event placement |
| `Secrecy.pv` | ProVerif model |
| `Secrecy.spthy` | Tamarin model |

## Running

```bash
proverif SecurityProperties/Confidentiality/Secrecy.pv
tamarin-prover --prove SecurityProperties/Confidentiality/Secrecy.spthy
```
