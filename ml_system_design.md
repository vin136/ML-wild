Goal:  our goal is generally to improve our metrics (engagement rate, etc.) while ensuring that we meet the capacity and performance requirements.

How to proceed ?

STEP 1: Broad Question

- Build a system that shows relevant ads for search engines.
- Extract all persons, locations, and organizations from a given corpus of documents.
- Recommend movies to a user on Netflix.

STEP 2: Get Specific

**Clarify**
For instance, you may be asked to design a search engine that displays the most relevant results in response to user queries. You could narrow down the problem’s scope by asking the following questions:

Is it a general search engine like Google or Bing or a specialized search engine like Amazon’s products search?

What kind of queries is it expected to answer?

This will allow you to precisely define your ML problem statement as follows:


Build a generic search engine that returns relevant results for queries like “Richard Nixon”, “Programming languages” etc.

**Understanding scale and latency requirements**
Latency requirements

If you were given the search engine problem, you would ask:

Do we want to return the search result in 100 milliseconds or 500 milliseconds?
Similarly, if you were given the Twitter feed problem, you would ask:

Do we want to return the list of relevant tweets in 300 milliseconds or 400 milliseconds?
Scale of the data

Again, for the search engine problem, you would ask:

How many requests per second do we anticipate to handle?

How many websites exist that we want to enable through this search engine?

If a query has 10 billion matching documents, how many of these would be ranked by our model?

And, for the Twitter feed problem, you would ask:

How many tweets would we have to rank according to relevance for a user at a time?

**Defining metrics#**

Metrics for offline testing

You will use offline metrics to quickly test the models’ performance during the development phase. You may have generic metrics; for example, if you are performing binary classification, you will use AUC, log loss, precision, recall, and F1-score. In other cases, you might have to come up with specific metrics for a certain problem. For instance, for the search ranking problem, you would use NDCG as a metric.

Metrics for online testing

Once you have selected the best performing models offline, you will use online metrics to test them in the production environment. The decision to deploy the newly created model depends on its performance in an online test.

While coming up with online metrics, you may need both component-wise and end-to-end metrics. Consider that you are making a search ranking model to display relevant results for search queries. You may use a component-wise metric such as NDCG to measure the performance of your model online. However, you also need to look at how the system (search engine) is performing with your new model plugged in, for which you can use end-to-end metrics. A commonly used end-to-end metric for this scenario is the users’ engagement and retention rate.

In another scenario, you may be asked to develop the ML system for a task that may be used as a component in other tasks. Again, you need both component level metrics and end-to-end metrics during online testing. For instance, you could be asked to design the ML system for entity linking which is going to be used to improve search relevance

**Architecture design**

Varies.

# 1 . Practical ML TECHNIQUES/CONCEPTS

## Performance and capacity consideration.

Major performance and capacity discussions come in during the following two phases of building a machine learning system:

Training time: How much training data and capacity is needed to build our predictor?

Evaluation time: What are the Service level agreement(SLA) that we have to meet while serving the model and capacity needs?



Machine learning algorithms have three different types of complexities:

Training complexity

The training complexity of a machine learning algorithm is the time taken by it to train the model for a given task.

Evaluation complexity

The evaluation complexity of a machine learning algorithm is the time taken by it to evaluate the input at testing time.

Sample complexity

The sample complexity of a machine learning algorithm is the total number of training samples required to learn a target function successfully.


Performance based SLA ensures that we return the results back within a given time frame (e.g. 500ms) for 99% of queries. Capacity refers to the load that our system can handle, e.g., the system can support 1000 QPS (queries per second).

## Layered/funnel based modeling approach#

To manage both the performance and capacity of a system, one reasonable approach that’s commonly used is to start with a relatively fast model when you have the most number of documents e.g. 100 million documents in case of the query “computer science” for search. In every later stage, we continue to increase the complexity (i.e. more optimized model in prediction) and execution time but now the model needs to run on a reduce number of documents e.g. our first stage could use a linear model and final stage can use a deep neural network. If we apply deep neural network for only top 500 documents, with 1ms evaluation time per document, we would need 500ms on a single machine. With five shards we can do it in around 100ms

`In ML systems like search ranking, recommendation, and ad prediction, the layered/funnel approach to modeling is the right way to solve for scale and relevance while keeping performance high and capacity in check.`

## Training data collection strategies.

**User’s interaction with pre-existing system (online)#**

