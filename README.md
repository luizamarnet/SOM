# Deep Clustering Project

The aim of this project is to cluter imagens using deep models. <br/>
The models trained in the [autoencoder](https://github.com/luizamarnet/autoencoder) repository will be used in this project.

## About the Project

The models were developed in Python using Keras.<br/>
The models were validated using 5-folds cross-validation and all of them were tested on the same dataset.<br/>
The models will be trained with 2 datasets: CIFAR-10 and MNIST.<br/>
For each dataset three steps will be carried out.
* The images will be flattened and clusterized using k-means;
* Each image will be inserted into the encoder derived from the autoendores of the other project. And the output of the encoder will be clustered using k-means. <br/>
* A clustering layer will be placed on the top of the encoder model and the new model will be trained as a self supervised model. This is the deep clusterinig model that we want to train. <br/>

As the autoencoder model was trained with 5-folds cross-validation, the 5 models will be used here. This way, the clusterization using the outpout of the encoder will be done 5 times and 5 deep clustering models will be traied. Moreover, the training part of each clusterization will be caried out with the respective subsets used in the traing of each autoendor during the cross-validation, and the same subset of images will be used as test dataset. Hence, the tests realized and the comparison between the models are fair.

## About the Deep Clustering Model
The clustering layer used was developed by Chengwei Zhang and copied from his public repository ([Keras_Deep_Clustering](https://github.com/Tony607/Keras_Deep_Clustering)). The 'metrics.py' code, used during training also was downloaded from the Zhang's repository.<br/>
The encoder used in the deep clustering model trained with the MNIST dataset was the one trained with the same dataset in the project from my respository ([autoencoder](https://github.com/luizamarnet/autoencoder)). The outpout of this encoder is an array of size 10x1.<br/>
As expalined by [Chengwei Zhang](https://www.dlology.com/blog/how-to-do-unsupervised-clustering-with-keras/), the clustering layer calculates the probability that each sample belongs to each cluster using  student's t-distribution. To do this, the weights that connect the clustering layer with the encoder output layer are used as center clusters. <br/>
Also, the labels used while training the deep clustering are updated after some iterations, updating the target distribution. For this reason the model is called self supervised.<br/>


## Results

Up to now, only the MNIST dataset was used in this project. The results obtained until now are presented below.<br/>
Although the true labels of the classes are not used during any part of the training, once it is a cluserization problem, they are used to avaliate the results and analyse if the models are able to separete the clusters according to the known classes. <br/>
The confusion matrix above shows the true labels against the clusterization resulted from flattening the image and apply k-means. Considering the class of each clustering as the majority class of the cluster, the accuracy obtained for the test dataset was: 59.41000 %.

<img src="https://user-images.githubusercontent.com/58445878/103501716-cd500380-4e2d-11eb-8139-65201d731444.jpg" width="600">

Next, using the outputs of the encoder and clusterizing then, the result were improved. Remembering that, since we used 5-folds cross-validation while training the autoencoders, the same respective 5 encoders were used here. This way, the new accuracy for the clusterization, testing the five encoders, was 87.22600 % with standard deviation equal to 3.13242 %. The two confusion matrix below show the results of the clusterization of the outputs of 2 of the 5 encoders.

<img src="https://user-images.githubusercontent.com/58445878/103501970-94fcf500-4e2e-11eb-8c87-a1cad7d894b7.jpg" width="600">

<img src="https://user-images.githubusercontent.com/58445878/103502006-acd47900-4e2e-11eb-9004-22be10bf261e.jpg" width="600">

Last, also considering the 5-folds cross-validation while traing the deep clustering models, the accuracy for the clusterization with the deep model was 93.47000 %, with standard deviation equal to 4.35613 %. The confusion matrix below show the results founded when training the deep clustering model with 2 of the 5 pretrained encoders.


<img src="https://user-images.githubusercontent.com/58445878/103502142-12286a00-4e2f-11eb-8614-cbfa0cc44f8c.jpg" width="600">

<img src="https://user-images.githubusercontent.com/58445878/103502146-15235a80-4e2f-11eb-88a7-30b4064040c5.png" width="600">


## Steps Concluded and Future Works

- [x] To cluster the MNIST dataset flattening the images and applying k-means;
- [x] To compress the MNIST dataset images using the encoders trained and to cluster their outputs applying k-means;
- [x] To trai the deep clustering model using the MNIST dataset;
- [ ] To cluster the CIFAR-10 dataset flattening the images and applying k-means;
- [ ] To compress the CIFAR-10 dataset images using the encoders trained and to cluster the outputs applying k-means;
- [ ] To train the deep clustering model using the CIFAR-10 dataset.


## Comments

As we see in the results, the deep clustering model huge improved the results of the clusterization of the MNIST dataset when comparing with the other two clusterizations. <br/>
Nevertheless, the models perfomed better in the deep clustering models trained with some of the pre trained encoders and get confused between some numbers in others. Maybe, improving the results of the autoencoders from which the encoders were taken could solve this problem.
