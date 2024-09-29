# P1 - Vacuum Cleaner

This practice consists of a robot that has to clean an entire house, all this without being able to use mapping or lidar. Below I will discuss the difficulties I have had and the solutions I have applied to solve them.

# Issues and Solutions to them:
## Global and local variables 
It may seem silly but this led me to waste a lot of time since the variable changed its value when entering a function in which it was not used, so I changed the necessary variables from local to global, that way the program did not create a new with the same"name"
## Spiral increase
At the beginning of the practice I tried to increase the angle of the spiral for each turn I made, without result, and therefore I began to do it with the speed, even so, it had to be minimal because otherwise it would advance too fast.
## Feeling "locked in"
At the beginning, after making some spirals, the robot ended up making the same movements, trapped in the room or hallway in which it was. Therefore, I implemented a function that is responsible for "taking it out". What it does is generate a random number, which in this case will be the time it will spend spinning, so that it has a greater chance of coming out. Another thing that I implemented in the function is that it does not feel released until it has been able to move straight for 4.5 seconds, so that we make sure that it has enough distance to make the spiral and is not stuck to the wall or obstacle
# State diagram shape
The image of this diagram can be found at [this link](practica1/Diagram.drawio.png) The video is at x5 speed
# Video to the program
In this [link](https://drive.google.com/file/d/1s10CYIOZQyCMoDkLsOZVXb_Nw3x3RDv7/view?usp=drive_link) you have a video where you can see how the robot cleans the area.
# Conclusions
This program is effective but I consider that by having a random variable in the trapped function, it has very different solutions, it can do the complete cleaning in 10 minutes or take 30 minutes to do it for the simple fact that it does not really know what areas it has visited. not even if it is in a room or in a hallway. From what I mentioned above, I consider that any program can finish cleaning, of course some will take longer than others, I only say this to clarify that the video I posted has given a thousand totally different results.
