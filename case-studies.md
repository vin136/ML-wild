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













