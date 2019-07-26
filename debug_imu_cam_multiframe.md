



# Bugs

### Abnormal initial cost

#### to diagnose: 

 - [x] the cost is from IMU factor or Cam factor?

   - it is not because of Cam factor.

   - [x] test  `update the calibration parameters used in the camera factor`

   - [x] the PI is inconsistent with observation, the error is large.

     - [x] IMU cam multiple frame looks erroneous 
     - [x] IMU sim looks normal except one vel axis
     - [x] IMU factor looks normal
     - [x] IMU sim multi frame looks normal.... 
       - [ ] ![1564114422587](/home/xiang.zhang/gitRepo/project/doc_sideslip/plots/1564114422587.png)

     

   - [x] check the data loaded? Not need for now.

   - [ ] Check the difference between imu multiple frame and imu-cam multiple frame when no cam.

     - located the culprit. // False positive!!

       - ```c++
         // use updated biasaccel_bias << speedbias_params[iter][3], speedbias_params[iter][4], speedbias_params[iter][5];gyro_bias << speedbias_params[iter][6], speedbias_params[iter][7], speedbias_params[iter][8];
         ```

       - PI looks OK. The state variable is wrong.
       - ![1564118155263](/home/xiang.zhang/gitRepo/project/doc_sideslip/plots/1564118155263.png)

     

      - [ ] check the `Qi` first
        	- [ ] The below is from bugged version.
         - [ ] ![1564118219687](/home/xiang.zhang/gitRepo/project/doc_sideslip/plots/1564118219687.png)

     - The below is from working IMU multiframe version
       - ![1564118399984](/home/xiang.zhang/gitRepo/project/doc_sideslip/plots/1564118399984.png)

     

     - [ ] Check the `Qi` error cause!
       - [ ] ![1564119661357](/home/xiang.zhang/gitRepo/project/doc_sideslip/plots/1564119661357.png)

     - blow from bug version

     ![1564119769712](/home/xiang.zhang/gitRepo/project/doc_sideslip/plots/1564119769712.png)

     - below from working version

     ![1564120022726](/home/xiang.zhang/gitRepo/project/doc_sideslip/plots/1564120022726.png)

     

     - below from working version. Note two pqv_ecefs have different type....
     - ![1564120325815](/home/xiang.zhang/gitRepo/project/doc_sideslip/plots/1564120325815.png)

     

     

     

     ![1564117968774](/home/xiang.zhang/gitRepo/project/doc_sideslip/plots/1564117968774.png)

