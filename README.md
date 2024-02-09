# Forecasting Superbowl LVIII: A Machine Learning Approach with Random Forest

<div align="justify">
The Super Bowl is a matter of days by now and despite not following the NFL throughout the year, I am genuinely looking forward to it. My interest in American football was piqued when I watched a few college football games and realized how complex and strategic this sport is. Before that, I was adamant that no sport could top soccer in terms of complexity and tactics, but I always stand to be corrected. In the words of my ancestor Socrates, "A wise man knows that he knows nothing" and as of now, I truly know nothing about football. However, being an avid sports fan and an aspiring analyst, I was given the chance to combine my passion for sports and data analysis and try the impossible; predict the Super Bowl! I used a simple Random Forest machine learning model to predict the winning team and the score before the champions are crowned on the field.
</div>
 
# Introduction

<div align="justify">
Being a graduate student in Business Analytics at UCI has its perks; we were gifted an unrealistically clean dataset containing 4 sheets of data for the 2023-2024 season. The first one contained detailed game-by-game statistics for the regular season, the second one was similar to the first sheet but included playoff game stats and a lot of variables that weren't included in the first one, the third one provided a ranking or classification of teams based on performance, strength, or expert analysis and the fourth one contained calculated metrics that compared team performances against averages.
  
<br/>
<br/>

In the introductory section, the groundwork for the model is laid. The aim was to harness the power of NFL game data, applying machine learning techniques to predict game outcomes. Except for predictions, this analysis aims to discover key performance indicators (KPIs) that define winning strategies in football. This project is not just about forecasting wins, but understanding the dynamics that drive success on the field. Here is what our dataset looked like before preprocessing:</div>
<br/>

<p align="center" width="100%">
    <img width="33%" src="https://github.com/dmousouroulis/Forecasting-Super-Bowl-LVIII/assets/156945591/351d58fc-019d-4f12-94b3-b4dd535aeb22">
</p>

# Data Preprocessing

<div align="justify">
Our quest begins with data, the bedrock of all predictions, and we already have a lot to work with. We started by loading our dataset from our main Excel sheets, each representing a unique aspect of the game data. Initial observations helped us gauge the dataset's structure, guiding our minor preprocessing efforts. Handling missing values and ensuring we are working with a homogenous dataset is a lengthy process for the inexperienced eye (i.e. mine). Similarly, converting categorical data into a machine-readable format sets the stage for our much-awaited model. This preparation stage ensures our dataset is ready for in-depth analysis.
  
<br/>
<br/>

Having merged our datasets by concatenating on identical columns, we ended up with a beautiful dataset containing 1,114 rows and 14 columns of rich, insightful data. For our analysis and subsequently our model, we polished our dataset in the following ways: we added a simple flag indicating playoff games, we dropped the final two rows as they referred to the upcoming Super Bowl, we added a column indicating the score difference, we added a binary classification for the winning team, and we added another column indicating the total points for both teams. Hint; one of them is our target variable.
</div>
<br/>

<p align="center" width="100%">
    <img width="33%" src="https://github.com/dmousouroulis/Forecasting-Super-Bowl-LVIII/assets/156945591/db9af04e-801b-4c64-ad73-c3618c1b5d63">
</p>

# Exploratory Data Analysis

<div align="justify">
Exploratory Data Analysis (EDA) is our opportunity to dive deep into the dataset and discover underlying patterns. Through visualizations like bar charts and scatter plots, we assessed the distribution and relationships of key variables in our dataset. Additionally, a couple of correlation matrices further highlight the interplay between different game metrics. This exploratory phase is important for conceptualizing our model, guiding our analysis toward meaningful insights, and ensuring that our modeling efforts are grounded in a strong understanding of the data.

<br/>
<br/>

Although scatter plots paint the picture quite well, the following regression plots were chosen in the end due to their effectiveness in showing linear relationships between variables. An upward slope shows just that, and for someone like me who is relatively unfamiliar with key NFL statistics, it is not surprising that more passes or rushing yards lead to higher scores and that the amount of turnovers appear to correlate with passes, whether the team is winning or losing.
</div>
<br/>

<p align="center" width="100%">
    <img width="33%" src="https://github.com/dmousouroulis/Forecasting-Super-Bowl-LVIII/assets/156945591/3d86eb36-e94d-4e36-9acc-bd76bdd70d76">
</p>

