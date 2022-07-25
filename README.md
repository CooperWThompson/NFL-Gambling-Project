# NFL-Gambling-Project

![Intro](../NFL-Gambling-Project/Images/Screenshot%20from%202022-07-22%2013-32-41.png)

## Business Understanding

According to sports betting market tracker PlayUSA, roughly $12 billion will be spent gambling on pro football this NFL season. Just over 45 million fans are expected to place wagers, the majority of which will lose money. We want to help give local degenerates a leg up against the casinos by creating a model that will predict the winner of NFL games given information on odds, location, weather, and rank. Using this model, we hope to be able to not only predict outcomes, but also identify the key variable (gameday conditions) most impactful in producing said outcome.

## Data Understanding

![threeanimals](../NFL-Gambling-Project/Images/aarondonald.jpeg)

Our data came from Kaggle; the host scraped sites such as NFL.com, ESPN, and Pro Football Reference. Each row in the dataframe represents a Sunday matchup, tracing back to 1966. The columns provide informational context and detail on the game. The original dataframe included over 13,000 games, but after cleaning, we used much less. 

Our final model uses only the past 20 years of data; football as a sport has changed drastically over time, and different eras are hard to compare against eachother. The extended period of time caused an additonal issue on instances when the team had moved or changed their name. We had to align all the games based on franchise, not mascot, which took a lot of work. 

Then, we needed to establish a baseline of team's strength year to year to educate the model on importance/competitiveness of individual matchups, so we decided to webscrape a NFL power index to add to our data. We went to TeamRankings to find this, and were provided rankings each year since 2003. 

Finally, our target column was a boolean answer to 'did the favorite win,' so in order for our model to actually work, we had to convert all the information in terms of the favorite. 

## Methods

![tackletheproblem](../NFL-Gambling-Project/Images/derrick-henry-josh-norman.jpg)

First we established a model-less baseline. This baseline showed that if a bettor were to pick the favorite to win every single game, they would be correct 66% of the time. An accuracy score of 0.66 makes sense in this context but does show a class imbalance, so we decided we were ready to build our models, keeping that in mind. It is worth noting that when we conducted the train-test split, we reserved the most recent 50 games as the test data for our final model's predictions. 

With that said, our first model was a logistic regression, but it returned train scores identical and test scores worse than the baseline. We then built a Decision Tree model, which performed comparably to logistic regression, but is more useful due to its handling of class imbalance. We aslo tried a Naive Bayes pipeline, but it returned the worst overall scores, so we chose to model with Decision Trees.

We still needed to tune the Decision Tree to improve our model's score. We first created a model with Random Forest pipeline, then tried a Random Forest gridsearch, neither of which made any improvements. Due to a lack of time and data, we had to settle for this low-scoring model. Even though the model did not predict the winner very well on the data as a whole, we were able to find gambling value in the model when looking at it's predictions on a game by game basis. 

We calculated the median spread of the last 50 games, then simualted a bettor placing money on the favorite of each game versus placing money on who our model picked to win each matchup. Our model would occasionally pick underdogs to win correctly; these instances make more money for bettors than if they correctly placed money on the favorite to win.

## Results

![Results](../NFL-Gambling-Project/Images/Screenshot%20from%202022-07-25%2015-21-23.png)

This simulation showed that if a bettor placed $100 on each of the last 50 games using our model's predicted winner, they would make over $400, whereas if they picked the facorite each instance, they would lose over $100. Therefore our model does in fact make bettors money, but it takes a lot of initial capital with minimal return ($5000 to win $400). 

## Recommendations

![Touchdown](../NFL-Gambling-Project/Images/touchdown.webp)

Our model shows that it will make gamblers money, but we want our service to be of value to everyday local degenerates, most of whom do not have a lump sum of $5000 to risk. To do this, we want to improve our model by including additional data. If we had information on players (injuries, rank, significance, matchups) or coaches (rank, scheme, supporting staff) our scores might be better and more reliable. We also think it would be interesting to determine the impact of playoff, divisional, or end of season games which may be harder to predict. It also would be valuable to create a function that would be able to identify and use odds for specific games, not just the median average. Home field advantage is an additional important factor, so we also could calculate which teams have the most hostile atmosphere for visitors and provide a ranking to influence the model.

## References

### Presentation
https://www.canva.com/design/DAFG_Zv3PNQ/B18ds6RmVhU1jXSigwbcEA/edit?utm_content=DAFG_Zv3PNQ&utm_campaign=designshare&utm_medium=link2&utm_source=sharebutton
### Data
https://www.kaggle.com/datasets/tobycrabtree/nfl-scores-and-betting-data
https://www.teamrankings.com/nfl/ranking/overall-power-ranking-by-team?date=2022-07-25