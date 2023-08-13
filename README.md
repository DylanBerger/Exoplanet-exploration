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


