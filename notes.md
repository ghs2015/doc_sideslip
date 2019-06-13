# Requirements
- estimation of sideslip
	- evalutation metrics:
		- emperically
			- sideslip angle estimation during forwarding, short term and long term

# Questions
- How to get the ground truth?
- How to evaluate the estimation accuary?
- What are basic methods? observer-based and ANN-based
- How does the paper (dual antenna) use the observations?

# Notes
- observations: dual antenna, trajectory, Novatel (inspvas, insspd? IN USE)
- ground truth: 1) post process (available). 2) mannual observation.
- Novatel performs instable for the truch compared with cars.
- Possible solutions:
	- IMU and GPS with dual antenna 
		- method level: OK
		- implementation level: to verify and evaluate

- hardware
	- propak6, propak7
  - 现在卡车B3/B4装得IMU是imu-igm-s1
	- https://www.novatel.com/products/gnss-receivers/enclosures/pwrpak7/propak7的手册在那个网里可以找到

# Todo:
- [ ] collect related reference
	- [x] some most relevant papers
	- [ ] 
- [ ] analyze the data
  - without postprocessing
		- 2018-10-13-10-05-07
	- with postprocessing
- [ ] evaluate the estimation performance from Novatel

# Paper reference:
- Estimation of Sideslip Angle Based on Extended Kalman Filter
- [ ] Integrating INS Sensors With GPS Measurements for Continuous Estimation of Vehicle Sideslip, Roll, and Tire Cornering Stiffness, 2006
- Vehicle Sideslip Estimation, 2009
- A Cost-Effective Sideslip Estimation MethodUsing Velocity Measurements from Two GPSReceivers, 2013
- Robust Vehicle Sideslip Estimation Based on Kinematic Considerations, 2017
- Vehicle sideslip estimation: A kinematic based approach, 2017
- [ ] On the Vehicle Sideslip Angle Estimation:A Literature Review of Methods, Models,and Innovations, 2018
