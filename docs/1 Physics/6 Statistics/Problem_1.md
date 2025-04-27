# Problem 1

## **Exploring the Central Limit Theorem through Simulations**


## **Motivation**

The Central Limit Theorem (CLT) is one of the most powerful and important results in all of statistics. It states that the distribution of the sample mean approaches a normal distribution as the sample size becomes large, regardless of the population's original distribution (provided the population has finite variance).

Understanding and visualizing the CLT is essential for grasping concepts such as confidence intervals, hypothesis testing, and the foundations of inferential statistics. By simulating different distributions and observing the behavior of sample means, we can deeply appreciate the practical implications of this theorem.

---

## **1. Simulating Sampling Distributions**

We will consider three fundamentally different population distributions:

- **Uniform Distribution**: All values within an interval are equally likely.
- **Exponential Distribution**: Models time between events in a Poisson process, highly skewed.
- **Binomial Distribution**: Discrete distribution modeling the number of successes in a fixed number of independent Bernoulli trials.

### **Generating Populations**

```python
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns

# Set random seed for reproducibility
np.random.seed(42)

# Population size
population_size = 100000

# Define populations
uniform_pop = np.random.uniform(0, 10, size=population_size)
exponential_pop = np.random.exponential(2, size=population_size)
binomial_pop = np.random.binomial(n=10, p=0.5, size=population_size)
```

---

## **2. Sampling and Visualization**

We will take repeated random samples of varying sizes and compute their means.

### **Sampling Process**

```python
def simulate_sampling(population, sample_size, num_samples=1000):
    means = [np.mean(np.random.choice(population, size=sample_size)) for _ in range(num_samples)]
    return means

sample_sizes = [5, 10, 30, 50]

populations = {
    "Uniform": uniform_pop,
    "Exponential": exponential_pop,
    "Binomial": binomial_pop
}

for pop_name, pop_data in populations.items():
    plt.figure(figsize=(18, 10))
    for i, size in enumerate(sample_sizes, 1):
        means = simulate_sampling(pop_data, size)
        plt.subplot(2, 2, i)
        sns.histplot(means, kde=True, stat="density", bins=30, color="skyblue")
        plt.title(f"{pop_name} Population - Sample Size {size}")
        plt.xlabel("Sample Mean")
        plt.ylabel("Density")
    plt.suptitle(f"Sampling Distribution of Sample Means ({pop_name} Population)", fontsize=18)
    plt.tight_layout(rect=[0, 0, 1, 0.95])
    plt.show()
```

---

## **3. Parameter Exploration**

### **Impact of Sample Size**

- **Small Sample Sizes (e.g., 5):** Sampling distributions retain the skewness or uniformity of the original population.
- **Moderate Sample Sizes (e.g., 30):** Distributions start to resemble a normal curve.
- **Large Sample Sizes (e.g., 50+):** Distributions are visibly normal even from heavily skewed populations.

### **Mathematical Confirmation**

The variance of the sample mean decreases with sample size:

$$
\sigma_{\bar{x}}^2 = \frac{\sigma^2}{n}
$$

where:
- $\sigma^2$ is the population variance,
- $n$ is the sample size.

Thus, as $n$ increases, the spread of the sampling distribution shrinks, leading to tighter, more concentrated distributions around the population mean.

### **Effect of Population Variance**

- Populations with higher variance yield wider sampling distributions.
- Larger samples mitigate this effect by reducing the sampling variance.

---

## **4. Practical Applications**

The Central Limit Theorem underpins many real-world statistical practices:

### **Estimation and Confidence Intervals**

- Allows statisticians to use sample means to estimate population means.
- Provides theoretical justification for constructing confidence intervals.

### **Quality Control in Manufacturing**

- Sample means are monitored to detect deviations from production norms.
- CLT ensures that the behavior of sample means follows predictable patterns.

### **Financial Modeling**

- Asset returns are often modeled assuming normality, an assumption justified by CLT for aggregated returns.

### **Polling and Surveys**

- Sample means and proportions from surveys are treated as approximately normal, enabling accurate inference about the larger population.

---

## **5. Advanced Topics and Extensions**

### **Skewness and Kurtosis Analysis**

- Measure the skewness and kurtosis of sampling distributions.
- Quantify how "normal" the sampling distribution becomes with increasing $n$.

### **Convergence Rates**

- Highly skewed distributions require larger $n$ for convergence.
- Symmetrical distributions (e.g., uniform) converge faster.

### **Visual Comparison**

Overlay the sampling histograms with a true normal curve:

```python
from scipy.stats import norm

mean = np.mean(means)
std = np.std(means)
x = np.linspace(min(means), max(means), 1000)
y = norm.pdf(x, mean, std)

plt.plot(x, y, color='red', label='Normal PDF')
plt.legend()
```

### **Heavy-Tailed Distributions**

- Explore cases where the population has infinite variance (e.g., Cauchy distribution) to observe the failure of the CLT.

---

## **Conclusion**

Through computational simulations:
- We observed the Central Limit Theorem's power and universality.
- Different populations (uniform, exponential, binomial) all produced approximately normal sampling distributions as sample sizes increased.
- Larger sample sizes improved the approximation to normality.

Thus, the CLT forms the backbone of many inferential techniques in statistics, making it one of the most celebrated results in mathematics.

Understanding and visualizing it through simulations solidifies foundational knowledge crucial for any scientific discipline.
