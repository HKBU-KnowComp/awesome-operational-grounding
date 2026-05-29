# Contribution Guidelines

Thank you for helping curate this list! Please follow these guidelines so entries stay consistent with the AOGC survey (Bai et al., 2026).

## Scope

**In scope**

- LLM-based construction, validation, or maintenance of schema-level grounding artifacts:
  - **D1** vocabulary / entity structure
  - **D2** constraints / rules / validation shapes
  - **D3** actions / workflows / API & tool contracts
  - **D4** governance / policy / compliance
  - **D5** maintenance / versioning / temporal validity
- Benchmarks, validators, and representations directly supporting AOGC
- Adjacent enterprise grounding architectures (clearly labeled)

**Out of scope**

- Pure instance-level KG population without schema construction
- Ontology *usage* without construction or maintenance
- General LLM or agent surveys unrelated to grounding-layer construction

## Pull request checklist

1. Add the entry in the **most specific section** (core tier → dimension, or extended corpus).
2. Use this format:

   ```markdown
   - [Title](url) (Author et al., YEAR) — One-line description of why it matters for AOGC. **D?** · **T?** · type
   ```

3. Include a working link (paper PDF, ACL Anthology, arXiv, official repo, or spec).
4. Tag dimensions (**D1**–**D5**) and autonomy tier (**T1**–**T3**) when applicable.
5. Keep descriptions factual and under ~200 characters.
6. Alphabetize within subsections unless chronological order is meaningful.
7. Do not add duplicate entries; update the existing line instead.

## Types

| Tag | Meaning |
|-----|---------|
| **T1** | Subtask tool — single predefined extraction/translation step |
| **T2** | Pipeline engine — fixed multi-step construction + checking |
| **T3** | Construction agent — autonomously plans grounding construction (rare) |
| benchmark | Evaluation resource or shared task |
| method | Algorithm or technique |
| system | End-to-end pipeline or platform |
| validator | External checker or compiler |
| representation | Target language, vocabulary, or format |
| tool | Infrastructure or quality tooling |
| adjacent | Related but not core AOGC construction |
| foundation | Foundational non-LLM work cited for context |

## License

By contributing, you agree that your contributions may be licensed under [CC0 1.0 Universal](https://creativecommons.org/publicdomain/zero/1.0/).
