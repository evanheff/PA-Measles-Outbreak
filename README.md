# PA-Measles-Outbreak
An analysis of Pennsylvania's 2026 measles outbreak, testing whether population density or vaccination rate better explains county-level cases counts and whether the outbreak's geographic pattern reflects density-driven spread or communal clustering of under-vaccination populations.

**Motivation**

PA's current measles outbreak has largely been concentrated in Lancaster County, home to a large Plain (Amish/Mennonite) community. A common intuition is that lower-density and more rural areas should see less disease spread than urban areas. This project tests that intuition directly against the alternative hypothesis that vaccination rate, and specifically social clustering of under-vaccination within insular communities is a better explanation of measles transmission, regardless of population density.

**Key Findings (As of 8/25/26)**

**Density has no measurable relationship with case counts**

Confirmed independently across Pearson, Spearman, and Kendall correlation, and in binomial and zero-inflated negative binomial regression controlling for vaccination rate.

**Vaccination rate is a significant predictor**

ZINB model holds this significance under multiple diagnostics.

**Cases cluster geographically**

Significant global Moran's I, specifically around Lancaster and its neighboring counties.

**Geographic adjacency alone does not explain the pattern**

Berks and Dauphin Counties, both directly bordering outbreak counties, show significant negative local clustering. This finding may, and likely will, change as the outbreak progresses.

**The mechanism is visible at the school level**

Lancaster County's Kindergarten MMR rate ranges from (26.1%, 100.0%) across its 83 reporting schools, the lowest rate in the state. Schools identifiable as plain community have significantly lower Kindergarten MMR vaccination rates (mean = 56.3%) than other county schools (mean = 88.6%).

**A large susceptible pocket is not sufficient on its own**

Allegheny County has a larger absolute number of under-vaccinated kindergarteners than Lancaster County, but currently has zero cases. I do expect this will change as the outbreak progresses.

**Methods**

**Correlation**

Pearson (r), Spearman (rho), Kendall (tau) run in parallel since case counts heavily zero-inflated and skewed, which violates the assumptions behind any single methods.
**Regression**

Poisson, negative binomial, zero-inflated negative binomial; each fit with a log population offset to model case rate rather than raw count. Model choice was driven by diagnosed overdispersion and at the outbreak's earlier stages, convergence of the plain negative binomial. This was resolved by the zero-inflated model, and becomes less of a concern as more counties report cases.

**Spatial autocorrelation**

Global and local Moran's I (spdep), using PA county adjacency (tigirs) to test whether cases cluster geographically beyond what density and proximity alone would predict.

**Within-county transmission mechanisms**

School-level MMR vaccination rate variance, with Wilcoxon and Welch's t-test comparing Plain-community schools in Lancaster county with all other schools in the county.

**Limitations**

**Cross-section**

Currently is only cross-sectional, but the outbreak progresses, some causality may be able to be seen.
**Live outbreak data**

Cases update three times per week (M, W, F). Conclusions about statistical significance must be checked again after each case count update.

**Small effective sample for county models**

Currently, about 1/3 of PA counties are reporting cases, so regression coefficients may carry uncertainty. This will likely become less of a concern as more counties report cases.

**Author**
Evan M. Heffelfinger
