# Dev-MyQuadcopter

Documentation for Create the world of simulation add with aruco + Adding the model pickup to the simulation
Caution: This is only for PX4-Autopilot v1.14. The other version may have another difference. 

Basically, You can actually running the simulation with open the PX4-Autopilot, and run this on the terminal
```javascript
make px4_sitl gz_x500
```
This command run the default.sdf world file and the quadcopter x500 model file.
You can find the world file on path (PX4-Autopilot/Tools/simulation/gz/worlds)
and the model file on path (PX4-Autopilot/Tools/simulation/gz/models)

Adding the aruco.sdf, on your world path. Also download the dependencies of the arucotag such png file, model.config and  model.sdf.
Put it down itu one file names aruco. Place it on the worlds file path
```shell
worlds<br/>
   aruco<br/>
      arucotag.png
      model.config
      model.sdf
   aruco.sdf
   default.sdf
```
