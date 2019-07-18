## TODO
### high priority

### low priority
- [ ]  Where is the generation code of accel ref?

### items to implement

### Code analysis
- `IntegrationBase`
	- [ ] bias handling.
- `IMUFactor`
- `test_imu_and_cam_pose_factor.cpp`

## Archived
- [x] fix the ENU2ECEF conversion.
- [x] `IO_utils.h`
- [x] Cam alt == lon??
- [x] debug `test_simulated_imu_factor.cpp'
- [x] check the parameter changes
- [x] read IMU data into the test script
	- [x] check the reference frame consistency
- [x] `test_initial_pose_factor`

## debug log

### results -001 for debug

![1562782106978](/home/xiang.zhang/gitRepo/project/doc_sideslip/plots/1562782106978.png)

![1562782121621](/home/xiang.zhang/gitRepo/project/doc_sideslip/plots/1562782121621.png)



![1562782149690](/home/xiang.zhang/gitRepo/project/doc_sideslip/plots/1562782149690.png)

### analysis

- the ecef position is wrong.

### results -002 for debug

```/home/xiang.zhang/gitRepo/sensor-fusion-navigation-v3/bin/test_simulated_imu_factor
skip the header
Loaded 30 frames.
loaded 30 frames
the first frame data 
=====frameINFO=====
======IMUData=====
 imu ts: 0
acc:  0.007047 -0.002631     9.798
gyro:  0.2373  0.1324 0.04544
======CamData=====
 cam ts: 0
position: 31.51 120.4 31.51
quaternion qw, qx, qy, qz: 0.9999 0.00561 0.009757 0.005156
======CamData=====
 cam ts: 0
position: 31.51 120.4 31.51
quaternion qw, qx, qy, qz: 0.9999 0.004775 0.009194 0.005355
======CamData=====
 cam ts: 0
position: 31.51 120.4 31.51
quaternion qw, qx, qy, qz: 0.9999 0.00428 0.01058 0.002985
======PVAX=====
 imu state ts: 0
position lat, lon, alt: 31.51 120.4     0
velocity:  0 25 -0
quaternion qw, qx, qy, qz: 1 0 0 0


the second frame data 
=====frameINFO=====
======IMUData=====
 imu ts: 0.232
acc:   0.01256 -0.003829     9.789
gyro: 0.009862  0.03137  -0.1756
======CamData=====
 cam ts: 0.232
position: 31.51 120.4 31.51
quaternion qw, qx, qy, qz: 0.9999 0.005807 0.01059 0.006587
======CamData=====
 cam ts: 0.232
position: 31.51 120.4 31.51
quaternion qw, qx, qy, qz: 0.9999 0.003642 0.009409 0.004289
======CamData=====
 cam ts: 0.232
position: 31.51 120.4 31.51
quaternion qw, qx, qy, qz: 0.9999 0.004893 0.008378 0.00439
======PVAX=====
 imu state ts: 0.232
position lat, lon, alt: 31.51 120.4     0
velocity:  0 25 -0
quaternion qw, qx, qy, qz: 1 0 0 0


pose_params[0]
6.374e+06,2.339e+05,6.081e+04,-0.1281,0.4715,0.842,-0.2288,
pose_params[1]
6.374e+06,2.339e+05,6.081e+04,-0.1281,0.4715,0.842,-0.2288,
speedbias_params[0]
6.612,-11.27,21.31,0,0,0,0,0,0,
speedbias_params[1]
6.612,-11.27,21.31,0,0,0,0,0,0,
iter      cost      cost_change  |gradient|   |step|    tr_ratio  tr_radius  ls_iter  iter_time  total_time
   0  3.932426e+08    0.00e+00    1.16e+08   0.00e+00   0.00e+00  1.00e+04        0    3.18e-04    4.28e-04
   1  3.042781e+02    3.93e+08    8.87e+04   1.54e+01   1.00e+00  3.00e+04        1    1.89e-04    6.39e-04
pose_params[0]
6.374e+06,2.339e+05,6.08e+04,-0.1281,0.4719,0.8418,-0.2287,
pose_params[1]
6.374e+06,2.339e+05,6.081e+04,-0.1298,0.4722,0.842,-0.2262,
speedbias_params[0]
4.261,-7.264,10.63,4.728e-07,8.994e-05,0.0001611,2.748e-06,7.829e-09,-1.277e-07,
speedbias_params[1]
3.282,-5.597,14.1,4.728e-07,8.991e-05,0.0001611,2.748e-06,7.829e-09,-1.277e-07,

Solver Summary (v 1.14.0-eigen-(3.2.92)-lapack-suitesparse-(4.4.6)-cxsparse-(3.1.4)-eigensparse-openmp-no_tbb)

                                     Original                  Reduced
Parameter blocks                            4                        4
Parameters                                 32                       32
Effective parameters                       30                       30
Residual blocks                             1                        1
Residuals                                  15                       15

Minimizer                        TRUST_REGION

Sparse linear algebra library    SUITE_SPARSE
Trust region strategy     LEVENBERG_MARQUARDT

                                        Given                     Used
Linear solver          SPARSE_NORMAL_CHOLESKY   SPARSE_NORMAL_CHOLESKY
Threads                                     1                        1
Linear solver ordering              AUTOMATIC                        4

Cost:
Initial                          3.932426e+08
Final                            3.042781e+02
Change                           3.932423e+08

Minimizer iterations                        2
Successful steps                            2
Unsuccessful steps                          0

Time (in seconds):
Preprocessor                         0.000110

  Residual only evaluation           0.000049 (2)
  Jacobian & residual evaluation     0.000080 (2)
  Linear solver                      0.000120 (2)
