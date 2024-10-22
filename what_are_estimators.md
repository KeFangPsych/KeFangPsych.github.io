<font face="Consolas" color=#2f9e44 size=5>StatsReview📈</font>

### 'What are estimators: How sample mean and variance can be understood as estimators'
author: "Ke Fang (kf2393@nyu.edu)"
date: "2023-10-08"


### **I. A general framework of statistical modelling**

In statistics, we commonly employ a theoretical framework known as a **Data Generating Process (DGP)** to model the generation of data. This DGP, defined by certain **parameters**, governs how data is generated probabilistically (Note 1). For instance, when dealing with a single variable, we may assume that our data comprises independent observations drawn from an identical normal distribution, with the parameters of interest being the mean and variance of the distribution. Alternatively, we might describe one variable as a linear transformation of another variable with the addition of Gaussian noise. In this case, the parameters define both the relationship between the variables and the characteristics of the added noise.

*Note 1: Parameters of the DGP could be but are not necessarily the statistical characteristics of the DGP (such as expectation or variance), it should be more abstractly understood as variable quantitatives that define the process. For example, for a Poisson distribution, there is only one $\lambda$ parameter, which coincidentally also is the expectation and variance. And the uniform distribution is defined by its lower and upper bounds, which are not direct statistical measures of central tendency or spread.*

The primary objective in statistics involves several key steps: first, specifying a plausible DGP; second, estimating the parameters or other quantities of interest (e.g., statistical characteritics) associated with this DGP from data; third, probabilistic statements or hypotheses about the DGP based on the sample data; and finally, assessing the adequacy of our assumed DGP and identifying any potential model shortcomings or violations. Additionally, when we have multiple possible DGPs to consider, we can compare them to determine the "best" one. These processes are often referred to as **model specification**, **parameter estimation**, **statistical inference**, **model diagnosis**, and **model comparison**.

**Model specification**, often referred to as specifying the Data Generating Process (DGP), is a " art and science" process that heavily depends on your prior knowledge about the underlying process, the specificity of DGP you are willing to make, and the data you have on hand as constraints.  For instance, if you are investigating the relationship between height and the biological sex of individuals, prior knowledge suggests that these two variables are related. Therefore, you might choose to model height as a function of sex with some added noise to account for variability. Another factor often considered is the specificty of the DGP. In some cases, if you are less willing to make assumptions, you might choose to roughly define you DGP (e.g., simply assume the heights are independently drawn from a distribution with finite expectation and variance), or more specifically define it (e.g., drawn from a normal distribution). This could have significant influence on the later estimation and inference processes. However, it's essential to consider the data you have at your disposal. If your dataset only includes the height variable and lacks information on sex or any other relevant factors, then attempting to model the data with this DGP may not be suitable or informative. Furthermore, once we have gone through the process of estimation and inference, we may evaluate the adequacy of our initially assumed DGP through model diagnosis. If the model appears to be inadequate in explaining the observed data, we can refine or select a different DGP and repeat the process.

### **II. Estimation**

**Estimation** in statistical modeling involves harnessing observed data to determine the parameters (or other quantities related to parameters) of interest within our Data Generating Process (DGP). The parameter (or related quantity) we seek to estimate is commonly known as the **estimand**, representing the quantity of interest or the specific DGP parameter we aim to pinpoint.

During the estimation phase, we use an **estimator**—a mathematical function of the observed data—to approximate a parameter inherent to the DGP. This estimator is tied to a specific **objective function**, often referred to as the loss, cost, error, or even reward function. This objective function, which is often a function of both the observed data and the parameters, quantifies the deviation between the model's predictions and the observed data. Ideally, the estimator is derived by optimizing this objective function to align closely with the parameter it seeks to estimate.

Thus, the estimation process is also often referred to as the process of "fitting the data to the model." This involves tweaking the model's parameters to most effectively match the observed data. Both estimation and fitting are achieved by optimizing the objective function, which essentially tries to pinpoint the parameter that best characterizes the data. This may seem less obvious for simple estimates such as sample mean and Ordinary Least Square (OLS) estimators (but we will prove that they indeed are), but more importantly, they are especially the case when the estimators are complicated and have no closed-form formula to directly calculate the parameter estimates such as Maximum Likelihood Estimators (MLE).

