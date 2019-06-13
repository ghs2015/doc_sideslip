# Summary:
- The best estimation of the sideslip angle in hand is the difference between `inspvax.azimuth` and `insspd.track_ground`.

- The above difference does indicate the sideslip angle, although there are some limitations:
	- sideslip seems not obvious (< 1 deg) when small cornering (< 30 deg)
	- sideslip seems obvious (0 to 10 deg) when significant cornering (> 90 deg)
	- track ground is not robust when the truck stops. 
	- 10.0 and more degrees sideslip angle could be normal

- The heading information performs similarly comparing with azimuth.
	- Heading is not robust as fusion results.
	- Simply applying an offset works for two bags from different days but not working for another.

- Some tricks and observations:
	- Monitor the status words can eliminate abnormal data: position type, ins status.
	- When passing under the bridge, heading from dual antenna heaviliy degrades.
	- There is an offset between azimuth and track ground. The offset is relatively stable for each trip.
	- Track ground is a fused result, while gnss's trk gnd is a raw observation.

# Select bags and associated segmentation
``` python
# all from B4 truck
straigt_datasets = ['2018-10-13-10-05-07', 
                    '2018-10-11-07-17-22', 
                    '2018-10-13-13-44-38',
                    '2019-05-13-15-50-55', 
                    '2019-05-14-15-37-09', 
                    '2019-05-14-15-53-39', 
                    '2019-05-14-18-01-39',
                    '2019-05-14-13-35-32'
                   ]  

straigt_timeslots = [[('11:00', '12:40'), ('14:50', '15:50'), ('28:50', '29:50'), ('40:50','41:20')], 
                     [('25:20', '27:20'), ('56:40', '58:20')],   
                     [('52:20', '54:00'), ('70:00', '71:20')], 
                     [('24:30', '26:30'), ('31:20', '33:00'), ('56:00', '57:20')], 
                     [('15:40', '16:20'), ('24:40', '25:20'), ('36:10', '37:00'), ('43:40', '44:30')], 
                     [('20:40', '22:40')], 
                     [('53:00', '57:40')], 
                     [('21:50', '26:30'), ('10:00', '40:30')]
                    ]

cornering_datasets = ['2018-10-13-10-05-07', 
                      '2018-10-11-07-17-22', 
                      '2018-10-13-13-44-38',
                      '2019-05-13-15-50-55', 
                      '2019-05-14-15-37-09', 
                      '2019-05-14-15-53-39', 
                      '2019-05-14-18-01-39',
                      '2019-05-14-13-35-32'
                     ]  # all from B4 truck

cornering_timeslots = [[('9:40', '10:50'), ('22:20', '22:50'), ('39:00', '39:20'), ('39:45', '40:10')], 
                       [('42:00', '43:40'), ('67:40', '69:00')],
                       [('67:20', '69:00'), ('69:20', '70:00')],
                       [('14:30', '15:00') , ('23:00', '24:50') , ('29:20', '31:20') , ('35:50', '37:00') , ('54:00', '55:30')], 
                       [('17:10', '18:40')], 
                       [('16:20', '18:00')], 
                       [('30:40', '31:30'), ('57:40', '58:50')], 
                       [('20:00', '21:40')]
                      ]
```

# Works done:
- 1. take a look at the output results and status code of Novatel system.
	- [x] quick play of bag and view azimuth vs. ground speed
  - [x] whole trip play, focus on ground speed, azimuth, heading, INS status, Pos type
- 2. find a solution to get heading or sideslip without drift
	- [x] use fetch data to view heading, azimuth, ins status, pos type
	- [x] try to get heading from "heading" WHEN heading is valid.
	- [x] try to get robust heading by sensor fusion.
- 3. select and plot straight and cornering trips.

# Possible future works:
- Use post processed data as the ground truth.
- Analyze the correlation between sideslip angle with other states, such attitude, roll rate, yaw rate, and etc.
- Discuss the data and required sideslip estimation accuracy with Zijie.
- Build a benchmark dataset and set up the regression tests.
- Consider further calibrations/estimation of relevant parameters, such as road tilting angle.

# Paper reference:
- Estimation of Sideslip Angle Based on Extended Kalman Filter
- Integrating INS Sensors With GPS Measurements for Continuous Estimation of Vehicle Sideslip, Roll, and Tire Cornering Stiffness, 2006
- Vehicle Sideslip Estimation, 2009
- A Cost-Effective Sideslip Estimation MethodUsing Velocity Measurements from Two GPSReceivers, 2013
- Robust Vehicle Sideslip Estimation Based on Kinematic Considerations, 2017
- Vehicle sideslip estimation: A kinematic based approach, 2017
- On the Vehicle Sideslip Angle Estimation:A Literature Review of Methods, Models,and Innovations, 2018
