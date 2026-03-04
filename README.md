# project-team13
DEGO 2606 Group Project – Credit Application Governance Analysis  
Nova School of Business and Economics | MSc Business Analytics

---

## Team Members
| Name | Role |
|---|---|
| Leonardo Baroni | Data Engineer |
| Arslan Mubarak | Data Scientist |
| Paul | Governance Officer |
| Caro | Product Lead |

---

## Executive Summary

This project audits the credit application dataset of **NovaCred**, a fictional 
fintech company under regulatory scrutiny for potential discrimination in lending. 
Acting as a Data Governance Task Force, our team analysed 500 credit applications 
for data quality issues, algorithmic bias, and GDPR/AI Act compliance gaps.

**Key conclusion:** NovaCred's credit scoring system exhibits pervasive, 
multi-dimensional bias across all dimensions tested. The system must not be 
deployed without fundamental algorithmic review and independent auditing.

---

## Data Quality Findings

*(To be completed by Data Engineer — summary of issues found in 01-data-quality.ipynb)*

---

## Bias Analysis Findings

Full analysis: notebooks/02-bias-analysis.ipynb

### Finding 1 — Gender Disparate Impact
| Metric | Value |
|---|---|
| Female Approval Rate | 50.6% |
| Male Approval Rate | 66.0% |
| DI Ratio | 0.7667 |
| Four-Fifths Threshold | 0.8 |
| Adverse Impact? | YES |

The DI ratio of 0.7667 falls below the recognised four-fifths rule threshold, 
indicating female applicants face statistically significant disadvantage. Confirmed 
independently by Fairlearn (DPR = 0.7667, DPD = 0.1539).

### Finding 2 — Age-Based Disparate Impact
| Age Group | Approval Rate |
|---|---|
| 18-30 | 43.2% |
| 31-40 | 61.0% |
| 41-50 | 67.9% |
| 51-65 | 58.0% |

Age DI Ratio: A value of 0.6369 shows it is more severe than gender bias. Young applicants (18-30) 
are systematically penalised. Fairlearn DPD = 0.2464 confirms significant disparity.

### Finding 3 — ZIP Code Proxy Discrimination
ZIP code shows a statistically significant correlation with loan outcomes 
(r = -0.1259, p = 0.0048). ZIP codes with 100% female applicants have staggeringly low approval 
rates while ZIP codes with 100% male applicants consistently achieve 100% approval. 
ZIP code acts as a direct proxy for gender, meaning removing gender from the model 
would not eliminate discriminatory outcomes.

### Finding 4 — Gender x Age Interaction Effects
| Group | Approval Rate |
|---|---|
| Female 18-30 | 31.7% |
| Male 41-50 | 76.3% |
| Interaction DI Ratio | 0.4162 |

Young female applicants face compounded discrimination. Males outperform females 
in every single age group without exception, ruling out coincidence and confirming 
a structural gender penalty in the algorithm.

### Bias Summary Table
| Finding | Metric | Value | Threshold | Status |
|---|---|---|---|---|
| Gender DI | DI Ratio | 0.7667 | 0.8 |
| Age DI | DI Ratio | 0.6369 | 0.8 | 
| ZIP Proxy | p-value | 0.0048 | 0.05 | 
| Gender x Age | DI Ratio | 0.4162 | 0.8 | 

---

## Privacy and Governance Assessment

*(To be completed by Governance Officer — summary from 03-privacy-demo.ipynb)*

---

## Governance Recommendations

---

## Repository Structure

---

## How to Run

    git clone https://github.com/leobbaroni/project-team13.git
    cd project-team13
    pip install pandas numpy matplotlib seaborn scipy fairlearn jupyterlab
    jupyter lab

---

Version 1.0 | DEGO 2606 | Nova SBE | March 2026

