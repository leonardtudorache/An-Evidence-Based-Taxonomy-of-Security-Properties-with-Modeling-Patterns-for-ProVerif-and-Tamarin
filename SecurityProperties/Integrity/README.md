# Integrity

_Section 4.2.2 of the paper._

## Informal definition

Biba defines integrity as maintaining data consistency, and ensuring that only authorized parties can modify data, where _authorized_ requires both that a party has access to the system and that it holds the appropriate access level to perform the modification. In addition to this base definition, the taxonomy includes two further levels of integrity: unforgeability and non-equivocation.

## Formal definition

- $accepted(d, i)$: data item $d$ was accepted (validated) at time $i$.
- $produced(d, P, j)$: data item $d$ was produced (sent/generated) by agent $P$ at time $j$.
- $honest(P)$: agent $P$ is honest (not controlled by the attacker).

$$
\forall d, i:\ accepted(d, i) \implies \exists P, j:\ produced(d, P, j) \land honest(P) \land j < i
$$

## Sub-properties

| Property         | Folder                                   |
| ---------------- | ---------------------------------------- |
| Unforgeability   | [`Unforgeability/`](Unforgeability/)     |
| Non-equivocation | [`Non-equivocation/`](Non-equivocation/) |
