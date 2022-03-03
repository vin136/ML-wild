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

This is about generating candidate set using item-item similarity on an Ecommerce site. They calculate item embeddings (word2vec,skipgram style) and when the user interacts
with an item, them can quickly fetch precalculated similarity item set and then use a different ranking model.

<img width="1016" alt="Screen Shot 2022-03-03 at 2 42 36 PM" src="https://user-images.githubusercontent.com/21222766/156640819-ab0c2868-1e6d-42c9-b97c-5c5a04950716.png">