Due to the inherent probabilistic nature of the DGP, the estimator is a random variable. When we apply this estimator to a specific data set, what we obtain is an **estimate**, representing a single realization or observation of the estimator.

### **III. Property of Estimators**

Estimators are mathematical functions used to estimate unknown parameters from observed data, and there can be many different estimators for the same parameter. Just as you can measure the length of a plastic snake using a tape measure or hand spans, you can estimate a person's big-five personality traits using various methods, such as the BFI-44, BFI-10, or, innovatively, by asking their family and friends to answer the scales? Each of these methods is essentially an estimator for the underlying personality traits. As you might felt that the tape measure is probably better than the hand span measure (more accurate, or more consistent when measured repeatedly?), some estimators are better than the others. And there are some quantity to judge them on.

Several properties or criteria are used to judge the goodness or quality of an estimator. To mathematically represent these properties of estimators, let's consider an estimator $\hat{\theta}$ of a parameter $\theta$, based on a sample $X_1, X_2, ..., X_n$:

#### 1. **Unbiasedness**

   An estimator is said to be unbiased if the expected value of the estimator equals the true parameter value.
   
   Specifically, the **bias** of an estimator is the expected difference between estimated value and the true parameter value. 

   $$\text{Bias}(\hat{\theta}) = E(\hat{\theta} -\theta) = E(\hat{\theta}) - \theta$$
   
   An estimator is said to be unbiased if its bias equals zero, which means that on average, the distance between the estimates and the estimand (DGP parameter) average out to be zero. 
   
   Mathematically, then:

   $$E(\hat{\theta}) = \theta \text{ or } E(\hat{\theta} -\theta) = 0$$

#### 2. **Efficiency**: 
  
   An efficient estimator is an estimator that estimates the quantity of interest in some “best possible” manner. The notion of “best possible” relies upon the choice of a particular loss function — the function which quantifies the relative degree of undesirability of estimation errors of different magnitudes.
     
##### **2.1 For unbiased estimator:**

   Among a class of unbiased estimators, the estimator with the smallest variance is said to be efficient. 
   
   The variance of an estimator of $\hat{\theta}$ is defined as the the squared distance, on average, between one estimate and the estimator. 
   
   Mathematically defined as:

   $$Var(\hat{\theta}) = E\left[\left(\hat{\theta} - E(\hat{\theta})\right)^2\right]$$
   
   Thus, for any two unbiased estimator $\hat{\theta}$ and $\tilde{\theta}$ of the estimand. $\hat{\theta}$ is said to be more efficient than $\tilde{\theta}$, if and only if:

   $$\text{Var}(\hat{\theta}) \leq \text{Var}(\tilde{\theta})$$

   The **Minimum Variance Unbiased Estimator (MVUE)** is an estimator that is both unbiased and has the minimum variance among all unbiased estimators.
  
   Mathematically, $\hat{\theta}$ is the MVUE if and only if:
  

   $$\forall\ \tilde{\theta} \text{ s.t. } E(\hat{\theta}) = \theta, \text{Var}(\hat{\theta}) \leq \text{Var}(\tilde{\theta})$$

   However, it's often not feasible to construct and evaluate all possible unbiased estimators to determine which one has the minimum variance.  The Cramér-Rao Lower Bound (CRLB) stipulates the best possible precision (lowest variance) that any unbiased estimator of a parameter can achieve. 
   
   $$\text{Var}(\hat{\theta}) \geq \frac{1}{I(\theta)}$$
   
   The CRLB is defined as the reciprocal of the Fisher Information. The Fisher Information, $I(\theta)$, measures the amount of information that an observable random variable $X$ carries about an unknown parameter $\theta$ upon which the probability of $X$ depends. It is calculated as the expected value of the squared score function, which is deined as the derivative of the log-likelihood function of $X$ with respect to the parameter $\theta$:
     
   $$I(\theta) = E\left[\left(\frac{\partial}{\partial \theta} \ln f(x; \theta)\right)^2\right]$$
   
   Thus, if an unbiased estimator reaches the CRLB, it is considered efficient and effectively the MVUE. 
   
   However, it should be noted that CRLB require a more well-defined DGP rather than the iid assumptions, the pdf of population has to be defined in order to calculate the likelihood. 
   
   Also, the CRLB does not necessarily indicate that an estimator achieving this bound exists, nor does it provide a method for constructing such an estimator.  
   
