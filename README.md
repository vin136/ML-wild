# ML-wild
Synthesizing insights for building Real-world ML systems.

There is a wide gap between machine learning in the Real-world and academia. This repo is a collection of notes to myself to avoid as much angst as possible for my future self. The challenges many challenges that I faced in my work but doesn't really seem to bother academic ML researchers. More importantly the experience I gained is largely visceral and can't even be easily transferred. This repo is an attempt at forcing myself to clearly articulate the tricks/tools and techniques needed to successfully develop ML-centric applications. 

# working thoughts(When not mentioned, Models largely refer to Deep Neural networks)

1. When should I retrain my models ?
How to identify, have a clear and a sound rule for retraning. Model updating-> I don't want to retrain but just update on the recent data. In my last job, we need to do this on Deep RL algorithms, completely hopeless endeovour. Can I identify data-set shift before model degradation ? In my experience it's based off historcial experience of the model coming from somebody older than you.

2.Quantifying improvement ?
How to quantify improvement. Esp with DEEPRL, no clear best model. 

3.What to monitor ? How to split the data ?
Not as simple as they seem. We want testing data as relective of production-data. In case of time-series we also want to have training data as close to real-world/testing data. Thus the latest data is contested by both traning-split and testing-split. What split is the best/reliable indicator of your model's live performance.

4. How to test Machine Learning Code ?
We avoided testing altogether. Well there were bunch of assert statements all over. Validation data is often limited. We need to track other metrics/properties of the model that are proxy for generalization. This also comes under testing, if we view tests as series of binary functions that all must assert True before putting the model to production.

5. Finally we want models that fail gracefully ?



END-END MLOPS Projects

[Don't need a bigger boat1](https://github.com/jacopotagliabue/you-dont-need-a-bigger-boat)
[MSYS Course material](https://github.com/jacopotagliabue/FREE_7773)
[no-ops ML](https://github.com/jacopotagliabue/no-ops-machine-learning)
[Another end-end project](https://www.mihaileric.com/posts/setting-up-a-machine-learning-project/)
[Robustness-gym and Mandaline](https://www.youtube.com/watch?v=mNkqAZ54wGo)
[DAG CARDS](https://arxiv.org/pdf/2110.13601.pdf) N [IT'S CODE](https://github.com/jacopotagliabue/dag-card-is-the-new-model-card)

[yugene yan's blog](https://eugeneyan.com/writing/patterns-for-personalization/)

Books
[Good Book on MLFLOW](https://github.com/outerbounds/dsbook)
## Research Papers:

[Mandoline: Model Evaluation under Distribution Shift](https://arxiv.org/abs/2107.00643)

[Model Patching: Closing the Subgroup Performance Gap with Data Augmentation](https://arxiv.org/abs/2008.06775)

[Understanding Dataset Shiftand Potential Remedies](https://vectorinstitute.ai/wp-content/uploads/2021/08/ds_project_report_final_august9.pdf)


## Good Quality to study ML from the foundations

`Practical Resources`

[AppliedAI notes](https://github.com/raveendarv/AppliedAiCourse-AssignmentAndNotes)

`Mathematics`

[Linear Algebra](https://www.youtube.com/watch?v=dn_VXccQrJo&list=PLwV-9DG53NDwKJIwF5sANj6Za7qZYywAq)
[Optimization](https://github.com/rishabhk108/AdvancedOptML)
[Another Course in Optimization though not as good](https://cs.uwaterloo.ca/~y328yu/mycourses/794/lecture.html)
[Robust ML Course](https://www.youtube.com/watch?v=txnftFoHHbo)

`Practice Oriented Courses/Resources`

[ML Course](https://github.com/parrt/msds621)
[Learn to build open Source Package](https://jacobtomlinson.dev/series/creating-an-open-source-python-project-from-scratch/)
[Bayesian Data Analysis](https://avehtari.github.io/BDA_course_Aalto/)

`Interview Prep Resources`
[This blog](https://pub.towardsai.net/4-types-of-machine-learning-interview-questions-for-data-scientists-and-machine-learning-engineers-b8135805ce1b)
## Broad Strokes.
Assorted notes from various sources.

Step 1: Store and Collect data

Step 2: Prepare Training data


a. Hand Labeling
- Linear(More people for more labels)
- Privacy Issues (Maybe you can't show the data to a person)
- Costly( Radiology reports vs comment-toxicity)
- Aren't adaptive( you now want to train on 3 classes instead of 2 which you previously handlabeled)

If you have to follow this route be careful with ambiguity( specify the task precisely and give instructions on how to label in ambiguos cases -> ensure quality labels), multiplicity(variation(label quality) due to different annotators,typically data from various sources/vendors is merged)

How to Deal with unlabeled Data ?

<img width="797" alt="Screen Shot 2022-01-07 at 10 25 18 PM" src="https://user-images.githubusercontent.com/21222766/148629986-75e84f18-ede7-4d55-b5b6-2458b68da28a.png">






