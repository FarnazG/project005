# **CONVOLUTIONAL NEURAL NETWORK IMAGE CLASSIFIER:**

This readme summarizes the work completed for a Fashion Brand Predictor Neural Network.


# **ABSTRACT:**

The goal of the project is to identify the brand name and price of a given clothing image using deep learning process. 


# **DATA PREPARATION:**
The dataset we are working with is the Farfetch Listings obtained from Kaggle website.

[data_preprocessing_notebook](https://github.com/FarnazG/project005/blob/master/notebooks/data_preprocessing.ipynb)
 
1. Data cleaning:
*   Check for missing data and place holders
*   Check for data types
*   Extract a sub-dataset to work on the project of interest 
*   Separate independent and target variables as X and Y
*   Download URL images and import it as a NumPy array using OpenCV (Open Source Computer Vision Library) 


2. Check data distribution for regression problem

![alt text](https://github.com/FarnazG/project005/blob/master/images/data-distribution.png)

* The price/target variable for regression analysis is not normally distributed, so log transfer was applied to normally distribute the price values, at the end the process will be reversed to predict the real price. 

![alt text](https://github.com/FarnazG/project005/blob/master/images/log-transferred.png)

3. check data balance for multi-class classification 

![brand distribution for a multi-classifier model](https://github.com/FarnazG/project005/blob/master/images/data-balance-bar-chart.png)

*   **Brand Distribution/target labels sounds balanced for a multi-classifier**  

4. Solving class imbalance problem for binary classification:
*   Generating labels to help the balance

 ![before generating labels](https://github.com/FarnazG/project005/blob/master/images/class-imbalance.png)

 ![after generating labels](https://github.com/FarnazG/project005/blob/master/images/class-balancing.png)


* Generating image for added labels through image augmentation

  ![original image](https://github.com/FarnazG/project005/blob/master/images/generated-image-1.png)

  ![flipped image](https://github.com/FarnazG/project005/blob/master/images/generated-image-2.png)

  ![rotated image](https://github.com/FarnazG/project005/blob/master/images/generated-image-3.png)

  ![rotated image](https://github.com/FarnazG/project005/blob/master/images/generated-image-4.png)


5. splitting train and test data
6. shuffling data for more accurate predictions 


 
 # **MODELING APPROACHES**:

In this project, six different CNN models have been developed to compare the results:

1. **Multi-class neural network classifier**

* For predicting brand names 

 [multiclass_classifier1_notebook](https://github.com/FarnazG/project005/blob/master/notebooks/multiclass_classifier1.ipynb)

 * Model Accuracy, Relu and Softmax activation functions

 ![relu activation](https://github.com/FarnazG/project005/blob/master/images/model-accuracy-1.png)

 [multiclass_classifier2_notebook](https://github.com/FarnazG/project005/blob/master/notebooks/multiclass_classifier2.ipynb)

  * Model Accuracy, Sigmoid and Softmax activation functions, decreasing dropout and batch normalization layers in the model 

 ![sigmoid activation](https://github.com/FarnazG/project005/blob/master/images/model-accuracy-2.png)

 [multiclass_classifier3_notebook](https://github.com/FarnazG/project005/blob/master/notebooks/multiclass_classifier3.ipynb) 

   * Model Accuracy, tanh and Softmax activation functions, dropping more hidden layers from the model

 ![tanh activation](https://github.com/FarnazG/project005/blob/master/images/model-accuracy-3.png.png)

As we can see, the accuracy of the models is not satisfying.

3. **Transfer learning for multi-classifiers**:
* Transfer learning uses pre-trained models when developing a new convolutional neural network.
* One or more layers and their weights from the previously trained model are used as a starting point for the training process of the new model on new but related problems.

 [transfer_learning1_notebook](https://github.com/FarnazG/project005/blob/master/notebooks/transfer_learning1.ipynb) 

 ![alt text](https://github.com/FarnazG/project005/blob/master/images/model-accuracy-4.png)

 [transfer_learning2_notebook](https://github.com/FarnazG/project005/blob/master/notebooks/transfer_learning2.ipynb)

 * Adding more layers to the custom model to higher the accuracy, but as shown below, it led to an overfit model

 ![alt text](https://github.com/FarnazG/project005/blob/master/images/model-accuracy-5.png)

 [transfer_learning3_notebook](https://github.com/FarnazG/project005/master/notebooks/transfer_learning3.ipynb)
 * Eliminating dropout layers, adding more convolutional layers to the custom model to reduce the number of trainable parameters in fully connected layers, adding bias_regularizer to the fully connected layers in order to reduce overfitting and increase the accuracy.

 ![alt text](https://github.com/FarnazG/project005/blob/master/images/model-accuracy-6.png)

* One more try:
 
 ![alt text](https://github.com/FarnazG/project005/blob/master/images/model-accuracy-7.png)

* our model still overfits the training data, also the accuracy of the validation is not acceptable, so we are moving to our next approach to compare the results. 

4. **One-vs-all approach**: 
*   This approach splits the multi-class classification into multiple binary classifications, and fits a binary classification model on each.

*   Each model predicts a class membership probability - probability score. The argmax of these scores (class index with the largest score) is then used to predict the class.

*   This approach is fairly reasonable when the total number of classes is small, but becomes inefficient as the number of classes increases.

  [one_vs_all_notebook](https://github.com/FarnazG/project005/blob/master/notebooks/one_vs_all.ipynb)

 ![alt text](https://github.com/FarnazG/project005/blob/master/images/model-accuracy-8.png)
*  As seen, the accuracy of the model is not good enough; this is partially because of the imbalanced count of data for one brand vs. the rest of brands in the binary model. Thus, in the next step, we balance the data for each binary model, and use transfer learning to train each binary model. 

4. **Combination of One-vs-all and Transfer learning**

  [one_vs_all_transfer_learning_notebook](https://github.com/FarnazG/project005/blob/master/notebooks/one_vs_all_transfer_learning.ipynb)

* Model accuracy for Chanel brand binary classification

  ![Channel](https://github.com/FarnazG/project005/blob/master/images/model-accuracy-channel.png) 

* Model accuracy for Dolce & Gabbana brand binary classification

  ![Dolce & Gabbana](https://github.com/FarnazG/project005/blob/master/images/model-accuracy-dolce-gabbana.png)
* Model accuracy for Prada brand binary classification

  ![Prada](https://github.com/FarnazG/project005/blob/master/images/model-accuracy-prada.png)

* Model accuracy for Saint Laurent brand binary classification

  ![Saint Laurent](https://github.com/FarnazG/project005/blob/master/images/model-accuracy-saint-laurent.png)
* Model accuracy for Gucci brand binary classification

  ![Gucci](https://github.com/FarnazG/project005/blob/master/images/model-accuracy-gucci.png)



5. **Neural network regression model**
*   For price prediction, 

  [regression_classifier_notebook](https://github.com/FarnazG/project005/blob/master/notebooks/regression_classifier.ipynb)


6. **Combination of regression and classification models**
*   For both brand name and price prediction


# **CONCLUSION**
After exploring all different models and comparing the results, the best results are obtained from **Combination of One-vs-all and Transfer learning** model.

![alt text](https://github.com/FarnazG/project005/blob/master/images/final-model-result.png)

The model shows %66 success rate at predicting the brand name.
![alt text](https://github.com/FarnazG/project005/blob/master/images/success-rate.png)


# **Non-technical Presentation**

[fashion-brand-classifier-presentation](https://github.com/FarnazG/project002/blob/master/fashion-brand-classifier-presentation.pdf)


# **FUTURE WORK**
 1. A similar procedure will be conducted with a regression classifier for the price estimation.

 2. Other features such as item description, gender and demographics, can be added to our CNN-based classifier.

 3. An online deployment of the predictive model will be delivered as a web service for fine apparel retailers.