Minimizer                            0.000637

Postprocessor                        0.000010
Total                                0.000757

Termination:                      CONVERGENCE (Parameter tolerance reached. Relative step_norm: 1.499279e-09 <= 1.000000e-08.)


Process finished with exit code 0
```

### analysis

- enu to ecef conversion is wrong.

### Results -003 simulated imu without noise

```
/home/xiang.zhang/gitRepo/sensor-fusion-navigation-v3/bin/test_simulated_imu_factor
skip the header
Loaded 30 frames.
loaded 30 frames
the first frame data 
=====frameINFO=====
======IMUData=====
 imu ts: 0
acc: -0.001906         0     9.794
gyro: -3.935e-06  6.217e-05  3.811e-05
======CamData=====
 cam ts: 0
position: 31.51 120.4 31.51
quaternion qw, qx, qy, qz: 0.9999 0.00561 0.009757 0.005156
======CamData=====
 cam ts: 0
position: 31.51 120.4 31.51
quaternion qw, qx, qy, qz: 0.9999 0.004775 0.009194 0.005355
======CamData=====
 cam ts: 0
position: 31.51 120.4 31.51
quaternion qw, qx, qy, qz: 0.9999 0.00428 0.01058 0.002985
======PVAX=====
 imu state ts: 0
position lat, lon, alt: 31.51 120.4     0
velocity:  0 25 -0
quaternion qw, qx, qy, qz: 1 0 0 0


the second frame data 
=====frameINFO=====
======IMUData=====
 imu ts: 0.232
acc: -0.001906         0     9.794
gyro: -3.935e-06  6.217e-05  3.811e-05
======CamData=====
 cam ts: 0.232
position: 31.51 120.4 31.51
quaternion qw, qx, qy, qz: 0.9999 0.005807 0.01059 0.006587
======CamData=====
 cam ts: 0.232
position: 31.51 120.4 31.51
quaternion qw, qx, qy, qz: 0.9999 0.003642 0.009409 0.004289
======CamData=====
 cam ts: 0.232
position: 31.51 120.4 31.51
quaternion qw, qx, qy, qz: 0.9999 0.004893 0.008378 0.00439
======PVAX=====
 imu state ts: 0.232
position lat, lon, alt: 31.51 120.4     0
velocity:  0 25 -0
quaternion qw, qx, qy, qz: 1 0 0 0


pose_params[0]
-2.754e+06,4.694e+06,3.314e+06,0.1281,-0.4715,-0.842,-0.2288,
pose_params[1]
-2.754e+06,4.694e+06,3.314e+06,0.02821,-0.5029,-0.7106,-0.37,
speedbias_params[0]
6.612,-11.27,21.31,0,0,0,0,0,0,
speedbias_params[1]
20.13,-3.337,21.31,0,0,0,0,0,0,
pre_integ evaluation result:
 0.0001023
      -5.8
   -0.5276
  9.13e-07
-1.442e-05
-8.842e-06
 0.0004257
-1.035e-06
    -4.548
         0
         0
         0
         0
         0
         0
iter      cost      cost_change  |gradient|   |step|    tr_ratio  tr_radius  ls_iter  iter_time  total_time
   0  5.175437e+07    0.00e+00    3.73e+07   0.00e+00   0.00e+00  1.00e+04        0    2.35e-04    3.09e-04
   1  2.672273e+05    5.15e+07    2.40e+06   1.17e+01   9.95e-01  3.00e+04        1    1.29e-04    4.55e-04
   2  2.448889e+01    2.67e+05    2.60e+04   8.37e-01   1.00e+00  9.00e+04        1    9.15e-05    5.55e-04
pose_params[0]
-2.754e+06,4.694e+06,3.314e+06,0.1018,-0.4894,-0.829,-0.2506,
pose_params[1]
-2.754e+06,4.694e+06,3.314e+06,0.1018,-0.4894,-0.8291,-0.2505,
speedbias_params[0]
10.39,-9.983,19.61,0.0003944,0.0005575,-0.0001546,-1.223e-05,1.018e-05,4.58e-06,
speedbias_params[1]
10.55,-8.026,23.02,0.0003944,0.0005575,-0.0001546,-1.223e-05,1.018e-05,4.58e-06,

Solver Summary (v 1.14.0-eigen-(3.2.92)-lapack-suitesparse-(4.4.6)-cxsparse-(3.1.4)-eigensparse-openmp-no_tbb)

                                     Original                  Reduced
Parameter blocks                            4                        4
Parameters                                 32                       32
Effective parameters                       30                       30
Residual blocks                             1                        1
Residuals                                  15                       15

Minimizer                        TRUST_REGION

Sparse linear algebra library    SUITE_SPARSE
Trust region strategy     LEVENBERG_MARQUARDT

                                        Given                     Used
Linear solver          SPARSE_NORMAL_CHOLESKY   SPARSE_NORMAL_CHOLESKY
Threads                                     1                        1
Linear solver ordering              AUTOMATIC                        4

Cost:
Initial                          5.175437e+07
Final                            2.448889e+01
Change                           5.175434e+07

Minimizer iterations                        3
Successful steps                            3
Unsuccessful steps                          0

Time (in seconds):
Preprocessor                         0.000074

  Residual only evaluation           0.000048 (3)
  Jacobian & residual evaluation     0.000070 (3)
  Linear solver                      0.000123 (3)
Minimizer                            0.000559

Postprocessor                        0.000008
Total                                0.000640

Termination:                      CONVERGENCE (Parameter tolerance reached. Relative step_norm: 8.606015e-10 <= 1.000000e-08.)


