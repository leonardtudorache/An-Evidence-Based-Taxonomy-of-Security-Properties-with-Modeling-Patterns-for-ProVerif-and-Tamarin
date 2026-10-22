# Privacy

*Section 4.2.4 of the paper.*

According to Westin, privacy is defined as *"the claim of individuals, groups, or institutions to determine for themselves when, how and to what extent information about them is communicated to others"*. We further include two subcategories of privacy in our taxonomy: anonymity and unlinkability.

Both of these properties employ the *indistinguishability* property, which is described as the general impossibility for an outside observer to distinguish two processes/systems, denoted $P \approx Q$. Indistinguishability is one of the most important elements for ProVerif and Tamarin during the verification phase, where if two processes are observationally equivalent, no adversary, no matter how powerful, can tell which one they are interacting with, and this is checked via biprocesses/`choice` (ProVerif) or `diff`-equivalence (Tamarin) rather than as a reachability query. Anonymity and unlinkability instantiate this general relation by varying a different piece of information between the two processes being compared: identity, in the case of anonymity, and session-to-identity linkage, in the case of unlinkability.

## Sub-properties

| Property | Folder |
|---|---|
| Anonymity | [`Anonymity/`](Anonymity/) |
| Unlinkability | [`Unlinkability/`](Unlinkability/) |
