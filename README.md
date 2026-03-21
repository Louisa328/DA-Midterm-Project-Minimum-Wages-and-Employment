# Replication: Card & Krueger (1994)
### Minimum Wages and Employment: A Case Study of the Fast-Food Industry

**Course**: ECON 5200 | Data Analytics | Northeastern University  
**Author**: Yun Deng  
**Track**: Difference-in-Differences (DID)

---

## Paper
Card, D., & Krueger, A. B. (1994). Minimum Wages and Employment: 
A Case Study of the Fast-Food Industry in New Jersey and Pennsylvania. 
*American Economic Review*, 84(4), 772–793.

## Research Question
Did New Jersey's 1992 minimum wage increase ($4.25→$5.05) affect 
fast-food employment? This project uses DID, comparing employment 
changes in NJ vs. Pennsylvania (control) before and after the policy.

## Data
Source: https://davidcard.berkeley.edu/data_sets.html  
"Minimum Wages and Employment: A Case Study of the Fast Food Industry 
in New Jersey and Pennsylvania." (with Alan Krueger), American Economic 
Review 84, (September 1994).

---

## Phase 1: Data Architecture
- Downloaded original dataset (public.dat) from David Card's Berkeley homepage
- 410 fast-food restaurants surveyed in NJ and eastern PA
- Two waves: February 1992 (pre-policy) and November 1992 (post-policy)
- Built GitHub repository structure with raw data and notebooks

## Phase 2: Replication
Manually replicated the core results of Card & Krueger (1994) without AI assistance.

**Table 2 Replication — Descriptive Statistics:**
- Reproduced means and standard errors for FTE employment, wages, 
  prices, and store characteristics by state and wave
- NJ FTE Before: 20.4 | NJ FTE After: 21.0
- PA FTE Before: 23.3 | PA FTE After: 21.2

**Manual DID Calculation:**
- NJ change: +0.59 FTE
- PA change: -2.17 FTE  
- DID estimate: **+2.75 FTE**

**Regression Results (Table 4 Replication):**
- Model: `FTE ~ treat + post + treat:post`
- Clustered standard errors at store level
- DID coefficient (treat:post): **2.75** (p = 0.036)
- Conclusion: The minimum wage increase did NOT reduce employment; 
  NJ fast-food restaurants increased FTE by 2.75 relative to PA

## Phase 3: Extension — Heterogeneous Treatment Effects

### Research Question
Does the employment effect of the 1992 NJ minimum wage increase differ between 
**franchise** and **company-owned** fast-food restaurants?

### Data Enrichment
- Merged BLS LAUS county-level unemployment rates via FRED API
- Coverage: all 21 NJ counties + 5 PA counties, February and November 1992
- Constructed `delta_unemp` (Nov − Feb) to control for local macroeconomic trends
- Geographic mapping: C&K region dummies (northj/centralj/southj/pa1/pa2) → 
  county-level BLS series

### Empirical Strategy
- Interaction term DID: `delta_fte ~ nj × co_owned + delta_unemp + controls`
- Subgroup regressions for 5 groups with forest plot visualization
- 4-model robustness check showing HTE stable across specifications

### Key Findings
| Subgroup | β (DID) | p-value |
|---|---|---|
| All restaurants (baseline) | +2.58 | 0.062* |
| Franchise (co_owned=0) | +3.58 | 0.084* |
| Company-owned (co_owned=1) | +1.54 | 0.282 |
| Low wage (wage_st ≤ 4.25) | +3.59 | 0.079* |
| High wage (wage_st > 5.05) | −7.06 | 0.026** |

- The `NJ × Company-owned` interaction coefficient remains stable at ≈ −1.0 
  across all specifications (p > 0.65), confirming the HTE is not driven by OVB
- Franchise restaurants drive the positive employment effect documented by C&K
- High-wage stores experience a significant employment decline, consistent with 
  Ropponen (2010)

---

## GenAI Usage
- **Tool**: Claude (Anthropic)
- **Usage**: FRED API data retrieval code, regression interaction term setup, 
  forest plot visualization, executive summary drafting
- All econometric logic, variable selection, and interpretation are the author's own

---

## References
- Card, D. & Krueger, A.B. (1994). Minimum Wages and Employment. *AER*, 84(4): 772–793.
- Ropponen, O. (2010). Replication of Card and Krueger (1994) Using the CIC Estimator. 
  MPRA Paper 25181.
- BLS LAUS data via FRED, Federal Reserve Bank of St. Louis.