##### **2.2 For biased estimators:**

   The idea of efficiency could also be extend to biased estimators, one of the intuitive way to evaluate the estimator integrating both bias and variance is to consider how much it deviate from the true value of the estimand, mathematically known as the mean standard error (MSE):

   $$
   \begin{align*}
   MSE(\hat{\theta}) =& E[(\hat{\theta} - \theta)^2] \\
   =& E(\hat{\theta}^2 - 2 \cdot \theta \cdot \hat{\theta} + \theta^2) \\
   =& E(\hat{\theta}^2) - 2\theta \cdot E(\hat{\theta}) + \theta^2 \\
   \\
   \text{ As }  Var(X)& = E(X^2) - E^2(X) \\
   \\
   MSE(\hat{\theta}) =& Var(\hat{\theta}) + E^2(\hat{\theta}) - 2\theta \cdot E(\hat{\theta}) + \theta^2 \\ 
   =& Var(\hat{\theta}) + [E(\hat{\theta}) - \theta)]^2 \\
   =& Var(\hat{\theta}) + Bias(\hat{\theta})^2
   \end{align*}
   $$


   In this case, a more efficient estimator is the one with smaller MSE, and the estimator with the smallest MSE is considered to be the most efficient among all estimators (biased or unbiased).
   
   Specifically, for any two estimators $\hat{\theta}$ and $\tilde{\theta}$ of the estimand. $\hat{\theta}$ is said to be more efficient than $\tilde{\theta}$, if and only if:

   $$\text{MSE}(\hat{\theta}) \leq \text{MSE}(\tilde{\theta})$$
   
   The lowest possible variance and MSE, is also provided by the generalized form of the Cramér-Rao Lower Bound (CRLB) such that:
   
   $$\text{Var}(\hat{\theta}) \geq {\frac {[1+{\frac{d\ Bias(\theta )}{d\theta}} ]^{2}}{I(\theta )}}$$
   Noted that the key difference here is the $\frac{d\ Bias(\theta )}{d\theta}$ term, suggesting that if the first order deravitives of bias regarding the estimand is negative, the estimator could have a smaller bound on variance. 
   
   $$\text{MSE}(\hat{\theta}) \geq {\frac {[1+{\frac{d\ Bias(\theta )}{d\theta}} ]^{2}}{I(\theta )}} + [\text{Bias}(\theta)]^2$$
   
   Similar to the variance, noted that although the $[\text{Bias}(\theta)]^2$ increased the bound, it is possible for the $\frac{d\ Bias(\theta )}{d\theta}$ term to overcome this increase resulting in the estimator could have a smaller bound on MSE. 
   
   Similarly noted: Generalized CRLB require a more well-defined DGP rather than the iid assumptions, the pdf of population has to be defined in order to calculate the likelihood. And the CRLB does not necessarily indicate that an estimator achieving this bound exists, nor does it provide a method for constructing such an estimator.
   
#### 3. **Consistency**: 

   An estimator is consistent if, as the sample size n grows to infinity, it converges in probability to the true parameter value. Formally, it can represented as

   $$\hat{\theta}_n \xrightarrow{P} \theta$$
   
   As $n \to \infty$, the estimator $\hat{\theta}_n$ converges in probability to the true parameter $\theta$.

   Note: $\xrightarrow{P}$ denotes **convergence in probability**. Mathematically, for every $\epsilon > 0$:
   
   $$\lim_{n \to \infty} P(|\hat{\theta}_n - \theta| > \epsilon) = 0$$
   
   This essentially means that the probability that $\hat{\theta}_n$ deviates from $\theta$ by more than $\epsilon$ goes to zero as $n$ increases.

   Informally, as we gather more data, the estimate gets closer and closer to the actual parameter.
   
