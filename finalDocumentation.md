# Artificial Intelligence in Medicine

---  
#### _Pneumonia Classification Based on Chest X-rays_

**Firstly** we load the data from their respective folder paths and store them in 2D arrays:  
&rarr; index[0] corresponds to the image array.
&rarr; index[1] corresponds to the label of said image.
&rarr; `label = 0` corresponds to the "Pneumonia" class.
&rarr; `label = 1` corresponds to the "Normal" class.
  
**Secondly** we make a simple plot to take a look at its distribution
![data distribution](./img/skewed_data.png)
We can notice that the data is fairly biased to `Pneumonia`. This means a few things:
* Results will inevitably be biased to Pneumonia.
* Overfitting will eventually occur.
* Data manipulation is very needed for this data.

This can be solved in few ways:
* Cutting the `Pneumonia` data to be equal to the `Normal` data.
    > This isn't a viable option since the data quantity is already small.
* Performing data augmentation on the `Normal` data to be equal to the `Pneumonia` data.
    > Logically this seems like a good option, but may result in some overfitting to the available `Normal` features.

Since our data is of type `image`, the data augmentation methods need to fit the image criteria:
![data augmentation methods](./img/data_augmentation.png)

#### Data augmentation libraries
1. _Augmentor_ &rarr; time consuming + high cpu usage
2. _Albumentations_ &rarr; **_used_**
3. _Imgaug_ &rarr; high cpu usage
4. _AutoAugment_ (DeepAugment) &rarr; errors in importing dependencies

#### Choice of number of PCA components
![pca components](./img/pca_components_plot.png)
According to the cumulative sum plot of the obtained PCA components, we can see that the variance is almost a constant straight line after roughly 1500 components.  
We picked `PCA(n_components = 1000)`

> #### PCA components = 700, Image dimensions = (80,80):
##### Cutting the `Pneumonia` data to be equal to the `Normal` data.
Scores were as follows:
* train score = 98.4%
* test score = 80.0%

> #### PCA components = 1000, Image dimensions = (100,100):
#### Augmenting the `Normal` data to be equal to the `Pneumonia` data.
Scores were as follows:
* train score = 98.4%
* test score = 78.0%

1. svm classifier:
    * train score = 98.11%
    * test score = 78.37%

1. logistic regression:
    * train score = 97.10%
    * test score = 74.68%

1. KNN classifier:
    * train score = 96.01%
    * test score = 76.60%

1. ensemble learning 1.0:
    * train score = 99.25%
    * test score = 77.56%

1. ensemble learning 2.0 with gradient boosting:
    * train score = 98.66%
    * test score = 75.80%

---  
#### Important Note  
Basic machine learning algorithms in this field are considered outdated given the huge advancements in the field of artificial intelligence. Deep learning models should prove more helpful in such cases.