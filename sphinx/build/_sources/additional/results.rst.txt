Result Discussion
====================

In this project, aiming to investigate the potential of using machine learning models to detect webcam spying, we speculated data on captured packets and decided to use samp_num and samp_size (on an ip-agnostic packet-level) as features to do both multiclass classification and binary classification. We resorted to both supervised and unsupervised techniques. In terms of supervised models, we used random forest, logistic regression, and multi-level perceptrons for both multiclass and binary classifications. In terms of unsupervised models, we tested out Kernel Density Estimation (KDE), Gaussian Mixture Model (GMM), One Class Support Vector Machine (OCSVM), and Isolation Forest (IF/IForest).

On a very high level for the supervised part, we find that random forest models perform better than both logistic regression models and multi-level perceptrons, and the latter two yield similar performances. For the unsupervised part, we see that Kernel Density Estimation and Gaussian Mixture Model overpower their peers. 

Here is a summary on the performance of the models:

1. Supervised Learning Models:
    a. Multiclass Classifications
        * Random Forest
            - Accuracy = 0.8
            - F-1 Scores = (1, 0.889, 0.8, 0.727, 0.5, 0.833)
        * Logistic Regression
            - Accuracy = 0.5
            - F-1 Scores = (1, 0, 0.571, 0, 0.588, 0.6)
        * Multi-layer perceptrons
            - Accuracy = 0.6
            - F-1 Scores = (1, 0.25, 0.6, 0.286, 0.5, 0.769)
    

    b. Binary Classifications
        * Random Forest
            - Accuracy = 0.933
            - F-1 Scores = (0.929,0.938)
        * Logistic Regression
            - Accuracy = 0.8
            - F-1 Scores = (0.8125,0.786)
        * Multi-layer perceptrons
            - Accuracy = 0.833
            - F-1 Scores = (0.839, 0.828)

2. Unsupervised Learning Models:
    * Kernel Density Estimation (KDE):
        - AUC = 0.907
    * One Class Support Vector Machine (OCSVM):
        - AUC = 0.529
    * Isolation Forest (IF/IForest):
        - AUC = 0.040 :(
    * Gaussian Mixture Model
        - AUC = 0.889


Following are several interesting findings from our result:
    1. *The utilization of deep learning does not help the model performance improve from logistic regression by too much.* We tried out other activations (e.g., "relu", "tanh"), but "logistic" activations peformed the best according to our cross-validation. We found 2 hidden layers to perform the best for multiclass classifications and 1 hidden layer to give the highest accuacy for binary classification. This implies that the relationship between features and labels are quite straightforward and do not require the construction of high level relationships. 
    2. *Tree Classifications (Random Forest) seem to perform better than probrabilistic estimations.* We see that Random Forest wins out fo both Binary and Multiclass classifications. We speculate that as the behavior of the spying application and our legit video applications may behave similarly in terms of networking, there is no clear separation in values of the features to tell the different classes apart, and as we are including a large quantity of features prabablistic estimation can be biased by ups and downs in the feature dataset. The first few values in the data set, on the other hand, would be able to better tell the different classes apart as per the speculation - Tree Classifications better exploit this phenomenon.
    3. *Probability-distribution-based unsupervised methods win out over region-based ones.* We see as the spying application can behave in conjunction with every video application (or simply run on its own), OCSVM and IForest would reasonably behave poorly under our investigated scenario. Prob-distribution based models, on the other hand, do a better job at taking holistic views at the whole dataset for making decisions.

Conclusively, we would argue that it would be promising to utilize Random Forest to detect webcams' spying behavior given that we can replicate the operations of the corresponding spying programs; also, we would like to point out that Gauxian Mixture Model and Kernel Density Estimation would be more plausible for anomaly detection in the context of webcam spying, and this would require less knowledge on the behavior of the spying program. Nevertheless, we admit that there may be (or certainly will be) changes in model preferences as data collection scenarios and data quantities change.

Limitations and Future Work
===========================
While we confirmed that our implementation was successful overall, there is room for further exploration that we depict in the following.

*Nevertheless, our project does have several limitations:*

*First, we do not have sufficient data to train deployment-ready data.* This is because both (1) we did not devote enough time into collecting data and (2) we are handling our data on a gradularity of "instances/files". Most models would yield a greater performance with more data to train and validate. Some models, such as deep learning, perform especially poorly with few data.

*Second, we only collected data with the applications transmitting data over a local network.* Most spying would happen over a distance and have different networks communicating with each other. Our data collection setup definitely underestimates factors such as latency and dns lookup time. Metrics such as inter-arrival time would thus not provide us with generalizable insights, and that is partially why we were not using it as a feature to our model. That said, the features we did choose to use would also have some validity issues, but these limitations arise mainly because of time and economic restrictions (this is just a course project anyways!).

*Finally, for our future work, we plan to deploy an app that sniffs traffic for every 10-second interval and judges if the webcam is spied.* To do that, we would like to collect more data related to various computer network states and spying behavior. 

Notes on Parameter Tuning
=========================
We tuned the parameters for each model we displayed in the Jupyter Notebook with cross validation (with respect to accuracy). However, we decided not to display every step we took as that would be too verbose. The final models in the Jupyter Notebook are all relatively optimized versions.

Conclusion
==========
Threats to privacy and security prevail. In this project, we explored the possibility of applying machine learning models networking data to detect if the embedded cameras in our laptops are spied. We investigated six scenarios:
    1. no video application is running; 
    2. only the spying application is running; 
    3. only WeChat Video Call is running; 
    4. both WeChat Video Call and the spying application are running; 
    5. only Zoom Video Conferencing is running, and 
    6. both Zoom Video Conferencing and the spying application are running. 

For each of these six scenarios, we collected 20 10-second instances, among which 5 are randomly chosen for testing. We performed both supervised (on both multiclass and binary classficaitions) and unsupervised (binary only, as it would be for anomaly detection) learning.

Among the supervised models, we found that our implementation of the random forest model reached 80% accuracy on multiclass classification and approximately 93.3% on binary classification, which is higher than both logistic regression and multi-layer perceptrons with logistic activations. We also discovered that the employment of multiple levels of perceptrons does not yield a performance that is significantly better than logistic regression. 

For the unsupervised models, we found that models that make decisions on probability distributions outperform the ones that resort to the region of data points. Specifically, KDE and GMM both reached testing AUC values of about 0.90. 

At the end of our project, we again point out the feasibility of applying machine learning models to detect spying behavior of embedded webcams. To help better tackling the formulated problem, we plan to gather more data points, consider more scenarios, and carry out the data collection process under more realistic settings. We also look forward to building an application that would automatically detect webcams' spying behavior.