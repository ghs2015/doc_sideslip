# Log
- data analysis
	- MKZ2 azimuth and track ground stability analysis.

# Note:
- Slip angle = f(wheel steering angles, tyre slip, reference point, Ackerman steering effects)
- track ground is approximately equal to azimuth, if we measure the track ground using position located at the rear of the vehicle.
	- We may use master antenna's position to obtain an independent track ground.
	- Also, we may use dual antenna heading to obtain an independent heading.
	![slip angles when small turning](images/normal_turning_manoeuvre.png)
	![slip angles when oversteering](images/oversteering.png)
- [ ] Method to measure slip angle.
- Method to measure tyre slip angle. (should be done for each wheel, due to Ackerman steering)
- Method for slip angle translation
- Thoughts, the azimuth is from fusion of IMU, GNSS (raw track ground, dual antenna). The causes to bad azimuth fusion:
	- Directly
		- bad **raw** track ground 
			- low/zero speed
			- degraded GNSS signal
		- bad heading from dual antenna
			- enviroment interruption
			- position relative to IMU changes
		- bad calibration
			- without calibration
			- inaccuate calibration
			- outdated calibration
			- affected by antenna-imu relative position changes 
	- Indirectly

# Todo:
- [ ] Build benchmark datasets according to locations. Quantitively evaluate the performance.
	- [x] Check the annotations of bags with bad performance.
	- [x] Check calibration topics of tested mkz1 bags.
	- [ ] Check std of trackground since std of zimuth seems to be relatively stable.
	- [x] Check the azimuth accuracy of recent bags. Some may not have heading topic, so ignore this topic.
	- [ ] Select datasets to use.
		- [x] Sync bags with heading from Tuscon repo.
			- [x] phase one, about 6 bags.
			- [x] phase two, about 10+ bags.
			- [x] phase three, about 20+ bags.
		- [ ] Find more test segments.
			- [x] three straight segments and one cornering segments.
- [] Compare the data from MKZ2 with others and find out the reason of performance difference.
	- Initial calibration may be a reason.

# Possible todos:
- [x] Use decision tree to analyze the important factors related to worse (azimuth - track ground).
- [ ] Check the initial difference between azimuth and heading.
- [ ] Organize the result in a systemtic and tracable way.
- [ ] Check the raw output from dual antenna, like trk gnd.
- [ ] Check the output of stationary status.
- [ ] Get more statistical information out of the data.
- [ ] Clarify the estimation model of sideslip angle.
- [ ] Determine the evaluation metrics of state variables of interests, such as sideslip angle, azimuth.
- [ ] Compare the azimuth accuracy and stability of cars and trucks, especially cars with fiber optical gyros.
- [ ] Consider calibration errors and current works done for calibration. Is leveling done?
- [ ] Capture the accuracy requirement from the control group.
- [ ] Calculate the current performance on selected datasets to get a benchmark.
- [ ] Analyze the azimuth fusion result with/without dual antenna information.
- [ ] sync the post-processed data with online data.

# Information to ask
- [x] Where the out IMU mounted? The front? Lower rear.
- [x] Where is the reference point to measure the slip angle? IMU center.

# Terms
- the effects of Ackerman steering

# Reference
## Documents
Slip Angle Explained, How to measure vehicle body slip angle usingVBOX equipment. [link](http://www.racelogic.co.uk/_downloads/vbox/Application_Notes/Slip%20Angle%20Explained.pdf)
[NovAtel Body to Vehicle Frame Rotation Calibration Routine](https://docs.novatel.com/OEM7/Content/SPAN_Operation/Vehicle_SPAN_Frame_Angular_Offsets.htm) 

## Publications
- Rajesh Rajamani, Vehicle Dynamics and Control Mechanical Engineering Series
## Code
- [sync post/online](https://github.com/TuSimple/LPS/blob/gt_tester/src/lps_test/gt_location_tester.py)
## Specs
- [The installation of IMU, and antenna.](https://docs.google.com/document/d/13KUritaB8zh45BmRR9_RFGHbJ8yspQYtlBqInEth6e0/edit#heading=h.wpujf9av13p3)
