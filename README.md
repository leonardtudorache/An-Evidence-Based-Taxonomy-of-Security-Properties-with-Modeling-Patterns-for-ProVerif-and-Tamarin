# Bridging Theory and Practice: An Evidence-Based Taxonomy of Security Properties with Modeling Patterns for ProVerif and Tamarin

[![DOI](https://zenodo.org/badge/1193461070.svg)](https://doi.org/10.5281/zenodo.19352739)

### **Project Overview**

Security is fundamentally critical for modern digital systems. As internet and cryptographic protocols govern almost all digital interactions, they must serve as reliable mechanisms that guarantee core security properties like **confidentiality** and **integrity**.

While formal verification tools such as **ProVerif** and **Tamarin** are widely used for automated protocol verification, they require specialized domain knowledge. This creates a significant learning curve for protocol designers who often possess a security background rather than a formal methods background.

### **The Taxonomy**

This repository accompanies a systematic and evidence-based taxonomy of security properties derived from a literature review of **53 recent studies (2022–2025)** that use ProVerif or Tamarin. It provides, for each property of the taxonomy, its definitions and executable modeling patterns in both tools, bridging the gap between theoretical definitions and practical verification models.

### **Key Features**

- **Systematic Categorization:** An up-to-date view of the properties verified in contemporary research, grouped into five categories: authentication, integrity, confidentiality, privacy and accountability.
- **Dual Definitions:** Every property has an **informal definition** for intuitive comprehension and a **formal definition** in first-order logic (or, for privacy properties, as an observational equivalence). The definitions are given in the article and in the `README.md` of each property folder.
- **Executable Modeling Patterns:** Ready-to-use example models in both **ProVerif (.pv)** and **Tamarin (.spthy)**, each with a sequence diagram showing where the events are raised.
- **Evidence-Based:** The properties are extracted from the models and property descriptions of the 53 selected studies, which are included in `Papers/`.
- **Reproducible:** Both provers can be run over the whole library with a single script, and the results are kept in version control.
- **DSL Foundation:** This work serves as the groundwork for a future **Domain-Specific Language (DSL)** aimed at further abstracting protocol verification.

---

## 📂 Repository Structure

### **`SecurityProperties/` — modeling patterns per property**

The models are organised to mirror the taxonomy in Figure 1 of the article: one directory per top-level category, one sub-directory per property.

```
SecurityProperties/
├── Authentication/
│   ├── README.md, authentication.{md,pv,spthy}   base property (Section 4.2.1)
│   ├── Aliveness/
│   ├── WeakAgreement/
│   ├── Non-injectiveAgreement/
│   ├── InjectiveAgreement/
│   └── MutualAuthentication/
├── Confidentiality/
│   ├── README.md, Secrecy.{md,pv,spthy}           base property (Section 4.2.3)
│   ├── ForwardSecrecy/
│   └── Post-compromiseSecurity/
├── Integrity/
│   ├── README.md                                  base property (Section 4.2.2)
│   ├── Unforgeability/
│   └── Non-equivocation/                          signer-side and channel-side
├── Privacy/
│   ├── README.md                                  indistinguishability (Section 4.2.4)
│   ├── Anonymity/
│   └── Unlinkability/
└── Accountability/
    ├── README.md                                  base property (Section 4.2.5)
    ├── Traceability/
    └── Non-repudiation/
```

Each property directory contains:

| File               | Purpose                                                                                                                                                                          |
| ------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `README.md`        | The informal and formal definition of the property from the article, the files in the folder, how to run them, and any notes on how the example model relates to the definition. |
| `<Property>.md`    | A Mermaid sequence diagram of the example protocol, annotated with the points at which each event is raised. Tool-independent notation.                                          |
| `<Property>.pv`    | The ProVerif model: events, queries and the process calculus encoding.                                                                                                           |
| `<Property>.spthy` | The Tamarin model: multiset rewriting rules, restrictions and lemmas.                                                                                                            |

The `README.md` at the root of each category directory gives the category's base definition. Where the base property has its own example model (`Authentication/authentication.*`, `Confidentiality/Secrecy.*`), it sits directly in the category directory. Integrity has no separate base model; `Integrity/Unforgeability/` is its signature-based instance.

`Integrity/Non-equivocation/` holds two pairs of models, one per formalization in the article: `Non-equivocation.*` (signer-side) and `Non-equivocation_lower_bound.*` (channel-side: faithfulness, in-order delivery, uniqueness).

**Notes on placement and scope.**

- `Accountability/Traceability/` currently holds a model of RFID **un**traceability, a related but opposite-flavoured privacy property, rather than the Traceability defined in Section 4.2.5. The file comments and the folder's `README.md` say so explicitly.
- Where an example model checks a variant or an approximation of the article's definition, the property's `README.md` states this under **Notes** (e.g., the secrecy-based approximation of anonymity, or the non-repudiation model without a separate judge role).

### **`CaseStudies/` — applying the patterns**

| Directory                   | Contents                                                                                                                                                                                                                                                                                                 |
| --------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `CaseStudies/Signcryption/` | A case study of Zheng's signcryption scheme (Section 5 of the article). `signcryption_initial.{pv,spthy}` implement only the algebraic logic of the scheme; `signcryption.{pv,spthy}` add the unforgeability and secrecy patterns from `SecurityProperties/`. `Signcryption.md` is the sequence diagram. |

The Tamarin models encode Bob's key recovery with a subterm-convergent equation (Bob recovers the ephemeral value and recomputes the shared key himself), so they pass Tamarin's wellformedness checks; the ProVerif models express the same step directly as a destructor. See the comment at the top of the `.spthy` files.

### **Verification harness**

| File              | Purpose                                                                                                                                                                 |
| ----------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `run_all.sh`      | Runs every `.pv` and `.spthy` under `SecurityProperties/` and `CaseStudies/` (or only under `MODEL_DIR`), writes `results/run-<stamp>.log` plus a summary table, exits non-zero on any failure. |
| `run_proverif.sh` | ProVerif only; writes `proverif-results.txt`.                                                                                                                           |
| `results/`        | Recorded tool output, kept in version control so the claims can be checked without installing either prover.                                                            |

Both scripts separate **security** queries (must hold) from **reachability** queries (must be reachable — an unreachable sanity event means the model cannot complete and every other result over it may be vacuous).

### **Research data**

| Directory             | Contents                                                                                                                                                                   |
| --------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `Papers/`             | The 53 reviewed studies (2022–2025): their verification models and a `Properties.md` with the property descriptions extracted from each paper.                             |
| `Datasets/`           | `dataset_original.json` holds the property terms as extracted from the papers; `dataset.json` holds the normalized terms used for the quantitative analysis (Section 4.1). |
| `Data Visualization/` | Jupyter notebooks producing the distribution figures: `MyNotebook.ipynb` from `dataset.json`, `MyNotebook_original_dataset.ipynb` from the original extraction.            |

### **Legacy directories**

`ProVerif Models of Properties/Other/` and `Protocol Sequence Diagrams/` predate the move to `SecurityProperties/` and hold exploratory models that were not migrated (access control, multi-factor authentication). They are kept for provenance and are **not** maintained; the models under `SecurityProperties/` supersede them.

**Disclaimer**:
The papers referenced in this work are not formally cited using standard academic citation formats. However, each paper can be traced and located through its title as mentioned in the text. Readers are encouraged to search for the original publications by title for full bibliographic details and further reading.

---

## 🛠 Usage

### **Prerequisites**

1. **ProVerif (>= 2.0):** for Dolev-Yao protocol analysis. Tested with 2.05.
2. **Tamarin Prover (>= 1.6.0):** for symbolic state-based analysis. Tested with 1.12.0.
3. **Python 3.x:** to run the visualization notebooks (`pandas`, `matplotlib`).
4. **GNU coreutils** (optional, macOS): the scripts use `timeout`/`gtimeout` to bound a run. Without it, a non-terminating model runs until interrupted.

### **Verifying the whole library**

```bash
./run_all.sh                                # both provers, SecurityProperties/ + CaseStudies/
./run_proverif.sh                           # ProVerif only
./run_all.sh Authentication                 # restrict to paths matching a substring
TIMEOUT=1200 ./run_all.sh                   # raise the per-model limit (default 600s)
MODEL_DIR="$PWD/CaseStudies" ./run_all.sh   # run only the case study models
```

### **Verifying a single property**

```bash
proverif SecurityProperties/Confidentiality/Secrecy.pv

tamarin-prover --prove SecurityProperties/Confidentiality/ForwardSecrecy/ForwardSecrecy.spthy
```

Observational-equivalence models must be run in diff mode:

```bash
tamarin-prover --diff --prove SecurityProperties/Privacy/Unlinkability/Unlinkability.spthy
```

`run_all.sh` detects this automatically by looking for `diff(` in the source. Each property's `README.md` lists the exact commands for its models.

**Locale note.** Tamarin reads source files using the system locale and aborts on any non-ASCII byte under `LANG=C`/`POSIX`. The models are ASCII-only for this reason, and both scripts force a UTF-8 locale so the outcome does not depend on the caller's environment.

---

## Verification status

Regenerate at any time with `./run_all.sh`; `results/` records the state of the committed result files. All security queries and lemmas in `SecurityProperties/` are proved by ProVerif 2.05 and Tamarin 1.12.0, and the case-study models in `CaseStudies/Signcryption/` verify in both tools.

**Sanity checks.** Every ProVerif trace model carries a reachability query, and most Tamarin models carry an `exists-trace` executability lemma, so a "verified" verdict is accompanied by evidence that the protocol can actually complete.
