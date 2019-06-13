# Bags
	- 2018-10-13-10-05-07

# Notes
- dataset visualization and analysis
	- octopus
	- fetch
	- middleware and ros
- observations
	- velocity
		- GNSS (freq may be too low)
	- heading and roll
		- dual-antenna
	- steering angle, etc.

# Todo
- 1. take a look at the output results and status code of Novatel system.
	- [x] quick play of bag and view azimuth vs. ground speed
  - [x] whole trip play, focus on ground speed, azimuth, heading, INS status, Pos type
- 2. find a solution to get heading or sideslip without drift
	- [x] use fetch data to view heading, azimuth, ins status, pos type
	- [x] try to get heading from "heading" WHEN heading is valid.
	- [x] try to get robust heading by sensor fusion.

- quick look at the bag
- extract relevant topics/messages??
- build a benchmark dataset??
- find and develop a basic algorithm for sideslip angle estimation??

# Code resources
- https://github.com/TuSimple/infra-dataset-store/blob/release/samples/basic_usage.py
- https://github.com/TuSimple/octopus-middleware

# Conclusion
- The built-in sensor fusion results should provide accurate heading and ground speed.
- The raw heading and ground speed may not support direct computing of sideslip.
- topics to use:
	- INSSPD
		- Trk gnd
		- Status (INS status)
	- INSPVAX
		- Azimuth
		- Azimuth sigma (check whether accurate)
		- INS status, Pos Type, Ext sol stat
- Current solutison:
	- Use Novatel fusion results.
	- Monitor the working status.
	- Consider further calibrations/estimation of relevant parameters, such as road tilting angle.

# Analysis:
- Issue: The ground speed diverges when the truck stops. 
	- Sideslip may be unavailable when stationary??
	- Can be seen from status code?
- Issue: ground track always has same offest symbol to azimuth
	- There is a constant offset??
	- One of the angle computation is wrong??
