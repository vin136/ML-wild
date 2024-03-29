## Basics (notes from MDM class)

Data :
a.We can ask users to rate items -> This approach is limited in its effectiveness, since generally
users are unwilling to provide responses, and the information from those
who do may be biased by the very fact that it comes from people willing
to provide ratings.

b.We can make inferences from users’ behavior






Eugene Yan's [blog](https://eugeneyan.com/writing/system-design-for-discovery/)

## [YouTube ranking](https://dl.acm.org/doi/pdf/10.1145/2959100.2959190)

Candidate Generation
 - Optimize click through rate (softmax,NN)

Importance sampling based softmax as the label-dimensionality is huge.

Ranking 
 - Optimize watch time((softmax,NN))
 
 Loss
 
 To predict expected watch
time we use the technique of weighted logistic regression,
which was developed for this purpose.
The model is trained with logistic regression under crossentropy loss (Figure 7). However, the positive (clicked)
impressions are weighted by the observed watch time on
the video. Negative (unclicked) impressions all receive unit
weight.
<img width="1052" alt="Screen Shot 2022-03-03 at 2 24 10 PM" src="https://user-images.githubusercontent.com/21222766/156637764-560c9b3a-3338-42f4-8aec-b1c405986e3d.png">


Interesting Points

- Features describing the frequency of past video impressions are also critical for introducing “churn” in recommendations (successive requests do not return identical lists). If
a user was recently recommended a video but did not watch
it then the model will naturally demote this impression on
the next page load.
- A continuous feature x with distribution f is transformed to ˜x by
scaling the values such that the feature is equally distributed
in [0, 1) using the cumulative distribution, ˜x =
R x
−∞ df.
This integral is approximated with linear interpolation on
the quantiles of the feature values computed in a single pass
over the data before training begins.
In addition to the raw normalized feature ˜x, we also input
powers ˜x
2
and √
x˜, giving the network more expressive power
by allowing it to easily form super- and sub-linear functions
of the feature

- The model is trained with logistic regression under crossentropy loss (Figure 7). However, the positive (clicked)
impressions are weighted by the observed watch time on
the video. Negative (unclicked) impressions all receive unit
weight.

## [ALIBABA](https://www.mendeley.com/reference-manager/reader/16d5962d-f7f4-3ad6-a164-7c3fd142e347/6898156a-4e8e-ebd7-2d62-a389cb4defcf)

KEY IDEA: Generate item-item graph based off user interaction history with node-weight given by his rating. Take a random-walk through this graph and train item-item embeddings(skipgram).
This is about generating candidate set using item-item similarity on an Ecommerce site. They calculate item embeddings (word2vec,skipgram style) and when the user interacts
with an item, them can quickly fetch precalculated similarity item set and then use a different ranking model.

<img width="1016" alt="Screen Shot 2022-03-03 at 2 42 36 PM" src="https://user-images.githubusercontent.com/21222766/156640819-ab0c2868-1e6d-42c9-b97c-5c5a04950716.png">

``Cold Start``
- We canalleviate the cold-start problem by incorporating side informationin graph embedding. For example, two hoodies (same category)from UNIQLO (same shop) may look alike, and a person who likesNikon lens may also has an interest in Canon Camera.
- Item embedding is the linear combination of (category embeddings + item-embedding), if a new item appears, since we know the pre-trained category embeddings we can take them and average them to get a good first approximation.
- A weighting scheme for side information is also given


<img width="534" alt="Screen Shot 2022-03-03 at 2 50 17 PM" src="https://user-images.githubusercontent.com/21222766/156641944-40163ec1-fec4-4a96-9792-5a3088668413.png">



# Rl for recsys
## 1.Netflix Artwork customization(https://netflixtechblog.com/artwork-personalization-c589f074ad76)

To reduce this regret, we move away from batch machine learning and consider online machine learning. This makes the cost of exploration per member negligible, which is an important consideration when choosing contextual bandits to drive a key aspect of our member experience. Randomization and exploration with contextual bandits would be less suitable if the cost of exploration were high.

Under our online exploration scheme, we obtain a training dataset that records, for each (member, title, image) tuple, whether that selection resulted in a play of the title or not. Furthermore, we can control the exploration such that artwork selections do not change too often. 

How to [evaluate (offline)?](https://dl.acm.org/doi/10.1145/1935826.1935878)

<img width="533" alt="Screen Shot 2022-03-03 at 3 46 10 PM" src="https://user-images.githubusercontent.com/21222766/156650156-54fe7f6f-118f-4c5f-ac43-da79bd0b2598.png">

2. [Youtube Reinforce](https://arxiv.org/abs/1812.02353)




Posing as Ranking problem
- [Bayesianranking](https://arxiv.org/pdf/1205.2618.pdf)
- [RL For recommender systems](https://eugeneyan.com/writing/reinforcement-learning-for-recsys-and-search/)
- [Search ranking in E-commerce using DL](https://www.mendeley.com/reference-manager/reader/884a6c73-5aea-367a-88f4-0db5eb0369b8/2e788f9f-7110-cec7-1af4-1a3b21c1d763)


MLOPOS LEARNERS

Can post-processing,reranking address bias in the data ?

bias:

1.Position bias, 2. some products might have invested more in ads and thus have more behaviorial data(like best image,thunbnail to show) thus have advantage.

Randomization: For eg: if bandit based ones,increase exploration.

Evaluation
Points to consider: bottomline-> can't evaluate defferent systems using the same metrics.
1. User intent: how specific user is in thier search
2. User context: How comfortable is the user with the system
3. How exactly is the recommendation presented to the user: N videos are presented @netflix. But in tiktok

What to do when covid hit?
Drop back to rulebased model(near random but not terrible) to collect data. And then train a new model after collecting enough data.

New online shopping place.we have lot of customers coming in? But leaving quickly. Current system: most popular items of the previous day.

- Lot's of new users coming in.
- Dynamic inventory.

Cold start: ITEM-ITEM EMBEDDING n then recommend based off initial few interactions. Use user's geographic location etc. Pre-empt this problem n let the users login via facebook,etc.

Use sequential information: Take current cohort that actually converted. And model that. Use it to predict  items for new customers. Use language modeling to get item-item embedding.

Ways of representing items/users ?
1. USE/train a pusedo tasks with available information and then use the last layers as the embeddings. eg: for item, use the one hot vectors of it's info
like product-category,etc and predict say the sales.
2. Treat session level data. Prod2vec.

Evaluation:
Heldout sessions , take the first few interactions and use KNN and measure the performance.
TO assess the semantic goodness of embeddings : their should be taxonomy for products, good embeddings should satisfy this (build a classifier).
Expert human evaluators to give relevant suggestion based on past interactions -> test the embeddings.(qualitative,human bias)

Solves cold start user problem with this. But still cold-start item ? If item is never seen,it wont be recommended often. but technically can use the category average and then randomly serve.

