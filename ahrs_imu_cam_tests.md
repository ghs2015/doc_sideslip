

## TODO

- [x] Fix the velocity inconsistency issue.
- [ ] Add accuracy print.
- [ ] Add camera observation interface.
- [ ] Test multiple key frames.

## Motion profiles

- `ts_motion_def_two_laps_ned.csv`
- `ts_motion_def_two_circles_ned.csv`
- `ts_motion_def_long_drive_ned.csv`

## Tests (NED, various motions)

#### Constant velocity `Vx=25m/s`
##### Without noises

```
/home/xiang.zhang/gitRepo/sensor-fusion-navigation-v3/bin/test_simulated_imu_factor
skip the header
Loaded 126 frames.
loaded 126 frames
the first frame data 
=====frameINFO=====
======IMUData=====
 imu ts: 0
acc:         0 -0.001906    -9.794
gyro:  6.217e-05 -3.935e-06 -3.811e-05
======CamData=====
 cam ts: 0
position: 31.51 120.4 -1.91
quaternion qw, qx, qy, qz: 1 -0.006604 0.004749 0.005157
======CamData=====
 cam ts: 0
position:  31.51  120.4 -2.295
quaternion qw, qx, qy, qz: 0.9998 0.008638 0.01899 -0.00318
======CamData=====
 cam ts: 0
position:  31.51  120.4 -2.757
quaternion qw, qx, qy, qz: 0.9998 -0.01743 0.005144 -0.005392
======PVAX=====
 imu state ts: 0
position lat, lon, alt: 31.51 120.4     0
velocity: 25  0  0
quaternion qw, qx, qy, qz: 1 0 0 0


the second frame data 
=====frameINFO=====
======IMUData=====
 imu ts: 1
acc:         0 -0.001906    -9.794
gyro:  6.217e-05 -3.935e-06 -3.811e-05
======CamData=====
 cam ts: 1
position:  31.51  120.4 -1.952
quaternion qw, qx, qy, qz: 0.9999 -0.007623 0.004841 0.005743
======CamData=====
 cam ts: 1
position:  31.51  120.4 -2.309
quaternion qw, qx, qy, qz: 0.9998 0.009209 0.0176 -0.003991
======CamData=====
 cam ts: 1
position:  31.51  120.4 -2.873
quaternion qw, qx, qy, qz: 0.9998 -0.01633 0.004613 -0.003581
======PVAX=====
 imu state ts: 1
position lat, lon, alt: 31.51 120.4     0
velocity: 25  0  0
quaternion qw, qx, qy, qz: 1 0 0 0


pose_params[0]
-2.754e+06,4.694e+06,3.314e+06,-0.7572,0.4336,-0.424,-0.2428,
pose_params[1]
-2.754e+06,4.694e+06,3.314e+06,-0.7572,0.4336,-0.424,-0.2428,
speedbias_params[0]
6.612,-11.27,21.31,0,0,0,0,0,0,
speedbias_params[1]
6.612,-11.27,21.31,0,0,0,0,0,0,
pre_integ evaluation result:
 0.0002432
 0.0005389
 0.0001928
-6.217e-05
-3.474e-16
 3.811e-05
 0.0004801
 0.0009763
 0.0003856
         0
         0
         0
         0
         0
         0
iter      cost      cost_change  |gradient|   |step|    tr_ratio  tr_radius  ls_iter  iter_time  total_time
   0  3.015925e-02    0.00e+00    1.01e+02   0.00e+00   0.00e+00  1.00e+04        0    3.13e-04    4.21e-04
   1  1.047392e-08    3.02e-02    1.57e-02   1.31e-03   1.00e+00  3.00e+04        1    1.62e-04    6.06e-04
pose_params[0]
-2.754e+06,4.694e+06,3.314e+06,-0.7572,0.4336,-0.424,-0.2428,
pose_params[1]
-2.754e+06,4.694e+06,3.314e+06,-0.7572,0.4336,-0.424,-0.2428,
speedbias_params[0]
6.612,-11.27,21.31,0,0,0,0,0,0,
speedbias_params[1]
6.613,-11.27,21.31,-2.831e-11,-5.903e-11,-2.281e-11,-9.457e-13,8.428e-13,-3.781e-13,
after optimization, pre_integ evaluation result:
  2.28e-07
 4.681e-07
 1.537e-07
 2.109e-08
-1.399e-08
 3.814e-09
 4.293e-07
  8.62e-07
 2.687e-07
         0
         0
         0
         0
         0
         0

Solver Summary (v 1.14.0-eigen-(3.2.92)-lapack-suitesparse-(4.4.6)-cxsparse-(3.1.4)-eigensparse-openmp-no_tbb)

                                     Original                  Reduced
Parameter blocks                            4                        2
Parameters                                 32                       16
Effective parameters                       30                       15
Residual blocks                             1                        1
Residuals                                  15                       15

Minimizer                        TRUST_REGION

Sparse linear algebra library    SUITE_SPARSE
Trust region strategy     LEVENBERG_MARQUARDT

                                        Given                     Used
Linear solver          SPARSE_NORMAL_CHOLESKY   SPARSE_NORMAL_CHOLESKY
Threads                                     1                        1
Linear solver ordering              AUTOMATIC                        2

Cost:
Initial                          3.015925e-02
Final                            1.047392e-08
Change                           3.015924e-02

Minimizer iterations                        2
Successful steps                            2
Unsuccessful steps                          0

Time (in seconds):
Preprocessor                         0.000108

  Residual only evaluation           0.000046 (2)
  Jacobian & residual evaluation     0.000074 (2)
  Linear solver                      0.000076 (2)
Minimizer                            0.000578

Postprocessor                        0.000009
Total                                0.000695

Termination:                      CONVERGENCE (Parameter tolerance reached. Relative step_norm: 1.784988e-13 <= 1.000000e-08.)


Process finished with exit code 0

```

