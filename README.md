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


## Notes On ML Engineering/Infrastructure
`Observations/obvious facts`
1. Building Models is being commoditized. The has been a continuos trend towards unification of methods in cv,nlp etc. AutoML can give you a fairly good model.

Over the next decade, there was a Cambrian explosion of web frameworks which started to converge to common infrastructure stacks like LAMP (Linux, Apache, MySQL, PHP/Perl/Python). By 2020, a number of components, such as the operating system, the web server and databases, have become commodities which few people have to worry about, allowing most developers to focus on the user-facing application layer e.g. using ReactJS

Layers
a. DataWarehouse
A key challenge is to lay out the data in a way that makes it easily discoverable and efficiently accessible by data science applications while maintaining a high degree of durability - naturally the data warehouse must not lose data. In addition, many data science applications care a lot about granular historical data, which can be used to train models, which poses an extra challenge for many traditional data warehousing solutions.

b.Compute Resources
A system that can provide computing resources on demand.

c.Job Scheduler
We want to feed fresh data in the algorithm at a regular cadence.

d.Architecture
At the architecture layer, you define what your application is and how it is going to work. This includes defining an algorithm or several algorithms and how the scheduling layer is supposed to connect the algorithms and the data pipelines together.

e.Versioning
experimentation and iteration
you can evaluate results reliably only if the applications are well isolated, that is, they must not interfere with each other. You must isolate the algorithms themselves, the input and output data, and the scheduled pipelines.

f.Model Operations
help to deploy, monitor, and assure validity of all models at all times, without hindering the speed of experimentation. To make this possible, the infrastructure needs to track metadata about all executions and models, from prototype to production.

g.Feature Engineering
h.Model Development

<img width="866" alt="Screen Shot 2022-01-09 at 10 21 53 PM" src="https://user-images.githubusercontent.com/21222766/148714869-738c5c68-4d74-45ec-b338-23cde8a62f48.png">


Netflix -> not just recommender system. But they also produce movies. Read scripts and predict the hits or watch video clips etc.(CV). So one app can have many applications.

Volume - we want to support a large number of data science applications.
Velocity - we want to make it easy and quick to prototype and productionize data science applications.
Validity - we want to make sure that the results are valid and consistent.
Variety - we want to support many different kinds of data science models and applications.

Data is the king unless -> a. Mission Critical/high stakes application b.Massive scale (here modeling starts to be crucial as improving acc from 99 to 99.5 may mean millions of dollars in revenue)

A self-driving car company has one special application, so they should focus on building a single custom application - they don’t have the variety and the volume that would necessitate a generalized infrastructure. A small startup pricing used cars using a predictive model can quickly put together a basic application to get the job done - again, no need to invest in infrastructure initially.In contrast, a large multinational bank has hundreds of data science applications from credit rating to risk analysis and trading, each of which can be solved using well-understood (albeit sophisticated - “common” doesn’t imply simple or unadvanced in this context) models, so a generalized infrastructure is well justified. Over time companies tend to gravitate towards generalized infrastructure, no matter where they start. A self-driving car company that initially had one custom application will eventually need data science applications to support sales, marketing, or customer service. 

Example of the complexity:
As a concrete example, consider a hypothetical mid-size e-commerce store: They have a custom recommendation engine (“These products are recommended to you!”), a model to measure effectiveness of marketing campaigns (“Facebook ads seem to be performing better than Google ads in Connecticut”), an optimization model for logistics (“It is more efficient to dropship category B vs. keeping them in stock”), and a financial forecasting model estimating churn the customer lifetime value (“customers buying X seems to churn less”). Each of these four applications is a factory in itself: They may involve multiple models, multiple data pipelines, multiple people, and multiple versions.


avoid introducing incidental complexity, i.e. complexity that is not necessitated by the problem itself but it is just an artifact of our approach. Incidental complexity is a huge problem for real-world data science because we have to deal with such a high level of inherent complexity that distinguishing between real problems and imaginary problems becomes hard.

Public clouds, such as Amazon Web Services, Google Compute Platform, and Microsoft Azure, have massively changed the infrastructure landscape by allowing anyone to access foundational layers that were previously available only for the largest companies.

Don't reinvent the wheel.

- Amazon S3 which provide a virtually unlimited amount of storage with close to a perfect level of durability and high availability. 
-  nearly infinite, elastically scaling, compute resources like Amazon EC2

Objective is to merge the first 4 roles onto a single individual:

Data Scientist or Machine Learning Researcher develops and prototypes machine learning or other data science models.
Machine Learning Engineer implements the model in a scalable, production-ready way.
Data Engineer sets up data pipelines for input and output data, including data transformations.
DevOps Engineer deploys applications in production and makes sure that all the systems stay up and running flawlessly.
Application Engineer integrates the model with other business components, e.g. web applications, which are the consumers of the model.
Infrastructure or Platform Engineer provides general pieces of infrastructure, such as data warehouses or compute platforms for many applications to use.

<img width="941" alt="Screen Shot 2022-01-09 at 11 00 09 PM" src="https://user-images.githubusercontent.com/21222766/148717100-6040e9db-b06c-4a25-ab55-d3957265623e.png">

Data Scientist -> Looking at data, writing code, evaluating it, and analyzing results. 


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




