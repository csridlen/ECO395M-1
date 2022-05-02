# Problem 1: Clustering and PCA

## Overview

The properties of 6500 different bottles of wine are included in the
`wine` dataset. Along with 11 chemical properties, we have an indicator
for whether the wine is red or white, and the quality of the wine, rated
on a scale from 1-10. The goal here is to use unsupervised learning
methods to categorize the information in the dataset. Additionally, we
want to determine if the analysis can distinguish higher quality wines
from lower quality ones.

## Clustering Analysis

First, I attempt to solve this problem through cluster analysis.
Specifically, I will be using the K-means algorithm. I normalize the
data with the `scale` function from the base R library. This function
centers the numeric columns of the dataset. To see if this algorithm
distinguishes reds from whites, I set the number of clusters to 2.

### K-means for wine color

![](DM_Homework_4_files/figure-markdown_strict/plot_colorkm-1.png)![](DM_Homework_4_files/figure-markdown_strict/plot_colorkm-2.png)

Here we see that the algorithm almost perfectly distinguishes reds from
whites. It only misses some whites that are similar to reds, so those
white wines must have more sugar or more acidity.

### K means for wine quality

![](DM_Homework_4_files/figure-markdown_strict/elbow_plot-1.png)

The crook of the elbow seems to occur at 4, or the marginal value of the
next k seems to peak at k = 4. This is something we can work with;
consider there to be 4 types of wine: high quality red wine, high
quality white wine, low quality red wine, and low quality white wine. I
create a variable `color_quality`, which is an indicator of whether the
wine is red or white and of high quality (≥ 5) or low quality (&lt; 5),
to distinguish these four types. The results are summarized in the two
plots below. See the table for reference as to what the colors mean in
the left plot.

![](DM_Homework_4_files/figure-markdown_strict/kmeans_quality_plots-1.png)

<table>
<thead>
<tr class="header">
<th>Category Name</th>
<th>Indicator</th>
<th>Corresponding Color</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>High quality red wine</td>
<td>1</td>
<td>Black</td>
</tr>
<tr class="even">
<td>Low quality red wine</td>
<td>2</td>
<td>Red</td>
</tr>
<tr class="odd">
<td>High quality white wine</td>
<td>3</td>
<td>Green</td>
</tr>
<tr class="even">
<td>Low quality white wine</td>
<td>4</td>
<td>Blue</td>
</tr>
</tbody>
</table>

It appears that K means is good at distinguishing high quality wine
wines and goes half and half with the quality of red wine. It’s possible
that wine snobs consider all red wine to be high quality when a lot of
it has characteristics of a low quality wine. Or, the wines that K-means
considers to be high or low quality (based on chemical properties) is
different than what wine snobs would consider to be high or low quality.

## Principal Components Analysis

<table>
<thead>
<tr class="header">
<th style="text-align: left;"></th>
<th style="text-align: right;">PC1</th>
<th style="text-align: right;">PC2</th>
<th style="text-align: right;">PC3</th>
<th style="text-align: right;">PC4</th>
<th style="text-align: right;">PC5</th>
<th style="text-align: right;">PC6</th>
<th style="text-align: right;">PC7</th>
<th style="text-align: right;">PC8</th>
<th style="text-align: right;">PC9</th>
<th style="text-align: right;">PC10</th>
<th style="text-align: right;">PC11</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;">Standard deviation</td>
<td style="text-align: right;">1.74</td>
<td style="text-align: right;">1.58</td>
<td style="text-align: right;">1.25</td>
<td style="text-align: right;">0.99</td>
<td style="text-align: right;">0.85</td>
<td style="text-align: right;">0.78</td>
<td style="text-align: right;">0.72</td>
<td style="text-align: right;">0.71</td>
<td style="text-align: right;">0.58</td>
<td style="text-align: right;">0.48</td>
<td style="text-align: right;">0.18</td>
</tr>
<tr class="even">
<td style="text-align: left;">Proportion of Variance</td>
<td style="text-align: right;">0.28</td>
<td style="text-align: right;">0.23</td>
<td style="text-align: right;">0.14</td>
<td style="text-align: right;">0.09</td>
<td style="text-align: right;">0.07</td>
<td style="text-align: right;">0.06</td>
<td style="text-align: right;">0.05</td>
<td style="text-align: right;">0.05</td>
<td style="text-align: right;">0.03</td>
<td style="text-align: right;">0.02</td>
<td style="text-align: right;">0.00</td>
</tr>
<tr class="odd">
<td style="text-align: left;">Cumulative Proportion</td>
<td style="text-align: right;">0.28</td>
<td style="text-align: right;">0.50</td>
<td style="text-align: right;">0.64</td>
<td style="text-align: right;">0.73</td>
<td style="text-align: right;">0.80</td>
<td style="text-align: right;">0.85</td>
<td style="text-align: right;">0.90</td>
<td style="text-align: right;">0.95</td>
<td style="text-align: right;">0.98</td>
<td style="text-align: right;">1.00</td>
<td style="text-align: right;">1.00</td>
</tr>
</tbody>
</table>