##### With noises

```c++
============ Process /mnt/truenas/scratch/xiang.zhang/imu_cam_two_laps_ned.csvwith noise flag: 1
skip the header
Loaded 126 frames.
loaded 126 frames
the first frame data 
=====frameINFO=====
======IMUData=====
 imu ts: 0
acc: 0.0004015 -0.001501    -9.794
gyro: -0.0007573  0.0002326 -0.0001503
======CamData=====
 cam ts: 0
position: 31.51 120.4 -1.91
quaternion qw, qx, qy, qz: 1 -0.006604 0.004749 0.005157
======CamData=====
 cam ts: 0
position:  31.51  120.4 -2.295
quaternion qw, qx, qy, qz: 0.9998 0.008638 0.01899 -0.00318
======CamData=====
 cam ts: 0
position:  31.51  120.4 -2.757
quaternion qw, qx, qy, qz: 0.9998 -0.01743 0.005144 -0.005392
======PVAX=====
 imu state ts: 0
position lat, lon, alt: 31.51 120.4     0
velocity: 25  0  0
quaternion qw, qx, qy, qz: 1 0 0 0


the second frame data 
=====frameINFO=====
======IMUData=====
 imu ts: 1
acc: 0.0004413 -0.001504    -9.794
gyro:  0.0002389 -0.0004143  -0.001059
======CamData=====
 cam ts: 1
position:  31.51  120.4 -1.952
quaternion qw, qx, qy, qz: 0.9999 -0.007623 0.004841 0.005743
======CamData=====
 cam ts: 1
position:  31.51  120.4 -2.309
quaternion qw, qx, qy, qz: 0.9998 0.009209 0.0176 -0.003991
======CamData=====
 cam ts: 1
position:  31.51  120.4 -2.873
quaternion qw, qx, qy, qz: 0.9998 -0.01633 0.004613 -0.003581
======PVAX=====
 imu state ts: 1
position lat, lon, alt: 31.51 120.4     0
velocity: 25  0  0
quaternion qw, qx, qy, qz: 1 0 0 0


pose_params[0]
-2.754e+06,4.694e+06,3.314e+06,-0.7572,0.4336,-0.424,-0.2428,
pose_params[1]
-2.754e+06,4.694e+06,3.314e+06,-0.7572,0.4336,-0.424,-0.2428,
speedbias_params[0]
6.612,-11.27,21.31,0,0,0,0,0,0,
speedbias_params[1]
6.612,-11.27,21.31,0,0,0,0,0,0,
pre_integ evaluation result:
-5.996e-06
 0.0004086
 1.765e-06
-6.811e-05
 2.202e-05
 7.948e-05
-0.0001379
 0.0006861
 2.444e-06
         0
         0
         0
         0
         0
         0
iter      cost      cost_change  |gradient|   |step|    tr_ratio  tr_radius  ls_iter  iter_time  total_time
   0  2.665952e-02    0.00e+00    1.04e+02   0.00e+00   0.00e+00  1.00e+04        0    4.69e-05    7.57e-05
   1  4.109106e-09    2.67e-02    1.14e-02   8.11e-04   1.00e+00  3.00e+04        1    7.67e-05    1.65e-04
pose_params[0]
-2.754e+06,4.694e+06,3.314e+06,-0.7572,0.4336,-0.424,-0.2428,
pose_params[1]
-2.754e+06,4.694e+06,3.314e+06,-0.7572,0.4336,-0.424,-0.2428,
speedbias_params[0]
6.612,-11.27,21.31,0,0,0,0,0,0,
speedbias_params[1]
6.613,-11.27,21.31,5.501e-12,-4.254e-11,-2.921e-13,-3.747e-13,-4.611e-13,-7.883e-13,
after optimization, pre_integ evaluation result:
-3.987e-08
 3.364e-07
 2.244e-09
 1.217e-08
  5.58e-09
 7.948e-09
-8.837e-08
 6.107e-07
 3.461e-09
         0
         0
         0
         0
         0
         0

Solver Summary (v 1.14.0-eigen-(3.2.92)-lapack-suitesparse-(4.4.6)-cxsparse-(3.1.4)-eigensparse-openmp-no_tbb)

                                     Original                  Reduced
Parameter blocks                            4                        2
Parameters                                 32                       16
Effective parameters                       30                       15
Residual blocks                             1                        1
Residuals                                  15                       15

Minimizer                        TRUST_REGION

Sparse linear algebra library    SUITE_SPARSE
Trust region strategy     LEVENBERG_MARQUARDT

                                        Given                     Used
Linear solver          SPARSE_NORMAL_CHOLESKY   SPARSE_NORMAL_CHOLESKY
Threads                                     1                        1
Linear solver ordering              AUTOMATIC                        2

Cost:
Initial                          2.665952e-02
Final                            4.109106e-09
Change                           2.665951e-02

Minimizer iterations                        2
Successful steps                            2
Unsuccessful steps                          0

Time (in seconds):
Preprocessor                         0.000029

  Residual only evaluation           0.000027 (2)
  Jacobian & residual evaluation     0.000034 (2)
  Linear solver                      0.000038 (2)
Minimizer                            0.000183

Postprocessor                        0.000004
Total                                0.000215

Termination:                      CONVERGENCE (Parameter tolerance reached. Relative step_norm: 1.104145e-13 <= 1.000000e-08.)

```