Process finished with exit code 0

```

### Results -004 simulated imu without noise ecef conversion checked

```
/home/xiang.zhang/gitRepo/sensor-fusion-navigation-v3/bin/test_simulated_imu_factor
skip the header
Loaded 25 frames.
loaded 25 frames
the first frame data 
=====frameINFO=====
======IMUData=====
 imu ts: 0
acc: -0.001906         0     9.794
gyro: -3.935e-06  6.217e-05  3.811e-05
======CamData=====
 cam ts: 0
position: 31.51 120.4 31.51
quaternion qw, qx, qy, qz: 0.9999 0.005953 0.01016 0.005017
======CamData=====
 cam ts: 0
position: 31.51 120.4 31.51
quaternion qw, qx, qy, qz: 0.9999 0.004804 0.01014 0.005375
======CamData=====
 cam ts: 0
position: 31.51 120.4 31.51
quaternion qw, qx, qy, qz: 0.9999 0.004257 0.009494 0.004704
======PVAX=====
 imu state ts: 0
position lat, lon, alt: 31.51 120.4     0
velocity:  0 25 -0
quaternion qw, qx, qy, qz: 1 0 0 0


the second frame data 
=====frameINFO=====
======IMUData=====
 imu ts: 0.192
acc: -0.001906         0     9.794
gyro: -3.935e-06  6.217e-05  3.811e-05
======CamData=====
 cam ts: 0.192
position: 31.51 120.4 31.51
quaternion qw, qx, qy, qz: 0.9999 0.005617 0.008113 0.00522
======CamData=====
 cam ts: 0.192
position: 31.51 120.4 31.51
quaternion qw, qx, qy, qz: 0.9999 0.006422 0.008212 0.006018
======CamData=====
 cam ts: 0.192
position: 31.51 120.4 31.51
quaternion qw, qx, qy, qz: 0.9999 0.00532 0.008679 0.00487
======PVAX=====
 imu state ts: 0.192
position lat, lon, alt: 31.51 120.4     0
velocity:  0 25 -0
quaternion qw, qx, qy, qz: 1 0 0 0


Q_enu2b
0
0
0
1
Q_ecef2b
-0.1281
 0.4715
  0.842
0.2288
V_enu
0,25,-0
V_ecef
6.612,-11.27,21.31
Q_enu2b
0
0
0
1
Q_ecef2b
-0.1281
 0.4715
  0.842
0.2288
V_enu
0,25,-0
V_ecef
6.612,-11.27,21.31
pose_params[0]
-2.754e+06,4.694e+06,3.314e+06,0.1281,-0.4715,-0.842,0.2288,
pose_params[1]
-2.754e+06,4.694e+06,3.314e+06,0.1281,-0.4715,-0.842,0.2288,
speedbias_params[0]
6.612,-11.27,21.31,0,0,0,0,0,0,
speedbias_params[1]
6.612,-11.27,21.31,0,0,0,0,0,0,
pre_integ evaluation result:
 7.769e-05
      -4.8
 0.0002898
 7.556e-07
-1.194e-05
-7.317e-06
 0.0003546
-7.091e-07
  0.003019
         0
         0
         0
         0
         0
         0
iter      cost      cost_change  |gradient|   |step|    tr_ratio  tr_radius  ls_iter  iter_time  total_time
   0  2.196773e+05    0.00e+00    1.80e+05   0.00e+00   0.00e+00  1.00e+04        0    3.11e-04    4.10e-04
   1  1.755323e+02    2.20e+05    5.89e+03   1.27e+00   9.99e-01  3.00e+04        1    1.86e-04    6.19e-04
pose_params[0]
-2.754e+06,4.694e+06,3.314e+06,0.1248,-0.4594,-0.8487,0.2306,
pose_params[1]
-2.754e+06,4.694e+06,3.314e+06,0.1248,-0.4594,-0.8487,0.2306,
speedbias_params[0]
7.004,-11.94,21.76,-2.402e-08,-6.06e-05,3.267e-05,1.394e-08,6.833e-11,-1.066e-11,
speedbias_params[1]
6.22,-10.6,20.86,-2.402e-08,-6.06e-05,3.267e-05,1.393e-08,6.834e-11,-1.067e-11,

Solver Summary (v 1.14.0-eigen-(3.2.92)-lapack-suitesparse-(4.4.6)-cxsparse-(3.1.4)-eigensparse-openmp-no_tbb)

                                     Original                  Reduced
Parameter blocks                            4                        4
Parameters                                 32                       32
Effective parameters                       30                       30
Residual blocks                             1                        1
Residuals                                  15                       15

Minimizer                        TRUST_REGION

Sparse linear algebra library    SUITE_SPARSE
Trust region strategy     LEVENBERG_MARQUARDT

                                        Given                     Used
Linear solver          SPARSE_NORMAL_CHOLESKY   SPARSE_NORMAL_CHOLESKY
Threads                                     1                        1
Linear solver ordering              AUTOMATIC                        4

Cost:
Initial                          2.196773e+05
Final                            1.755323e+02
Change                           2.195018e+05

Minimizer iterations                        2
Successful steps                            2
Unsuccessful steps                          0

Time (in seconds):
Preprocessor                         0.000099

  Residual only evaluation           0.000050 (2)
  Jacobian & residual evaluation     0.000078 (2)
  Linear solver                      0.000120 (2)
Minimizer                            0.000622

Postprocessor                        0.000009
Total                                0.000731

Termination:                      CONVERGENCE (Parameter tolerance reached. Relative step_norm: 4.046248e-09 <= 1.000000e-08.)


