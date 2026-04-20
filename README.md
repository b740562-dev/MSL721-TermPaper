Estimating the Causal Return to Education
An Instrumental Variables Approach Using the Card (1995) Dataset

Overview
This project implements a complete econometric workflow to estimate the causal return to education using the Card (1995) dataset from the National Longitudinal Survey of Young Men (NLSYM, 1976). The analysis identifies and corrects three classical violations of OLS assumptions — multicollinearity, heteroskedasticity, and endogeneity — and compares naive OLS against a two-stage least squares (2SLS) estimator.

Key Finding
ModelReturn to EducationNaive OLS7.36% per yearOLS + HC3 Robust SE7.36% per yearIV / 2SLS8.22% per year
The 0.86 percentage point gap between OLS and 2SLS is consistent with downward ability bias — more able individuals select into education regardless of cost, causing OLS to understate the true return.

Dataset

Source: Card (1995), accessed via the wooldridge Python package
Sample: National Longitudinal Survey of Young Men, 1976
Observations: 3,003
Dependent variable: Log of hourly wage (lwage)
Key regressor: Years of education (educ)
Instrument: Proximity to a 4-year college (nearc4)


Problems Addressed
1. Multicollinearity

Detection: Variance Inflation Factor (VIF)
Finding: age creates perfect collinearity (VIF = ∞) with educ and exper due to the identity age ≈ educ + exper + 6
Fix: Drop age from the model

2. Heteroskedasticity

Detection: Breusch-Pagan test and White's test
Finding: Tests fail to reject homoskedasticity but visual diagnostics suggest mild fanning
Fix: HC3 heteroskedasticity-consistent standard errors (White, 1980)

3. Endogeneity

Detection: Durbin-Wu-Hausman test
Finding: Ability bias causes Cov(educ, ε) ≠ 0 — education is endogenous
Fix: IV/2SLS using college proximity (nearc4) as instrument
Instrument strength: First-stage F-statistic = 227.53 (far above Stock-Yogo threshold of 10)


Project Structure
├── Card_Econometrics_Model.ipynb   # Main annotated Jupyter notebook
├── term_paper.tex                  # LaTeX source for term paper
├── term_paper.pdf                  # Compiled term paper
└── README.md                       # This file

Requirements
bashpip install wooldridge statsmodels linearmodels scipy numpy pandas matplotlib seaborn

How to Run
bash# Clone the repository
git clone https://github.com/b740562-dev/econometrics-card-1995.git
cd econometrics-card-1995

# Launch Jupyter
jupyter notebook Card_Econometrics_Model.ipynb

References

Card, D. (1995). Using geographic variation in college proximity to estimate the return to schooling. University of Toronto Press.
Hausman, J. A. (1978). Specification tests in econometrics. Econometrica, 46(6), 1251–1271.
Mincer, J. (1974). Schooling, Experience, and Earnings. NBER.
Stock, J. H. & Yogo, M. (2005). Testing for weak instruments in linear IV regression. Cambridge University Press.
White, H. (1980). A heteroskedasticity-consistent covariance matrix estimator. Econometrica, 48(4), 817–838.
Wooldridge, J. M. (2019). Introductory Econometrics: A Modern Approach (7th ed.). Cengage.


Author
Bebo — 2023ME10055
Department of Mechanical Engineering, IIT Delhi
Course: MSL721 Econometrics