#### 4. **Linearity**: 

   An estimator is linear if it is a linear combination of the observations.

   $$\hat{\theta} = X \cdot\vec{a} = a_0 + \sum_{i=1}^{n} a_i X_i$$
   where $\vec{a} = (a_0, a_1, ..., a_n)$ is a real numbered vector.
   
   Additionally, the **Best Linear Unbiased Estimator (BLUE)** is an estimator that is a unbiased linear unbiased estimator and has the minimum variance among all linear unbiased estimators.
  
   Mathematically, $\hat{\theta}$ is the BLUE if and only if:
  

   $$\forall\ \tilde{\theta}\ \text{ s.t. }\ \tilde{\theta} = X \cdot \vec{a}\ \ \text{and }\ E(\hat{\theta}) = \theta,\\ \text{Var}(\hat{\theta}) \leq \text{Var}(\tilde{\theta})$$
   However, it is worth noting that, although BLUEs are bounded by the Cramér-Rao Lower Bound (CRLB), the BLUEs may not reach it even if other unbiased non-linear estimators may have lower variances or do reach CRLM. 
   
   So BLUE is often proved in other ways (see OLS and Gaussian-Markov notes).
   
   Of course, if the variance of a linear unbiased estimator actually reach the CRLB, it would be a BLUE as there is no smaller variance can be reached among all unbiased estimators (including linearly unbiased ones). 
   

#### 5. **Asymptotic Normality** 

   An estimator is said to be asymptotically normal if, as $n \to \infty$, the distribution of the estimator (often normalized estimators) converges in distribution to a normal distribution (if normalized estimator, with mean 0 and some variance $\sigma^2$).
   
   Mathematically:

   $$\sqrt{n}(\hat{\theta}_n - \theta) \xrightarrow{D} N(0, \sigma^2)$$
   
   Note: $\xrightarrow{D}$ denotes **convergence in distribution** (or weak convergence). 
   
   For any real number $z$:
   
   $$\lim_{n \to \infty} P(\sqrt{n}(\hat{\theta}_n - \theta) \leq z) = \Phi(z;\,0,\,\sigma^2)$$
   
   where $\Phi$ is the cumulative distribution function of the normal distribution.