Process finished with exit code 0
```

## Previous simulations including ENU ref frame based 
### Static simulation

#### Motion profile

![1562953942338](/home/xiang.zhang/gitRepo/project/doc_sideslip/plots/1562953942338.png)

#### Sim results: set `G=[0, 0, 0]` ENU

```c++
/home/xiang.zhang/gitRepo/sensor-fusion-navigation-v3/bin/test_simulated_imu_factor
skip the header
Loaded 126 frames.
loaded 126 frames
the first frame data 
=====frameINFO=====
======IMUData=====
 imu ts: 0
acc:     0     0 9.794
gyro:         0 6.217e-05 3.811e-05
======CamData=====
 cam ts: 0
position: 31.51 120.4  2.25
quaternion qw, qx, qy, qz: 0.9999 0.006452 0.008034 0.004337
======CamData=====
 cam ts: 0
position: 31.51 120.4 2.219
quaternion qw, qx, qy, qz: 0.9999 0.003607 0.009144 0.005026
======CamData=====
 cam ts: 0
position: 31.51 120.4 2.243
quaternion qw, qx, qy, qz: 0.9999 0.005887 0.008617 0.00631
======PVAX=====
 imu state ts: 0
position lat, lon, alt: 31.51 120.4     0
velocity:  0  0 -0
quaternion qw, qx, qy, qz: 1 0 0 0


the second frame data 
=====frameINFO=====
======IMUData=====
 imu ts: 1
acc:     0     0 9.794
gyro:         0 6.217e-05 3.811e-05
======CamData=====
 cam ts: 1
position: 31.51 120.4 2.309
quaternion qw, qx, qy, qz: 0.9999 0.004709 0.008169 0.005845
======CamData=====
 cam ts: 1
position: 31.51 120.4 2.249
quaternion qw, qx, qy, qz: 0.9999 0.00469 0.007986 0.005551
======CamData=====
 cam ts: 1
position: 31.51 120.4 2.279
quaternion qw, qx, qy, qz: 0.9999 0.006924 0.008275 0.005177
======PVAX=====
 imu state ts: 1
position lat, lon, alt: 31.51 120.4     0
velocity:  0  0 -0
quaternion qw, qx, qy, qz: 1 0 0 0


Q_enu2b
0
0
0
1
Q_ecef2b
-0.1281
 0.4715
  0.842
0.2288
V_enu
0,0,-0
V_ecef
0,-0,0
Q_enu2b
0
0
0
1
Q_ecef2b
-0.1281
 0.4715
  0.842
0.2288
V_enu
0,0,-0
V_ecef
0,-0,0
pose_params[0]
-2.754e+06,4.694e+06,3.314e+06,0.1281,-0.4715,-0.842,0.2288,
pose_params[1]
-2.754e+06,4.694e+06,3.314e+06,0.1281,-0.4715,-0.842,0.2288,
speedbias_params[0]
6.951e-310,1.492e-316,9.158e-72,0,0,0,0,0,0,
speedbias_params[1]
6.951e-310,1.492e-316,7.872e-67,0,0,0,0,0,0,
pre_integ evaluation result:
-0.0001015
 -9.67e-10
    -4.897
-7.275e-27
-6.217e-05
-3.811e-05
-0.0003045
-3.868e-09
    -9.794  //b frame, Vz decreases by a abs(g), which means gb = [0, 0, 9.794], which means the body frame is defined as RIGHT, FORWARD, DOWN
         0
         0
         0
         0
         0
         0
iter      cost      cost_change  |gradient|   |step|    tr_ratio  tr_radius  ls_iter  iter_time  total_time
   0  1.199119e+06    0.00e+00    1.80e+05   0.00e+00   0.00e+00  1.00e+04        0    2.99e-04    3.99e-04
   1  6.052895e-01    1.20e+06    1.07e+02   1.09e+01   1.00e+00  3.00e+04        1    1.48e-04    5.71e-04
pose_params[0]
-2.754e+06,4.694e+06,3.314e+06,0.1281,-0.4715,-0.842,0.2288,
pose_params[1]
-2.754e+06,4.694e+06,3.314e+06,0.1281,-0.4715,-0.842,0.2288,
speedbias_params[0]
6.951e-310,1.492e-316,9.158e-72,0,0,0,0,0,0,
speedbias_params[1]  // The estimated speed error is just the g projected to ECEF, which mean reference frame conversion is right, optimation is right. Need to make body frames consistent for simulation and pre-integration.
-4.223,7.197,5.115,-1.958e-09,-1.165e-09,5.729e-07,3.595e-11,-5.968e-11,3.774e-13,

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
Initial                          1.199119e+06
Final                            6.052895e-01
Change                           1.199119e+06

Minimizer iterations                        2
Successful steps                            2
Unsuccessful steps                          0

Time (in seconds):
Preprocessor                         0.000100

  Residual only evaluation           0.000044 (2)
  Jacobian & residual evaluation     0.000069 (2)
  Linear solver                      0.000073 (2)
Minimizer                            0.000545

Postprocessor                        0.000007
Total                                0.000652

Termination:                      CONVERGENCE (Parameter tolerance reached. Relative step_norm: 1.220482e-09 <= 1.000000e-08.)

 4.225
-7.202
-5.119

Process finished with exit code 0

```

#### Sim results: set `G=[-4.225, 7.202, 5.119]` ENU

```C++
/home/xiang.zhang/gitRepo/sensor-fusion-navigation-v3/bin/test_simulated_imu_factor
skip the header
Loaded 125 frames.
loaded 125 frames
the first frame data 
=====frameINFO=====
======IMUData=====
 imu ts: 0