<div align="justify">
The following graphs contain a histogram of the distribution of 'Total_Points' and the score distribution for winning and losing teams respectively. The former displays the highest, lowest, and mean points, with those values being 3.0, 43.67, and 90.00 points respectively - scores you will most likely never see in professional soccer (let's not forget the thrashing that the legendary Brazilian team suffered against Germany in the 2014 FIFA World Cup with an unforgettable 1-7 scoreline). Therefore, we assume the benchmark of ~44 points per game in the current season. The latter, displays the score distribution for winning and losing teams respectively, with the mean score for winning teams being ~27 points and the mean score for losing teams being ~16 points.
</div>
<br/>

<p align="center" width="100%">
    <img width="33%" src="https://github.com/dmousouroulis/Forecasting-Super-Bowl-LVIII/assets/156945591/4c6f572f-1092-462a-b1d5-cd8f8f1ea8d2">
</p>

<div align="justify">
A simple yet effective correlation heatmap, visualizes the Pearson correlation coefficients calculated from our dataframe, focusing on columns 5 through 15. Interpreting the output of this heatmap reveals key insights: both Team 1 and Team 2 show a positive correlation (0.516723) between passing yards and scores, indicating that effective passing strategies boost scoring chances. Similarly, both Team and Team 2 show a correlation (between 27 and 30 respectively) between rushing yards and scores. Conversely, Team 1 and Team 2’s turnovers show a moderate negative correlation (-0.316225) with their scoring, suggesting that minimizing turnovers is crucial.
</div>
<br/>

<p align="center" width="100%">
    <img width="33%" src="https://github.com/dmousouroulis/Forecasting-Super-Bowl-LVIII/assets/156945591/be57f0e2-621d-4b18-8f6c-233a2d16d3f7">
</p>

# Super Bowl LVIII Teams Analysis

<div align="justify">
As the focal point of our analysis, this section assessed the teams contending in Super Bowl LVIII. By comparing their performance across various metrics, we aimed to shed light on their strengths and weaknesses. This targeted analysis not only informed our predictions but also enriched our understanding of what it takes to compete at the highest level of American football. This comparison is key to making informed predictions about the Super Bowl outcome.

<br/>
<br/>

The following bar chart, both in graphical and tabular display, shows how both teams performed on average throughout the year. This visualization offers an insightful summary into the mean values of our key metrics, further annotating the distinct strategic profiles of the San Francisco 49ers and the Kansas City Chiefs. The comparative strengths in scoring, passing, rushing, and turnovers is clear, which also emphasizes the tactical nuances each team brings to the field. Our analysis highlights the importance of balancing aggressive play with strategic discipline, as evidenced by the pivotal role of turnovers. So far, we have gained valuable insights into what might tip the scales in this highly anticipated final, demonstrating the impact of data-driven analysis in understanding the complexities of football strategies.
</div>
<br/>

<p align="center" width="100%">
    <img width="33%" src="https://github.com/dmousouroulis/Forecasting-Super-Bowl-LVIII/assets/156945591/59164739-5066-4f99-93da-fc5049b12afa">
</p>

<p align="center" width="100%">
    <img width="33%" src="https://github.com/dmousouroulis/Forecasting-Super-Bowl-LVIII/assets/156945591/b8229736-e365-4806-86bb-0d833724f825">
</p>

# Model Setup

<div align="justify">
Model preparation involves the final tweaks and adjustments to our dataset before the modeling begins. Encoding categorical variables and ensuring the data is in the correct format for analysis proved to be important steps. This preparation is the bridge between raw data and the machine learning algorithms that will follow; it's about setting the stage for our models to learn from the data as effectively as possible. Having processed the data, analyzed it carefully, and visualized it as effectively as possible, in combination with the analysis of our finalists, we are confident with our feature selection process. This is where we identified the variables most likely to influence our predictions. By focusing on team statistics such as passing yards, rushing yards, and turnovers, we aimed to construct a model that captures the essence of game-winning strategies.
</div>
<br/>

<p align="center" width="100%">
    <img width="33%" src="https://github.com/dmousouroulis/Forecasting-Super-Bowl-LVIII/assets/156945591/28c4b023-61c4-4f87-a0eb-94ce87463bb5">
</p>

# Random Forest Classifier for Winning Team Prediction

<div align="justify">
In this section, we introduced the Random Forest Classifier, a powerful machine learning algorithm known for its versatility and accuracy. The classifier was trained to predict game outcomes based on the features we selected. This setup included splitting the data into training and testing sets, fitting the model, and evaluating its performance. Games from weeks 1 to 9 were used for training, while games from week 10 onwards were used for testing. This temporal split simulates predicting future games based on past data.
</div>
<br/>

## RFC Performance

<p align="center" width="100%">
    <img width="33%" src="https://github.com/dmousouroulis/Forecasting-Super-Bowl-LVIII/assets/156945591/7e006d69-e397-4331-b332-6d62fa5ce97a">
</p>

<div align="justify">
In evaluating our Random Forest Classifier model, the three key metrics of accuracy, confusion matrix and precision score painted a comprehensive picture of its performance. The model can make predictions with an accuracy rate of 77.99%, showing its ability to correctly predict outcomes across a wide array of games. This is further dissected by the confusion matrix, where our model can correctly predict the losing team in 226 out of 293 games (TN) and can also correctly predict the winning team in 217 out of 275 games (TP). This leads us to our model's precision score of 78.91%, which exceeds its overall accuracy; the higher precision indicates our model's ability in minimizing false positives and thus making it effective at identifying winning teams.
</div>
<br/>

## Winning Team Prediction

<div align="justify">
As we near the moment of prediction, it's important to fine-tune the predictive model with the most influential variables: ‘Team1_Passing’, ‘Team1_Rushing’, and ‘Team1_Turnovers’. These metrics are gathered from a comprehensive analysis of the two finalists' performance data as analyzed previously. In our Random Forest Classifier, the San Francisco 49ers were designated as the first team. Consequently, the RFC delivered its verdict: a prediction of (1) implies victory for the 49ers, while a (0) represents a loss. This binary classification formed the predictive power of our model in determining the likely winner of the Super Bowl.
</div>
<br/>

<p align="center" width="100%">
    <img width="33%" src="https://github.com/dmousouroulis/Forecasting-Super-Bowl-LVIII/assets/156945591/59a9cc70-59d6-4eb8-b53c-f3ef7e7a05e3">
</p>

<p align="center" width="100%">
    <img width="33%" src="https://github.com/dmousouroulis/Forecasting-Super-Bowl-LVIII/assets/156945591/0e60cfb2-968e-46aa-8dc4-884ba4031d53">
</p>

<div align="justify">
The Random Forest Classifier simplified our prediction to a single outcome: it forecasted the San Francisco 49ers as the winners of Super Bowl LVIII, assigning a (1) based on our team performance analysis. However, to understand the certainty of this prediction, we dug deeper using the ‘predict_proba’ method, which yielded probabilities for each class. It returned an array [0.29, 0.71], indicating a 29% probability of a loss (class 0) and a 71% probability of a win (class 1) for the 49ers. These probabilities are visually represented in the above bar chart, providing a clear probabilistic forecast alongside the binary prediction.
</div>

# Random Forest Regressor for Score Prediction

<div align="justify">
Transitioning from classification to regression, we employed the Random Forest Regressor to predict specific game scores. This approach allowed us to quantify the expected performance of teams in numerical terms, providing a more granular perspective on game outcomes. By training the regressor on our preprocessed dataset, we aimed to capture the subtleties that influence scoring in NFL games. This prediction model serves as a tribute to the predictive power of machine learning in sports analytics.
</div>
<br/>

## RFR Performance
                  
<p align="center" width="100%">
    <img width="33%" src="https://github.com/dmousouroulis/Forecasting-Super-Bowl-LVIII/assets/156945591/660dba50-d58f-41fa-88eb-a41d1f31ab2c">
</p>

<div align="justify">
When assessing the effectiveness of our Random Forest Regressor, we relied on accuracy and the distribution of errors (residuals) to gauge its predictive capabilities This model demonstrated an accuracy of 66.66%, signifying its ability to forecast scores with reasonable precision. The distribution of residuals, primarily clustered around the zero mark as depicted by the histogram, implied that the model's predictions were generally aligned with the true scores. Such a distribution pattern suggests a model that is adept and unbiased in its estimations, and capable of reliable performance across various game scenarios.
</div>
<br/>

## Score Predictions

<div align="justify">
Reaching the final piece of the puzzle, our score predictions, we were once again basing them on the most influential variables: ‘Team1_Passing’, ‘Team1_Rushing’, and ‘Team1_Turnovers’. We therefore used these variables once more and tasked our Random Forest Regressor to make an educated prediction of the Super Bowl LVIII score.
</div>
<br/>

<p align="center" width="100%">
    <img width="33%" src="https://github.com/dmousouroulis/Forecasting-Super-Bowl-LVIII/assets/156945591/59a9cc70-59d6-4eb8-b53c-f3ef7e7a05e3">
</p>

<p align="center" width="100%">
    <img width="33%" src="https://github.com/dmousouroulis/Forecasting-Super-Bowl-LVIII/assets/156945591/d3b69941-c8e3-44a1-800a-5228c92492b9">
</p>
<br/>

<div align="justify">
Following the Random Forest Classifier’s prediction, which suggested the San Francisco 49ers as the potential Super Bowl LVIII champions, we have further utilized the power of the Random Forest Regressor to predict the game's score. The RFR model, trained by the same insightful team statistics, projected a scoreline of San Francisco 49ers scoring 29 points against Kansas City Chiefs scoring 20 points. While our classifier model indicated a 71% probability of a 49ers' victory, the regressor model offers a numerical edge, quantifying the anticipated lead with an accuracy rate of 66.6%. These combined insights from our two-fold predictive approach, delivered a reasonable forecast for the upcoming Super Bowl, where statistics seem to suggest a victory for the 49ers.
</div>
<br/>

<p align="center" width="100%">
    <img width="33%" src="https://github.com/dmousouroulis/Forecasting-Super-Bowl-LVIII/assets/156945591/4371725d-dc47-4318-ba25-3ffb9ff02df1">
</p>
<br/>

# Conclusion

<div align="justify">
Through strategic manipulation of our dataframe and careful application of both RFC for win/loss predictions and RFR for score predictions, we have created a satisfactory prediction model as far as performance goes. This dual-model approach not only predicts the likely winner of Super Bowl LVIII but it also estimates the scoreline, enriching our predictive insights with a depth that accounts for the multifaceted nature of football game outcomes. It’s not hard to notice that the model is pointing to a relatively possible outcome, however the results could be very different if we were to introduce additional variables like injuries, and strength of schedule, which could be the foundation for a future direction. Excited to see what the outcome will be!
</div>
