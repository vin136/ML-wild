# Case-Studies:Recommender Systems

## Design Search ranking of Air-bnb experiences

**What**
Airbnb is a two-sided market place. Hosts design `experiences` and travellers choose between them during their travel to explore the place.

**Step-1**:
Start with rule based almost random ranking of experiences.This will give us some data.

All users are shown same rankings
`experience` = list of features (cost,duration, timing, Avg.user-rating etc)
`users` = logged in users and unlogged users
`output` = which ones are booked.

- Build a classification model using `experience features` to predict whether it will be booked or not.
- Eg model -> Gradient Boosted Trees (powerful enough but with great interpretability)
- Do offline testing,feat-importance. 
- Do A/B testing. If,All satisfied and sensible -> **Step-2**
Here any user search queries will only act as filters.


Implementation Concerns/details:
- Training/inference can be done offline. Periodically update. Simple DataFlow tool like `AirFlow` will do the job.
How to deal with new listings as it might not have some features like `avg.user` rating yet ?

Potential Concerns:
- Once we start moving away from random listing, we introduce bias-> the ones shown on first page are likely to be booked more often.

**Step-2**

`Customization`

`User data` = (Duration of stay,number of people,stay location,nationality etc)

Add these features. Split data carefully here(time-aware split unlike previous case to avoid label leakage.). Here we have more rows as each (listing,user pair) contributes
a row, whereas earlier a single row for each listing.

Do offline testing -> A/B testing -> deploy.

Implementation Concerns/details:

Here there would be different rankings for different users. Not one single list of ranking. Periodically pre-computing and serving => compute intensive. Let's limit this to only
most frequent(booking wise) users(top 1000).

Monitor results.

**Step-3**:

Online ML: The lag between availability of data and Model-serving is order of few-minutes. Why is this required ?

`Using Query features`

Consider user search words inside `airbnb`. Arguably this contain the most informtion for serving `experiences`. This would need new infrastructure set-up though.

This is often the final stage done only in mature companies. We deal with lot of complexity here. Different data is stored at different places. Aggregate and serve with 
latency requirements => big engineering challenge.
------------
Metrics:

ranking metrics => AUC, NDCG

**Stage-4**:

Realize that our ml-model is not perfect even from modeling/optimization perspective => (bias introduced by tog ranked models as users are unlikely to choose a potentially good experience long down the list)
Ranking is done via `prob of booking` values by the classifier. Tweaking the model, gathering/trying out additional features is an ongoing process. 
Until now we ignored everything post-booking. User-ratings,comments etc. 

- We want to improve user-experience overall and form long-term relationship with the customer. We can't do this via ML tivially.
Among the data gathered,rerank them based on these rules. Always monitor the effects. This is a two sided market place. We would want hosts to have insights about what improves there chance of rebooking.

- Diveristy of ranking.



## 150 Successful Machine Learning Models: [6 Lessons Learned at Booking.com](https://blog.kevinhu.me/2021/04/25/25-Paper-Reading-Booking.com-Experiences/bernardi2019.pdf)

`Background`

Booking.com is a two sided market place. Some interesting traits of their scenario.
relevant metrics:  sales diversification, conversion rate or loyalty.

- contant cold start: users travel only 1 or 2times a year.
- High stakes: unlike movie recommendation,once booked and reached a destination..it's hard to undo.
- Delayed feedback.
-  classification problems the Bayes Error is a good estimate for learnability of the model since it only depends on the data set, we apply methods from the work of Tumer & Ghosh
- As just described, constructing label and observation spaces can easily introduce selection bias. How to identify selection bias 

construct a classification problem that classifies each observation into the class of the observations for which a target variable can be computed and the class of the observations for which a target variable cannot be computed. If this classification problem is easy (in the sense that a simple algorithm performs significantly better than random) then the bias is severe and must be addressed.

-  lack of correlation is not between offline and online performance, but between offline performance gain and business value gain.
-   standard performance metric for Machine Translation (BLEU) exhibits a “rather tenuous” correlation with human metrics. Only where the offline metric is almost exactly the business metric, a correlation can be observed.

Why ?

- we apply triggered analysis to make sure we only consider the users exposed to a change, that is, users for which the models disagree. As models improve on each other, this disagreement rate goes down, reducing the population of users that are actually exposed to a treatment.
- Optimization vs Business metric:we might build a recommender system based on Click Through Rate because we know that CTR has a strong correlation or even causation with Conversion Rate, the business metric we really care about in this case.

 (An example of this is a model that learned to recommend very similar hotels to the one a user is looking at, encouraging the user to click (presumably to compare all the very similar hotels), eventually drowning them into the paradox of choice and hurting conversion.)

We often don't want to optimize on single metrics.

so we create a challenger model that although still minimizes RMSE, somehow produces higher diversity. It is likely that this new model has a higher RMSE, but as long as it succeeds at increasing diversity and gives a reasonable RMSE, it will be used to test the hypothesis “diversity matters”