```c++
/home/xiang.zhang/gitRepo/sensor-fusion-navigation-v3/bin/test_simulated_imu_cam_factor_multiframe
Process /mnt/truenas/scratch/xiang.zhang/imu_cam_two_laps_ned.csv with noise flag: 0
skip the header
Loaded 26 frames.
iter      cost      cost_change  |gradient|   |step|    tr_ratio  tr_radius  ls_iter  iter_time  total_time
   0  7.238760e+07    0.00e+00    6.55e+07   0.00e+00   0.00e+00  1.00e+04        0    9.59e-04    1.09e-03
   1  2.114968e+01    7.24e+07    1.17e+04   1.24e+01   1.00e+00  3.00e+04        1    1.23e-03    2.36e-03
   2  5.027262e+00    1.61e+01    2.28e+00   7.80e-01   1.00e+00  9.00e+04        1    1.34e-03    3.78e-03

Solver Summary (v 1.14.0-eigen-(3.2.92)-lapack-suitesparse-(4.4.6)-cxsparse-(3.1.4)-eigensparse-openmp-no_tbb)

                                     Original                  Reduced
Parameter blocks                            5                        3
Parameters                                 39                       23
Effective parameters                       36                       21
Residual blocks                             3                        3
Residuals                                  27                       27

Minimizer                        TRUST_REGION

Sparse linear algebra library    SUITE_SPARSE
Trust region strategy     LEVENBERG_MARQUARDT

                                        Given                     Used
Linear solver          SPARSE_NORMAL_CHOLESKY   SPARSE_NORMAL_CHOLESKY
Threads                                     1                        1
Linear solver ordering              AUTOMATIC                        3

Cost:
Initial                          7.238760e+07
Final                            5.027262e+00
Change                           7.238760e+07

Minimizer iterations                        3
Successful steps                            3
Unsuccessful steps                          0

Time (in seconds):
Preprocessor                         0.000126

  Residual only evaluation           0.002774 (3)
  Jacobian & residual evaluation     0.002156 (3)
  Linear solver                      0.000118 (3)
Minimizer                            0.005683

Postprocessor                        0.000014
Total                                0.005824

Termination:                      CONVERGENCE (Parameter tolerance reached. Relative step_norm: 2.102410e-11 <= 1.000000e-08.)


Estimation errors of pose error, P_xyz, Q_xyzw
Frame: 0
0   0   0   0   0   0   0   
Frame: 1
1.43193   1.71918   -0.798989   0.0851131   -0.0487498   0.0476597   -0.265767   

Estimation errors of speedbias error, V_xyz, Ba_xyz, Bg_xyz
Frame: 0
0   0   0   0   0   0   0   0   0   
Frame: 1
7.34349   8.57287   -4.34687   -3.9162e-11   -5.98875e-11   -4.64475e-11   9.34248e-12   5.08624e-12   -1.1237e-11   
0.0140683,0.65284,0.817354,0.221273,-0.125558,0.126365,0.958804,
error of lever arm x, y, z (meter): -0.1, -0.15, 0.2
error of imu to cam rotation: 0.122812

Process finished with exit code 0
	
```







- log 

  ```c++
  /home/xiang.zhang/gitRepo/sensor-fusion-navigation-v3/bin/test_simulated_imu_cam_factor_multiframe
  Process /mnt/truenas/scratch/xiang.zhang/imu_cam_two_laps_ned.csv with noise flag: 0
  skip the header
  Loaded 101 frames.
  gt_pqv_ecef
  -2.75438e+06,4.69436e+06,3.31406e+06,-0.596493,0.341601,-0.333996,-0.451392,13.5878,-2.64998,17.6711,
  
  Process finished with exit code 0
  
  ```

  

```c++
/home/xiang.zhang/gitRepo/sensor-fusion-navigation-v3/bin/test_simulated_imu_factor_multiframe
Process /mnt/truenas/scratch/xiang.zhang/imu_cam_two_laps_ned.csv with noise flag: 0
skip the header
Loaded 101 frames.
pqv_ecef
-2.75438e+06,4.69436e+06,3.31406e+06,-0.75716,0.433612,-0.423959,-0.242794,6.61198,-11.269,21.3141,

Process finished with exit code 0
	
```



```c++
/home/xiang.zhang/gitRepo/sensor-fusion-navigation-v3/bin/test_simulated_imu_factor_multiframe
Process /mnt/truenas/scratch/xiang.zhang/imu_cam_two_laps_ned.csv with noise flag: 0
skip the header
Loaded 101 frames.
=====frameINFO=====
======IMUData=====
 imu ts: 0
acc:         0 -0.001906    -9.794
gyro:  6.217e-05 -3.935e-06 -3.811e-05
======CamData=====
 cam ts: 0
position: 31.51 120.4    -2
quaternion qw, qx, qy, qz: 0.9999 0.004325 -0.008745 0.004325
======CamData=====
 cam ts: 0
position:  31.51  120.4 -2.264
quaternion qw, qx, qy, qz: 0.9998 0.01774 0.01213 -0.002176
======CamData=====
 cam ts: 0
position:  31.51  120.4 -2.762
quaternion qw, qx, qy, qz: 0.9998 0.007286 -0.01568 -0.004503
======PVAX=====
 imu state ts: 0
position lat, lon, alt: 31.51 120.4     0
velocity: 25  0  0
quaternion qw, qx, qy, qz: 1 0 0 0


pqv_ecef
-2.754e+06,4.694e+06,3.314e+06,-0.7572,0.4336,-0.424,-0.2428,6.612,-11.27,21.31,

```

