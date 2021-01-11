# Kohonen's Self-Organizing Maps

The aim of this project is to test the method of self-organizing maps to images. <br/>
Besides that, two map plots were developed in the file 'som_plos'. Both were inspired in plots used by the MATLAB plots for SOM ('plotsomhits' and 'plotsomnd'). <br/>
The SOM implementation used is the [MiniSom](https://github.com/JustGlowing/minisom).<br/>
The encoders developed in my [autoencoder](https://github.com/luizamarnet/autoencoder) repository were used to compress the images before clusterization.<br/>

## About the Project

The models were validated using 5-folds cross-validation and all of them were tested on the same dataset.<br/>
The models will be trained with 2 datasets: CIFAR-10 and MNIST.<br/>
The results presented so far are preliminary and we intend to continue to improve them.<br/>

## About SOM Chosen Parameters and Hyperparameters
According to MiniSom documentation, a good choice for the number of neurons in the map is 5\*sqrt(N), where N is the number of samples in the dataset to analyze.<br/>
As claimed by Haykin, in his book __'Neural Networks: A Comprehensive Foundation'__, during SOM's training there are two phases, the ordering phase and the convergence phase. The ordering phase is when occurs the topological ordering of the map. During the convergence phase, the map weights are fine-tuned.<br/>
Haykin says that the ordering phase should last at least 1000 iterations and that the convergence phase should last 500\*(number of neurons in the map) iterations or more. He also states that the learning rate should start the training with a value close to 0.1 and be in the order of 0.01 during the convergence phase. As for the neighborhood, he says that it should start covering almost all neurons in the map and be reduced to 1 or no neuron in the convergence phase.<br/>
The learning rate and the neighborhood are controlled by the same rate decay in MiniSom. Because of it, it is difficult to meet both recommendations of Haykin about these hyperparameters. <br/>
More tests were done on the choice of parameters and hyperparameters for training with MNIST dataset than with CIFAR-10 dataset. After many tests, the parameters and hyperparameters that lead to a clearer neuron distance map for MNIST were chosen. For a first test, the same values were used during the training of SOM with CIFAR-10. However, better values must be found.<br/>

## Results

Below we present some results that were find in this project.<br/>
For both the MNIST and the CIFAR-10 datasets, the autoencoders developed in the [autoencoder](https://github.com/luizamarnet/autoencoder) project were validated with 5-folds cross-validation. Because of it, 5 encoders were developed for each of these datasets. Here, we trained one SOM for each encoders' output, resulting in five self-organizing maps for MNIST and five for CIFAR-10.<br/>
The known labels of each sample were not used in any part of the training. However they were used to analyze the quality of the trained maps, including to analyze whether the maps were ordered according to the different classes.<br/>

### MNIST Dataset

Before training the maps with the encoders' outputs, we tested training one SOM with the flattened images. Below are three kinds of plots that can be analyzed.  
In this first plot we can see what was the majority class of the samples that activated each neuron. If the neuron was not activated by any sample, no annotation was made inside of it.<br/>

<img src="https://user-images.githubusercontent.com/58445878/104128994-51801a80-5349-11eb-8996-40c825234f6a.jpg" width="500"> 

In the image below, the plots show the neurons' activations per class. The blue hexagons size is proportional to the number of samples that activated each neuron. While looking at these plots is important to keep in mind that the blue hexagons size is normalized by the number of activations in each plot and not by the number of activations in the hole set of plots. <br/>
 
<img src="https://user-images.githubusercontent.com/58445878/104129149-34981700-534a-11eb-9a61-446d4cff9cdf.jpg" width="1000">

Lastly, the plot below on the left shows the distance between neurons in the map. Each black hexagon represents one neuron and the color between each neuron represents the Euclidean distance between them. The lightest color represents the more similar neurons, and the darkest color represents the more distant neurons. Remembering that when we talk about near and far neurons, we are talking about how similar the neurons weights are. The plot below on the right is the same as the plot on the left, but with the clusters drawn according to groups of neurons of the same class that are next to each other. We are considering the class of the neuron as the majority class of the samples that activated each neuron, as in the 'Map of Neurons Classes' above. <br/>

<img src="https://user-images.githubusercontent.com/58445878/104129357-d7509580-534a-11eb-951f-f46d493ea2fd.jpg" width="500"/> <img src="https://user-images.githubusercontent.com/58445878/104136966-37116580-5378-11eb-94e4-752c332cf675.jpg" width="500"/>

Considering each neuron as a cluster,  the clusterization purity is equal to 0.92120 and the Shannon's entropy is equal to 0.32130. <br/>

After that, we trained SOM maps with the encoded imagens. The plots below are from one of the five SOMs trained with the outputs of the encoders. <br/>

<img src="https://user-images.githubusercontent.com/58445878/104131496-6ebae600-5355-11eb-96eb-452c2a1e1d4a.jpg" width="500">

<img src="https://user-images.githubusercontent.com/58445878/104131497-711d4000-5355-11eb-9f49-9be04dde89ed.jpg" width="1000">

<img src="https://user-images.githubusercontent.com/58445878/104131503-75e1f400-5355-11eb-9c12-7d7d173e04dd.jpg" width="500"/> <img src="https://user-images.githubusercontent.com/58445878/104137056-c585e700-5378-11eb-8417-a65893377e3c.jpg" width="500"/>

As we can see, when comparing the two neuron distance maps above, the second map, representing the SOM trained with the encoded imagens, is better organized. In this second map, the division between the clusters is easier to visualize and the number of clusters better correnponds to the number of known classes (10 classes).

Considering the results of the 5 self-organizing maps trained, the mean purity was equal to 0.95974 with standard deviation equal to 0.00113. And the Shannon's entropy is equal to 0.16495, with standard deviation equal to 0.00476<br/>

### CIFAR-10 Dataset

We trained SOM maps with the encoded CIFAR-10 imagens. The plots below are from one of the five SOMs trained with the outputs of the encoders.

<img src="https://user-images.githubusercontent.com/58445878/104132136-2fdb5f00-535a-11eb-8f1f-8c50159b6074.jpg" width="500">

<img src="https://user-images.githubusercontent.com/58445878/104132137-32d64f80-535a-11eb-95eb-ce2c76b1d868.jpg" width="1000">

<img src="https://user-images.githubusercontent.com/58445878/104132141-3669d680-535a-11eb-98bd-8ab7dd50f793.jpg" width="500">

Considering the results of the 5 self-organizing maps trained, the mean purity was equal to 0.42812 with standard deviation equal to 0.00246. And the Shannon's entropy is equal to 2.10176, with standard deviation equal to 0.01177<br/>


## Comments

As we see in the results, the purity for the MNIST clustering was extremely high. Also, looking at the neuron distance map plot for the clusterization using the encoded MNIST imagens, it is possible to identify the regions where the neurons are closer (where are the clusters) separated by regions of more distant neurons. <br/>
For the CIFAR-10 dataset, it is possible to see in the hit maps that the model is traying to put the samples of the same class together. But these results need to be highly improved, since the samples of different classes still mixed in the map. Also, the purity for this clustering is low. <br/>
The values for the parameters and hyperparameters need to be further investigated. <br/>
Perhaps a solution for getting better results would be to adapt the MiniSom algorithm so that the learning rate decay and the neighborhood decay are controlled by different rates. <br/>
