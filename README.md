# Capstone_Project_WallStreetBets_Sentiment_Analysis
 This is a sentiment analysis project of the WallStreetBets (WSB) subreddit as part of my Digital Futures coursework portfolio.

**Context:**

**WallStreetBets (WSB)** is a popular, and somewhat infamous, sub-reddit with a hobbyist community focused on the stock market.

In **2020**, events in this subreddit led to:

- One man gaining **$79,000,000 in a single day.**
- A **congressional investigation** by the US House Financial Committee.
- Adaptation into a **Netflix documentary** and blockbuster film releasing this year.

The **GameStop Short Squeeze** was an infamous financial event during which many retail traders *(those not affiliated with financial institutions)* made lifechanging returns on their investment to the GameStop or GME stock.

- Whilst hedge funds and traditional traders lost roughly $838 million in a single day.
- This was team effort, with WallStreetBets being a major player acting as a platform, organizing retail investors.
- Enabling a large influx of investment increasing volatility in the company’s publicly traded stock.

**Why did I choose WallStreetBets (WSB)?**

**The community** of members in WSB was likely integral to the success of the events that took place in 2020.

- One term: **“diamond hands”** provides insight into how the culture of this subreddit acted as an enabling factor for the GME short.
    - Many members of this sub-reddit take pride in not selling stocks they own despite market downturns.
    - They add diamond emojis to their posts – signifying they have diamond hands and are brave enough to wait for a big pay-off.
- Interestingly, this leads to a dilemma in sentiment analysis of this sub-reddit:
    - Often negative sentiment, like expressing annoyance that a stock isn’t performing well, doesn’t necessarily reflect poorly on the stock.
    - There are many posts with a seemingly bad sentiment towards a stock that are followed by rocket and diamond emojis: symbolizing a prediction towards a successful future for the stock: i.e. a positive sentiment.

So, the subreddit is directly relevant to the stock market as it represents a community of retail traders that were integral to a recent major financial event. Furthermore, modelling sentiment of this community presents bespoke challenges specifically in regards to generating useful sentiment measurements of stock related media.

An analysis of this community, therefore, may provide insight into effective and nuanced methodologies for measuring public perception of individual stock performance, whilst also developing a way of tracking the WSB subreddit, potentially foreseeing future events like the GameStop short.

**Previous works/the validity of monitoring social media sentiment for stock performance:**

- **Justina Deveikyte** and colleagues found social media sentiment was strongly negatively correlated with next day market volatility.
- Suwan Long and colleagues found across 30 minute intervals the net sentiment in the wallstreetbets subreddit significantly impacted the GME stock returns.

**Where does this project fit in?**

Whilst peer review research on this topic is novel, there is clearly potential for sentiment analyses of the WSB sub-reddit to aid stock price prediction.

- Similar projects to this one do exist, however, from personal research none reported a strong correlation between sentiment and stocks outside of a single trading bot.
- Furthermore, Suwan Long’s team incorporated a custom lexicon, bespoke to the WSB sub-reddit. Other similar projects often use more general sentiment analysis libraries, likely limiting them.
- This project was an attempt to combine the work of these academic papers and apply them to current data, leading to actionable insights of the stock market.

**Tools & Limitations:**

- **VADER**, Valence Aware Dictionary and Sentiment Reasoner is a **pre-trained natural language processing tool**. Optimised for social media text data and provides functionality to create a **custom lexicon** for enhanced sentiment analysis in bespoke use cases.
    - The custom lexicon was integral to this project due to the previously highlighted quirks (i.e. diamond hands) of how the WSB community communicates in posts.
    - Furthermore, this had been used by other successful stock market predictive projects involving twitter.
- **PRAW**, the Python Reddit API Wrapper was used to access posts and comments from the sub-reddit.
    - This has been used by others conducting similar analyses and provided easy to use classes and methods to enhance readability and reduce complexity when collecting data from a submission(a.k.a. post).
- **Custom Lexicon**
    - Through a series of personal experiments I came to the conclusion ChatGPT was effective at interpreting the sentiment of WSB sub-reddit posts. It could decode the slang used effectively and quickly generate a keyword list of specific communication patterns used throughout the sub-reddit.
        - So I chose to create a custom VADER lexicon with every slang term ChatGPT could produce for WSB.
        This yielded 99 unique terms and emoji combinations, each with a VADER sentiment score to be used by the model.

**Limitations:**

- **Reddit API restrictions/throttling**
    - It became clear the reddit API limited requests to the **most recent 1000 posts**, including comments.
    - The initial goal of data collection was to gather 60,000 text-based posts or comments for a two-week period. It appeared this would enable a robust training dataset for the sentiment analysis model and this was the same size of dataset used in other successful projects.
        - Soon into data collection I realised this was not feasible.
        - For a two-week period, the number of posts in the sub-reddit was around 1000, and even with 20 comments per post, I would only be able to collect a third of the observations.
    - I explored alternative options including using a **higher functionality reddit API called PushShift.IO**
        - This API has tools to combat throttling, contains a bank of historical reddit data, and data can be gathered per timeframe.
        - However, access to this API required moderator access and to achieve this was not feasible in the time frame of the project.
- **Labelling**
    
    As 1000 posts was not enough data to train and fit a robust model, I sourced a historical WSB dataset from Kaggle, containing **50,000 unlabelled observations**. Prior to building the model. The data required sentiment labels.
    
    - As this was a supervised learning task, in order to train the model and generate performance metrics the data needed to be labelled with accurate sentiment before being used in training.
        - There was not enough time allocated for the project to label 50,000 observations with the available man power.
        - I could not afford paid labelling services and their utility is debatable, especially in a quirky labelling problem like trying to understand what slang means in a niche corner of the internet.
        - Using a large language model (LLM) for labelling was explored, however, the metrics generated from an AI labelled dataset would be limited to the unquantified capability of the AI to understand the sentiment of each post.
            - Furthermore, if an AI was effective enough to label my training data, training a model would be redundant. The LLM would be able to completely replace the sentiment analysis model.
        - **Therefore, as a pre-trained model built to analyse social media I made the decision to omit the labelling and build the VADER model without fitting or performance metrics.**