```c++
/home/xiang.zhang/gitRepo/sensor-fusion-navigation-v3/bin/test_simulated_imu_cam_factor_multiframe
Process /mnt/truenas/scratch/xiang.zhang/imu_cam_two_laps_ned.csv with noise flag: 0
skip the header
Loaded 101 frames.
=====frameINFO=====
======IMUData=====
 imu ts: 0
acc:         0 -0.001906    -9.794
gyro:  6.217e-05 -3.935e-06 -3.811e-05
======CamData=====
 cam ts: 0
position: 31.51 120.4    -2
quaternion qw, qx, qy, qz: 0.9999 0.004325 -0.008745 0.004325
======CamData=====
 cam ts: 0
position:  31.51  120.4 -2.264
quaternion qw, qx, qy, qz: 0.9998 0.01774 0.01213 -0.002176
======CamData=====
 cam ts: 0
position:  31.51  120.4 -2.762
quaternion qw, qx, qy, qz: 0.9998 0.007286 -0.01568 -0.004503
======PVAX=====
 imu state ts: 0
position lat, lon, alt: 31.51 120.4     0
velocity: 25  0  0
quaternion qw, qx, qy, qz: 1 0 0 0


gt_pqv_ecef
-2.754e+06,4.694e+06,3.314e+06,-0.7572,0.4336,-0.424,-0.2428,6.612,-11.27,21.31,

Process finished with exit code 0

```

上面这样调试结果正常。但是用IDE的run跑了几次还是不正常。包括之前调试也是不正常。重新编译后，从命令行运行又正常输出了。

打开cam的几行代码后，用IDE编译，命令行跑又出现下面奇怪的结果。

![1564122419892](/home/xiang.zhang/gitRepo/project/doc_sideslip/plots/1564122419892.png)

![1564122483578](/home/xiang.zhang/gitRepo/project/doc_sideslip/plots/1564122483578.png)

但是加了一行打印语句，重新用IDE 编译后，又正常输出了。

