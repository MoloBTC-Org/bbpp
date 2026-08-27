# Bitcoin Best Practice Protocol
## Participation Standards & Guidelines — Draft v0.1

**Status**: Draft  
**Date**: 2026-08-14  
**Parent document**: BBPP-00-Charter.md

---

### 1. Who This Document Applies To

- Core maintainers and regular contributors
- Occasional patch authors
- Node operators who run BBPP in production
- Miners / pools that integrate BBPP for template construction
- Reviewers and auditors
- Anyone proposing policy or performance changes

Participation is voluntary and unilateral. These standards define the expected conduct and quality bar for work that claims the BBPP name or is merged into the reference implementation.

---

### 2. Contribution Principles

1. **Incentive alignment first**  
   Every proposed change (policy default, filter, performance optimisation, RPC, documentation) must be evaluated against the Charter’s three-force model. Changes that primarily subsidise permanent non-monetary data storage are out of scope.

2. **Consensus is sacred**  
   No contribution may alter, weaken, or conditionalise consensus validation. Divergence from Bitcoin’s consensus rules is grounds for immediate rejection and, if shipped, loss of the BBPP designation.

3. **Defaults are policy statements**  
   Changing a default is a public claim about best practice. It requires explicit rationale, metrics where possible, and a clear migration path for operators who disagree.

4. **Performance regressions are policy-relevant**  
   A change that materially worsens IBD time, peak memory during validation, or block relay latency for lean workloads must be justified as a net improvement under the Charter’s success metrics.

5. **Transparency of trade-offs**  
   If a change improves one metric at the expense of another (e.g., stricter filtering vs. edge-case compatibility), both sides must be stated in the pull request or design document.

---

### 3. Technical Participation Standards

| Area | Minimum Expectation |
|------|---------------------|
| Consensus code | Must pass full differential testing / validation against reference Bitcoin behaviour on mainnet history (or equivalent rigorous equivalence proof). |
| Policy / filters | Defaults must be documented with the economic rationale from the Charter. Configuration knobs for operators who want different behaviour are preferred. |
| Performance work | Accompanied by before/after measurements on representative hardware and workloads (lean vs. heavy blocks). |
| Mining / template tools | Must support generation of filtered, lean templates; must not require operators to accept non-monetary data to remain functional. |
| Documentation | User-facing defaults and their rationale must be understandable by a competent node operator without reading the full codebase. |
| Security | New attack surface introduced by performance or filtering logic must be explicitly analysed. |

---

### 4. Review and Merge Expectations

- At least one independent review focused on incentive alignment and consensus safety.
- Clear statement of whether the change affects default policy, optional policy, or pure performance.
- For policy-default changes: a short “Charter impact” section in the PR description.
- No silent default changes in minor releases.

---

### 5. Operator Participation

Node operators and miners who run BBPP are participants in the broader experiment. They are encouraged (but never required) to:

- Publish high-level operational metrics (optional, privacy-preserving).
- Report measurable differences in resource use or orphan rates when switching to/from BBPP defaults.
- Contribute filter rules, performance observations, or edge-case findings.

There is no formal membership, token, or governance token. Influence is earned through demonstrated contribution quality and operational results.

---

### 6. Conduct

- Technical disagreement is expected and valuable.
- Claims of “best practice” must be backed by reference to the Charter’s incentive model or concrete measurements.
- Personal attacks, ideological purity tests unrelated to the three-force model, and attempts to bind the project to external political or corporate agendas are outside the scope of productive participation.

---

### 7. Versioning and Designation

Software that substantially departs from the Charter’s principles (especially consensus divergence or systematic subsidisation of permanent non-monetary data) may not use the Bitcoin Best Practice Protocol name or related trademarks/designations.

---

**End of Participation Standards Draft**
