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

## Phase 3: Extension 
Heterogeneous Treatment Effects (HTE) analysis by ownership structure:
- Research question: Does the minimum wage effect differ between 
  corporate-owned and franchised restaurants?
- Hypothesis: Corporate-owned stores absorb wage cost increases more 
  easily than franchised stores, leading to larger employment gains
- Method: Subgroup DID comparing `co_owned = 1` vs `co_owned = 0`

## Repository Structure
```
├── data/
│   ├── raw/          # Original public.dat (immutable)
│   └── processed/    # Cleaned data files
├── notebooks/
│   ├── 01_Data_Cleaning.ipynb
│   ├── 02_Replication_Analysis.ipynb
│   └── 03_Extension_and_Results(HTE).ipynb
└── README.md
```