```c++
➜  bin git:(ahrs) ✗ ./test_simulated_imu_cam_factor_multiframe                   
Process /mnt/truenas/scratch/xiang.zhang/imu_cam_two_laps_ned.csv with noise flag: 0
skip the header
Loaded 101 frames.
=====frameINFO=====
======IMUData=====
 imu ts: 0
acc:         0 -0.001906    -9.794
gyro:  6.217e-05 -3.935e-06 -3.811e-05
======CamData=====
 cam ts: 0
position: 31.51 120.4    -2
quaternion qw, qx, qy, qz: 0.9999 0.004325 -0.008745 0.004325
======CamData=====
 cam ts: 0
position:  31.51  120.4 -2.264
quaternion qw, qx, qy, qz: 0.9998 0.01774 0.01213 -0.002176
======CamData=====
 cam ts: 0
position:  31.51  120.4 -2.762
quaternion qw, qx, qy, qz: 0.9998 0.007286 -0.01568 -0.004503
======PVAX=====
 imu state ts: 0
position lat, lon, alt: 31.51 120.4     0
velocity: 25  0  0
quaternion qw, qx, qy, qz: 1 0 0 0


gt_pqv_ecef
-2.754e+06,4.694e+06,3.314e+06,-0.7572,0.4336,-0.424,-0.2428,6.612,-11.27,21.31,
=====frameINFO=====
======IMUData=====
 imu ts: 0.2
acc:         0 -0.001906    -9.794
gyro:  6.217e-05 -3.935e-06 -3.811e-05
======CamData=====
 cam ts: 0.2
position: 31.51 120.4    -2
quaternion qw, qx, qy, qz: 0.9999 0.004325 -0.008745 0.004325
======CamData=====
 cam ts: 0.2
position:  31.51  120.4 -2.169
quaternion qw, qx, qy, qz: 0.9998 0.01704 0.01041 -0.003265
======CamData=====
 cam ts: 0.2
position:  31.51  120.4 -2.717
quaternion qw, qx, qy, qz: 0.9998 0.006801 -0.01596 -0.003579
======PVAX=====
 imu state ts: 0.2
position lat, lon, alt: 31.51 120.4     0
velocity: 25  0  0
quaternion qw, qx, qy, qz: 1 0 0 0


gt_pqv_ecef
-2.754e+06,4.694e+06,3.314e+06,-0.7572,0.4336,-0.424,-0.2428,6.612,-11.27,21.31,
=====frameINFO=====
======IMUData=====
 imu ts: 0.4
acc:         0 -0.001906    -9.794
gyro:  6.217e-05 -3.935e-06 -3.811e-05
======CamData=====
 cam ts: 0.4
position: 31.51 120.4    -2
quaternion qw, qx, qy, qz: 0.9999 0.004325 -0.008745 0.004325
======CamData=====
 cam ts: 0.4
position:  31.51  120.4 -2.264
quaternion qw, qx, qy, qz: 0.9998 0.01686 0.01023 -0.003693
======CamData=====
 cam ts: 0.4
position: 31.51 120.4 -2.85
quaternion qw, qx, qy, qz: 0.9998 0.005744 -0.01595 -0.005066
======PVAX=====
 imu state ts: 0.4
position lat, lon, alt: 31.51 120.4     0
velocity: 25  0  0
quaternion qw, qx, qy, qz: 1 0 0 0


gt_pqv_ecef
-2.754e+06,4.694e+06,3.314e+06,-0.7572,0.4336,-0.424,-0.2428,6.612,-11.27,21.31,
=====frameINFO=====
======IMUData=====
 imu ts: 0.6
acc:         0 -0.001906    -9.794
gyro:  6.217e-05 -3.935e-06 -3.811e-05
======CamData=====
 cam ts: 0.6
position: 31.51 120.4    -2
quaternion qw, qx, qy, qz: 0.9999 0.004325 -0.008745 0.004325
======CamData=====
 cam ts: 0.6
position:  31.51  120.4 -2.271
quaternion qw, qx, qy, qz: 0.9998 0.01865 0.009833 -0.0006232
======CamData=====
 cam ts: 0.6
position: 31.51 120.4 -2.84
quaternion qw, qx, qy, qz: 0.9998 0.006875 -0.01718 -0.003751
======PVAX=====
 imu state ts: 0.6
position lat, lon, alt: 31.51 120.4     0
velocity: 25  0  0
quaternion qw, qx, qy, qz: 1 0 0 0


gt_pqv_ecef
-2.754e+06,4.694e+06,3.314e+06,-0.7572,0.4336,-0.424,-0.2428,6.612,-11.27,21.31,
=====frameINFO=====
======IMUData=====
 imu ts: 0.8
acc:         0 -0.001906    -9.794
gyro:  6.217e-05 -3.935e-06 -3.811e-05
======CamData=====
 cam ts: 0.8
position: 31.51 120.4    -2
quaternion qw, qx, qy, qz: 0.9999 0.004325 -0.008745 0.004325
======CamData=====
 cam ts: 0.8
position:  31.51  120.4 -2.224
quaternion qw, qx, qy, qz: 0.9998 0.0186 0.009267 -0.003264
======CamData=====
 cam ts: 0.8
position:  31.51  120.4 -2.783
quaternion qw, qx, qy, qz: 0.9998 0.006676 -0.01613 -0.003159
======PVAX=====
 imu state ts: 0.8
position lat, lon, alt: 31.51 120.4     0
velocity: 25  0  0
quaternion qw, qx, qy, qz: 1 0 0 0


gt_pqv_ecef
-2.754e+06,4.694e+06,3.314e+06,-0.7572,0.4336,-0.424,-0.2428,6.612,-11.27,21.31,
iter      cost      cost_change  |gradient|   |step|    tr_ratio  tr_radius  ls_iter  iter_time  total_time
   0  3.423276e-01    0.00e+00    2.88e+01   0.00e+00   0.00e+00  1.00e+04        0    7.23e-04    7.97e-04
   1  5.427743e-07    3.42e-01    9.57e-02   2.69e-01   1.00e+00  3.00e+04        1    9.53e-04    1.77e-03
iter      cost      cost_change  |gradient|   |step|    tr_ratio  tr_radius  ls_iter  iter_time  total_time
   0  2.481995e-01    0.00e+00    1.69e+03   0.00e+00   0.00e+00  1.00e+04        0    1.15e-03    1.18e-03
   1  1.120970e-01    1.36e-01    3.37e-01   8.97e-02   1.00e+00  3.00e+04        1    1.84e-03    3.03e-03
iter      cost      cost_change  |gradient|   |step|    tr_ratio  tr_radius  ls_iter  iter_time  total_time
   0  9.369383e-01    0.00e+00    4.95e+03   0.00e+00   0.00e+00  1.00e+04        0    1.74e-03    1.76e-03
   1  3.362409e-01    6.01e-01    7.34e-01   8.98e-02   1.00e+00  3.00e+04        1    2.73e-03    4.51e-03
iter      cost      cost_change  |gradient|   |step|    tr_ratio  tr_radius  ls_iter  iter_time  total_time
   0  2.479558e+00    0.00e+00    9.62e+03   0.00e+00   0.00e+00  1.00e+04        0    2.19e-03    2.22e-03
   1  5.987548e-01    1.88e+00    1.27e+00   7.17e-02   1.00e+00  3.00e+04        1    3.49e-03    5.71e-03

Solver Summary (v 1.14.0-eigen-(3.2.92)-lapack-suitesparse-(4.4.6)-cxsparse-(3.1.4)-eigensparse-openmp-no_tbb)

                                     Original                  Reduced
Parameter blocks                           11                        7
Parameters                                 87                       55
Effective parameters                       81                       51
Residual blocks                             9                        9
Residuals                                  90                       90

Minimizer                        TRUST_REGION

Sparse linear algebra library    SUITE_SPARSE
Trust region strategy     LEVENBERG_MARQUARDT

                                        Given                     Used
Linear solver          SPARSE_NORMAL_CHOLESKY   SPARSE_NORMAL_CHOLESKY
Threads                                     1                        1
Linear solver ordering              AUTOMATIC                        7

Cost:
Initial                          2.479558e+00
Final                            5.987548e-01
Change                           1.880804e+00

Minimizer iterations                        2
Successful steps                            2
Unsuccessful steps                          0

Time (in seconds):
Preprocessor                         0.000026

  Residual only evaluation           0.002400 (2)
  Jacobian & residual evaluation     0.004336 (2)
  Linear solver                      0.000114 (2)
Minimizer                            0.006976

Postprocessor                        0.000008
Total                                0.007009

Termination:                      CONVERGENCE (Parameter tolerance reached. Relative step_norm: 6.619672e-13 <= 1.000000e-08.)


Estimation errors of pose error, P_xyz, Q_xyzw
Frame: 0
0   0   0   0   0   0   0   
Frame: 1
6.193e-07   5.29e-07   -2.277e-07   -1.455e-06   -1.485e-06   -7.624e-07   3.218e-06   
Frame: 2
1.051e-06   9.807e-07   -4.256e-07   -1.927e-06   -1.608e-06   -7.199e-07   4.394e-06   
Frame: 3
5.742e-07   5.737e-07   -2.501e-07   -1.436e-06   -9.785e-07   -3.592e-07   3.358e-06   
Frame: 4
0   0   0   0   0   0   0   

Estimation errors of speedbias error, V_xyz, Ba_xyz, Bg_xyz
Frame: 0
0   0   0   0   0   0   0   0   0   
Frame: 1
4.006e-06   3.644e-06   -1.568e-06   -5.571e-09   -1.462e-08   -4.626e-09   6.618e-10   4.351e-11   -4.643e-10   
Frame: 2
-1.828e-07   2.125e-07   -9.847e-08   -7.379e-09   -1.951e-08   -6.176e-09   1.014e-09   1.62e-11   -6.237e-10   
Frame: 3
-3.82e-06   -3.694e-06   1.616e-06   -5.494e-09   -1.463e-08   -4.635e-09   8.529e-10   -2.874e-11   -4.643e-10   
Frame: 4
0   0   0   0   0   0   0   0   0   
-0.006693,-0.01007,0.01332,3.232e-05,5.913e-05,-3.151e-05,1,
error of lever arm x, y, z (meter): 0.09993, 0.1498, -0.2001
error of imu to cam rotation: 0.1218
```

