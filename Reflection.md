# Project Intro
In this project, the simulator for the lake race track will provide us with the cross track error (CTE) the velocity (mph) and angle. We'll use this data to implement a PID controller which will compute the appropriate steering angle inorder to maneuver the vehicle around the race track!
# Approach
After inspecting the PID class files and main class.
I implemented the Init, UpdateError and TotalErrors functions

Now lets test drive.
Main initialized the PID class with random picked params `pid.Init(0.2,0.004,2.0);`
then i just called `pid.UpdateError(cte)` and set `steer_value = pid.TotalError();`

Results from test drive was pretty rough. The car swinged very often, however it stayed within the road boundries. 
# Parameter Optimization
**The P** is inversely proportional to the cte, so a larger cte will result in a larger P value will be streer the car strongly to the opposite direction

**The D value** provides a means to control by reducing the P value as it approaches the center line so it doesn't overshoot. A swinging motion is an indicator of a bad D value.

**The I value** is suppose to account for subtle bias,slips and drifts which could prevent the P from reaching the center line.

Picking an optimal set of values of PID values is key for a smooth maneuver on the track.
How can we ensure a smoother ride?  Lets Tune the init params a bit. 
Since P=0.2 seemed a bit strong. lets try other values. We'll optimize the parameters one at a time so with, I and D set to 0. We test out the values below for P  

with I=0.0 and D = 0.0  
When P is  
0.1 = much better than 0.2. less over-shooting or swing motion  
0.07 = much better movement but hits curb around the corners  
0.06 = less swinging still hitting curb  
  
Adding D param:I=0.0 and P = 0.06  
2.0 = Now it's able to get around the corners still touching curb  
3.0 = car swings a bit, value too high  
1.6 = turns around corners are much smoother, but still overshoots right curve  

Adding I param:D=1.6 and P = 0.06  
0.001 = over-shooting right curve!  
0.002 = over-shooting right curve!  
0.003 = Ok on left and right curve  
0.004 = Ok on left and right curve, much smoother curves  
  
Final Values Selected **I= 0.004, D=1.6 and P = 0.06**  

Here's a [link to my video result][![Alt text](https://img.youtube.com/vi/9vtaXm4QdrQ/0.jpg)](https://www.youtube.com/watch?v=9vtaXm4QdrQ)
