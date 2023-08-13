# Overview

The aim of this project was to explore planet classes by comparing features and then seeing how well machine learning can classify planets without any labels. 

# Exoplanet Data Exploration

The first part of this project was to explore the planet classes. I did this by plotting two features and then coloring the datapoints based on class. 

Since mass is a definitive feature to have when classifying planets, that was the constant feature throughout all of these. 

I first started with oribital period and mass: 

![image](https://github.com/DylanBerger/Exoplanet-exploration/assets/82914031/a67f9143-30ef-4ac4-9093-4e14f402ebe1)

As orbital period went up, mass did not necessarily go up. While the planets with the largest orbital periods do happen to be Gas Giants, it is not a constant occurance as many Neptune-like and even some Super Earth planets have orbital periods that compare to the largest of planets. This is even evident in our own solar system where Jupiter is the largest, but by no means has the longest orbital period. Neptune's is 13.75 times longer! This is somewhat explained by the fact that orbital period and mass have an inverse relationship as shown below: 

![image](https://github.com/DylanBerger/Exoplanet-exploration/assets/82914031/589cdbb2-fbf5-4787-b34a-f12ca2a7839c)

The semi-major axis and star mass matters much more than the planets mass. 

The next is density and mass:

![image](https://github.com/DylanBerger/Exoplanet-exploration/assets/82914031/f8fb4818-7d4f-4b3c-aa03-2437f2ade0ee)

There is an obvious correlation here as mass/volume is density. But the crux of this is that the categories are really defined. Super Earth and Terrestrial planets have lower mass but higher density, Neptune-like planets have a mass only a step up from Super Earths, but have a lower density, and Gas Giants have large mass and the lowest density overall. This makes for an interesting clustering option

The next one is orbital distance and mass:

![image](https://github.com/DylanBerger/Exoplanet-exploration/assets/82914031/8172e3b5-7443-4e33-9544-1aaf72ac773c)

There doesn't appear to be a clear correlation between a planets mass and the semi-major axis. This is because the planets mass (most of the time) won't affect its semi-major axis. The mass of the planet can be ignored when it is insignificant compared to the mass of the host star, as is the case for a spacecraft orbiting a planet. However, some gas giants, and neptune-like planets are significant enough, so their semi-major axis will be larger. This is why the planets with the largest semi-major axis are the larger gas giants. 

Next is star mass and planet mass:

![image](https://github.com/DylanBerger/Exoplanet-exploration/assets/82914031/082926ca-b0c0-4986-a243-5340d6952887)

There is no apparent correlation. This is because most discovered planets are around similar or smaller stars than our own. We are currently unable to detect planets in systems with very large stars, they are simply too bright. Someday we may find countess planets around these bigger stars, but for now our technology is too limited. Besides, giant stars are in the minority of stars in our universe, current estimates say they make up less than 1% of all stars. 

Lastly, we have radius and mass: 

![image](https://github.com/DylanBerger/Exoplanet-exploration/assets/82914031/2fd7896f-5d78-4b9d-bba5-758cd99d8ae4)

There is not that much to be said, planets with a larger mass have a higher radius. There are some interesting outliers but that's it.

# Data Preprocessing

After exploring the data, it is necessary to process it. 

I applied normalization and selected my features (density, mass, and orbital period)

![image](https://github.com/DylanBerger/Exoplanet-exploration/assets/82914031/10931477-ae01-420b-9057-68754cdbb8d7)

I then shuffled the dataset and applied UMAP (Uniform Manifold Approximation and Projection) to reduce the dimensions of my data from three to two (I originally had more features which made this more necessary, but I eliminated features for reasons I will explain, and the model still worked best after applying UMAP so I kept it). 

![image](https://github.com/DylanBerger/Exoplanet-exploration/assets/82914031/a97b8840-fd00-488f-9d1a-6e0c4e9a6ed5)

# Feature Selection

As you can see I only normalized the orbital period, mass, and density. I started originally with six features (planet radius, star mass, orbital period, semi-major axis, planet mass, and planet density), but it didn't exactly work out. I ran clustering with so many combinations, but it worked best on mass, density, and orbital period. So naturally I kept them.

# Clustering 

I used the kmeans algorithm to perform clustering. Now there are four categories of planets but I found that the model had a very hard time discovering terrestrial planets and it actually messed with clustering in the other categories, so I decided to go with three classes: rocky planets (Super Earth and Terrestrial), Neptune-like planets, and Gas Giants. The model clustered very well with three categories as you can see: 

![image](https://github.com/DylanBerger/Exoplanet-exploration/assets/82914031/5bf5289e-2f8b-479d-a9e6-fe5316f97d9d)

The clustering is cool and all, but it wasn't enough to determine how accurate the model clustered without labels.

Luckily I have a dataset with planet names and classes!

# Evaluation 

I first printed the number of planets in each cluster, here are the results: 

![image](https://github.com/DylanBerger/Exoplanet-exploration/assets/82914031/2d625dfe-7bd1-41ef-939d-e3ccb998e023)

This was the first good sign because the counts of each category were similar to the actual counts of each category (with the number of Super Earth and Terrestrial planets merged into one). The actual counts are as follows: 1733 Gas Giant, 1859 Terrestrial and Super Earth, 1881 Neptune-like. 

Next step is to actually calculate the accuracy, which took several steps.

- First I added the class corresponding to each planet name
  
![image](https://github.com/DylanBerger/Exoplanet-exploration/assets/82914031/11c7814f-9c69-43a0-8c99-1008a8e7ea02)

- Then I encoded the classes 

![image](https://github.com/DylanBerger/Exoplanet-exploration/assets/82914031/bc320e7a-713c-4c2f-9ac2-7944cdccc75a)

- Then matched the clustering labels with the encoded classes (I needed to make a dictionary to do so)

![image](https://github.com/DylanBerger/Exoplanet-exploration/assets/82914031/0ad3aa51-b154-4a2a-9e83-7d740d603497)

- Then finally, calculating the percentage of encoded labels that matched the actual labels (first I had to convert data types)

![image](https://github.com/DylanBerger/Exoplanet-exploration/assets/82914031/7eea3085-f9dc-4979-bf84-268b391761c2)

The accuracy was 82.4% which was surprising!

From my own analysis, the ones it mainly classified wrong were the smaller neptune-like planets, and the larger super earths which makes sense.

# Next Steps

The model did very well without labels. One thing I would try in the future is to do multiple clusterings. I tried clustering with two categories in a previous iteration of the project, and it seperated the gas giants and everything else almost perfectly. I then tried to apply clustering on the cluster with everything else and then merge them, but it didn't work. It is something I would like to revisit someday. I also would do more indepth data exploration.

Regardless, I consider the project a success, hope you enjoyed!
