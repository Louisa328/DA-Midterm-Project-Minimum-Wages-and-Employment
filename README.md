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
- Coverage: representative county per region (Hudson NJ, Middlesex NJ, Camden NJ, 
  Montgomery PA, Philadelphia PA), February and November 1992
- Used pre-treatment unemployment level (`unemp_feb92`) as BLS control variable,
  capturing structural labor market differences across regions
- Geographic mapping: C&K region dummies (northj/centralj/southj/pa1/pa2) → 
  single representative county per region
- Parallel trends verified using state-level BLS data (1990–1992): NJ and PA 
  followed closely aligned unemployment trajectories prior to April 1992

### Empirical Strategy
- Interaction term DID: `delta_fte ~ nj × co_owned + unemp_feb92 + controls`
- Subgroup regressions for 5 groups with coefficient forest plot visualization
- 4-model robustness check showing HTE stable across specifications

### Key Findings
| Subgroup | β (DID) | p-value |
|---|---|---|
| All restaurants (baseline) | +1.86 | 0.238 |
| Franchise (co_owned=0) | +2.81 | 0.234 |
| Company-owned (co_owned=1) | −0.03 | 0.983 |
| Low wage (wage_st ≤ 4.25) | +2.88 | 0.293 |
| High wage (wage_st > 5.05) | −5.82 | 0.039** |

- The `NJ × Company-owned` interaction coefficient remains stable across all 
  specifications (−1.095 → −0.795 → −0.592), confirming the HTE is not driven 
  by regional economic confounding
- Franchise restaurants show a larger positive employment response than 
  company-owned stores, consistent with independent operators bearing full 
  marginal labor costs
- High-wage stores experience a significant employment decline, echoing 
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