#### Cornering `3 deg/s`
##### Without noises
```c++
============ Process /mnt/truenas/scratch/xiang.zhang/imu_cam_two_circles_ned.csvwith noise flag: 0
skip the header
Loaded 126 frames.
loaded 126 frames
the first frame data 
=====frameINFO=====
======IMUData=====
 imu ts: 0
acc:      0  0.129 -9.794
gyro:  6.217e-05 -3.935e-06   0.005198
======CamData=====
 cam ts: 0
position:  31.51  120.4 -1.783
quaternion qw, qx, qy, qz: 0.9999 -0.008621 0.006169 0.004459
======CamData=====
 cam ts: 0
position:  31.51  120.4 -2.329
quaternion qw, qx, qy, qz: 0.9998 0.008237 0.01819 -0.003225
======CamData=====
 cam ts: 0
position:  31.51  120.4 -2.774
quaternion qw, qx, qy, qz: 0.9998 -0.0165 0.004973 -0.004706
======PVAX=====
 imu state ts: 0
position lat, lon, alt: 31.51 120.4     0
velocity: 25  0  0
quaternion qw, qx, qy, qz: 1 0 0 0


the second frame data 
=====frameINFO=====
======IMUData=====
 imu ts: 1
acc:      0  1.307 -9.794
gyro:   6.21e-05 -6.955e-06    0.05232
======CamData=====
 cam ts: 1
position:  31.51  120.4 -1.875
quaternion qw, qx, qy, qz: 0.9995 -0.008371 0.005399 0.02991
======CamData=====
 cam ts: 1
position:  31.51  120.4 -2.338
quaternion qw, qx, qy, qz: 0.9996 0.009432 0.01828 0.02142
======CamData=====
 cam ts: 1
position:  31.51  120.4 -2.742
quaternion qw, qx, qy, qz: 0.9996 -0.01707 0.005748 0.02041
======PVAX=====
 imu state ts: 1
position lat, lon, alt: 31.51 120.4     0
velocity: 25  0  0
quaternion qw, qx, qy, qz: 0.9997 0 0 0.02429


pose_params[0]
-2.754e+06,4.694e+06,3.314e+06,-0.7572,0.4336,-0.424,-0.2428,
pose_params[1]
-2.754e+06,4.694e+06,3.314e+06,-0.7675,0.4151,-0.4179,-0.253,
speedbias_params[0]
6.612,-11.27,21.31,0,0,0,0,0,0,
speedbias_params[1] //??
6.612,-11.27,21.31,0,0,0,0,0,0,
pre_integ evaluation result:
 0.0004466
 -0.008671
 0.0001575
-6.217e-05
-5.004e-09
  -0.09729
   0.03015
    -1.218
 0.0002748
         0
         0
         0
         0
         0
         0
iter      cost      cost_change  |gradient|   |step|    tr_ratio  tr_radius  ls_iter  iter_time  total_time
   0  8.236225e+04    0.00e+00    1.53e+05   0.00e+00   0.00e+00  1.00e+04        0    4.64e-05    7.37e-05
   1  3.948162e-03    8.24e+04    1.04e+01   1.22e+00   1.00e+00  3.00e+04        1    7.55e-05    1.62e-04
pose_params[0]
-2.754e+06,4.694e+06,3.314e+06,-0.7572,0.4336,-0.424,-0.2428,
pose_params[1]
-2.754e+06,4.694e+06,3.314e+06,-0.7464,0.4519,-0.4298,-0.2324,
speedbias_params[0]
6.612,-11.27,21.31,0,0,0,0,0,0,
speedbias_params[1]
5.554,-11.87,21.29,3.565e-10,4.764e-08,5.874e-11,1.547e-09,1.315e-12,9.676e-10,
after optimization, pre_integ evaluation result:
 9.267e-06
-0.0002994
-7.724e-06
 -2.35e-05
 5.845e-07
-9.745e-06
 2.153e-05
-0.0006355
-2.081e-05
         0
         0
         0
         0
         0
         0

Solver Summary (v 1.14.0-eigen-(3.2.92)-lapack-suitesparse-(4.4.6)-cxsparse-(3.1.4)-eigensparse-openmp-no_tbb)

                                     Original                  Reduced
Parameter blocks                            4                        2
Parameters                                 32                       16
Effective parameters                       30                       15
Residual blocks                             1                        1
Residuals                                  15                       15

Minimizer                        TRUST_REGION

Sparse linear algebra library    SUITE_SPARSE
Trust region strategy     LEVENBERG_MARQUARDT

                                        Given                     Used
Linear solver          SPARSE_NORMAL_CHOLESKY   SPARSE_NORMAL_CHOLESKY
Threads                                     1                        1
Linear solver ordering              AUTOMATIC                        2

Cost:
Initial                          8.236225e+04
Final                            3.948162e-03
Change                           8.236225e+04

Minimizer iterations                        2
Successful steps                            2
Unsuccessful steps                          0

Time (in seconds):
Preprocessor                         0.000027

  Residual only evaluation           0.000028 (2)
  Jacobian & residual evaluation     0.000036 (2)
  Linear solver                      0.000037 (2)
Minimizer                            0.000182

Postprocessor                        0.000003
Total                                0.000213

Termination:                      CONVERGENCE (Parameter tolerance reached. Relative step_norm: 1.103424e-10 <= 1.000000e-08.)
```