#### 6. **Other properties**: 

   There are other properties can be considered when evaluating an estimator that we may not cover, such as **sufficiency** (this is more mathematically involved and less practically used) and **robustness** (related to model diagnosis and evaluation, a more qualitative property measuring whether the estimator's performance deteriorate significantly when assumptions about the underlying data distribution are violated).

### **IV. Example 1: The Sample Mean**

Our data generating process (DGP) assumes that our $n$ (sample size) observations of a random variable $X$ are independently drawn from one identical distribution (i.i.d.) with expectation $E(X) = \mu$ and variance $Var(X) = \sigma^2$. 

The sample mean is defined as:

$$\bar{X} = \frac{\sum^{n}_{i=1}X_i}{n}$$

#### **1. Sample mean as an estimator**

There are two intuitive schemes of using the sample mean as an estimator:

##### **1.1 Sample mean as method of moments (MoM) estimator**

First, if you are familiar with the method of moment (MoM) estimation in mathematical statistics, the sample mean is the MoM estimator of the population expectation. 

Simply put, the $n$th order moment of $X$ is defined as:

$$E(X^k) = \int^{\infty}_{-\infty} x^k \cdot pdf(x^k) dx$$

In MoM, intuitively from a frequentist approach, the observed frequency in sample converge to the true probability (proved by the Glivenko-Cantelli Theorem).

So it is intuitive to construct the sample moment as 

$$\bar{X}^k = \sum_{x^k_i \in X^k} \left[x^k_i \cdot \frac{n | X^k = x^k_i}{n} \right] = \frac{\sum x^k_i}{n}$$ 

These estimators of the (raw) moments are unbiased for the corresponding population moments.

$$
\begin{align*}
E(\bar{X}^k) =& E(\frac{1}{n} \cdot \sum x^k_i) \\
=& \frac{1}{n} \cdot E(\sum x^k_i) \\
=& \frac{1}{n} \cdot \sum E(x^k_i) \\
\text{As } x_i &\text{ are } i.i.d\\
=& \frac{1}{n} \cdot n \cdot E(X^k) \\ 
=& E(X^k)
\end{align*}
$$

**Note:** Although the MoM estimator of population **(raw) moments** are unbiased, this doesn't mean the other MoM estimators are also unbiased. As we will very shortly see, the MoM estimator estimating the population variance is actually biased.

According to the Law of Lagre Number, the sample moments actually converge to the population moment.

If we are interested in other parameters that are not directly related to moments. We can construct the pdf of the population distribution of X as $F(x, \vec{\theta})$. The vector $\vec{\theta}$ is the parameters governing the population distribution. For example, in a uniform distribution, $\vec{\theta}$ would be a two-dimensional vector including the upper and lower limit of the distribution $\vec{\theta} = (a, b)$, for a normal distribution, it would be a 2-dimensional vector including $\vec{\theta} = (\mu, \sigma^2)$, for a Possion distribution , it would be a scalar $\theta = \lambda$. 

In order to estimate $\vec{\theta}$, we can construct a set of equations using the moments of $X$. The number of euqations needed should equal to the number of elements in $\vec{\theta}$. Especially, as the higher order moments guarenteen the existence of lower order moments, we could always start with the first moments. Of course, for MoM to work, this means the moments of must exist.

The set of function we would use is:

$$E(X^k) = g_k(\vec{\theta}),\ k = 1, ..., norm(\vec{\theta})$$

Lastly, in order to solve for $\vec{\theta}$, we will replace the left of the equations with the sample moments.

Although the when we defined $F(x, \vec{\theta})$, the equation will also simplify as $\frac{\sum x_i}{n} = \mu$. The population expectation (first moment), even without specifying the specific $F(x, \vec{\theta})$, is estimated using the sample mean $\bar{X}$.

##### **1.2. Sample mean as a least square estimator**

Secondly, the sample mean could be understand as the least square (LS) estimator of the population expectaion.

The method of least squares estimation estimates parameters by optimizing/minimizing the sum of squared discrepancies between the statistics of each observed data, and their expected values.

Thus, given a set of observation of $X: X_1, X_2, ..., X_n$, we could construct an estimator of the population expectation as:

$$loss = \sum^n_{i} \left[ (X_i - \mu)^2 \right]$$

$$\hat{\mu}_{LS} = \arg\min_{\mu} \left[ \sum (X_i - \mu)^2\right]$$

$$\frac{d}{d \mu} \left[ \sum (X_i - \mu)^2\right] = -2\sum X_i + 2n \mu = 0$$

Thus:

$$\hat{\mu}_{LS} = \frac{\sum X_i}{n} = \bar{X}$$

#### **2. Property of the sample mean as estimator**

Once we have constructed this estimator, we could evaluate it based on the standard we mentioned before:

To evaluate the bias in estimator, we calculate the expectation of the sample mean (actually already proved in the MoM section):

$$
\begin{align*}
E(\bar{X}) =& E(\frac{1}{n} \cdot \sum^n_i(X_i)) \\ 
=& \frac{1}{n} \cdot \sum^n_iE(X_i)\\
\text{As } X_i &\text{ are  from indentical distributions}\\
=&\frac{1}{n}\cdot n \cdot \mu\\
=& \mu
\end{align*}
$$

and the variance of the sample mean would be: 

$$
\begin{align*}
Var(\bar{X}) =& Var(\frac{1}{n} \cdot \sum^n_i(X_i))\\
=& \frac{1}{n^2} \cdot \sum^n_i Var(X_i)\\
=&\frac{1}{n^2} \cdot n \cdot \sigma^2\\
=& \frac{\sigma^2}{n}\\[2ex]
*\text{Note: } & Var(X_1 +X_2) = Var(X_1) + Var(X_2) + Cov(X_1, X_2)\\
&\text{As the samples are drawn individually, } Cov(X_1, X_2) =0, \\
&Var(X_1 +X_2) = Var(X_1) + Var(X_2)\\
\end{align*}
$$



### **IV. Example 2: The Sample Variance**

The estimator for variance could also be constructed in using the same logic:

Suppose $X_1, X_2, ... X_n$ are iid random variables from a population with mean $\mu$ and variance $\sigma^2$. 

#### **1. Constructing an estimator for population variance**

##### **1.1. The method of moments estimator (MoM) of the population variance**

Given the definition of variance of a random variable, we know:

$$
\sigma^2 = E[X - E(X)]^2 = E(X^2) - E^2(X)
$$

Then the MoM estimator of the population would just replace the population moments $E(X^2)$ and $E(X)$ with corresponding sample moments.

$$\hat{\sigma^2}_{MoM} = \frac{\sum (X^2_i)}{n} - \left[\frac{\sum (X_i)}{n}\right]^2$$

##### **1.2 The least square (LS) estimator of the population variance**

**(1) If we assume population expectation is known $\mu$**

$$loss = \sum^n_{i} \left[ (X_i - \mu)^2 - \sigma^2\right]^2$$

$$\hat{\sigma^2}_{LS} = \arg\min_{\sigma^2} \sum^n_{i} \left[ (X_i - \mu)^2 - \sigma^2\right]^2$$

$$\frac{d\ loss}{d \sigma^2} = -2 \sum \left[ (X_i- \mu)^2 - \sigma^2 \right] = 0$$

Thus:

$$\hat{\sigma^2}_{LS_1} = \frac{\sum (X_i - \mu)^2}{n}$$

**(2) we assume population expectation is unknown and we use the sample mean (also LS estimator) as its estimator**

$$loss = \sum^n_{i} \left[ (X_i - \bar{X    })^2 - \sigma^2\right]^2$$

$$\hat{\sigma^2}_{LS} = \arg\min_{\sigma^2} \sum^n_{i} \left[ (X_i - \bar{X})^2 - \sigma^2\right]^2$$

$$\frac{d\ loss}{d \sigma^2} = -2 \sum \left[ (X_i- \bar{X})^2 - \sigma^2 \right] = 0$$

Thus:

$$\hat{\sigma^2}_{LS_2} = \frac{\sum (X_i - \bar{X})^2}{n}$$

We can see the $\hat{\mu}_{LS_2}$ estimator is identical to the MoM estimator $\hat{\mu}_{MoM}$.

$$
\begin{align*}
\hat{\sigma^2}_{LS_2} =& \frac{\sum (X_i - \bar{X})^2}{n} \\
=& \frac{\sum (X^2_i - 2\bar{X}X_i + \bar{X})}{n} \\
=& \frac{\sum (X^2_i) - 2\bar{X}\sum X_i + \sum (\bar{X}^2)}{n} \\
=& \frac{\sum (X^2_i) - 2\bar{X}\cdot n\bar{X} + n\bar{X}^2}{n} \\
=& \frac{\sum (X^2_i) - n\bar{X}^2}{n} \\
=& \frac{\sum (X^2_i)}{n} - \bar{X}^2 \\
=& \frac{\sum (X^2_i)}{n} - \left[\frac{\sum (X_i)}{n}\right]^2 = \hat{\sigma^2}_{MoM}
\end{align*}
$$

This is because in MoM, we replaced all the population moments with sample moments (assume $\mu$ is unknown and use the sample mean as estimator for first moment).

#### **2. Property of the population variance estimators**

Now we can evaluate the two estimators we have:

First, if the population mean $\mu$ is known, the LS estimator is unbiased:

$$
\begin{align*}
E(\hat{\sigma^2}_{LS_1}) =& E \left[ \frac{\sum (X_i - \mu)^2}{n} \right] \\
=& \frac{1}{n }E \left[ \sum (X^2_i - 2\mu X_i + \mu^2) \right] \\
=& \frac{1}{n }E \left[ \sum (X^2_i) - 2\mu \sum (X_i) + n\mu^2) \right] \\
=& \frac{1}{n } \left[ E \left( \sum (X^2_i) \right) - 2\mu \cdot E \left(\sum (X_i) \right) + n\mu^2 \right] \\
=& \frac{1}{n } \left[ \sum E \left( X^2_i \right) - 2\mu \cdot \sum E(X_i) + n\mu^2 \right] \\
=& \frac{1}{n } \left[ \sum \left[ Var(X_i) +E^2(X_i) \right] - 2\mu \cdot \sum E(X_i) + n\mu^2 \right] \\
=& \frac{1}{n } \left[ n \sigma^2 + n\mu^2 - 2\mu \cdot n\mu + n\mu^2 \right] \\
=& \sigma^2 \\
\end{align*}
$$

