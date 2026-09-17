# Datasheets for Datasets — Reading Notes

**Course:** SEIS 651: AI Ethics · University of St. Thomas
**Paper:** Gebru, T., Morgenstern, J., Vecchione, B., Vaughan, J.W., Wallach, H., Daumé III, H., Crawford, K. (2021). Datasheets for Datasets. arXiv:1803.09010v8 [cs.DB]
**Source PDF:** `readings/Datasheets for Datasets.pdf` (18 pages)
**Authors:** Timnit Gebru (Black in AI), Jamie Morgenstern (UW), Briana Vecchione (Cornell), Jennifer Wortman Vaughan / Hanna Wallach / Hal Daumé III / Kate Crawford (Microsoft Research)

## TL;DR

Every ML model is shaped by its training/evaluation datasets. No standardized documentation process exists for ML datasets, unlike electronics (component datasheets). The authors propose **datasheets for datasets**: a structured questionnaire accompanying every dataset covering motivation, composition, collection, preprocessing, uses, distribution, and maintenance — to increase transparency, accountability, reproducibility, reduce bias/harm, and help consumers choose appropriate datasets.

Documentation must be **manual/reflection-driven, not automated** — the point is to force creators to reflect on assumptions, risks, and implications.

## 1. Problem / Motivation

- Dataset characteristics fundamentally determine model behavior.
- Train/deploy mismatch or embedded societal bias → poor performance, revenue/PR loss, and severe harm in high-stakes domains: criminal justice, hiring, critical infrastructure, finance.
- Models reproduce/amplify bias in training data (e.g., word embeddings, Gender Shades, Amazon hiring tool).
- World Economic Forum recommendation: document provenance, creation, use to avoid discriminatory outcomes.
- Data provenance is well-studied in databases, rarely discussed in ML. No standard for documenting ML datasets.

## 2. Objectives — Two Stakeholder Groups

**Dataset creators:** encourage careful reflection on creation, distribution, maintenance — assumptions, risks/harms, implications of use.

**Dataset consumers:** give them information to make informed decisions, select appropriate datasets, avoid unintentional misuse.

**Secondary audiences:** policymakers, consumer advocates, journalists, data subjects, people impacted by models. Also aids reproducibility — others can recreate similar datasets from the datasheet alone.

**Non-prescriptive:** questions adapt by domain / org workflow (academic release vs. internal product data; language data can integrate Bender & Friedman Data Statements).

## 3. Development Process (~2 years, iterative)

1. Initial questions from authors' diverse research experience (bias, misuse).
2. Tested by writing example datasheets for Labeled Faces in the Wild and Pang & Lee polarity dataset — revealed gaps, redundancies.
3. Piloted with product teams at two major US tech companies; observed where questions failed.
4. Public draft on arXiv/social media (Mar 2018) → dozens of researcher/practitioner/policymaker comments + legal review.
5. Revisions: reordered to dataset lifecycle, discouraged yes/no answers, added **Uses** section, folded legal/ethical questions into lifecycle stages (product teams answered them more readily there), removed explicit compliance questions → replaced with factual questions (no legal judgment required).

## 4. The Questionnaire — 7 Lifecycle Stages

Answer as many as possible; skip N/A. Read relevant section *before* starting that lifecycle stage.

### 3.1 Motivation
Why was it created? Specific task/gap? Who created (team/entity)? Who funded (grantor/number)?

### 3.2 Composition
Read before collection; answer after. Core consumer info + GDPR-relevant facts.
- What instances represent; how many; full population or sample (what larger set? representative? how validated?).
- Per-instance data (raw vs. features); labels/targets; missing info; explicit relationships; recommended splits + rationale; errors/noise/redundancy.
- Self-contained vs. external resources (persistence guarantees? archival copy? licenses/fees?).
- Confidential data? Offensive/threatening content?
- If relates to people (broad reading — e.g., human-written text counts): subpopulations + distributions; identifiability (direct/indirect); sensitive attributes (race, gender, religion, politics, health, biometrics, IDs, criminal history).

### 3.3 Collection Process
Read before collection; helps others replicate.
- How acquired (observable / reported / inferred — validated how?); mechanisms (sensors, curation, APIs — validated how?); sampling strategy; who collected + compensation; timeframe (collection vs. creation); ethical review (IRB + outcomes/links).
- If relates to people: sourced directly or third-party? Notice given? Consent (exact language + mechanism)? Revocation mechanism? Data-protection impact analysis?

### 3.4 Preprocessing / Cleaning / Labeling
Read before preprocessing. Was any done (tokenization, bucketing, filtering, etc.)? Raw data saved (link)? Preprocessing software available?

### 3.5 Uses
Reflect on appropriate/inappropriate tasks.
- Already used for? Repository of papers/systems? Other possible tasks? Composition/collection artifacts that could cause unfair treatment or legal/financial harm + mitigations? Explicit non-recommended tasks?

### 3.6 Distribution
Answer before distribution (internal or external).
- Will it go to third parties? How (website tarball, API, GitHub)? DOI? When? License/ToU + fees? Third-party IP restrictions? Export controls / regulatory restrictions?

### 3.7 Maintenance
Answer before distribution; communicate plan to consumers.
- Who supports/hosts? Contact? Erratum? Update cadence/who/how communicated? Retention limits for human data + enforcement? Older versions supported or sunset plan? Contribution mechanism + validation + distribution?

## 5. Appendix Example: Pang & Lee Polarity Dataset

Movie-review sentiment (positive/negative) from `rec.arts.movies.reviews` / IMDb. 1,400 (v1.x) → 2,000 (v2.0) instances, ≤40 posts/author. Star-rating → polarity mapping, neutral discarded; downcased, HTML/boilerplate stripped. No IRB, no notice/consent (public crawl). Self-contained, public on Cornell site, no license (cite EMNLP 2002). Minimal harm risk (names/emails removed in preprocessed version); warn against using movie-domain model for consequential decisions about people without verification. Authors answer several questions "Unknown to the authors of the datasheet" — illustrating that even non-creators can write useful datasheets.

## 6. Impact and Challenges

**Traction (as of 2021):** academic adoptions; pilots at Microsoft, Google, IBM; Google Model Cards + Open Images Data Card; IBM FactSheets; Dataset Nutrition Label; Partnership on AI ABOUT ML guidance.

**Challenges/limits:**
- Must be adapted to org infrastructure; awkward for dynamic/streaming datasets (recommend versioned datasheets).
- Does not solve bias alone — creators can't foresee all uses; demographic labels needed for bias audits may be unavailable (privacy).
- Human-data collection may require anthropology/sociology/STS expertise; respect is contextual.
- Imposes overhead — orgs must change workflows/incentives. Benefit (fewer one-off questions, transparency signal) argued to outweigh cost.

## Key Takeaways for AI Ethics

1. **Transparency as harm reduction:** documentation shifts burden from harmed parties to creators.
2. **Process > artifact:** value is in forced reflection, hence anti-automation stance.
3. **Lifecycle framing matters:** embedding ethics questions per-stage gets better compliance than a separate ethics section.
4. **Reproducibility + accountability:** datasheets serve consumers, auditors, journalists, and data subjects alike.

## Discussion Prompts

- Should datasheets be mandatory for publication / product launch / procurement? Who enforces?
- How to handle consent for public web-crawled data (cf. polarity dataset: "public, therefore usable")?
- How to document foundation-model-scale datasets where full provenance is infeasible?
- Balance: demographic labels for bias auditing vs. privacy/data minimization?
