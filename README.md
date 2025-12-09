# GroupProject2025
Data Mining Group Project - INFO 3233

Dataset:https://www.kaggle.com/datasets/vrindakallu/new-york-dataset 

Video presentation: https://drive.google.com/file/d/10Ep81559Hlm7zXM60uBb5WZvd_UWAE3v/view?usp=drive_link 

Project Poster: https://www.canva.com/design/DAG51Qi3g34/m_dAl-6TTANWLCMgyWGtmg/view?utm_content=DAG51Qi3g34&utm_campaign=designshare&utm_medium=link2&utm_source=uniquelinks&utlId=hb1d57bf4b1 

<img width="847" height="633" alt="image" src="https://github.com/user-attachments/assets/2cac0567-5af2-44e3-9794-2a35824d8d6b" />


# Introduction

Short-term rentals in New York City vary widely, and hosts and renters often struggle to understand why some listings are priced the way they are. In this project, we investigate patterns in NYC rental listings to answer two main questions: (1) How do listing characteristics—such as bedrooms, beds, baths, and review activity—naturally group together? and (2) Can a simple linear model predict price from these features? Our overall goal is to identify meaningful rental segments and test whether basic listing attributes are strong predictors of price.

# About the Data

We used the 2024 New York City Airbnb-style listings dataset from Kaggle. The dataset provides information about rental features, host activity, and general listing characteristics. For our analysis, we focused on:

Numeric features: price, bedrooms, beds, baths, number_of_reviews, reviews_per_month

Categorical features: room type, borough (neighbourhood_group)

Before analysis, we cleaned the dataset by converting “Studio” to 1 bedroom, turning baths into numeric values, and removing rows with missing values so that all entries had complete information. Dummy variables were created for room type and borough to support modeling.

To better understand patterns in the data, we produced several visual summaries, including a correlation heatmap to show how numeric features relate to each other and scatterplots of price vs. bedrooms, colored by clusters. These early visuals helped us see that price had only modest correlations with the basic size features and almost no correlation with review activity.

# Methods
Preprocessing

We prepared the dataset through the following steps:

Converted non-numeric entries (e.g., baths, “Studio”) into usable numeric forms.

Removed incomplete rows to avoid bias from missing data.

Encoded room type and borough into dummy variables for modeling.

Standardized numeric features (price, bedrooms, beds, baths, reviews, reviews_per_month) for clustering using StandardScaler.

Clustering

We used K-Means clustering to group listings based on their size, price, and review activity. We tested values of k from 2 to 9, guided by both the elbow plot (inertia) and silhouette scores. Silhouette scores were:

k=2 → 0.518

k=3 → 0.515

k=4 → 0.476

k=5 → 0.414

k=6 → 0.437

k=7 → 0.441

k=8 → 0.405

k=9 → 0.409

While k=2 had the highest score, k=4 provided a clearer and more interpretable segmentation for describing rental market patterns on a poster. This choice balanced performance and storytelling.

Linear Regression Model

To test whether basic listing features can predict price, we trained a baseline linear regression model using an 80/20 train-test split. The model used bedrooms, beds, baths, reviews, reviews_per_month, and dummy variables as predictors. We then evaluated how well the model predicted prices based on listing features. Overall, our workflow involved data cleaning, feature engineering, clustering, and regression.

# Evaluation
Clustering Performance

Silhouette scores suggest that clusters up to k=4 show meaningful structure, and our scatterplots confirmed that k=4 produced understandable grouping patterns. The four clusters reflect distinct rental categories, such as small low-priced rooms, mid-range units, and higher-priced larger apartments.

Regression Performance

The linear regression model performed poorly overall:

R² = 0.0908

RMSE ≈ 325.73

Our analysis revealed clear patterns in Airbnb listing characteristics across New York City. The regression model provided further insight by quantifying how strongly these features influence price, although the model achieved a relatively low R² value of approximately 0.09, indicating that only about 9% of price variation is explained by the included variables. The RMSE of around 300 suggests substantial variability in listing prices that cannot be fully captured by the available features, likely due to unmeasured factors such as amenities, building quality, or neighborhood desirability. Visualizations such as the actual vs. predicted plot and residual plot showed that the model systematically underestimates and overestimates prices for certain listings, reinforcing the high variability in Airbnb pricing. Overall, the results highlight meaningful relationships between listing attributes and price, while also demonstrating the limitations of predicting Airbnb prices using only structural and review-based features.

# Storytelling & Conclusion
Key Insights

Clustering revealed meaningful rental segments.
Our clusters separated listings into groups based on price and size, helping us describe different “types” of rentals in NYC. This is useful for market segmentation and can guide both hosts and renters.

Price is not well explained by basic features.
The weak R² score shows that price depends on more than bedrooms, beds, baths, and review activity. Other factors—such as micro-location, building quality, seasonal demand, or host strategy—likely play much bigger roles.

Limitations

We removed rows with missing values, which may introduce bias.

The linear model assumes straight-line relationships that cannot capture nonlinear pricing patterns.

Price outliers (extremely high listings) likely increased error levels.

Future Work

To improve future analysis, we would:

Include more detailed location features (latitude/longitude or neighborhood clustering).

Try non-linear models such as Random Forests or Gradient Boosting.

Log-transform price or trim outliers to reduce skew.

Add time-based features like last review date or seasonal availability.

What We Learned

This project helped us practice end-to-end data science: cleaning messy data, preparing categorical variables, scaling for clustering, choosing k using proper metrics, and evaluating model fit. We learned that clustering can reveal useful descriptive insights, while prediction requires deeper feature engineering and more flexible models.

# Impact Section

Data projects involving housing always come with social and ethical implications. While understanding rental patterns can help hosts set fair prices and help renters compare listings, the same insights can influence markets in unintended ways. For example, more efficient pricing algorithms could lead to rising rental prices or worsen housing scarcity in certain neighborhoods. Additionally, data-driven decision-making that ignores community needs or local regulations could amplify existing inequalities.

Because of this, analytical tools like ours should be used carefully. Stakeholders should consider neighborhood impacts, community feedback, and regulatory guidelines before applying segmentation or pricing models to real markets. Our project highlights the importance of using data responsibly, especially in housing-related markets. Understanding the potential social and ethical impacts is just as important as the technical findings.