##### With noises

```c++
============ Process /mnt/truenas/scratch/xiang.zhang/imu_cam_two_circles_ned.csvwith noise flag: 1
skip the header
Loaded 126 frames.
loaded 126 frames
the first frame data 
=====frameINFO=====
======IMUData=====
 imu ts: 0
acc: 0.0003989    0.1294    -9.794
gyro: -0.0004495  0.0001901   0.005234
======CamData=====
 cam ts: 0
position:  31.51  120.4 -1.783
quaternion qw, qx, qy, qz: 0.9999 -0.008621 0.006169 0.004459
======CamData=====
 cam ts: 0
position:  31.51  120.4 -2.329
quaternion qw, qx, qy, qz: 0.9998 0.008237 0.01819 -0.003225
======CamData=====
 cam ts: 0
position:  31.51  120.4 -2.774
quaternion qw, qx, qy, qz: 0.9998 -0.0165 0.004973 -0.004706
======PVAX=====
 imu state ts: 0
position lat, lon, alt: 31.51 120.4     0
velocity: 25  0  0
quaternion qw, qx, qy, qz: 1 0 0 0


the second frame data 
=====frameINFO=====
======IMUData=====
 imu ts: 1
acc: 0.0003366     1.307    -9.794
gyro: -0.0002049  0.0001968    0.05197
======CamData=====
 cam ts: 1
position:  31.51  120.4 -1.875
quaternion qw, qx, qy, qz: 0.9995 -0.008371 0.005399 0.02991
======CamData=====
 cam ts: 1
position:  31.51  120.4 -2.338
quaternion qw, qx, qy, qz: 0.9996 0.009432 0.01828 0.02142
======CamData=====
 cam ts: 1
position:  31.51  120.4 -2.742
quaternion qw, qx, qy, qz: 0.9996 -0.01707 0.005748 0.02041
======PVAX=====
 imu state ts: 1
position lat, lon, alt: 31.51 120.4     0
velocity: 25  0  0
quaternion qw, qx, qy, qz: 0.9997 0 0 0.02429


pose_params[0]
-2.754e+06,4.694e+06,3.314e+06,-0.7572,0.4336,-0.424,-0.2428,
pose_params[1]
-2.754e+06,4.694e+06,3.314e+06,-0.7675,0.4151,-0.4179,-0.253,
speedbias_params[0]
6.612,-11.27,21.31,0,0,0,0,0,0,
speedbias_params[1]
6.612,-11.27,21.31,0,0,0,0,0,0,
pre_integ evaluation result:
 0.0003523
 -0.008925
-5.339e-05
 -9.69e-05
-4.053e-05
  -0.09727
   0.03003
    -1.219
-0.0001747
         0
         0
         0
         0
         0
         0
iter      cost      cost_change  |gradient|   |step|    tr_ratio  tr_radius  ls_iter  iter_time  total_time
   0  8.237536e+04    0.00e+00    1.53e+05   0.00e+00   0.00e+00  1.00e+04        0    3.88e-05    6.01e-05
   1  3.954556e-03    8.24e+04    1.04e+01   1.22e+00   1.00e+00  3.00e+04        1    7.18e-05    1.43e-04
pose_params[0]
-2.754e+06,4.694e+06,3.314e+06,-0.7572,0.4336,-0.424,-0.2428,
pose_params[1]
-2.754e+06,4.694e+06,3.314e+06,-0.7464,0.4519,-0.4298,-0.2324,
speedbias_params[0]
6.612,-11.27,21.31,0,0,0,0,0,0,
speedbias_params[1]
5.554,-11.87,21.29,3.646e-10,4.768e-08,8.264e-11,1.549e-09,1.618e-12,9.675e-10,
after optimization, pre_integ evaluation result:
 9.205e-06
-0.0002997
-7.905e-06
-2.352e-05
 5.837e-07
-9.744e-06
 2.143e-05
 -0.000636
-2.114e-05
         0
         0
         0
         0
         0
         0

Solver Summary (v 1.14.0-eigen-(3.2.92)-lapack-suitesparse-(4.4.6)-cxsparse-(3.1.4)-eigensparse-openmp-no_tbb)

                                     Original                  Reduced
Parameter blocks                            4                        2
Parameters                                 32                       16
Effective parameters                       30                       15
Residual blocks                             1                        1
Residuals                                  15                       15

Minimizer                        TRUST_REGION

Sparse linear algebra library    SUITE_SPARSE
Trust region strategy     LEVENBERG_MARQUARDT

                                        Given                     Used
Linear solver          SPARSE_NORMAL_CHOLESKY   SPARSE_NORMAL_CHOLESKY
Threads                                     1                        1
Linear solver ordering              AUTOMATIC                        2

Cost:
Initial                          8.237536e+04
Final                            3.954556e-03
Change                           8.237536e+04

Minimizer iterations                        2
Successful steps                            2
Unsuccessful steps                          0

Time (in seconds):
Preprocessor                         0.000021

  Residual only evaluation           0.000027 (2)
  Jacobian & residual evaluation     0.000032 (2)
  Linear solver                      0.000034 (2)
Minimizer                            0.000169

Postprocessor                        0.000003
Total                                0.000194

Termination:                      CONVERGENCE (Parameter tolerance reached. Relative step_norm: 1.104371e-10 <= 1.000000e-08.)

```



#### With Cam

motion profile: static
motion profile: `ts_motion_def_two_circles_ned.csv`
motion profile: `ts_motion_def_two_laps_ned.csv`
motion profile: `ts_motion_def-long_drive_ned.csv`

##### Without noises
##### With noises