- **Untested Lexicon**
    - The effectiveness of ChatGPT to understand the slang used in the WallStreetBets sub-reddit has not been verified in any method other than my own opinion.
    - Therefore, issues with ChatGPT’s understanding of the WallStreetBets slang terminology, or how it values the sentiment of each phrase are unchecked.
        - I have provided a text file of the custom lexicon, if you are to find any issues with it, or have ideas for improving it, please reach out :)
- **Unexhaustive List of Valid stock market tickers**
    - To generate an exhaustive list of publicly traded stocks is a large task and in the two week period of this project doing so was far out of scope.
    - I have provided the list of stock market tickers I used for verification in this model as a csv file titled: “**stock market tickers.csv**”.
    - With more time and resources, paid financial services would have been used to query the stock market further and generate a more exhaustive list.
        - I aim to improve this over time.
- **Over-generalised**
    - Stock sentiment is bespoke to the subreddit, however, sentiment of a post containing multiple stock tickers cannot be accurately stratified.
        - Therefore, complex posts referencing multiple stocks with varied sentiment to each will not be accurately captured by this model.
        - I aim to improve this over time.
    
    **The results**
    
    The final model is able to provide sentiment insights for the previous two weeks on the subreddit.
    
    - Sentiment score for a post has been weighted by the number of comments and upvotes that post received.
    - A visual check of the sentiment data before and after incorporating the custom lexicon revealed the model did a better job of accurately measuring the sentiment of posts in relation to stocks after introducing the lexicon.
    
    Sentiment data was grouped per stock, highlighting Nvidia, Ingersoll Rand, and Electronic Arts as the most mentioned in the last two weeks.
    
    - While NVIDIA stayed generally neutral, EA had a few days of positive sentiment between the 22nd and the 24th of June
    - And Ingersoll Rand received a lot of negative sentiment just after the 21st of June.
        - The day of their annual report of employee stock plans: https://investors.irco.com/financials/sec-filings/sec-filings-details/default.aspx?FilingId=17635091

      **Please note:** Results mentioned here are seen in the visualisation named: original_time_series_for_project
       - The visualisation generated and seen in the notebook was made after the notebook was updated for ease of access and improved readability
          - This occured in a different time horizon to the original project and therefore displays different results.
    
    Summary:
    
    Ultimately, the utility of this project at present is limited.
    
    - With insufficient labelled data for training, the model has not been fit or tested for accuracy.
    - Due to a lack of time, correlation between the sentiment measured and returns in the stock market was not explored.
    - Improvements made by the custom lexicon are anecdotal and unquantified.
    - Comment data could not be included due to reddit API throttling and sentiment was weighted solely by upvotes.
    - Likely omitting important measurements for calculating sentiment.
    
    With more time, a large amount of WSB labelled data would be used to train the model and test it with a number of metrics to assess robustness.
    
    - This would also enable improvements by the custom lexicon to be quantified.
    - Furthermore, provided sufficient correlations are found, the model could be used to make predictions on stock performance based on historical data.
    
    Overall, there is evidence that monitoring social media for financial forecasting is worthwhile, however, this model requires many improvements before it is of any use.
    
    **Sources:**
    
    1, Keith Gill Gain Value: https://investorplace.com/2024/06/how-much-did-keith-gill-make-from-gamestop-gme-stock-this-weeks-staggering-figures/#:~:text=This%20move%20comes%20as%20investors,gain%20of%20around%20%2479%20million.
    
    2, Keith Gill Gain Value 2: https://www.cnbc.com/2024/06/04/how-roaring-kittys-wealth-went-from-53000-to-nearly-300-million-and-could-one-day-top-1-billion.html
    
    3, Average stock volatility: https://www.fosterandmotley.com/insights/2019/02/20/what-is-volatility-and-is-it-normal
    
    4, Academic article found strong correlation between social media sentiment and volatility: https://www.frontiersin.org/journals/artificial-intelligence/articles/10.3389/frai.2022.836809/full
    
    5, Similar project outlines need for further research and limited causality, contradictory to 1: https://www.reddit.com/r/wallstreetbets/comments/wrlg86/i_did_sentiment_analysis_on_reddityes_that/
    
    6, Academic Paper Quantifying sentiment relationship with GME stock returns: https://eprints.soton.ac.uk/471991/1/Gamestop_Reddit_Sentiments_3_.pdf
    
    7,The trading bot: https://www.reddit.com/r/Python/comments/nmdy7n/used_python_to_build_a_rwallstreetbets_sentiment/
    
    - Uses VADER and introduces a custom lexicon
    
    8, Academic article found strong correlation between social media sentiment and volatility: https://www.frontiersin.org/journals/artificial-intelligence/articles/10.3389/frai.2022.836809/full
    
    9, Similar project outlines need for further research and limited causality, contradictory to 1: https://www.reddit.com/r/wallstreetbets/comments/wrlg86/i_did_sentiment_analysis_on_reddityes_that/
    
    10, Academic Paper Quantifying sentiment relationship with GME stock returns: https://eprints.soton.ac.uk/471991/1/Gamestop_Reddit_Sentiments_3_.pdf
    
    11, ChatGPT for labelling: https://www.linkedin.com/pulse/chatgpt-outperforms-humans-labelling-some-data-other-ais-sayeed/