acc:     0     0 9.794
gyro:         0 6.217e-05 3.811e-05
======CamData=====
 cam ts: 0
position: 31.51 120.4  2.25
quaternion qw, qx, qy, qz: 0.9999 0.006452 0.008034 0.004337
======CamData=====
 cam ts: 0
position: 31.51 120.4 2.219
quaternion qw, qx, qy, qz: 0.9999 0.003607 0.009144 0.005026
======CamData=====
 cam ts: 0
position: 31.51 120.4 2.243
quaternion qw, qx, qy, qz: 0.9999 0.005887 0.008617 0.00631
======PVAX=====
 imu state ts: 0
position lat, lon, alt: 31.51 120.4     0
velocity:  0  0 -0
quaternion qw, qx, qy, qz: 1 0 0 0


the second frame data 
=====frameINFO=====
======IMUData=====
 imu ts: 0.992
acc:     0     0 9.794
gyro:         0 6.217e-05 3.811e-05
======CamData=====
 cam ts: 0.992
position: 31.51 120.4 2.357
quaternion qw, qx, qy, qz: 0.9999 0.004819 0.008998 0.00447
======CamData=====
 cam ts: 0.992
position: 31.51 120.4 2.195
quaternion qw, qx, qy, qz: 0.9999 0.007007 0.009129 0.00495
======CamData=====
 cam ts: 0.992
position: 31.51 120.4 2.362
quaternion qw, qx, qy, qz: 0.9999 0.005122 0.009324 0.005347
======PVAX=====
 imu state ts: 0.992
position lat, lon, alt: 31.51 120.4     0
velocity:  0  0 -0
quaternion qw, qx, qy, qz: 1 0 0 0


Q_enu2b
0
0
0
1
Q_ecef2b
-0.1281
 0.4715
  0.842
0.2288
V_enu
0,0,-0
V_ecef
0,-0,0
Q_enu2b
0
0
0
1
Q_ecef2b
-0.1281
 0.4715
  0.842
0.2288
V_enu
0,0,-0
V_ecef
0,-0,0
pose_params[0]
-2.754e+06,4.694e+06,3.314e+06,0.1281,-0.4715,-0.842,0.2288,
pose_params[1]
-2.754e+06,4.694e+06,3.314e+06,0.1281,-0.4715,-0.842,0.2288,
speedbias_params[0]
6.929e-310,6.929e-310,0,0,0,0,0,0,0,
speedbias_params[1]
6.929e-310,6.929e-310,0,0,0,0,0,0,0,
pre_integ evaluation result:
    -2.079
     3.544
      -2.3
-6.253e-27
-6.167e-05
-3.781e-05
    -4.191
     7.144
    -4.638
         0
         0
         0
         0
         0
         0
iter      cost      cost_change  |gradient|   |step|    tr_ratio  tr_radius  ls_iter  iter_time  total_time
   0  1.578916e-02    0.00e+00    6.48e+01   0.00e+00   0.00e+00  1.00e+04        0    2.91e-04    3.95e-04
   1  9.411204e-09    1.58e-02    1.51e-02   1.22e-03   1.00e+00  3.00e+04        1    1.42e-04    5.62e-04
pose_params[0]
-2.754e+06,4.694e+06,3.314e+06,0.1281,-0.4715,-0.842,0.2288,
pose_params[1]
-2.754e+06,4.694e+06,3.314e+06,0.1281,-0.4715,-0.842,0.2288,
speedbias_params[0]
6.929e-310,6.929e-310,0,0,0,0,0,0,0,
speedbias_params[1]
-0.001088,3.919e-05,-0.0002222,5.11e-11,-2.862e-11,2.207e-11,8.456e-13,2.307e-12,3.719e-13,


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
Initial                          1.578916e-02
Final                            9.411204e-09
Change                           1.578915e-02

Minimizer iterations                        2
Successful steps                            2
Unsuccessful steps                          0

Time (in seconds):
Preprocessor                         0.000105

  Residual only evaluation           0.000041 (2)
  Jacobian & residual evaluation     0.000067 (2)
  Linear solver                      0.000071 (2)
Minimizer                            0.000528

Postprocessor                        0.000007
Total                                0.000640

Termination:                      CONVERGENCE (Parameter tolerance reached. Relative step_norm: 1.691364e-13 <= 1.000000e-08.)

 4.225
-7.202
-5.119

Process finished with exit code 0
```

#### Sim results: set `G=[4.225, -7.202, -5.119]`, NED

```c++
/home/xiang.zhang/gitRepo/sensor-fusion-navigation-v3/bin/test_simulated_imu_factor
skip the header
Loaded 26 frames.
loaded 26 frames
the first frame data 
=====frameINFO=====
======IMUData=====
 imu ts: 0
acc:      0      0 -9.794
gyro:  6.217e-05          0 -3.811e-05
======CamData=====
 cam ts: 0
position: 0 0 0
quaternion qw, qx, qy, qz: 0 0 0 0
======CamData=====
 cam ts: 0
position: 0 0 0
quaternion qw, qx, qy, qz: 0 0 0 0
======CamData=====
 cam ts: 0
position: 0 0 0
quaternion qw, qx, qy, qz: 0 0 0 0
======PVAX=====
 imu state ts: 0
position lat, lon, alt: 31.51 120.4     0
velocity: 0 0 0
quaternion qw, qx, qy, qz: 0 1 0 0


the second frame data 
=====frameINFO=====
======IMUData=====
 imu ts: 0.2
acc:      0      0 -9.794
gyro:  6.217e-05          0 -3.811e-05
======CamData=====
 cam ts: 0.2