## Results after debug

```c++
➜  sensor-fusion-navigation-v3 git:(ahrs) ✗ ./bin/test_simulated_imu_cam_factor_multiframe
Process /mnt/truenas/scratch/xiang.zhang/imu_cam_two_laps_ned.csv with noise flag: 0
skip the header
Loaded 101 frames.
=====frameINFO=====
======IMUData=====
 imu ts: 0
acc:         0 -0.001906    -9.794
gyro:  6.217e-05 -3.935e-06 -3.811e-05
======CamData=====
 cam ts: 0
position: 31.51 120.4    -2
quaternion qw, qx, qy, qz: 0.9999 0.004325 -0.008745 0.004325
======CamData=====
 cam ts: 0
position:  31.51  120.4 -2.264
quaternion qw, qx, qy, qz: 0.9998 0.01774 0.01213 -0.002176
======CamData=====
 cam ts: 0
position:  31.51  120.4 -2.762
quaternion qw, qx, qy, qz: 0.9998 0.007286 -0.01568 -0.004503
======PVAX=====
 imu state ts: 0
position lat, lon, alt: 31.51 120.4     0
velocity: 25  0  0
quaternion qw, qx, qy, qz: 1 0 0 0


gt_pqv_ecef
-2.754e+06,4.694e+06,3.314e+06,-0.7572,0.4336,-0.424,-0.2428,6.612,-11.27,21.31,
=====frameINFO=====
======IMUData=====
 imu ts: 0.2
acc:         0 -0.001906    -9.794
gyro:  6.217e-05 -3.935e-06 -3.811e-05
======CamData=====
 cam ts: 0.2
position: 31.51 120.4    -2
quaternion qw, qx, qy, qz: 0.9999 0.004325 -0.008745 0.004325
======CamData=====
 cam ts: 0.2
position:  31.51  120.4 -2.169
quaternion qw, qx, qy, qz: 0.9998 0.01704 0.01041 -0.003265
======CamData=====
 cam ts: 0.2
position:  31.51  120.4 -2.717
quaternion qw, qx, qy, qz: 0.9998 0.006801 -0.01596 -0.003579
======PVAX=====
 imu state ts: 0.2
position lat, lon, alt: 31.51 120.4     0
velocity: 25  0  0
quaternion qw, qx, qy, qz: 1 0 0 0


gt_pqv_ecef
-2.754e+06,4.694e+06,3.314e+06,-0.7572,0.4336,-0.424,-0.2428,6.612,-11.27,21.31,
=====frameINFO=====
======IMUData=====
 imu ts: 0.4
acc:         0 -0.001906    -9.794
gyro:  6.217e-05 -3.935e-06 -3.811e-05
======CamData=====
 cam ts: 0.4
position: 31.51 120.4    -2
quaternion qw, qx, qy, qz: 0.9999 0.004325 -0.008745 0.004325
======CamData=====
 cam ts: 0.4
position:  31.51  120.4 -2.264
quaternion qw, qx, qy, qz: 0.9998 0.01686 0.01023 -0.003693
======CamData=====
 cam ts: 0.4
position: 31.51 120.4 -2.85
quaternion qw, qx, qy, qz: 0.9998 0.005744 -0.01595 -0.005066
======PVAX=====
 imu state ts: 0.4
position lat, lon, alt: 31.51 120.4     0
velocity: 25  0  0
quaternion qw, qx, qy, qz: 1 0 0 0


gt_pqv_ecef
-2.754e+06,4.694e+06,3.314e+06,-0.7572,0.4336,-0.424,-0.2428,6.612,-11.27,21.31,
=====frameINFO=====
======IMUData=====
 imu ts: 0.6
acc:         0 -0.001906    -9.794
gyro:  6.217e-05 -3.935e-06 -3.811e-05
======CamData=====
 cam ts: 0.6
position: 31.51 120.4    -2
quaternion qw, qx, qy, qz: 0.9999 0.004325 -0.008745 0.004325
======CamData=====
 cam ts: 0.6
position:  31.51  120.4 -2.271
quaternion qw, qx, qy, qz: 0.9998 0.01865 0.009833 -0.0006232
======CamData=====
 cam ts: 0.6
position: 31.51 120.4 -2.84
quaternion qw, qx, qy, qz: 0.9998 0.006875 -0.01718 -0.003751
======PVAX=====
 imu state ts: 0.6
position lat, lon, alt: 31.51 120.4     0
velocity: 25  0  0
quaternion qw, qx, qy, qz: 1 0 0 0


gt_pqv_ecef
-2.754e+06,4.694e+06,3.314e+06,-0.7572,0.4336,-0.424,-0.2428,6.612,-11.27,21.31,
=====frameINFO=====
======IMUData=====
 imu ts: 0.8
acc:         0 -0.001906    -9.794
gyro:  6.217e-05 -3.935e-06 -3.811e-05
======CamData=====
 cam ts: 0.8
position: 31.51 120.4    -2
quaternion qw, qx, qy, qz: 0.9999 0.004325 -0.008745 0.004325
======CamData=====
 cam ts: 0.8
position:  31.51  120.4 -2.224
quaternion qw, qx, qy, qz: 0.9998 0.0186 0.009267 -0.003264
======CamData=====
 cam ts: 0.8
position:  31.51  120.4 -2.783
quaternion qw, qx, qy, qz: 0.9998 0.006676 -0.01613 -0.003159
======PVAX=====
 imu state ts: 0.8
position lat, lon, alt: 31.51 120.4     0
velocity: 25  0  0
quaternion qw, qx, qy, qz: 1 0 0 0


gt_pqv_ecef
-2.754e+06,4.694e+06,3.314e+06,-0.7572,0.4336,-0.424,-0.2428,6.612,-11.27,21.31,
p_imu2cam_noisy  2.1
-1.35
  1.8
delta_p0
0
0
delta_q0
0
0,1
iter      cost      cost_change  |gradient|   |step|    tr_ratio  tr_radius  ls_iter  iter_time  total_time
   0  3.423276e-01    0.00e+00    2.88e+01   0.00e+00   0.00e+00  1.00e+04        0    7.66e-04    8.59e-04
   1  5.427743e-07    3.42e-01    9.57e-02   2.69e-01   1.00e+00  3.00e+04        1    9.72e-04    1.86e-03
p_imu2cam_noisy   2
-1.5
   2
delta_p-0.09998
   -0.15
     0.2
delta_q 0.0004403
 0.0008763
-0.0004263,1
iter      cost      cost_change  |gradient|   |step|    tr_ratio  tr_radius  ls_iter  iter_time  total_time
   0  2.481995e-01    0.00e+00    1.69e+03   0.00e+00   0.00e+00  1.00e+04        0    1.45e-03    1.49e-03
   1  1.120970e-01    1.36e-01    3.37e-01   8.97e-02   1.00e+00  3.00e+04        1    2.31e-03    3.82e-03
p_imu2cam_noisy1.933
 -1.6
2.133
delta_p-0.06665
-0.09994
  0.1334
delta_q 0.0002906
 0.0005846
-0.0002826,1
iter      cost      cost_change  |gradient|   |step|    tr_ratio  tr_radius  ls_iter  iter_time  total_time
   0  9.369383e-01    0.00e+00    4.95e+03   0.00e+00   0.00e+00  1.00e+04        0    2.19e-03    2.23e-03
   1  3.362409e-01    6.01e-01    7.34e-01   8.98e-02   1.00e+00  3.00e+04        1    4.08e-03    6.32e-03
p_imu2cam_noisy  1.9
-1.65
  2.2
delta_p-0.0333
-0.0499
0.06672
delta_q 0.0001417
 0.0002929
-0.0001395,1
iter      cost      cost_change  |gradient|   |step|    tr_ratio  tr_radius  ls_iter  iter_time  total_time
   0  2.479558e+00    0.00e+00    9.62e+03   0.00e+00   0.00e+00  1.00e+04        0    2.74e-03    2.78e-03
   1  5.987548e-01    1.88e+00    1.27e+00   7.17e-02   1.00e+00  3.00e+04        1    4.35e-03    7.14e-03

Solver Summary (v 1.14.0-eigen-(3.2.92)-lapack-suitesparse-(4.4.6)-cxsparse-(3.1.4)-eigensparse-openmp-no_tbb)

                                     Original                  Reduced
Parameter blocks                           11                        7
Parameters                                 87                       55
Effective parameters                       81                       51
Residual blocks                             9                        9
Residuals                                  90                       90

Minimizer                        TRUST_REGION

Sparse linear algebra library    SUITE_SPARSE
Trust region strategy     LEVENBERG_MARQUARDT

                                        Given                     Used
Linear solver          SPARSE_NORMAL_CHOLESKY   SPARSE_NORMAL_CHOLESKY
Threads                                     1                        1
Linear solver ordering              AUTOMATIC                        7

Cost:
Initial                          2.479558e+00
Final                            5.987548e-01
Change                           1.880804e+00

Minimizer iterations                        2
Successful steps                            2
Unsuccessful steps                          0

Time (in seconds):
Preprocessor                         0.000041

  Residual only evaluation           0.002932 (2)
  Jacobian & residual evaluation     0.005394 (2)
  Linear solver                      0.000180 (2)
Minimizer                            0.008707

Postprocessor                        0.000013
Total                                0.008762

Termination:                      CONVERGENCE (Parameter tolerance reached. Relative step_norm: 6.619672e-13 <= 1.000000e-08.)


Estimation errors of pose error, P_xyz, Q_xyzw
Frame: 0
0   0   0   0   0   0   0   
Frame: 1
6.193e-07   5.29e-07   -2.277e-07   -1.455e-06   -1.485e-06   -7.624e-07   3.218e-06   
Frame: 2
1.051e-06   9.807e-07   -4.256e-07   -1.927e-06   -1.608e-06   -7.199e-07   4.394e-06   
Frame: 3
5.742e-07   5.737e-07   -2.501e-07   -1.436e-06   -9.785e-07   -3.592e-07   3.358e-06   
Frame: 4
0   0   0   0   0   0   0   

Estimation errors of speedbias error, V_xyz, Ba_xyz, Bg_xyz
Frame: 0
0   0   0   0   0   0   0   0   0   
Frame: 1
4.006e-06   3.644e-06   -1.568e-06   -5.571e-09   -1.462e-08   -4.626e-09   6.618e-10   4.351e-11   -4.643e-10   
Frame: 2
-1.828e-07   2.125e-07   -9.847e-08   -7.379e-09   -1.951e-08   -6.176e-09   1.014e-09   1.62e-11   -6.237e-10   
Frame: 3
-3.82e-06   -3.694e-06   1.616e-06   -5.494e-09   -1.463e-08   -4.635e-09   8.529e-10   -2.874e-11   -4.643e-10   
Frame: 4
0   0   0   0   0   0   0   0   0   
-0.006693,-0.01007,0.01332,3.232e-05,5.913e-05,-3.151e-05,1,
error of lever arm x, y, z (meter): 0.09993, 0.1498, -0.2001
error of imu to cam rotation: 0.1218

```

