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
The world file is already, its time to configure it to your simulation.
Define the parameter on the file airframe configuration file. In my case, i use the x500 quadcopter series.
The parameter file access on path (PX4-Autopilot/ROMFS/px4fmu_common/init.d-posix/airframes/4001_gz_x500)
The default is define in line 11.
```javascript
PX4_SIMULATOR=${PX4_SIMULATOR:=gz}
PX4_GZ_WORLD=${PX4_GZ_WORLD:=default}
PX4_SIM_MODEL=${PX4_SIM_MODEL:=x500}
```
change the `default` to `aruco`.
its define the worlds that must execute is the aruco file.
If you want to get another worlds, it can be downloaded through this [here](https://github.com/PX4/PX4-gazebo-models.git)