position: 0 0 0
quaternion qw, qx, qy, qz: 0 0 0 0
======CamData=====
 cam ts: 0.2
position: 0 0 0
quaternion qw, qx, qy, qz: 0 0 0 0
======CamData=====
 cam ts: 0.2
position: 0 0 0
quaternion qw, qx, qy, qz: 0 0 0 0
======PVAX=====
 imu state ts: 0.2
position lat, lon, alt: 31.51 120.4     0
velocity: 0 0 0
quaternion qw, qx, qy, qz: 0 1 0 0


pose_params[0]
-2.754e+06,4.694e+06,3.314e+06,-0.2428,-0.424,-0.4336,0.7572,
pose_params[1]
-2.754e+06,4.694e+06,3.314e+06,-0.2428,-0.424,-0.4336,0.7572,
speedbias_params[0]
6.937e-310,9.168e-317,1.181e-95,0,0,0,0,0,0,
speedbias_params[1]
6.937e-310,9.168e-317,0,0,0,0,0,0,0,
pre_integ evaluation result:
    0.0845
     0.144
    0.2983
-1.243e-05
-7.206e-27
 7.622e-06
     0.845
      1.44
     2.983
         0
         0
         0
         0
         0
         0
iter      cost      cost_change  |gradient|   |step|    tr_ratio  tr_radius  ls_iter  iter_time  total_time
   0  3.294853e-03    0.00e+00    2.09e+01   0.00e+00   0.00e+00  1.00e+04        0    3.09e-04    4.08e-04
   1  1.136898e-09    3.29e-03    5.73e-02   1.87e-04   1.00e+00  3.00e+04        1    1.43e-04    5.76e-04
pose_params[0]
-2.754e+06,4.694e+06,3.314e+06,-0.2428,-0.424,-0.4336,0.7572,
pose_params[1]
-2.754e+06,4.694e+06,3.314e+06,-0.2428,-0.424,-0.4336,0.7572,
speedbias_params[0]
6.937e-310,9.168e-317,1.181e-95,0,0,0,0,0,0,
speedbias_params[1]
0.0001778,-3.228e-05,4.481e-05,1.142e-12,1.553e-12,-8.82e-13,3.331e-14,-6.71e-15,-1.463e-14,


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
Initial                          3.294853e-03
Final                            1.136898e-09
Change                           3.294852e-03

Minimizer iterations                        2
Successful steps                            2
Unsuccessful steps                          0

Time (in seconds):
Preprocessor                         0.000099

  Residual only evaluation           0.000043 (2)
  Jacobian & residual evaluation     0.000065 (2)
  Linear solver                      0.000073 (2)
Minimizer                            0.000551

Postprocessor                        0.000007
Total                                0.000657

Termination:                      CONVERGENCE (Parameter tolerance reached. Relative step_norm: 2.078245e-14 <= 1.000000e-08.)

 4.225
-7.202
-5.119

Process finished with exit code 0


    
```



### Debug log +

```c++
0.2645    0.8625   -0.4315
  -0.4508    0.5061    0.7353
   0.8526 6.918e-19    0.5226
Qi：
-0.2428 a
 -0.424 b
-0.4336 c
0.7572 d
    
    Qi：
 -0.424 b
-0.4336 c
 0.7572 d 
-0.2428 a
```

- [x] `quaternion` component order may be wrong.

  - check all places using vector for storing quaternion.

    - ```
      for (int i = 0; i < 2; ++i) 
      {problem.AddParameterBlock(pose_params[i], SIZE_POSE, local_parameterization);    
      problem.AddParameterBlock(speedbias_params[i], SIZE_SPEEDBIAS);}
      ```

    - ```c++
      problem.AddResidualBlock(cost_function, nullptr,
                                   pose_params[0], speedbias_params[0],
                                   pose_params[1], speedbias_params[1]); 
      ```

      

    - ```
      std::cout << pre_integ->evaluate(p_a, q_a, v_a, accel_bias, gyro_bias, p_b, q_b, v_b, accel_bias, gyro_bias);
      ```

  - The initialization of Quaternion for `evaluate function` is wrong.

### Results without imu noise

```c++
Loaded 26 frames.
loaded 26 frames
the first frame data 
=====frameINFO=====
======IMUData=====
 imu ts: 0
acc:      0      0 -9.794
gyro:  6.217e-05          0 -3.811e-05
======CamData=====
 cam ts: 0
position: 0 0 0
quaternion qw, qx, qy, qz: 0 0 0 0
======CamData=====
 cam ts: 0
position: 0 0 0
quaternion qw, qx, qy, qz: 0 0 0 0
======CamData=====
 cam ts: 0
position: 0 0 0
quaternion qw, qx, qy, qz: 0 0 0 0
======PVAX=====
 imu state ts: 0
position lat, lon, alt: 31.51 120.4     0
velocity: 0 0 0
quaternion qw, qx, qy, qz: 0 1 0 0


the second frame data 
=====frameINFO=====
======IMUData=====
 imu ts: 0.2
acc:      0      0 -9.794
gyro:  6.217e-05          0 -3.811e-05
======CamData=====
 cam ts: 0.2
position: 0 0 0
quaternion qw, qx, qy, qz: 0 0 0 0
======CamData=====
 cam ts: 0.2
position: 0 0 0
quaternion qw, qx, qy, qz: 0 0 0 0
======CamData=====
 cam ts: 0.2
position: 0 0 0
quaternion qw, qx, qy, qz: 0 0 0 0
======PVAX=====
 imu state ts: 0.2
