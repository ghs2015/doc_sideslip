# Azimuth estimation accuracy evaluation
# Summary
## 
## Main factors may be related to pose estimation
- Variable lever arm.
	- This may lead to degraded GNSS observations used for estimating IMU pose errors.
	- This may cause a variable body-to-vehicle-frame rotation.
- Variable body-to-vehicle-frame rotation

# Possible solutions
## Investigate and reduce the installation impact to cars and truck
	- By configuring Novatel system to handle this.
	> The most important thing is that the lever arm standard deviations provided in the SETIMUTOANTOFFSET command are at least as large as the true uncertainty in the lever arm.[6] 
	- Use Novatel postprocessing software, like Waypoint, to estimate the lever arm and compare with the setting.
	- Seek a stable installation approach.
	- `quick notes` uncertainty setting for lever arm and SETIMUTOANTOFFSET is very important
## Calibration
	- Consider dynamic lever arm and compensation. But this is needed to dynamically apply to fusion results in some way.

# Analysis and experiments
## Comparison between MKZ1,2 and trucks

## Factors related to (Azimuth - Track ground)
### Based on product user manual
### Data driven analysis: use decision tree to estimate factor importance
### Based on publications

# Inbox
- calibraition matters
- azimuth accuracy from the manual
- What can definitely improve the performance?
	- Good lever arm calibration.
		- `best` "Measure the lever arm using survey methodology and equipment, for example, a total station."
		- Perform lever arm calibration routine.
		> It is important that the lever arm between the centre of the IMU and the GPS L1 phase centre be measuredcorrectly in the field. Otherwise, the attitudeinformation will not be optimal, especially in heading. This problem is particularly severe duringturns. [ref link](http://www.softnav.com/discounts/InertialExplorer800_Manual.pdf) 
		> To enable the dual-antenna ALIGN solution to aid the INS alignment and provide heading updates, theoffset between the antennas and the IMU must be known. This is achieved by entering lever arms to bothantennas, using the SETIMUTOANTOFFSET and SETIMUTOANTOFFSET2 commands.
		> Alternately, the angular offset between the dual-antenna baseline (from primary GNSS antenna tosecondary GNSS antenna) and the IMU frame forward axis is entered directly via the EXTHDGOFFSETcommand. We recommend entering the lever arms rather than entering the angular offset as this iseasier to measure and will lead to better overall accuracy. 

	- Good Body to Vehicle Frame Rotation Calibration (depends on accurate lever arm)
	- Constant relative position between IMU and antenna.

- What may improve the performance?
	- If the Novatel system has the algorithm to estitmate calibration errors, maneuvers help the estimation.
		> Start to move the system. The lever arm is not observable while the system is stationary. Immediately, drive a series of maneuvers such as figure eights. The turns should alternate between directions, and you should make an equal number of turns in each direction. Some height variation in the route is also useful for providing observability in the Z-axis.
- Good alignment.
	> The accuracy of the initial attitude of the system following the kinematic alignment varies and depends on the dynamics of the vehicle. The attitude accuracy will converge to within specifications once **some motion** is observed by the system. This transition can be observed by monitoring the INS Status field in the INS logs.
- Observations:
	- C1, C3, C4 has similar scales of lever arms as MKZ1 and MKZ2. These cars has beed calibrated for lever arm and automatically calibrated for body-to-frame rotation. However, the performance (azimuth - track ground) seems bad given 50 samples.

#Supplement
## Benchmark road segments

## Performance

# Reference
1. [Novatel Lever Arm Calibration Routine](https://docs.novatel.com/oem7/Content/SPAN_Operation/Lever_Arm_Calibration_Routine.htm)
2. [System Start-Up and Alignment Techniques](https://docs.novatel.com/oem7/Content/SPAN_Operation/Startup_Alignment_Techniques.htm)
3. [Body to Vehicle Frame Rotation Calibration Routine](https://docs.novatel.com/oem7/Content/SPAN_Operation/Vehicle_SPAN_Frame_Angular_Offsets.htm?tocpath=Operation%7CSPAN%20Operation%7CReal-Time%20Operation%7C_____6)
4. [om-20000139](https://www.novatel.com/assets/Documents/Manuals/om-20000139.pdf)
5. [Inertial Explorer](http://www.softnav.com/discounts/InertialExplorer800_Manual.pdf)
6. [What is the Effect of Bad Lever Arms in the GNSS/INS Filter?](https://www.novatel.com/support/known-solutions/what-is-the-effect-of-bad-lever-arms-in-the-gnssins-filter/)

# Papers
- `relevant` [GNSS/INS Fusion with Virtual Lever-Arm Measurements](https://www.mdpi.com/1424-8220/18/7/2228/htm)
- `relevant` [Experimental study on the estimation of lever arm in GPS/INS](https://ieeexplore.ieee.org/abstract/document/1608624)
- `relevant` Lever arm compensation for GPS/INS/Odometer integrated system
- [Automatic Estimation of Dynamic Lever Arms for a Position and Orientation System](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC6308725/)
