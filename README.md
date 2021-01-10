# Kohonen's Self Organizing Maps

The aim of this project is to test applying the method of self organizing maps to images. <br/>
Besides that two map plots were developed in the file som_plos. Both of them were inpired in plots used by the MATLAB plots for SOM ('plotsomhits' and 'plotsomnd'). 
The SOM implamantation used here is the [MiniSom](https://github.com/JustGlowing/minisom).
The encoders developed in my [autoencoder](https://github.com/luizamarnet/autoencoder) repository were used here to compress the images before clusterization.

## About the Project

The models were validated using 5-folds cross-validation and all of them were tested on the same dataset.<br/>
The models will be trained with 2 datasets: CIFAR-10 and MNIST.<br/>
The results presented so far are preliminary and we intend to continue to improve them.<br/>

As the autoencoder model was trained with 5-folds cross-validation, the 5 models will be used here. This way, the clusterization using the outpout of the encoder will be done 5 times and 5 deep clustering models will be traied. Moreover, the training part of each clusterization will be caried out with the respective subsets used in the traing of each autoendor during the cross-validation, and the same subset of images will be used as test dataset. Hence, the tests realized and the comparison between the models are fair.

## About SOM Chosen Parameters and Hyperparameters
According to MiniSom documentation, a good choice for the number of neurons in the map is 5\*sqrt(N) is neurons, where N is the number of samples in the dataset to analyze.<br/>
As claimed by Haykin, in his book __'Neural Networks: A Comprehensive Foundation'__, during SOM's training there are two phases, the ordering phase and the convergence phase. The ordering phase is when occurs the topological ordering of the map. During the convergence phase a fine tuning of maps weights takes place.<br/>
Haykin says that the ordering phase should last at least 1000 iterations and that the convergence phase should last 500\*(number of neuron in the map) iterations or more. He also states that the learning rate should start the training with a value close to 0.1 and be in the order of 0.01 during the convergence phase. As for the neighborhood, he says that it should start covering almost all neurons in the map and be reduced to 1 or no neuron in the convergence phase.<br/>
The learning rate and the neighborhood are controlled by the same rate decay in MiniSom. Because of it, it is difficult to meet both recommendations of Haykin about these hyperparameters. <br/>
More tests were done on the choice of parameters and hyperparameters for training with MNIST dataset than with CIFAR-10 dataset. After many tests, the parameters and hyperparameters that lead to a clearer neurons distance map for MNIST were chosen. For a first test, the same values were used during the training of SOM with CIFAR-10. However, better values must be found.<br/>

## Results

Below we present some results that were find in this project.<br/>
For both the MNIST and the CIFAR-10 dataset, the autoencoders developed in the [autoencoder](https://github.com/luizamarnet/autoencoder) project were validated with 5-folds cross-validation. Because of it, 5 encoders were developed for each of tehse dataset. Here, we trained one SOM for each encoders output, resulting in five self organizing maps for MNIST and five for CIFAR-10.<br/>
The known labels of each sample were not used in any part of the training, but they were used to analyse the maps trained and to analyze with the maps were ordered according to the different classes.<br/>

### MNIST Dataset

Before training the maps with the encoders outputs, we tested training one SOM with the flattened images. Below are three kinds of plots that can be analysed.  
In this first plot we can see what was the majoruty class that activated each neuron. If the neuron was not activated by any sample, no anotation was made inside of it.<br/>

<img src="https://user-images.githubusercontent.com/58445878/104128994-51801a80-5349-11eb-8996-40c825234f6a.jpg" width="600">

In the image below, the plots show the neuros activations per class. The blue hexagons size are proportional to the number of samples that activated each neuron. While looking at these plots is important to keep in mind that the blue hexagons size are normalized by the number of activation in each plot and not by the number of activation in the hole set of plots. <br/>
 
<img src="https://user-images.githubusercontent.com/58445878/104129149-34981700-534a-11eb-9a61-446d4cff9cdf.jpg" width="900">

Lastly, the next plot show the distance between neurons in the map. Each black hexagon represents one neuron and the color between each neuron representes the euclidian distance between them. The clearest color represents the more similar neuros and the darkest color represents the more distante neurons. Remebmering that when we talk about close or distant neurons we are talking about how similar the neurons weights are. <br/>

<img src="https://user-images.githubusercontent.com/58445878/104129357-d7509580-534a-11eb-951f-f46d493ea2fd.jpg" width="600">

Considering each neuron as a cluster,  the clusterization purity is equal to 0.92120 and the Shannon's entropy is equal to 0.32130. <br/>

After that, we trained maps with the encoded imagens. The plots below are from one of the five SOMs trained with the outputs of the encoders. <br/>


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