position lat, lon, alt: 31.51 120.4     0
velocity: 0 0 0
quaternion qw, qx, qy, qz: 0 1 0 0


pose_params[0]
-2.754e+06,4.694e+06,3.314e+06,-0.2428,-0.424,-0.4336,0.7572,
pose_params[1]
-2.754e+06,4.694e+06,3.314e+06,-0.2428,-0.424,-0.4336,0.7572,
speedbias_params[0]
6.95e-310,6.436e-317,1.181e-95,0,0,0,0,0,0,
speedbias_params[1]
6.95e-310,6.436e-317,0,0,0,0,0,0,0,
pre_integ evaluation result:
-9.986e-06
-1.331e-05
  7.71e-06
-1.243e-05
-3.542e-17
 7.622e-06
-9.986e-05
-0.0001371
 7.709e-05
         0
         0
         0
         0
         0
         0
iter      cost      cost_change  |gradient|   |step|    tr_ratio  tr_radius  ls_iter  iter_time  total_time
   0  3.294853e-03    0.00e+00    2.09e+01   0.00e+00   0.00e+00  1.00e+04        0    2.30e-04    3.09e-04
   1  1.136898e-09    3.29e-03    5.73e-02   1.87e-04   1.00e+00  3.00e+04        1    1.02e-04    4.26e-04
pose_params[0]
-2.754e+06,4.694e+06,3.314e+06,-0.2428,-0.424,-0.4336,0.7572,
pose_params[1]
-2.754e+06,4.694e+06,3.314e+06,-0.2428,-0.424,-0.4336,0.7572,
speedbias_params[0]
6.95e-310,6.436e-317,1.181e-95,0,0,0,0,0,0,
speedbias_params[1]
0.0001778,-3.228e-05,4.481e-05,1.142e-12,1.553e-12,-8.82e-13,3.331e-14,-6.71e-15,-1.463e-14,
after optimization, pre_integ evaluation result:
-7.995e-09
-1.063e-08
 6.388e-09
-2.057e-09
 5.868e-10
 7.621e-10
-7.069e-08
-9.707e-08
 5.396e-08
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
Initial                          3.294853e-03
Final                            1.136898e-09
Change                           3.294852e-03

Minimizer iterations                        2
Successful steps                            2
Unsuccessful steps                          0

Time (in seconds):
Preprocessor                         0.000079

  Residual only evaluation           0.000030 (2)
  Jacobian & residual evaluation     0.000047 (2)
  Linear solver                      0.000052 (2)
Minimizer                            0.000399

Postprocessor                        0.000005
Total                                0.000483

Termination:                      CONVERGENCE (Parameter tolerance reached. Relative step_norm: 2.078245e-14 <= 1.000000e-08.)
```

### Results with IMU noise

```c++
skip the header
Loaded 26 frames.
loaded 26 frames
the first frame data 
=====frameINFO=====
======IMUData=====
 imu ts: 0
acc: 0.007547  0.01831   -9.778
gyro: -0.001002   0.00163 -0.002839
======CamData=====
 cam ts: 0
position: 0 0 0
quaternion qw, qx, qy, qz: 0 0 0 0
======CamData=====
 cam ts: 0
position: 0 0 0
quaternion qw, qx, qy, qz: 0 0 0 0
======CamData=====
 cam ts: 0
position: 0 0 0
quaternion qw, qx, qy, qz: 0 0 0 0
======PVAX=====
 imu state ts: 0
position lat, lon, alt: 31.51 120.4     0
velocity: 0 0 0
quaternion qw, qx, qy, qz: 0 1 0 0


the second frame data 
=====frameINFO=====
======IMUData=====
 imu ts: 0.2
acc: 0.007823 0.006077     -9.8
gyro:  -0.001302  -0.002959 -0.0005025
======CamData=====
 cam ts: 0.2
position: 0 0 0
quaternion qw, qx, qy, qz: 0 0 0 0
======CamData=====
 cam ts: 0.2
position: 0 0 0
quaternion qw, qx, qy, qz: 0 0 0 0
======CamData=====
 cam ts: 0.2
position: 0 0 0
quaternion qw, qx, qy, qz: 0 0 0 0
======PVAX=====
 imu state ts: 0.2
position lat, lon, alt: 31.51 120.4     0
velocity: 0 0 0
quaternion qw, qx, qy, qz: 0 1 0 0


pose_params[0]
-2.754e+06,4.694e+06,3.314e+06,-0.2428,-0.424,-0.4336,0.7572,
pose_params[1]
-2.754e+06,4.694e+06,3.314e+06,-0.2428,-0.424,-0.4336,0.7572,
speedbias_params[0]
6.904e-310,7.262e-317,1.181e-95,0,0,0,0,0,0,
speedbias_params[1]
6.904e-310,7.261e-317,0,0,0,0,0,0,0,
pre_integ evaluation result:
 5.196e-05
 1.327e-05
 9.175e-05
-0.0001291
-4.394e-05
 3.777e-05
 0.0003614
 7.841e-05
 0.0007883
         0
         0
         0
         0
         0
         0
iter      cost      cost_change  |gradient|   |step|    tr_ratio  tr_radius  ls_iter  iter_time  total_time
   0  1.815881e-01    0.00e+00    8.06e+02   0.00e+00   0.00e+00  1.00e+04        0    3.00e-04    4.01e-04
   1  3.122364e-08    1.82e-01    3.48e-01   8.79e-04   1.00e+00  3.00e+04        1    1.46e-04    5.72e-04
