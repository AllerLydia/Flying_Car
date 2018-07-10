## Project: 3D Motion Planning
![Quad Image](./misc/enroute.png)

---


# Required Steps for a Passing Submission:
1. Load the 2.5D map in the colliders.csv file describing the environment.
2. Discretize the environment into a grid or graph representation.
3. Define the start and goal locations.
4. Perform a search using A* or other search algorithm.
5. Use a collinearity test or ray tracing method (like Bresenham) to remove unnecessary waypoints.
6. Return waypoints in local ECEF coordinates (format for `self.all_waypoints` is [N, E, altitude, heading], where the drone’s start location corresponds to [0, 0, 0, 0].
7. Write it up.
8. Congratulations!  Your Done!

## [Rubric](https://review.udacity.com/#!/rubrics/1534/view) Points
### Here I will consider the rubric points individually and describe how I addressed each point in my implementation.  

---
### Writeup / README

#### 1. Provide a Writeup / README that includes all the rubric points and how you addressed each one.  You can submit your writeup as markdown or pdf.  

You're reading it! Below I describe how I addressed each rubric point and where in my code each point is handled.

### Explain the Starter Code

#### 1. Explain the functionality of what's provided in `motion_planning.py` and `planning_utils.py`
These scripts contain a basic planning implementation that include manual -> arming -> palnning -> takeoff -> waypoint -> landing -> disarming -> manual in motion planning. planning_utils.py is called by motion_planning.py. It implemented waypoint prune with collinearity and A* search to help planning waypoint. 

### Implementing Your Path Planning Algorithm

#### 1. Set your global home position
Here students should read the first line of the csv file, extract lat0 and lon0 as floating point values and use the self.set_home_position() method to set global home. Explain briefly how you accomplished this in your code.

This part is line 128 and onward.

And here is a lovely picture of our downtown San Francisco environment from above!
![Map of SF](./misc/map.png)

#### 2. Set your current local position

Use global_to_local to convert global to local position. 

#### 3. Set grid start position from local position
Use east_offset and north_offset to get the start position from local position. line 149 and onward.

#### 4. Set grid goal position from geodetic coords
Use a random position close to local position, then (lat, lon) converted from gloabl_to_local. line 152 and onward.

#### 5. Modify A* to include diagonal motion (or replace A* altogether)
Implemented in palnning_utils.py - class Action.

#### 6. Cull waypoints 
Line 170 and onward. Defined a collinearity_check and prune_path function to check collinearity of the waypoint, then prune_path to remove waypoints that are collinear. 



### Execute the flight
#### 1. Does it work?
It works!

<a href="https://imgflip.com/gif/2dpgpg"><img src="https://i.imgflip.com/2dpgpg.gif" title="made at imgflip.com"/></a>
### Double check that you've met specifications for each of the [rubric](https://review.udacity.com/#!/rubrics/1534/view) points.
  
# Extra Challenges: Real World Planning

For an extra challenge, consider implementing some of the techniques described in the "Real World Planning" lesson. You could try implementing a vehicle model to take dynamic constraints into account, or implement a replanning method to invoke if you get off course or encounter unexpected obstacles.

