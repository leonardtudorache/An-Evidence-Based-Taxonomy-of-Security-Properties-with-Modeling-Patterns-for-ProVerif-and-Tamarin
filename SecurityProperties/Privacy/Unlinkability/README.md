# Unlinkability

_Section 4.2.4 of the paper._

## Informal definition

Unlinkability represents the impossibility for the adversary to determine if two runs of a process use the same or different identities.

## Formal definition

$$
!\,\mathit{new}\ s.\ P(s)\ \approx\ !\,\mathit{new}\ s.\ !\,P(s)
$$

The notation expresses unlinkability over an unbounded number of sessions (Hirschi et al.). On the left-hand side, replication generates unboundedly many sessions, each using its own freshly generated, distinct value $s$. On the right-hand side, a single $s$ is generated once and reused across unboundedly many replicated sessions. The two systems are observationally equivalent when no external observer, having seen any number of sessions, can distinguish whether they were run with distinct identities or with the same identity.

## Notes

- The models compare `!session(U) | !session(choice[U, V])` (ProVerif) and the corresponding `diff(~U, ~V)` rule (Tamarin): unboundedly many sessions of a fixed identity against sessions that may use a second identity. This is the worked example of Section 4.3 (Listings 1 and 2).
- Equivalence models carry no reachability check: ProVerif rejects correspondence queries together with `choice`, and Tamarin's `--diff` mode has no `exists-trace` lemmas.

## Files

| File                  | Content                                                                  |
| --------------------- | ------------------------------------------------------------------------ |
| `Unlinkability.md`    | Sequence diagram (Mermaid) of the example protocol, with event placement |
| `Unlinkability.pv`    | ProVerif model                                                           |
| `Unlinkability.spthy` | Tamarin model                                                            |

## Running

```bash
proverif SecurityProperties/Privacy/Unlinkability/Unlinkability.pv
tamarin-prover --diff --prove SecurityProperties/Privacy/Unlinkability/Unlinkability.spthy
```
