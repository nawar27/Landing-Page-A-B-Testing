# E-Commerce Landing Page A/B Testing

## Introduction

![source Images](https://www.leadpages.com/_next/image?url=https%3A%2F%2Fcdn.sanity.io%2Fimages%2F1ux2e04i%2Fproduction%2Ffd589b7e2d13df423596040b64792a6767bebe5e-1580x828.png%3Fauto%3Dformat&w=1080&q=75)

A/B testing (also known as bucket testing, split-run testing, or split testing) is a user experience research method. A/B tests consist of a randomized experiment that usually involves two variants (A and B), although the concept can be also extended to multiple variants of the same variable. It includes application of statistical hypothesis testing or "two-sample hypothesis testing" as used in the field of statistics. [wikipedia](https://en.wikipedia.org/wiki/A/B_testing)

Here, we'll use an e-commerce landing page for A/B testing. The goal of e-commerce's landing page development is to increase sales. And how many users who "convert" who decide to pay for the company's product. Dataset from [kaggle](https://www.kaggle.com/datasets/putdejudomthai/ecommerce-ab-testing-2022-dataset1)

## 1. Import Data

We look at our data

| user_id | timestamp | group     | landing_page | converted |
|---------|-----------|-----------|--------------|-----------|
| 851104  | 11:48.6   | control   | old_page     | 0         |
| 804228  | 01:45.2   | control   | old_page     | 0         |
| 661590  | 55:06.2   | treatment | new_page     | 0         |
| 853541  | 28:03.1   | treatment | new_page     | 0         |
| 864975  | 52:26.2   | control   | old_page     | 1         |

- The data have some variable (`user_id`, `time_stamp`, `group`, `landing_page`, `converted`)
- `group` : the `control` group represents the original version, while the `treatment` group is exposed to the modified version to evaluate the impact of the changes.
- `landing_page` :  Compare the old page and the new page to statistically test whether the landing page redesign has a significant impact on revenue.
- `converted` : The `converted` variable is 1 if the user converted (e.g., made a purchase), and 0 if they did not.

Verify whether the `user_id` variable contains duplicate data. Because in A/B testing every user must be unique

At this stage, we need to verify whether the `treatment ` group received the `old landing page` and the `control` group received the new one. Data collection systems can sometimes encounter errors that assign users to the wrong group, so it's important to ensure that each user was shown the correct landing page based on their assigned group.

The treatment group is expected to be shown the new landing page, whereas the control group should see the old landing page version.


## 2. Find the number of users, the number of conversions, and the conversion rate

In this section, we will fill in the table

<center>

|Group|Total Users|Count Converted|Conversion Rate|
|:--|:--:|:--:|:--:|
|Control|146196|17601|0.120|
|Treatment|146240|17374|0.118|

</center>

We do visualization

![visual](https://github.com/nawar27/Landing-Page-A-B-Testing/blob/main/picture/1.png)

The conversion rate for the Control group is slightly higher than that of the Treatment group. Specifically, the Control group has a conversion rate of 0.120 (12.0%) with 17,601 conversions out of 146,196 users, while the Treatment group has a conversion rate of 0.118 (11.8%) with 17,374 conversions out of 146,240 users.

Although the difference in conversion rates between the two groups is minimal (0.002 or 0.2 percentage points), the Control group performs marginally better in terms of user conversions. Further statistical testing (e.g., a z-test for proportions) would be required to determine whether this difference is statistically significant.

## 3. Statistic Test
In this case, we aim to test whether the new landing page has a positive impact on revenue.

$$
H_0 : \theta = \theta_0 \\

H_1 : \theta > \theta_0
$$

<center>

| Alpha (α) | P-value | Z-Statistic | Z-Critical |
|-----------|---------|-------------|------------|
|   0.05    | 0.9072  |  -1.3236    |  1.6448    |

</center>

- A hypothesis test was conducted to evaluate whether the new landing page had a statistically significant impact on revenue.
The results yielded a z-statistic of **-1.3236** and a p-value of **0.9072**.

- Given that the p-value is substantially greater than the typical significance level (0.05), **we fail to reject the null hypothesis**.

- Subsequently, we determined the critical z-value for a one-tailed test at the 5% significance level, which was **1.6448**.
Since the computed z-statistic (**-1.3236**) is less than the critical value, **we fail to reject the null hypothesis**.

**Visualization**

- we visualization our result statistic test
![chart](https://github.com/nawar27/Landing-Page-A-B-Testing/blob/main/picture/2.png)

- Based on the graph, the test statistic (z-statistic = -1.3236) lies to the left of the normal distribution and does not exceed the z-critical value (z-critical = 1.6449)
- Since the z-statistic falls within the acceptance region (green), we fail to reject the null hypothesis.
- At a significance level of 0.05, there is insufficient evidence to conclude that the tested effect or difference is statistically significant.

## Conclusion
- The difference in conversion rates is not statistically significant.
- So, we can say The new landing page does not provide sufficient statistical evidence that it significantly increases revenue.

To view the full analysis, can check in [jupyter notebook](D:\Output\Python\ecommerce_ab_testing_2022_dataset1\ab_testing.ipynb)