However, if we use the MoM estimator, or the LS estimator when the population expetectation is estimated using sample mean. The estimator is actually biased:

$$
\begin{align*}
E[\hat{\sigma^2}_{MoM}] = E(\hat{\sigma^2}_{LS_2}) =& E \left[ \frac{\sum (X_i - \bar{X})^2}{n} \right] \\
=& \frac{1}{n }E \left[ \sum (X^2_i - 2\bar{X} X_i + \bar{X}^2) \right] \\
=& \frac{1}{n }E \left[ \sum (X^2_i) - 2\bar{X} \sum (X_i) + n\bar{X}^2) \right] \\
=& \frac{1}{n } \left[ E \left( \sum (X^2_i) \right) - 2 E \left(\bar{X} \cdot \sum (X_i) \right) + nE (\bar{X}^2 ) \right] \\
=& \frac{1}{n } \left[\sum E(X^2_i) - 2 E \left(\bar{X} \cdot n\bar{X} \right) + nE (\bar{X}^2 ) \right] \\
=& \frac{1}{n } \left\{\sum \left[ Var(X_i) + E^2(X_i)\right] -  nE (\bar{X}^2 ) \right\} \\
=& \frac{1}{n } \left\{n\left[ Var(X_i) + E^2(X_i)\right] -  n \left[ Var(\bar{X}) + E^2(\bar{X})) \right] \right\} \\
=& \frac{1}{n } \left[n \sigma^2 + n\mu^2 -  n \frac{\sigma^2}{n} - n \mu^2 \right] \\
=& \left(1 - \frac{1}{n}\right) \cdot \sigma^2\\
=& \frac{n-1}{n} \cdot \sigma^2\\
\end{align*}
$$