By summarizing the statistics of the principal components, we learn
that:

-   First 2 principal components explain about 50% of the cumulative
    variance in the dataset

-   First 4 principal components explain about 80% of the cumulative
    variance in the dataset

![](DM_Homework_4_files/figure-markdown_strict/qplot_wine_pca-1.png)

We see that PCA performs similarly for categorizing wine color.
Interpreting quality is a little more ambiguous. Additionally, PCA shows
that four principal components are the most explanatory of the variance
in the data. However, if we want to learn anything through
visualization, we would have to plot $\\binom{4}{2} = 6$ different plots
to learn exactly how those four different components separate the data.

## Conclusion

**Clustering works better here for distinguishing reds with whites.**
The process is much more simple and pretty efficient at characterizing
the wines. PCA is not as useful here because there is a lot of overlap
between the points. If the data could be organized into different
components more evenly, the results would be better for interpretation.

However, PCA suggests that the four clusters found in K-means are most
explanatory of the data. This might confirm the “four-types” hypothesis
I proposed from K-means.

# Problem 2: Market Segmentation

## Overview

In this problem, I want to use exploratory data analysis to optimize
marketing schemes for NutrientH2O’s twitter followers. There are about
7900 Twitter users that follow the account and their tweets were
observed for seven days. For each tweet observed, the general topic of
the tweet was placed into one of 36 categories, such as “current
events”, “travel”, “photo sharing.” I use K-means clustering to find
interesting results from tweet category counts.

## Organizing Followers by Tweets

In terms of what we will do with the data, we have to find a suitable
unsupervised method. Clustering makes the most sense here because we
don’t know much about the relationship between the categories.
Understanding the components would be really tough. Similarly, in
customer data a hierarchical model might not work as well for
interpretability; there are too many observations. So, I proceed with
K-means.

First, I normalize tweet counts as tweet *frequencies* to scale the
observations for cluster analysis. To find the optimal number of
clusters *k* I produce a scree plot, or a plot showing the improvement
in the within-sum-of-squares of the clusters as the number of clusters
increases. I use the “elbow test,” or I try to find the number of *k* in
the plot where there is a “crook” in the elbow.

![](DM_Homework_4_files/figure-markdown_strict/elbow_2-1.png)

The scree plot indicates we should use two clusters.

### K-means with 2 clusters

Since there are so many observations and overlap within accounts,
plotting the data was not very useful. However, I summarized the two
clusters into two bar graphs. The top 5 tweet categories are highlighted
in a pinkish color.

![](DM_Homework_4_files/figure-markdown_strict/kmeans_bar-1.png)

## Conclusion

It appears that we can categorize NutrientH20’s followers into two
categories by their tweets’ categorical frequencies. In cluster 1, the
top 5 tweet categories are photo sharing, personal fitness, outdoors,
health/nutrition, and cooking. These seem like the types of people that
the account can market to by promoting the health and fitness benefits
of the drink. Maybe they can post a picture of someone hiking with their
NutrientH20 drink!

In cluster 2, the top categories are travel, sports, politics, photo
sharing, and current events. These are also probably the top categories
for young men on Twitter in general. To market to this audience,
NutrientH20 should just try to stay relevant in Twitter culture. People
in cluster 2 would totally buy NutrientH20 just because one of their
funny tweets went viral.

# Problem 3: Market Basket Analysis

## Overview

In the `groceries` dataset, each row is a “basket” of grocery items
purchased. The goal here is to find the most interesting association
rules between items purchased. This is also known as market basket
analysis.

## Working with the data

First, I summarize the top 5 most purchased items in each basket in a
bar plot.

![](DM_Homework_4_files/figure-markdown_strict/item_freq-1.png)

To calculate the association rules, I used the `apriori` function in R,
choosing a support of 0.0009 and a confidence of 0.5. So I want rules
that happen about 0.09% of the time and that we are about 50% confident
will occur in a given transaction. I choose these parameters because I
want to isolate rules that are less common (low support) but have a high
confidence of occurring together (confidence). This just makes our
results more interesting.

In this table, I summarize the top 10 rules with the highest lifts.

