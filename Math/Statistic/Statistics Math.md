
英文<img width="20px" />|符号|中文<img width="120px" />|解释
---|---|---|---
summation|∑|求和
mean|μ (mu)|平均数
variance|$$σ^2$$|方差|数据波动的稳定性 描述数据与平均值的偏离程度<br>Standard deviation measures the spread of a data distribution. **The more spread out a data distribution is, the greater its standard deviation.**
standard deviation|$\sigma = \sqrt{\frac{\sum_{i=1}^{N}(x_i-\mu)^2}{N}}$|（总体）标准差|![[标准差解释.png]]
unbiased sample variance|$S_x = \sqrt{\frac{\sum_{i=1}^{n}(x_i-\bar{x})^2}{n-1}}$<br>$\bar(x)$ sample mean|（样本）标准差|


<br>

### Range / 极差
最大 - 最小

<br>

### Sample Variance

[Why N-1](https://www.khanacademy.org/math/statistics-probability/summarizing-quantitative-data/more-on-standard-deviation/v/another-simulation-giving-evidence-that-n-1-gives-us-an-unbiased-estimate-of-variance)

![[Sample Size vs Variance.png | 300]]

<br>

### Interquartile range (IQR)

IQR = Q3 - Q1
基于中位数
25% - 75%


Mean → Standard Deviation
Median → Interquartile Range

<br>

### Percentile 百位分数
% of the data is at | below the amount
Cumulative relative frequency graph → percentile graph

<br>

### z score / z分数

Standard deviation from mean

$$z = \frac{\text{data point − mean}}{\text{standard deviation}}$$ 

<br>

$$z = \frac{x - \mu}{\sigma}$$


z分数（z-score），也叫标准分数（standard score）是一个数与平均数的差再除以标准差的过程。 

can apply to non-normal distribution

[table](https://www.math.arizona.edu/~rsims/ma464/standardnormaltable.pdf)

<br>

### Density Curve

curve area = 1, 100%
![[density_curve.png | 300]]
![[skewed-distrubution-mean-median.png]]

<br>

### Normal Distribution

![[normal-distributions.png | 300]]

[# Normal distributions review- Khan Academy](https://www.khanacademy.org/math/statistics-probability/modeling-distributions-of-data/normal-distributions-library/a/normal-distributions-review)

> -   symmetric bell shape
> -   mean and median are equal; both located at the center of the distribution

<br>

##### Empirical Rule
![[Empirical-Rule.jpg | 300]]

> -   ≈68% the data falls within 1 standard deviation of the mean
> -   ≈95% of the data falls within 2 standard deviations of the mean
> -   ≈99.7% of the data falls within 3 standard deviations of the mean

<br>

### Standard Normal Distribution
$\mu$ = 0, $\sigma$ = 1
![[standard-normal-distibution.png | 300]]

<br>

### Scatter Plot
A scatterplot is a type of data display that shows the relationship between two numerical variables.

Positive correlation|Negative correlation|No correlation
---|---|---
![[positive-corelation.png]]|![[negative-corelation.png]]|![[no-corelation.png]]

<br>

##### Description
**Direction**: positive/negative
**Strength**: strong/weak
**Form**: linear/nonlinear
outlier
clusters

###### Example description
![[example-description.png | 300]]

A quick description of the association in a scatterplot should always include a description of the form, direction, and strength of the association, along with the presence of any outliers.

> "This scatterplot shows a ==strong, negative, linear== association between age of drivers and number of accidents. There don't appear to be any ==outliers== in the data.”

<br>

### Correlation Coefficient (相关系数)

aka Pearson correlation coefficient PCC

[Correlation coefficient](https://www.khanacademy.org/math/statistics-probability/describing-relationships-quantitative-data/scatterplots-and-correlation/a/correlation-coefficient-review)

The correlation coefficient _r_ measures the direction and strength of a linear relationship.

-   It always has a value between `−1 ≤ r ≤ 1`.
-   Strong positive linear relationships have values of _r_ closer to 1.
-   Strong negative linear relationships have values of _r_ closer to −1.
-   Weaker relationships have values of _r_ closer to 0

Equation:

$r = \frac{1}{n-1} \sum(\frac{x_i - \bar{x}}{S_x})(\frac{y_i - \bar{y}}{S_y})$

$r = \frac{1}{n-1} \sum( \text{z score x} )(\text{z score y} )$

![[r-process.png]]

<br>

##### Residuals

A residual is a measure of how well a line fits an individual data point.
residual = actual - expected

This vertical distance is known as a residual. The residual is 4
![[residual.png|300]]

r → residual
$$\sum(|r_n|)$$ 
$$\sum(r_n)^2$$


[$r^2$ intuition](https://www.khanacademy.org/math/statistics-probability/describing-relationships-quantitative-data/assessing-the-fit-in-least-squares-regression/a/r-squared-intuition)

$r^2$ is also called → coefficient of determination.

<br>

Least sqaured 
$$m = r \frac{s_y}{s_x} + b$$

<br>

Residual plot
![[residual-plot.png]]

<br>



### Permutations & Combination 排列组合

Permutation

> Factorial 阶乘  $5! = 5 \times 4 \times 3 \times 2 \times 1 = 120$
> $1! = 1$
> $0! = 1$

Seat Arrangement

Formula:
$P(n,r)=\frac{n!}{(n-r)!}$

Example:
$_nP_r=_{26}P_3 = 26 \times 25 \times 24= \frac{26!}{(26-3)!}$

n -> 整个数量
r -> 椅子数量

<br>

Combination

多少种组合？
`A,B,C,D` 和 `D,A,B,C` 算一种

Formula: $_nC_K=\frac{\frac{n!}{(n-K!)}}{K!}=\frac{n!}{K!(n-K)!}$
多了除以“椅子”的组合数量
4！4 x 3 x 2 x 1