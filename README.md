# Overview

The aim of this project was to explore planet classes by comparing features and then seeing how well machine learning can classify planets without any labels. 

# Exoplanet Data Exploration

The first part of this project was to explore the planet classes. I did this by plotting two features and then coloring the datapoints based on class. 

Since mass is a definitive feature to have when classifying planets, that was the constant feature throughout all of these. 

I first started with oribital period and mass: 

![image](https://github.com/DylanBerger/Exoplanet-exploration/assets/82914031/ea9eab3c-dab6-48e7-a35c-46825360499e)

As orbital period went up, mass did not necessarily go up. While the planets with the largest orbital periods do happen to be Gas Giants, it is not a constant occurance as many Neptune-like and even some Super Earth planets have orbital periods that compare to the largest of planets. This is even evident in our own solar system where Jupiter is the largest, but by no means has the longest orbital period. Neptune's is 13.75 times longer! This is somewhat explained by the fact that orbital period and mass have an inverse relationship as shown below: 

![image](https://github.com/DylanBerger/Exoplanet-exploration/assets/82914031/2ee5532a-f078-4e21-ab82-253403e043d1)

The semi-major axis and star mass matters much more than the planets mass. 

The next is density and mass:

![image](https://github.com/DylanBerger/Exoplanet-exploration/assets/82914031/e01e5382-01c3-4efd-a92b-9c60185f3d87)

There is an obvious correlation here as mass/volume is density. But the crux of this is that the categories are really defined. Super Earth and Terrestrial planets have lower mass but higher density, Neptune-like planets have a mass only a step up from Super Earths, but have a lower density, and Gas Giants have large mass and the lowest density overall. This makes for an interesting clustering option

The next one is orbital distance and mass:

![image](https://github.com/DylanBerger/Exoplanet-exploration/assets/82914031/3552cc1a-c368-4a74-91d4-34069db00256)

There doesn't appear to be a clear correlation between a planets mass and the semi-major axis. This is because the planets mass (most of the time) won't affect its semi-major axis. The mass of the planet can be ignored when it is insignificant compared to the mass of the host star, as is the case for a spacecraft orbiting a planet. However, some gas giants, and neptune-like planets are significant enough, so their semi-major axis will be larger. This is why the planets with the largest semi-major axis are the larger gas giants. 

Next is star mass and planet mass:

![image](https://github.com/DylanBerger/Exoplanet-exploration/assets/82914031/9fb63d06-db1f-45c1-8c32-de544036fb45)

There is no apparent correlation. This is because most discovered planets are around similar or smaller stars than our own. We are currently unable to detect planets in systems with very large stars, they are simply too bright. Someday we may find countess planets around these bigger stars, but for now our technology is too limited. Besides, giant stars are in the minority of stars in our universe, current estimates say they make up less than 1% of all stars. 

Lastly, we have radius and mass: 

![image](https://github.com/DylanBerger/Exoplanet-exploration/assets/82914031/717dae81-6520-4020-8cd5-6d01dd565b87)

There is not that much to be said, planets with a larger mass have a higher radius. There are some interesting outliers but that's it.

# Data Preprocessing

After exploring the data, it is necessary to process it. 

I applied normalization and selected my features (density, mass, and orbital period)

![image](https://github.com/DylanBerger/Exoplanet-exploration/assets/82914031/22ddf185-1cf1-4288-b7db-801cedd28f1b)

I then shuffled the dataset and applied UMAP (Uniform Manifold Approximation and Projection) to reduce the dimensions of my data from three to two (I originally had more features which made this more necessary, but I eliminated features for reasons I will explain, and the model still worked best after applying UMAP so I kept it). 

![image](https://github.com/DylanBerger/Exoplanet-exploration/assets/82914031/2354a26e-6ff8-4c80-a4f7-983119d46c96)

# Feature Selection

As you can see I only normalized the orbital period, mass, and density. I started originally with six features (planet radius, star mass, orbital period, semi-major axis, planet mass, and planet density), but it didn't exactly work out. I ran clustering with so many combinations, but it worked best on mass, density, and orbital period. So naturally I kept them.

# Clustering 

I used the kmeans algorithm to perform clustering. Now there are four categories of planets but I found that the model had a very hard time discovering terrestrial planets and it actually messed with clustering in the other categories, so I decided to go with three classes: rocky planets (Super Earth and Terrestrial), Neptune-like planets, and Gas Giants. The model clustered very well with three categories as you can see: 

![image](https://github.com/DylanBerger/Exoplanet-exploration/assets/82914031/c9eee9d0-1f24-4711-aa49-aa33e519559c)

The clustering is cool and all, but it wasn't enough to determine how accurate the model clustered without labels.

Luckily I have a dataset with planet names and classes!

# Evaluation 

I first printed the number of planets in each cluster, here are the results: 

![image](https://github.com/DylanBerger/Exoplanet-exploration/assets/82914031/12162f25-5a35-449e-a874-3c3de1ca2f43)

This was the first good sign because the counts of each category were similar to the actual counts of each category (with the number of Super Earth and Terrestrial planets merged into one). The actual counts are as follows: 1733 Gas Giant, 1859 Terrestrial and Super Earth, 1881 Neptune-like. 

Next step is to actually calculate the accuracy, which took several steps.

- First I added the class corresponding to each planet name
- 
![image](https://github.com/DylanBerger/Exoplanet-exploration/assets/82914031/dc827d1f-668a-4abc-b1c5-8dc344d7e83d)

- Then I encoded the classes 

![image](https://github.com/DylanBerger/Exoplanet-exploration/assets/82914031/a025113e-aac2-4c6e-979d-97f87cd1b7c2)

- Then matched the clustering labels with the encoded classes (I needed to make a dictionary to do so)

![image](https://github.com/DylanBerger/Exoplanet-exploration/assets/82914031/045d516b-c083-4753-b84c-18e0b0114549)

- Then finally, calculating the percentage of encoded labels that matched the actual labels (first I had to convert data types)

![image](https://github.com/DylanBerger/Exoplanet-exploration/assets/82914031/d94283e2-2569-40ae-92fb-c75f4dc352d3)

The accuracy was 82.4% which was surprising!

From my own analysis, the ones it mainly classified wrong were the smaller neptune-like planets, and the larger super earths which makes sense.

# Next Steps

The model did very well without labels. One thing I would try in the future is to do multiple clusterings. I tried clustering with two categories in a previous iteration of the project, and it seperated the gas giants and everything else almost perfectly. I then tried to apply clustering on the cluster with everything else and then merge them, but it didn't work. It is something I would like to revisit someday. I also would do more indepth data exploration.

Regardless, I consider the project a success, hope you enjoyed!
