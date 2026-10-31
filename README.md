[README.md](https://github.com/user-attachments/files/34208844/README.md)
# Diagnosing Experimental Failures in A/B Testing

## Objective

I examined how coding mistakes, assignment problems, marketplace interference and repeated testing can lead to misleading A/B test results.

## Methodology

- Fixed three CUPED bugs involving the adjustment coefficient, centering and standard-error calculation.
- Tested treatment–control splits for sample ratio mismatch.
- Compared an individual-level marketplace experiment with a full rollout.
- Compared Bayesian decisions with a frequentist permutation test.
- Wrote `bayes_ab()` and checked it on the original counts and a larger experiment.
- Simulated repeated peeking in experiments with no true effect.

## Key Findings

**CUPED:** The original code reported **0.0% variance reduction**. After the fixes, the reduction was **82.7%**, and the standard error fell from **0.1539 to 0.0641**.

**Sample ratio mismatch:** A **0.6 percentage-point** imbalance among **100,000 users** produced a chi-squared statistic of **14.40**. A smaller **0.05-point** imbalance among **20 million users** produced **20.00**. I found that statistical significance alone does not tell us how concerning an imbalance is.

**Marketplace interference:** The naive ATE was **0.1861**, compared with **0.1428** for a full rollout. The overstatement was **23.3% of the naive estimate**, because inventory competition hurt controls more.

**Bayesian testing:** With **P(B > A) = 0.8866** and expected loss **0.000473**, the rule did not ship B because the probability threshold failed. The permutation test also failed to reject, with **p = 0.2302**. With four times the users, my function returned **P(B > A) = 0.9951**, and the shipping rule passed.