We can see that this bias is introduced due to the variance of $\bar{X}$. More generally, $E(\bar{X}) = \mu$ only guarantee linear transformation of $\bar{X}$ will remain unbiased, but as the MoM estimator is a non-linear transformation, the unbiasness no longer holds (i.e.,  $g(\cdot)$ is linear $\rightarrow$ $E[g(X)] = g(E[X])$, but without such constraints, the equality is not always true, see also the Jensen's Inequality).

Specifically, this biased estimator always underestimate the population by a factor of $\frac{n-1}{n}$, as expectation has the linearity property (i.e., $E(aX) = a\cdot E(X)$). We can easily adjust for this bias by:

$$
\text{Let } S^2 \text{ be an unbiased estiamtor of } \sigma^2 \text{ and } S^2 = b \cdot \hat{\sigma^2}_{MoM}\\
E(b \cdot \hat{\sigma^2}_{MoM}) = b \cdot \frac{n-1}{n} \cdot \sigma^2 = \sigma^2 \Rightarrow b = \frac{n}{n-1}\\
S^2 = \frac{n}{n-1} \cdot\frac{\sum (X_i - \bar{X})^2}{n} = \frac{\sum (X_i - \bar{X})^2}{n-1}
$$

Thus, the sample variance, which is the adjusted MoM or LS estimator of population variance, is an unbiased estimator of population variance when the population expectation is unknown. The adjustment is known as the Bessel's correction.

$$S^2  = \frac{\sum (X_i - \bar{X})^2}{n-1}$$

The variance of the sample variance estimator is (the detailed proof can be found [O’Neill, 2014](https://doi.org/10.1080/00031305.2014.966589)):

$$
\begin{align*}
Var(S^2) &= E\bigg[ \Big[S^2 - E(S^2) \Big]^2\bigg] \\
&= \bigg(\kappa - \frac{n-3}{n-1} \bigg) \frac{\sigma^4}{n}\\
\\
\text{with }\ \kappa =& E \left[ \left(\frac{X - \mu}{\sigma} \right)^4 \right] = \frac{E [(X - \mu)^4]}{\sigma^4}
\end{align*}
$$

$\kappa$ is the kurtosis of the population, which is defined as the fourth standardize moments. $\kappa$ is bounded by $[1, \infty)$. Specifically, $\kappa \geq 1 +\gamma^2$, where $\gamma = E[(X_i - \mu)^3] / \sigma^3$ is the skewness (third standardized moment) of the population.

According to the property of variance, we could also calculate the variance for the MoM estimator.

$$
\begin{align*}
Var \left( \hat{\sigma^2}_{MoM} \right) =& Var \left( \frac{n-1}{n} \cdot S^2 \right) \\
=& \left( \frac{n-1}{n} \right)^2 Var(S^2) \\
=& \left( \frac{n-1}{n} \right)^2 \bigg(\kappa - \frac{n-3}{n-1} \bigg) \frac{\sigma^4}{n}
\end{align*}
$$

We can see that the biased MoM estimator always have a lower variance than the sample variance.

The bias of the MoM estimator is:

$$
\begin{align*}
Bias \left( \hat{\sigma^2}_{MoM} \right) = \sigma^2 - \frac{n-1}{n} \cdot \sigma^2 = \frac{\sigma^2}{n} 
\end{align*}
$$

We can also potentially compare these two estimators using MSE.

The MSE of the MoM estimator is:

$$
MSE\left( \hat{\sigma^2}_{MoM} \right) = Var\left( \hat{\sigma^2}_{MoM} \right) + \left[ Bias\left( \hat{\sigma^2}_{MoM} \right) \right]^2 \\
= \left( \frac{n-1}{n} \right)^2 \bigg(\kappa - \frac{n-3}{n-1} \bigg) \frac{\sigma^4}{n} +\frac{\sigma^4}{n^2} \\
$$

As sample variance is an unbiased estimator, its MSE is its variance:

$$
MSE(S^2) = \bigg(\kappa - \frac{n-3}{n-1} \bigg) \frac{\sigma^4}{n}
$$

The difference between the MSEs of the two estimators is:

$$
MSE(S^2) - MSE( \hat{\sigma^2}_{MoM}) = \left[ (2 - \frac{1}{n})(\kappa - \frac{n-3}{n-1}) -1\right] \frac{\sigma^4}{n^2} \\
\text{As for the sample variance estimator to exist } n \geq 2, \\
2 > (2 - \frac{1}{n}) \geq 1.5, \text{ with } \lim_{n \rightarrow \infty} (2 - \frac{1}{n}) = 2;\\
\kappa -1 < (\kappa - \frac{n-3}{n-1}) \leq \kappa + 1, \text{ with } \lim_{n \rightarrow \infty} (\kappa - \frac{n-3}{n-1}) = \kappa -1\\
$$

So as long as $\kappa \geq 2$, $\hat{\sigma^2}_{MoM}$ always has a smaller MSE. This gives us some intuition of balancing different aspects when selecting an estimator. For example, the biased estimator has a smaller MSE under certain conditions, indicating that on average, the squared distance between the estimated values and the true value are smaller, although the distance does not average out to be zero. Also, as the variance of the biased estimator is always smaller than it of the unbiased one, by adding biases, we might be able to shrink our variance (bias-variance trade-off).




