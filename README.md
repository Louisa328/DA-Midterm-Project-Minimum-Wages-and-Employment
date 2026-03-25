# Minimum Wages and Employment: Replication & Extension
### Card & Krueger (1994) — A DID Case Study

**Course**: ECON 5200 | Data Analytics | Northeastern University  
**Author**: Yun Deng  
**Track**: Difference-in-Differences (DID)

---

## Executive Memo

### The Bottom Line
New Jersey's 1992 minimum wage increase did not reduce fast-food employment — 
replicating Card & Krueger (1994)'s landmark finding. Extending their analysis, 
we find that this positive effect is directionally concentrated among franchise-operated 
restaurants and wage-constrained stores, while company-owned stores and initially 
high-wage stores respond differently, revealing meaningful heterogeneity beneath the 
average treatment effect.

### The Mechanism
This study uses a **Difference-in-Differences (DID)** design. Think of it as a natural 
experiment: in April 1992, New Jersey raised its minimum wage from $4.25 to $5.05, 
while neighboring Pennsylvania did nothing. By comparing employment changes in NJ 
fast-food restaurants (treatment) against PA restaurants (control) before and after 
the policy, we isolate the causal effect of the wage increase — just as a doctor 
compares a treated patient against an untreated one. The key assumption — that NJ and 
PA would have followed similar employment trends without the policy — is validated by 
BLS unemployment data showing parallel pre-treatment trends from 1990 to 1992.

### Visual Evidence

![Heterogeneous Treatment Effects Forest Plot](outputs/forest_plot_HTE.png)

*Figure 1: Coefficient forest plot showing DID estimates (β) and 95% confidence 
intervals for five subgroups. Blue = significant (p < 0.1). Controls: chain brand 
fixed effects. The positive employment effect is concentrated among low-wage stores 
(β = +4.14**), while high-wage stores show a significant decline (β = −4.44*). 
Franchise stores (β = +2.51) outperform company-owned stores (β = +1.24), consistent 
with independent operators responding more flexibly to labor cost shocks.*

### Policy Implications
1. **For policymakers**: Minimum wage increases need not reduce employment in the 
   fast-food sector — but effects are heterogeneous. Stores already paying above the 
   new minimum may face adjustment costs; targeted transition support could mitigate 
   this.
2. **For franchisors**: Franchise operators demonstrate greater employment resilience 
   than corporate-owned stores, suggesting decentralized labor cost management may be 
   an effective buffer against minimum wage shocks.
3. **For researchers**: Average treatment effects mask substantial heterogeneity by 
   ownership type and initial wage level — subgroup analysis is essential for accurate 
   policy evaluation.

---

## Paper
Card, D., & Krueger, A. B. (1994). Minimum Wages and Employment: 
A Case Study of the Fast-Food Industry in New Jersey and Pennsylvania. 
*American Economic Review*, 84(4), 772–793.

---

## Repository Structure
```
├── README.md                          # Executive Memo & project overview
├── data/
│   ├── raw/public.dat                 # Original C&K survey data (410 restaurants)
│   └── processed/                     # Cleaned data ready for modeling
├── notebooks/
│   ├── 01_Data_Cleaning.ipynb         # Phase 1: Data setup
│   ├── 02_Replication_Analysis.ipynb  # Phase 2: C&K replication
│   └── 03_Extension_and_Results.ipynb # Phase 3: HTE extension
├── outputs/
│   ├── forest_plot_HTE.png            # Figure 1: Coefficient forest plot
│   ├── parallel_trends_check.png      # Figure 2: Parallel trends validation
│   └── regression_table.html          # Table 2: Stargazer regression table
└── requirements.txt                   # Python dependencies
```

---

## Phase 1: Data Architecture
- Downloaded original dataset (public.dat) from David Card's Berkeley homepage
- 410 fast-food restaurants surveyed in NJ and eastern PA
- Two waves: February 1992 (pre-policy) and November 1992 (post-policy)
- Built GitHub repository structure with raw data and notebooks

---

## Phase 2: Replication
Manually replicated the core results of Card & Krueger (1994) without AI assistance.

**Table 2 Replication — Descriptive Statistics:**
- Reproduced means and standard errors for FTE employment, wages, 
  prices, and store characteristics by state and wave
- NJ FTE Before: 20.4 | NJ FTE After: 21.0
- PA FTE Before: 23.3 | PA FTE After: 21.2

**Manual DID Calculation:**
- NJ change: +0.59 FTE
- PA change: −2.17 FTE  
- DID estimate: **+2.75 FTE**

**Regression Results (Table 4 Replication):**
- Model: `FTE ~ treat + post + treat:post`
- Clustered standard errors at store level
- DID coefficient: **2.75** (p = 0.036)
- Conclusion: The minimum wage increase did NOT reduce employment

---

## Phase 3: Extension — Heterogeneous Treatment Effects

### Research Question
Does the employment effect of the 1992 NJ minimum wage increase differ between
**franchise** and **company-owned** fast-food restaurants?

### Data Enrichment
- Merged BLS LAUS county-level unemployment rates via FRED API
- Coverage: all NJ counties (21) and PA counties (5), Feb and Nov 1992
- Computed labor-force-weighted regional averages (weighted by county LFN)
- BLS data used for: (1) parallel trends verification (2) descriptive statistics
- Not used as regression control — chain fixed effects provide a cleaner approach

### Empirical Strategy
- Interaction term DID: `delta_fte ~ nj × co_owned + C(chain) + wage_st`
- Chain brand fixed effects control for structural heterogeneity across restaurants
- Subgroup regressions for 5 groups with coefficient forest plot
- 4-model robustness check confirming HTE stability across specifications

### Key Findings
| Subgroup | β (DID) | p-value |
|---|---|---|
| All restaurants (baseline) | +2.32 | 0.088* |
| Franchise (co_owned=0) | +2.51 | 0.195 |
| Company-owned (co_owned=1) | +1.24 | 0.363 |
| Low wage (wage_st ≤ 4.25) | +4.14 | 0.033** |
| High wage (wage_st > 5.05) | −4.44 | 0.051* |

- `NJ × Company-owned` coefficient stable across specifications
  (−0.441 → −0.480 → −0.994), confirming HTE not driven by brand composition
- Franchise restaurants show larger positive response than company-owned stores
- High-wage stores experience significant employment decline, echoing Ropponen (2010)

---

## GenAI Usage
- **Tool**: Claude (Anthropic)
- **Usage**: FRED API data retrieval and county series ID verification, 
  labor-force weighted average computation, regression interaction term setup, 
  parallel trends visualization, forest plot and Stargazer table code, 
  executive summary drafting
- All econometric logic, variable selection, interpretation, and methodological 
  decisions are the author's own

---

## References
- Card, D. & Krueger, A.B. (1994). Minimum Wages and Employment. *AER*, 84(4): 772–793.
- Ropponen, O. (2010). Replication of Card and Krueger (1994) Using the CIC Estimator. 
  MPRA Paper 25181.
- BLS LAUS data via FRED, Federal Reserve Bank of St. Louis.