<table style="width:100%;">
<colgroup>
<col style="width: 49%" />
<col style="width: 13%" />
<col style="width: 8%" />
<col style="width: 8%" />
<col style="width: 8%" />
<col style="width: 7%" />
<col style="width: 4%" />
</colgroup>
<thead>
<tr class="header">
<th style="text-align: left;">LHS</th>
<th style="text-align: left;">RHS</th>
<th style="text-align: right;">support</th>
<th style="text-align: right;">confidence</th>
<th style="text-align: right;">coverage</th>
<th style="text-align: right;">lift</th>
<th style="text-align: right;">count</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;">{curd,other vegetables,whipped/sour cream,whole milk,yogurt}</td>
<td style="text-align: left;">{cream cheese }</td>
<td style="text-align: right;">0.0009151</td>
<td style="text-align: right;">0.8181818</td>
<td style="text-align: right;">0.0011185</td>
<td style="text-align: right;">20.63287</td>
<td style="text-align: right;">9</td>
</tr>
<tr class="even">
<td style="text-align: left;">{Instant food products,soda}</td>
<td style="text-align: left;">{hamburger meat}</td>
<td style="text-align: right;">0.0012201</td>
<td style="text-align: right;">0.6315789</td>
<td style="text-align: right;">0.0019319</td>
<td style="text-align: right;">18.99565</td>
<td style="text-align: right;">12</td>
</tr>
<tr class="odd">
<td style="text-align: left;">{popcorn,soda}</td>
<td style="text-align: left;">{salty snack}</td>
<td style="text-align: right;">0.0012201</td>
<td style="text-align: right;">0.6315789</td>
<td style="text-align: right;">0.0019319</td>
<td style="text-align: right;">16.69779</td>
<td style="text-align: right;">12</td>
</tr>
<tr class="even">
<td style="text-align: left;">{baking powder,flour}</td>
<td style="text-align: left;">{sugar}</td>
<td style="text-align: right;">0.0010168</td>
<td style="text-align: right;">0.5555556</td>
<td style="text-align: right;">0.0018302</td>
<td style="text-align: right;">16.40807</td>
<td style="text-align: right;">10</td>
</tr>
<tr class="odd">
<td style="text-align: left;">{curd,flour,whole milk}</td>
<td style="text-align: left;">{sugar}</td>
<td style="text-align: right;">0.0009151</td>
<td style="text-align: right;">0.5294118</td>
<td style="text-align: right;">0.0017285</td>
<td style="text-align: right;">15.63593</td>
<td style="text-align: right;">9</td>
</tr>
<tr class="even">
<td style="text-align: left;">{ham,processed cheese}</td>
<td style="text-align: left;">{white bread}</td>
<td style="text-align: right;">0.0019319</td>
<td style="text-align: right;">0.6333333</td>
<td style="text-align: right;">0.0030503</td>
<td style="text-align: right;">15.04549</td>
<td style="text-align: right;">19</td>
</tr>
<tr class="odd">
<td style="text-align: left;">{Instant food products,whole milk}</td>
<td style="text-align: left;">{hamburger meat}</td>
<td style="text-align: right;">0.0015252</td>
<td style="text-align: right;">0.5000000</td>
<td style="text-align: right;">0.0030503</td>
<td style="text-align: right;">15.03823</td>
<td style="text-align: right;">15</td>
</tr>
<tr class="even">
<td style="text-align: left;">{curd,other vegetables,whipped/sour cream,yogurt}</td>
<td style="text-align: left;">{cream cheese }</td>
<td style="text-align: right;">0.0010168</td>
<td style="text-align: right;">0.5882353</td>
<td style="text-align: right;">0.0017285</td>
<td style="text-align: right;">14.83409</td>
<td style="text-align: right;">10</td>
</tr>
<tr class="odd">
<td style="text-align: left;">{chocolate,flour}</td>
<td style="text-align: left;">{sugar}</td>
<td style="text-align: right;">0.0009151</td>
<td style="text-align: right;">0.5000000</td>
<td style="text-align: right;">0.0018302</td>
<td style="text-align: right;">14.76727</td>
<td style="text-align: right;">9</td>
</tr>
<tr class="even">
<td style="text-align: left;">{hard cheese,tropical fruit,whipped/sour cream}</td>
<td style="text-align: left;">{butter}</td>
<td style="text-align: right;">0.0009151</td>
<td style="text-align: right;">0.8181818</td>
<td style="text-align: right;">0.0011185</td>
<td style="text-align: right;">14.76480</td>
<td style="text-align: right;">9</td>
</tr>
</tbody>
</table>

## Results

If we want people to purchase more vegetables, which grocery items
should they be placed by?

Below I have summarized in two graphs rules that include “other
vegetables” and “soda” on the right hand side. If we want people to
consume more vegetables, we can place these food items near the
vegetables. Similarly, if a soda company wants more people to buy its
product, it can place their sodas next to these products. It seems that
people mostly consumer sodas with other drinks. For calculating the
association rules for these two products, I let the support equal 0.001
and the confidence equal 0.5, using a similar logic as before.

![](DM_Homework_4_files/figure-markdown_strict/arules_graphs-1.png)![](DM_Homework_4_files/figure-markdown_strict/arules_graphs-2.png)

Overall, the results are pretty standard because we’re dealing with
grocery items. However, the `apriori` algorithm on this dataset could be
useful for suppliers of common grocery items.
