# Replication: Card & Krueger (1994)
### Minimum Wages and Employment: A Case Study of the Fast-Food Industry

**Course**: ECON 5200 | Northeastern University  
**Author**: Yun Lou  
**Track**: Difference-in-Differences (DID)

---

## 📌 Research Question
Does raising the minimum wage reduce employment?  
This project replicates Card & Krueger (1994), which uses a 
Difference-in-Differences strategy to estimate the causal effect 
of New Jersey's 1992 minimum wage increase ($4.25→$5.05/hr) on 
fast-food restaurant employment, using Pennsylvania as the control group.

## 🔬 Identification Strategy
- **Method**: Difference-in-Differences (DID)  
- **Treatment**: NJ minimum wage increase (April 1, 1992)  
- **Control Group**: Fast-food restaurants in Pennsylvania  
- **Key Assumption**: Parallel trends between NJ and PA absent the policy

## 📊 Data Source
- **Paper**: Card, D. & Krueger, A.B. (1994). *Minimum Wages and Employment.* AER, 84(4), 772–793.
- **Data**: Downloaded from [David Card's Berkeley Homepage](https://davidcard.berkeley.edu/data_sets.html)
- **Sample**: 410 fast-food restaurants (NJ + eastern PA)
- **Time periods**: February 1992 (pre-policy) & November 1992 (post-policy)

## 📁 Repository Structure
```
├── data/
│   ├── raw/          # Original public.dat (immutable)
│   └── processed/    # Cleaned CSV files
├── notebooks/
│   ├── 01_Data_Cleaning.ipynb
│   └── 02_Replication.ipynb
└── README.md
```

## 📅 Project Timeline
| Phase | Due | Status |
|-------|-----|--------|
| Phase 1: Data Architecture | Feb 27, 2026 | ✅ Complete |
| Phase 2: Replication | Mar 6, 2026 | ⏳ Upcoming |
| Phase 3: Extension + AI | Mar 22, 2026 | ⏳ Upcoming |
| Phase 4: Executive Briefing | Mar 25, 2026 | ⏳ Upcoming |

## 📚 Reference
Card, D., & Krueger, A. B. (1994). Minimum wages and employment: 
A case study of the fast-food industry in New Jersey and Pennsylvania. 
*American Economic Review*, 84(4), 772–793.
```
