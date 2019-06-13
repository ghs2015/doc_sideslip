### InertialExplorer800_Manual
> In all likelihood, the initial computed estimates areonly accurate to the nearest 30 cm or 40 cm. 
> Iterateand re-process until you have lever arm values which do not change significantly. These might be good to 10cm or so. 
> Alternatively, if this offset is not precisely known, orsimply not known at all, enable the Solve lever armval ues as additional Kalman filter states option. Theaccuracy achieved via this option depends on the typeof IMU used, but is normally better than 10cm.
> It is important that the lever arm between the centreof the IMU and the GPS L1 phase centre be measuredcorrectly in the field. Otherwise, the attitudeinformation will not be optimal, especially inheading. This problem is particularly severe duringturns.  
> Combined Separation PlotThis plot shows the coordinates diff erences between theforward and reverse IMU process. This plot should a lsobe reflective of the GPS combined separation. It is notexactly the same, but should be in the same region errorwise.A common problem is a sub-metre or decimeter leveldifference between forward and reverse.  This may be dueto a lever arm problem. Make sure you fix your lever ar msat some value before outputting your final coordinates.Otherwise, y our forward/reverse separation floats alongwith the filtered value of the lever arm states. This willbias the coordinates you deliver to your client.

### Dynamic Lever Arm Error Compensation of POS Used for Airborne Earth Observation
> For the first-level dynamic lever arm error compensation, the flight experiment equipment includes an experiment plane (YUN-VIII), SAR, servo machines, and the ring laser gyroscope (RLG) POS which consists of an RLG IMU, POS computer system, and carrier phase differential GPS. The RLG IMU consists of three ring laser gyroscopes with constant and random drifts (0.01°/h) and quartz mechanical accelerometers with constant and random biases (50 μg) assembled in orthogonal triads.
> With the proposed first-level dynamic lever arm error compensation, the latitude, longitude, and height errors have been reduced from 0.9377 m, 2.0680 m, and 2.4657 m to 0.0348 m, 0.0259 m, and 0.0800 m, respectively. The east, north, and upward velocity errors have been reduced from 0.0089 m/s, 0.0085 m/s, and 0.0131 m/s to 0.0067 m/s, 0.0077 m/s, and 0.0091 m/s, respectively. The heading, pitch, and roll angle errors have been reduced from 0.0382°, 0.0132°, and 0.0034° to 0.0266°, 0.0115°, and 0.0027°, respectively.
> With the proposed first-level dynamic lever arm error compensation, the latitude, longitude, and height errors have been reduced from 0.5470 m, 0.5738 m, and 0.1816 m to 0.2921 m, 0.2805 m, and 0.0544 m, respectively. The east, north, and upward velocity errors have been reduced from 0.0230 m/s, 0.0283 m/s, and 0.0140 m/s to 0.0210 m/s, 0.0255 m/s, and 0.0132 m/s, respectively. The heading, pitch, and roll angle errors have been reduced from 0.0530°, 0.1224°, and 7.0999° to 0.0221°, 0.0062°, and 0.0045°, respectively.

### Accuracy assessmentof real-time kinematics(rtk) meas urement onunmanned aerialvehicles (uav) fordirect geo-referencing

### Lever arm corrections during ins transfer alignmentwith wide angle initial heading error 

### Lever arm offset and velocity, acceleration, and sideslip errors
>Of the measurements we need to shift, some are far easier than others. From simple to complex and problematic:Altitude: assuming that the vehicle is a rigid body then the altitude at any point on the vehicle is the same and there is no action needed.Position: this is trivial, the system simply takes the measured position and attitude and corrects with the lever arm offsets directly. Although in theory some position noise could be introduced through attitude noise, in practice this is negligible and the output position signal is not degraded in any way.Velocity: shifting velocity is mathematically relatively simple, but in practice it introduces noise into the output primarily due to gyro noise, but also through mechanical vibration. Typical extra noise for a lever arm of 1m horizontally + 1m vertically is in the region of 0.01kph.Acceleration: shifting acceleration is mathematically rather more complicated than velocity, but the result is similar to with velocity, but even more pronounced. The reason for this is that body acceleration is the differential of body velocity. Acceleration is hence particularly affected by high-frequency gyro noise when a lever arm is used. Typical extra noise for a lever arm of 1m horizontally + 1m vertically is in the region of 0.1g.

>Derived variables or states: 
>Direction of travel variables, including gradient: Since these are calculated from the vehicles velocities they are subject to the same problems as velocity.Slip angle: This is calculated as the difference between the yaw and heading and, as above, subject to the same problems as velocity.Distance: This is calculated by integrating velocity, and whilst the velocity appears to be noisy with long lever arms, it is still mathematically correct, and the process of integrating very largely negates the effects. In practice distance is very robust to lever arm offsets.
[link](https://www.race-technology.com/wiki/index.php/GPSTheoryAndBackground/LeverArmOffset)

### Apollo 1.0 hardware system installation guide
>Installing the GPS Receiver and AntennaThis section 
>provides general information about installing one of two choices:
>Option 1: GPS-IMU: NovAtel SPAN-IGM-A1
>Option 2: GPS-IMU: NovAtel SPAN® ProPak6™ and NovAtel IMU-IGM-A1
>Taking the Lever Arm MeasurementWhen the SPAN-IGM-A1 and the GPS Antenna are in position,the distance from the SPAN-IGM-A1 to the GPS Antenna must be measured. The distance should be measured as: X offset, Y offset, and Z offset.The error of offset must be within one centimeter to achieve high accuracy. For more information, see the SPAN-IGM™ Quick Start Guide, page 5, for a detailed diagram.
[link](https://github.com/ApolloAuto/apollo/blob/master/docs/quickstart/apollo_1_0_hardware_system_installation_guide.md)

### Lever arm accuracy requirement
> A typical RTK GNSS solution is accurate to a few centimetres. For the integrated INS/GNSS system tohave this level of accuracy, the offset must be measured to within one centimetre.
[link](https://www.novatel.com/assets/Documents/Manuals/GM-14915114.pdf)
