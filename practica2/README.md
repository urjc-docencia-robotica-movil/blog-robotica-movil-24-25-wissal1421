# Switching from RGB to HSV

At first, I was trying to detect the red line using RGB. It seemed like a good idea, but I ran into a lot of problems. Basically, there are lines on the sides that are red, not just the line I was supposed to follow. This causes it to turn in the wrong direction or turn sharply when it's not right.

## What did I do?

I decided to change the color detection system to HSV. Why? Because in HSV space it is easier to isolate colors. In short, HSV allows me to better separate color from brightness, which makes it much easier to detect the red line without confusing it with other objects. Since I made this change, the robot has greatly improved in its accuracy in following the correct line.

# Two Search Methods: Shallow and Deep

This is where things get interesting. I implemented two different ways to search for the red line in the image the robot sees: a quick search and a more detailed one.

## Shallow Search

This is a quick search that looks at a specific row of the image, right in the middle. If the line is visible and the robot is on the right path, red pixels should appear in that central area. It is fast and usually works well when the robot follows the line stably.

## Deep Search

When shallow search fails to find the line (for example, in very tight curves), deep search comes into play. Here I go through the entire image, row by row, to find any trace of the red line. It is slower, but it is super useful when the robot has strayed or lost sight of the line.

## Why the two searches?

I decided to use both to balance speed and accuracy. Shallow search is fast and sufficient most of the time, but deep search saves the robot when the line is out of its view or at the edges. Since I added this combined approach, the robot takes much less time to "recover" the line when it loses it.

# PID Control for Linear Velocity

At first, I only used PID control for the robot's angular velocity, i.e. to make it turn and align its camera with the red line. Everything was going well until I tried it on sharper curves. There I realized that the robot was maintaining too high a linear velocity, and either going off the curve or not being able to correct in time.

## What did I do?

I decided to apply PID to the linear velocity as well. Now, the robot reduces its speed when the error in the line position increases, meaning it goes slower in curves and faster in a straight line. This makes the robot much more stable when taking sharp turns. Thus, it can correct its direction without losing the line or making sudden movements.

## Version Ackermann
To make this version the only thing that was necessary was to modify the PID parameters.

# Video
[video](https://drive.google.com/file/d/1IrzWxycD7VqUsIdzumuLnZYj5xwMiQsz/view?usp=sharing)