pose_params[0]
-2.754e+06,4.694e+06,3.314e+06,-0.2428,-0.424,-0.4336,0.7572,
pose_params[1]
-2.754e+06,4.694e+06,3.314e+06,-0.2427,-0.424,-0.4336,0.7572,
speedbias_params[0]
6.904e-310,7.262e-317,1.181e-95,0,0,0,0,0,0,
speedbias_params[1]
0.0001768,-0.0004561,-0.0007196,-4.729e-12,-1.103e-12,-9.505e-12,2.446e-13,1.126e-13,-7.251e-14,
after optimization, pre_integ evaluation result:
 3.597e-08
 7.609e-09
 6.803e-08
 -1.25e-08
-6.883e-09
 3.777e-09
 3.081e-07
  5.92e-08
 5.906e-07
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
Initial                          1.815881e-01
Final                            3.122364e-08
Change                           1.815881e-01

Minimizer iterations                        2
Successful steps                            2
Unsuccessful steps                          0

Time (in seconds):
Preprocessor                         0.000101

  Residual only evaluation           0.000044 (2)
  Jacobian & residual evaluation     0.000072 (2)
  Linear solver                      0.000072 (2)
Minimizer                            0.000545

Postprocessor                        0.000007
Total                                0.000653

Termination:                      CONVERGENCE (Parameter tolerance reached. Relative step_norm: 1.056207e-13 <= 1.000000e-08.)

g_ecef
 4.225
-7.202
-5.119

Process finished with exit code 0
```

## Acceleration simulation

- Use the second segment of the static-acceleration motion profile.

### Results

```c++
skip the header
Loaded 26 frames.
loaded 26 frames
the first frame data 
=====frameINFO=====
======IMUData=====
 imu ts: 60
acc:   0.05      0 -9.794
gyro:  6.217e-05          0 -3.811e-05
======CamData=====
 cam ts: 60
position: 0 0 0
quaternion qw, qx, qy, qz: 0 0 0 0
======CamData=====
 cam ts: 60
position: 0 0 0
quaternion qw, qx, qy, qz: 0 0 0 0
======CamData=====
 cam ts: 60
position: 0 0 0
quaternion qw, qx, qy, qz: 0 0 0 0
======PVAX=====
 imu state ts: 60
position lat, lon, alt: 31.51 120.4     0
velocity: 0 0 0
quaternion qw, qx, qy, qz: 0 1 0 0


the second frame data 
=====frameINFO=====
======IMUData=====
 imu ts: 60.2
acc:     0.4677 -5.075e-06     -9.794
gyro:  6.217e-05 -1.048e-08 -3.811e-05
======CamData=====
 cam ts: 60.2
position: 0 0 0
quaternion qw, qx, qy, qz: 0 0 0 0
======CamData=====
 cam ts: 60.2
position: 0 0 0
quaternion qw, qx, qy, qz: 0 0 0 0
======CamData=====
 cam ts: 60.2
position: 0 0 0
quaternion qw, qx, qy, qz: 0 0 0 0
======PVAX=====
 imu state ts: 60.2
position lat, lon, alt: 31.51 120.4     0
velocity: 0.06658       0       0
quaternion qw, qx, qy, qz: 0 1 0 0


pose_params[0]
-2.754e+06,4.694e+06,3.314e+06,-0.2428,-0.424,-0.4336,0.7572,
pose_params[1]
-2.754e+06,4.694e+06,3.314e+06,-0.2428,-0.424,-0.4336,0.7572,
speedbias_params[0]
0,-0,0,0,0,0,0,0,0,
speedbias_params[1]
0.01761,-0.03001,0.05677,0,0,0,0,0,0,
pre_integ evaluation result:
-0.0005044
-1.327e-05
 7.711e-06
-1.243e-05
  1.64e-09
 7.622e-06
 -0.001771
-0.0001364
 7.709e-05
         0
         0
         0
         0
         0
         0
iter      cost      cost_change  |gradient|   |step|    tr_ratio  tr_radius  ls_iter  iter_time  total_time
   0  2.208566e+00    0.00e+00    1.05e+04   0.00e+00   0.00e+00  1.00e+04        0    2.38e-04    3.14e-04
   1  3.602837e-07    2.21e+00    1.61e+00   1.85e-03   1.00e+00  3.00e+04        1    1.13e-04    4.42e-04
pose_params[0]
-2.754e+06,4.694e+06,3.314e+06,-0.2428,-0.424,-0.4336,0.7572,
pose_params[1]
-2.754e+06,4.694e+06,3.314e+06,-0.2428,-0.424,-0.4336,0.7572,
speedbias_params[0]
0,-0,0,0,0,0,0,0,0,
speedbias_params[1]
0.01823,-0.0308,0.05823,3.257e-11,1.544e-12,-8.85e-13,3.326e-14,-1.779e-13,-1.424e-14,
after optimization, pre_integ evaluation result:
-2.747e-07
-1.058e-08
 6.221e-09
-2.052e-09
  1.68e-08
 7.306e-10
-2.245e-06
-9.648e-08
 5.322e-08
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
Initial                          2.208566e+00
Final                            3.602837e-07
Change                           2.208566e+00

Minimizer iterations                        2
Successful steps                            2
Unsuccessful steps                          0

Time (in seconds):
Preprocessor                         0.000076

  Residual only evaluation           0.000033 (2)
  Jacobian & residual evaluation     0.000047 (2)
  Linear solver                      0.000060 (2)
Minimizer                            0.000423

Postprocessor                        0.000005
Total                                0.000504

Termination:                      CONVERGENCE (Parameter tolerance reached. Relative step_norm: 3.552920e-13 <= 1.000000e-08.)


Process finished with exit code 0
```

