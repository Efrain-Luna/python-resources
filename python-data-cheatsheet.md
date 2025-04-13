# 🐍 Python Cheat Sheet for Data Analysis

This cheat sheet covers essential functions and formulas used for A/B Testing and statistical analysis in Python.

---

## 📊 A/B Testing – Sample Size Calculator

```python
import math
from scipy import stats

def ABTest_sample_size(p1, mde, alpha, beta, n_side):
    """
    p1 : Baseline conversion rate
    mde : Minimum detectable effect
    alpha : Significance level (e.g., 0.05)
    beta : Type II error (e.g., 0.20 for 80% power)
    n_side : 1 for one-tailed, 2 for two-tailed test
    """
    p2 = p1 + mde
    z_crit = stats.norm.ppf(alpha / n_side)
    z_crit2 = stats.norm.ppf(1 - beta)
    n_sample = ((z_crit * math.sqrt(2 * p1 * (1 - p1))) + 
                (z_crit2 * math.sqrt(p1 * (1 - p1) + p2 * (1 - p2))))**2 / mde**2
    return math.ceil(n_sample)