For many cases, the early version built for solving relevance or ranking problem is a rule-based system. With the rule-based system in place, you build an ML system for the task (which is then iteratively improved). So when you build the ML system, you can utilize the user’s interaction with the in-place/pre-existing system to generate training data for model training. Let’s get a better idea with an example: building a movie recommender system.

Assume that you are asked to recommend movies to a Netflix user. You will be training a model that will predict which movies are more likely to be enjoyed/viewed by the user. You need to collect positive examples (cases where user liked a particular movie) as well as negative examples (cases where the user didn’t like a particular movie) to feed into your model.

Here, the consumer of the system (the Netflix user) can generate training data through their interactions with the current system that is being used for recommending movies.
If a user likes/watches a movie recommendation, it will count as a positive training example, but if a user dislikes/ignores a movie recommendation, it will be seen as a negative training example.

**Human labelers (offline)**

1.Crowdsourcing

2.Specialized labelers

3.Open-source datasets

Targeted data gathering

Offline training data collection is expensive. So, you need to identify what kind of training data is more important and then target its collection more. To do this, you should see where the system is failing, i.e., areas where the system is unable to predict accurately. Your focus should be to collect training data for these areas.
Continuing with the autonomous vehicle example, you would see where your segmentation system is failing and collect data for those scenarios. For instance, you may find that it performs poorly for night time images and where multiple pedestrians are present. Therefore, you will focus more on gathering and labeling night time images and those with multiple pedestrians.

**Additional creative techniques**

Build the product in a way that it collects data from user

Let’s consider an example where people go to explore their interests on Pinterest. You want to show a personalized selection of pins to the new users to kickstart their experience. This requires data that would give you a semantic understanding of the user and the pin. This can be done by tweaking the system in the following way:

Ask users to name the board (collection) to which they save each pin. The name of the board will help to categorize the pins according to their content.
Ask new users to choose their interests in terms of the board names specified by existing users.

<img width="970" alt="Screen Shot 2022-05-29 at 4 17 38 PM" src="https://user-images.githubusercontent.com/21222766/170889782-b3782aed-ef94-4352-a87e-6fd4d2a10290.png">



Creative manual expansion

We can expand training data using creative ways. Assume that we are building a system that detects logos in images (object detection) and we have some images containing the logos we want to detect. We can expand/enhance the training data by manually placing those logos on a different set of images as well. This logo placement can be done in different positions and sizes. The enhanced training data will enable us to build a more robust logo detector model, which will be able to identify logos of all sizes at different positions and from various kinds of images.

**Splitting**
While splitting training data, you need to ensure that you are capturing all kinds of patterns in each split. For example, if you are building a movie recommendation system like Netflix, your training data would consist of users’ interactions with the movies on the platform.
After analysing the data, you may conclude that, generally, the user’s interaction patterns differ throughout the week. Different genres and movie lengths are preferred on different days. Hence, you will use the interaction with recommendations throughout a week to capture all patterns in each split.

**Quantify the effect of traning data**

<img width="640" alt="Screen Shot 2022-05-29 at 4 25 09 PM" src="https://user-images.githubusercontent.com/21222766/170890128-669ced17-73af-460d-b93c-a8469a45109b.png">

**Training data filtering#**

Cleaning up data

General guidelines are available for data cleaning such as handling missing data, outliers, duplicates and dropping out irrelevant features.

**Removing bias**

The pre-existing recommender is showing recommendations based on popularity. As such, the popular movies always appear first and new movies, although they are good, always appear later on as they have less user engagement. Ideally, the user should go over the whole recommendation list so that he/she can discover the good, new movies as well. This would allow us to classify them as positive training examples so that the model can learn to put them on top, once re-trained. However, due to the user’s time constraints, he/she would only interact with the topmost recommendations resulting in the generation of biased training data. The model hence trained, will continue considering the previous top recommendation to be the top recommendation this time too. Hence, the “rich getting richer” cycle will continue.

Therefore, we show “randomized” recommendations instead of “popular first” for a small portion of traffic for gathering training data. The users’ engagement with the randomized recommendations provides us with unbiased training data. This data really helps in removing the current positional and engagement bias of the system.

**Bootstrapping new items**

 For example, in the movie recommendation system, new movies face the cold start problem. We can boost new movies by recommending them based on their similarity with the user’s already watched movies, instead of waiting for the new movies to catch the attention of a user by themselves. Similarly, we may be building a system to display ads, and the new ads face the cold start problem. We can boost them by increasing their relevance scores a little, thereby artificially increasing their chance of being viewed by a person
 
## Online Experimentation




