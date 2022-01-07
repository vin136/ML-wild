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



[END-END MLOPS Project](https://github.com/jacopotagliabue/you-dont-need-a-bigger-boat)

[Robustness-gym and Mandaline](https://www.youtube.com/watch?v=mNkqAZ54wGo)

## Research Papers:

[Mandoline: Model Evaluation under Distribution Shift](https://arxiv.org/abs/2107.00643)

[Model Patching: Closing the Subgroup Performance Gap with Data Augmentation](https://arxiv.org/abs/2008.06775)

[Understanding Dataset Shiftand Potential Remedies](https://vectorinstitute.ai/wp-content/uploads/2021/08/ds_project_report_final_august9.pdf)


## Good Quality to study ML from the foundations

`Mathematics`
[Linear Algebra](https://www.youtube.com/watch?v=dn_VXccQrJo&list=PLwV-9DG53NDwKJIwF5sANj6Za7qZYywAq)
