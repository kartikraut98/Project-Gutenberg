# Project-Gutenberg

In this project we analyze the role of information revelation in the popularity of English-language fiction books.

We used KLD scores which measure the amount of “information revelation”, measured in terms of Kullback-Liebler divergence, for each subsequent section of the corresponding book. For details on how this measure was constructed, see https://ceur-ws.org/Vol-3558/paper6166.pdf

## Steps of Analysis:

1. Build book-level measures of the characteristics of the Kullback-Liebler divergence.
 
2. Relate these book-level measures of KLD to book popularity by regressing them against log(downloads) at the book level. Include as many controls as you believe are appropriate and that you can build from the information you have access to.
 
3. Investigate heterogeneity of effects across genres and use LASSO to infer which variables are most independently predictive of log(downloads).


## Dataset
### 1. metadata.csv
This file includes book-level attributes for each book, such as:

Book IDs: Unique identifiers for each book.
Download Counts: The number of times each book has been downloaded.
Other Attributes: Additional metadata related to the books.
### 2. KLDscores.csv
This file contains the Kullback-Liebler divergence scores, which measure the "narrative revelation" of each book. The scores are provided in the form of Python lists and are formatted as follows:

Book IDs: Corresponding identifiers for each book.
Narrative Revelation Scores: Lists of Kullback-Liebler divergence scores that quantify the information revelation for each subsequent section of the book.


## Findings
## Book-Level Analysis
### Narrative Revelation Trends:

The analysis of Kullback-Leibler Divergence (KLD) scores reveals a general trend where over 17,000 books show increasing narrative revelation towards the end. This trend suggests that authors tend to build up information and revelations progressively, enhancing reader engagement as the book progresses.
The slope of the KLD score trend, which measures the rate of narrative revelation, shows that a higher slope indicates more significant narrative development over time.
### Correlation with Downloads:

Slope: There is a negative correlation between the slope of the KLD scores and the logarithm of download counts. Books with steeper increases in narrative revelation tend to have fewer downloads, implying that readers may prefer a more steady flow of information rather than a dramatic buildup towards the end.<br>
Sentiment Volatility: There is a positive correlation between sentiment volatility and the logarithm of download counts. Books with higher fluctuations in sentiment are more likely to be downloaded, suggesting that emotionally dynamic narratives are more popular.<br>
## Analysis Across Genres
### Genre-Specific Insights:
Western Genre: Sentiment volatility is a primary predictor of download counts, indicating that variability in sentiment is crucial for this genre.<br>
Science Fiction Genre: Both the slope (rate of narrative revelation) and sentiment volatility are significant predictors of downloads, highlighting the importance of both the narrative trend and emotional variation in this genre.<br>
## Lasso Regularization Findings
### Feature Impact:

Sentiment_avg: Shows a strong negative impact on download counts.<br>
Sentiment_volatility: Exhibits a moderate positive impact on downloads.<br>
Slope: Has a moderate negative impact on the target variable.<br>
Wordcount: Displays a small positive impact.<br>
Revelation Score: Shows a slight negative impact.<br>
### Key Influential Features:

Sentiment_avg and Sentiment_volatility are the most influential features.<br>
Slope also has a significant impact compared to other features.
## Regression Analysis
### Variable Usage:

Variables like Sentiment_avg, Sentiment_volatility, wordcount, and Speed are used directly from the dataset without additional calculations or transformations.
Slope is derived from a linear regression on KLD scores to evaluate narrative consistency over time.
The Book Level Score or Revelation Score is calculated by assigning weights to the mean, median, standard deviation, and slope of KLD scores.
### Data Normalization:

Wordcount is scaled to normalize its influence, ensuring it does not disproportionately affect the model due to its larger magnitude.
Genre-Specific Models:

Separate regression models for each genre are developed to identify genre-specific predictors. However, the data cleaning process resulted in the removal of a significant portion of the data, which may affect the accuracy and reliability of the regression results.
