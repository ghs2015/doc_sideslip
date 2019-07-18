## todo
- refactor a little
- generate cam NED
- test cam factor
- test imu cam calibration

## maybe
- C++ auto format
- C++ code checker

## notes
- csv -> c++ -> corresponding objects (frame or imu??)
- [x] write code to load csv data.
	- use a single csv file to store all the data, fetch whatever you want
- [x] write a test case for simu.csv loading.
- [x] quickly read test case: test cam pose factor.cpp
- [x] csv data to frame or key frame

## Inbox
- [ ] recap quaternion

## archived
- [x] Use quaterion representation.
	- [x] Change the data simulator side.
		- [x] extract only needed columns
		- [x] convert all NED to ENU
		- [x] add quaterion to all attitude
	- [x] Generate a new data sheet.
	- [x] Change the C++ data loading side. 0.5 - 1 hr
- [x] Write IMUState class and add to Frame's attributes 1 hr
- [x] Write Pvax class and add to Frame's attr to store ground truth. 0.5 hr
- [x] merge CamDataabc to a vector 0.5 hr
- [x] associate CamData with its calib info 0.5~1.0 hr
- [x] debug ~1.5 hr

- [x] Move CSV reader to IOutils 1.0 hr

