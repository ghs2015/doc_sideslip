# Requirements:
Questions interested in:
1. [ ] What is relationship between lever arm errors and pose errors?
	- [x] Any existing reference?
		- [x] Documents and manuals.
		- [x] papers
	- [ ] `experiment` Using post-processing, for B4, how does the azimuth std and azimuth/track_ground difference change given different setting of lever arm?
		- `note` use a segment where GNSS signal is good.
		- `note` use PPP instead of Differential GNSS
		- review in/out novatel performance and mounting position 
	- [ ] `experiment` By modeling and simulation?
2. [ ] Can we improve the pose estimation accuary by using more accurate lever arm?
3. [ ] If we can, how to obtain more accurate lever arms?
	- [ ] Is it possible using postprocess software to estimate accurate leverarm?
		- probably not, the correction is withing the software's estimation precision.

# Log
## preprocessing checks
	- comparison between offset changes
## solve lever arms
### single time
- B4
	- 2018-10-05-10-46-36 
		- comparison among input offset and two directional solved offsets
### iteratively

## process without preprocessing

## process
	- Esimated heading accuracy (this is a important measure, which should be compared between cars and tracks.)
	![estimated heading accuracy](images/toadd)
	- Estimated position accuracy can be compared with difference between lever arm solved result and preset values.
	- IMU heading COG difference is useful.
	- There seems to be an offset of lateral speed.

# experiments:
- solve lever arm
	- same vehicle with multiple iterations of solving
	- car and truck with a single solving

# Questions:
	- [ ] preprocessing checks, the IMU to Antenna offset and vehicle-to-imu rotation is slightly different from before-check
		- [ ] [preprocessing checks](https://docs.novatel.com/Waypoint/Content/Utilities/Pre-processing_Checks.htm)
	- [ ] what is the profile file, use??

# Reference
	- data path "file:///mnt/truenas/scratch/yiluo/novatel_post/localization_benchmark/novatel_log"
	- [dataset description table](https://docs.google.com/spreadsheets/d/1v93qTb2Nwn7DREK33cBAvTctEAT8BQdINWMPoRmNxwE/edit?ts=5ce33355#gid=0)
	- [waypoint 8.80 user guide](https://www.novatel.com/assets/Documents/Waypoint/Waypoint-Software-User-Manual-OM-20000166.pdf)
		- 5.3.2 pre-processing checks
		- maps of stations (https://www.google.com/maps/d/u/0/viewer?mid=13Q9IzEQJ5BWNZDGGYCPxeYDM-4dPh9An&ll=32.254595842716746%2C-110.92956037343276&z=13)
