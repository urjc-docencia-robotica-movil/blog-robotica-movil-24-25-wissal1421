# Global Navigation

In this project, we were tasked with implementing gradient-based navigation through a city. The assignment was quite dense, as it required calculating cost maps, expanding obstacles, and finally, executing the navigation itself. The navigation is semi-reactive, traversing the city based on the cost of neighboring cells. It took me longer than expected because I didn't have the car image in Unibotics. Below, I will explain the problems I encountered and the solutions I applied.

## Problem 1: Loading Only the Necessary Part of the Map

This was the first issue I faced. Given the structure of my code, I encountered many errors when trying to implement it as explained in class. To avoid leaving it unfinished and to prevent unnecessary obstacles from being analyzed, I applied a mask. This way, although the entire map loads the first time, the rest of the code ignores it.

## Problem 2: What Costs Should I Assign to Obstacles?

I was unsure about this because I could assign a very high cost that the map would never actually reach, but that didn't quite convince me. Ultimately, I decided to use infinite costs. This ensures that the map will always function correctly because it will never have infinite costs elsewhere.

## Problem 3: Map with Costs on Obstacles

Initially, I considered generating the cost map and expanding obstacles simultaneously. However, this approach was inefficient and didn't work as intended. Therefore, I decided to first load the general cost map and then expand the obstacles afterward.

## Problem 4: Narrow Streets

While navigating, the car would spend a lot of time turning and adjusting at narrow street intersections. To address this, I expanded the obstacle costs in a circular manner, which helped the car handle intersections more smoothly.

## Problem 5: Semi-Reactivity

At first, I structured all the code so that only the navigation part was in the main loop. Later, I changed this because the program was getting stuck in a while loop within the get_target() function. This wasn't acceptable, so I implemented a state machine in the main loop. One drawback of this method is the lack of clarity—it becomes difficult to divide the code into multiple functions without having to return numerous variables, which can make the code less readable.

## Video

Here is a video showcasing the entire implementation (video)[].
