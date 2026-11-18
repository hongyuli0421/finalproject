# BST260 Final Project Proposal

**To:** BST260 Teaching Team, Fall 2026

## Project overview

I propose two exploratory analyses using datasets listed in the [BST260
project
instructions](https://vjcitn.github.io/bst260project-template/articles/instructions.html):
the NHANES data from the `NHANES` R package and the CDC foodborne and
waterborne outbreak data included in this project as `waterborne`. Each
analysis will have its own vignette, research question, descriptive
summaries, figures, and discussion of limitations.

## Analysis 1: BMI and systolic blood pressure in adults aged 40 and older

**Research question:** Among adults aged 40 years and older in the
2009–2012 NHANES educational dataset, how is body mass index associated
with average systolic blood pressure?

**Data and population.** I will use
[`NHANES::NHANES`](https://rdrr.io/pkg/NHANES/man/NHANES.html), an
educational dataset derived from the National Center for Health
Statistics’ 2009–2010 and 2011–2012 National Health and Nutrition
Examination Surveys. Its source and variable definitions are documented
in the [`NHANES` package](https://cran.r-project.org/package=NHANES) and
the [CDC NHANES website](https://www.cdc.gov/nchs/nhanes/). The unit of
analysis is a participant record in the resampled educational dataset;
the analysis will include records with `Age >= 40`. The dataset samples
participant records with replacement, so some participant IDs appear
more than once. I will retain the educational sample as supplied and
describe that resampling when interpreting the results.

**Exposure and outcome.** The exposure is `BMI` in kg/m², analyzed as a
continuous variable, with the association reported per 5 kg/m². The
outcome is `BPSysAve`, average systolic blood pressure in mm Hg, also
continuous. I will exclude records with missing BMI, blood pressure, or
prespecified adjustment variables from the adjusted model, report
missingness and the number excluded, and compare basic characteristics
of included and excluded records where possible. Missing values will not
be coded as zero.

**Analysis plan.** Before examining associations, I will prespecify age
(`Age`, continuous), sex (`Gender`), and race/ethnicity (`Race1`) as
adjustment variables because they may relate to both BMI and blood
pressure. I will summarize participant characteristics, BMI and blood
pressure using counts, percentages, medians and interquartile ranges,
and display a scatterplot with a smooth trend. I will fit an unadjusted
and an adjusted linear regression, report estimates and 95% confidence
intervals, inspect residuals and the shape of the BMI association, and
describe exploratory age and sex interactions if sample sizes permit.
The resampled data and cross-sectional design limit precision and causal
interpretation; the package describes this dataset as adapted for
teaching, not a research database. Results will be presented as
exploratory associations, not definitive population estimates.

## Analysis 2: Water exposure and reported outbreak size

**Research question:** Among reported U.S. waterborne disease outbreaks
in the project’s CDC dataset, how does the number of reported illnesses
differ between drinking-water and treated recreational-water outbreaks?

**Data and population.** I will use
`data("waterborne", package = "finalproject")`, the CDC outbreak data
supplied with the course template; its documented source is the [CDC
data API](https://data.cdc.gov/api/v3/views/5xkq-dg7x/query.json). The
dataset contains outbreaks with multiple transmission modes, so I will
restrict this analysis to records with `primary_mode` equal to `Water`.
The unit of analysis is one reported outbreak, not one person. The
analysis population is the subset of these records with exactly one of
the two selected water exposure categories.

**Exposure and outcome.** The exposure is `water_exposure`, coded as
`Drinking water` or `Recreational water -- treated`; outbreaks with
multiple listed exposure types, other categories, or missing exposure
will be excluded from the main comparison and counted separately. The
outcome is `illnesses`, a nonnegative count of reported illnesses per
outbreak. I will parse it as numeric, treat missing or invalid values as
missing rather than zero, and report exclusions and missingness. These
counts describe outbreak size, not infection risk or incidence rates.

**Analysis plan.** I will summarize counts of eligible outbreaks and the
median and interquartile range of reported illnesses by exposure, and
plot the distribution on a log-scaled axis where appropriate. Before
comparing outcomes, I will choose outbreak year (`year`) and state
(`state`) as adjustment variables: differences in time and location may
affect exposure patterns, surveillance, and outbreak reporting. I will
inspect category sizes and missingness first; if the data support it, I
will fit a negative binomial regression for illness counts with
exposure, year, and state, reporting the adjusted ratio of expected
reported illnesses with a 95% confidence interval. If the model is
unstable, I will report the descriptive comparison and explain why
rather than present unreliable estimates. Differences in investigation,
reporting, outbreak setting, pathogen, and the number of people exposed
can confound the comparison; the data lack a common population-at-risk
denominator. Therefore, I will not interpret the results as causal
effects or population incidence.

## Deliverables

The final site will include two reproducible analysis vignettes with
data provenance, descriptive statistics, visualizations, methods,
findings, uncertainty, and limitations. The proposal states intended
analyses; it does not claim results before they have been calculated.
