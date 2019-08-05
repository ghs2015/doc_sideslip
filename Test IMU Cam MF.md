### Test IMU Cam MF

### To to
- [x] quick refactor
	- [x] data driven using json config and remove magic numbers
		- [x] move config related to json.
		- [x] read from json
- [x] Add cam noise (bias + noise) option for loading.
- [x] debug of unstable data loading.
- [x] Add cam noise option
- [x] More tests
  - [x] test more key frames
  - [x] test with noises, using noisy cam and noisy IMU data.
- [ ] quickly refactor IMU-CAM single frame?? need??
- [ ] Add all three cams?


### To debug

- [x] calibration over optimized? => caused by fixed cam factor and updated calibration parameters.
- [x] lock PVA and optimize only calibration( or and bias). => similar results.
- [x] more print 





### Log

- calibration over optimized

  ```c++
  p_imu2cam_noisy:  2.1, -1.35, 1.8;
  delta_p:  0, 0, 0;
  delta_q:  0, 0, 0; 1
  
  iter      cost      cost_change  |gradient|   |step|    tr_ratio  tr_radius  ls_iter  iter_time  total_time
     0  3.423276e-01    0.00e+00    2.88e+01   0.00e+00   0.00e+00  1.00e+04        0    1.37e-03    1.50e-03
     1  5.427743e-07    3.42e-01    9.57e-02   2.69e-01   1.00e+00  3.00e+04        1    1.87e-03    3.40e-03
  
  p_imu2cam_noisy:  2, -1.5, 2;
  delta_p:  -0.09998, -0.15, 0.2;
  delta_q:  0.0004403, 0.0008763, -0.0004263; 1
  
  iter      cost      cost_change  |gradient|   |step|    tr_ratio  tr_radius  ls_iter  iter_time  total_time
     0  2.481995e-01    0.00e+00    1.69e+03   0.00e+00   0.00e+00  1.00e+04        0    1.48e-03    1.52e-03
     1  1.120970e-01    1.36e-01    3.37e-01   8.97e-02   1.00e+00  3.00e+04        1    2.03e-03    3.56e-03
  
  p_imu2cam_noisy:  1.933, -1.6, 2.133;
  delta_p:  -0.06665, -0.09994, 0.1334;
  delta_q:  0.0002906, 0.0005846, -0.0002826; 1
  
  iter      cost      cost_change  |gradient|   |step|    tr_ratio  tr_radius  ls_iter  iter_time  total_time
     0  9.369383e-01    0.00e+00    4.95e+03   0.00e+00   0.00e+00  1.00e+04        0    1.75e-03    1.79e-03
     1  3.362409e-01    6.01e-01    7.34e-01   8.98e-02   1.00e+00  3.00e+04        1    2.81e-03    4.61e-03
  
  p_imu2cam_noisy:  1.9, -1.65, 2.2;
  delta_p:  -0.0333, -0.0499, 0.06672;
  delta_q:  0.0001417, 0.0002929, -0.0001395; 1
  
  iter      cost      cost_change  |gradient|   |step|    tr_ratio  tr_radius  ls_iter  iter_time  total_time
     0  2.479558e+00    0.00e+00    9.62e+03   0.00e+00   0.00e+00  1.00e+04        0    2.34e-03    2.39e-03
     1  5.753269e-01    1.90e+00    1.23e+00   7.18e-02   1.00e+00  3.00e+04        1    3.65e-03    6.05e-03
  
  p_imu2cam_noisy:  1.893, -1.66, 2.213;
  delta_p:  -0.006614, -0.009869, 0.01339;
  delta_q:  2.291e-05, 5.991e-05, -2.528e-05; 1
  
  iter      cost      cost_change  |gradient|   |step|    tr_ratio  tr_radius  ls_iter  iter_time  total_time
     0  5.353079e+00    0.00e+00    1.55e+04   0.00e+00   0.00e+00  1.00e+04        0    2.78e-03    2.81e-03
     1  7.836501e-01    4.57e+00    2.24e+00   5.08e-02   1.00e+00  3.00e+04        1    4.40e-03    7.21e-03
  
  Estimation errors of pose error, P_xyz, Q_xyzw
  Frame: 0:  0   0   0   0   0   0   0   
  Frame: 1:  1.079e-06   9.844e-07   -4.065e-07   -1.883e-06   -1.901e-06   -9.771e-07   4.182e-06   
  Frame: 2:  2.336e-06   2.307e-06   -9.579e-07   -2.807e-06   -2.348e-06   -1.065e-06   6.42e-06   
  Frame: 3:  2.272e-06   2.402e-06   -9.96e-07   -2.791e-06   -1.947e-06   -7.472e-07   6.532e-06   
  Frame: 4:  1.004e-06   1.107e-06   -4.582e-07   -1.851e-06   -1.098e-06   -3.416e-07   4.407e-06   
  Frame: 5:  0   0   0   0   0   0   0   
  
  Estimation errors of speedbias error, V_xyz, Ba_xyz, Bg_xyz
  Frame: 0:  0   0   0   0   0   0   0   0   0   
  Frame: 1:  7.897e-06   7.591e-06   -3.138e-06   -7.176e-09   -1.901e-08   -6.176e-09   8.277e-10   8.773e-11   -6.249e-10   
  Frame: 2:  3.532e-06   4.323e-06   -1.797e-06   -1.069e-08   -2.855e-08   -9.288e-09   1.434e-09   7.196e-11   -9.449e-10   
  Frame: 3:  -3.993e-06   -3.494e-06   1.474e-06   -1.061e-08   -2.857e-08   -9.303e-09   1.616e-09   -5.153e-12   -9.396e-10   
  Frame: 4:  -7.399e-06   -8.106e-06   3.365e-06   -7.014e-09   -1.904e-08   -6.197e-09   1.194e-09   -6.325e-11   -6.166e-10   
  Frame: 5:  0   0   0   0   0   0   0   0   0   
  
  last calib_error_params estimation: : 0.01218,0.01823,-0.02448,-5.024e-05,-0.0001062,4.789e-05,1
  
  error of lever arm x, y, z (meter):  0.1065, 0.1597, -0.2135;
  error of imu to cam rotation: 0.1297
  
  ```

  locked the PVA:

  ```c++
  p_imu2cam_noisy:  2.1, -1.35, 1.8;
  delta_p:  0, 0, 0;
  delta_q:  0, 0, 0; 1
  
  iter      cost      cost_change  |gradient|   |step|    tr_ratio  tr_radius  ls_iter  iter_time  total_time
     0  3.423276e-01    0.00e+00    2.88e+01   0.00e+00   0.00e+00  1.00e+04        0    1.34e-03    1.46e-03
     1  5.427743e-07    3.42e-01    9.57e-02   2.69e-01   1.00e+00  3.00e+04        1    1.63e-03    3.13e-03
  lock paramter for key frame 1
  
  p_imu2cam_noisy:  2, -1.5, 2;
  delta_p:  -0.09998, -0.15, 0.2;
  delta_q:  0.0004403, 0.0008763, -0.0004263; 1
  
  iter      cost      cost_change  |gradient|   |step|    tr_ratio  tr_radius  ls_iter  iter_time  total_time
     0  2.481995e-01    0.00e+00    1.69e+03   0.00e+00   0.00e+00  1.00e+04        0    8.95e-04    1.36e-03
     1  1.120989e-01    1.36e-01    3.32e-01   8.97e-02   1.00e+00  3.00e+04        1    1.27e-03    2.65e-03
  lock paramter for key frame 2
  
  p_imu2cam_noisy:  1.933, -1.6, 2.133;
  delta_p:  -0.06665, -0.09994, 0.1334;
  delta_q:  0.0002905, 0.0005844, -0.0002825; 1
  
  iter      cost      cost_change  |gradient|   |step|    tr_ratio  tr_radius  ls_iter  iter_time  total_time
     0  9.409373e-01    0.00e+00    4.96e+03   0.00e+00   0.00e+00  1.00e+04        0    7.07e-04    1.32e-03
     1  3.362484e-01    6.05e-01    7.30e-01   8.98e-02   1.00e+00  3.00e+04        1    1.11e-03    2.43e-03
  lock paramter for key frame 3
  
  p_imu2cam_noisy:  1.9, -1.65, 2.2;
  delta_p:  -0.0333, -0.0499, 0.06672;
  delta_q:  0.0001415, 0.0002924, -0.0001391; 1
  
  iter      cost      cost_change  |gradient|   |step|    tr_ratio  tr_radius  ls_iter  iter_time  total_time
     0  2.532609e+00    0.00e+00    9.72e+03   0.00e+00   0.00e+00  1.00e+04        0    7.92e-04    1.68e-03
     1  5.753322e-01    1.96e+00    1.30e+00   7.18e-02   1.00e+00  3.00e+04        1    1.19e-03    2.88e-03
  lock paramter for key frame 4
  
  p_imu2cam_noisy:  1.893, -1.66, 2.213;
  delta_p:  -0.006612, -0.00986, 0.0134;
  delta_q:  2.259e-05, 5.887e-05, -2.463e-05; 1
  
  iter      cost      cost_change  |gradient|   |step|    tr_ratio  tr_radius  ls_iter  iter_time  total_time
     0  5.668886e+00    0.00e+00    9.17e-01   0.00e+00   0.00e+00  1.00e+04        0    4.17e-04    1.87e-03
     1  5.633094e+00    3.58e-02    1.00e-03   5.08e-02   1.00e+00  3.00e+04        1    5.34e-04    2.42e-03
  
  Estimation errors of pose error, P_xyz, Q_xyzw
  Frame: 0:  0   0   0   0   0   0   0   
  Frame: 1:  1.543e-05   2.268e-05   -4.438e-06   -3.161e-06   -5.519e-06   -1.77e-06   3.091e-06   
  Frame: 2:  5.892e-05   8.896e-05   -1.747e-05   -6.31e-06   -1.062e-05   -3.203e-06   6.297e-06   
  Frame: 3:  0.0001265   0.0001961   -3.852e-05   -9.454e-06   -1.552e-05   -4.469e-06   9.563e-06   
  Frame: 4:  0.0002143   0.0003414   -6.689e-05   -1.26e-05   -2.038e-05   -5.702e-06   1.284e-05   
  Frame: 5:  0   0   0   0   0   0   0   
  
  Estimation errors of speedbias error, V_xyz, Ba_xyz, Bg_xyz
  Frame: 0:  0   0   0   0   0   0   0   0   0   
  Frame: 1:  0.0001508   0.0002247   -4.415e-05   -1.135e-12   -2.807e-12   -8.839e-13   1.023e-13   4.408e-15   -7.2e-14   
  Frame: 2:  0.0002811   0.000436   -8.586e-05   -6.798e-12   -1.399e-11   2.116e-12   9.293e-12   1.536e-11   -1.11e-11   
  Frame: 3:  0.0003918   0.0006336   -0.0001243   -1.633e-11   -3.292e-11   5.74e-12   2.299e-11   3.839e-11   -2.759e-11   
  Frame: 4:  0.0004835   0.0008173   -0.0001592   -2.932e-11   -5.92e-11   7.266e-12   3.756e-11   6.296e-11   -4.516e-11   
  Frame: 5:  0   0   0   0   0   0   0   0   0   
  
  last calib_error_params estimation: : 0.01225,0.01839,-0.02442,-5.641e-05,-0.0001069,5.354e-05,1
  
  error of lever arm x, y, z (meter):  0.1065, 0.1597, -0.2135;
  
  ```

  summary 

  ```c++
  
  gt_pqv_ecef
  -2.754e+06,4.694e+06,3.314e+06,-0.7572,0.4336,-0.424,-0.2428,6.612,-11.27,21.31,
  
  delta_p (meter):  0, 0, 0;
  delta_q:  0, 0, 0; 1
  new p_imu2cam estimation:  2.1, -1.35, 1.8;
  error of lever arm x, y, z (meter):  -0.1, -0.15, 0.2;
  error of imu to cam rotation (degree): 0.1228
  iter      cost      cost_change  |gradient|   |step|    tr_ratio  tr_radius  ls_iter  iter_time  total_time
     0  3.423276e-01    0.00e+00    2.88e+01   0.00e+00   0.00e+00  1.00e+04        0    1.22e-03    1.36e-03
     1  5.427743e-07    3.42e-01    9.57e-02   2.69e-01   1.00e+00  3.00e+04        1    1.51e-03    2.90e-03
  
  delta_p (meter):  -0.09998, -0.15, 0.2;
  delta_q:  0.0004403, 0.0008763, -0.0004263; 1
  new p_imu2cam estimation:  2, -1.5, 2;
  error of lever arm x, y, z (meter):  -2.01e-05, -4.657e-05, 7.758e-06;
  error of imu to cam rotation (degree): 0.0004413
  iter      cost      cost_change  |gradient|   |step|    tr_ratio  tr_radius  ls_iter  iter_time  total_time
     0  2.481995e-01    0.00e+00    1.69e+03   0.00e+00   0.00e+00  1.00e+04        0    1.43e-03    1.46e-03
     1  1.120970e-01    1.36e-01    3.37e-01   8.97e-02   1.00e+00  3.00e+04        1    2.21e-03    3.69e-03
  
  delta_p (meter):  -0.06665, -0.09994, 0.1334;
  delta_q:  0.0002906, 0.0005846, -0.0002826; 1
  new p_imu2cam estimation:  1.933, -1.6, 2.133;
  error of lever arm x, y, z (meter):  0.06663, 0.09989, -0.1334;
  error of imu to cam rotation (degree): 0.08124
  iter      cost      cost_change  |gradient|   |step|    tr_ratio  tr_radius  ls_iter  iter_time  total_time
     0  9.369383e-01    0.00e+00    4.95e+03   0.00e+00   0.00e+00  1.00e+04        0    1.82e-03    1.86e-03
     1  3.362409e-01    6.01e-01    7.34e-01   8.98e-02   1.00e+00  3.00e+04        1    2.74e-03    4.62e-03
  
  delta_p (meter):  -0.0333, -0.0499, 0.06672;
  delta_q:  0.0001417, 0.0002929, -0.0001395; 1
  new p_imu2cam estimation:  1.9, -1.65, 2.2;
  error of lever arm x, y, z (meter):  0.09993, 0.1498, -0.2001;
  error of imu to cam rotation (degree): 0.1218
  iter      cost      cost_change  |gradient|   |step|    tr_ratio  tr_radius  ls_iter  iter_time  total_time
     0  2.479558e+00    0.00e+00    9.62e+03   0.00e+00   0.00e+00  1.00e+04        0    2.35e-03    2.38e-03
     1  5.753269e-01    1.90e+00    1.23e+00   7.18e-02   1.00e+00  3.00e+04        1    3.61e-03    6.00e-03
  
  delta_p (meter):  -0.006614, -0.009869, 0.01339;
  delta_q:  2.291e-05, 5.991e-05, -2.528e-05; 1
  new p_imu2cam estimation:  1.893, -1.66, 2.213;
  error of lever arm x, y, z (meter):  0.1065, 0.1597, -0.2135;
  error of imu to cam rotation (degree): 0.1297
  iter      cost      cost_change  |gradient|   |step|    tr_ratio  tr_radius  ls_iter  iter_time  total_time
     0  5.353079e+00    0.00e+00    1.55e+04   0.00e+00   0.00e+00  1.00e+04        0    2.79e-03    2.83e-03
     1  7.836501e-01    4.57e+00    2.24e+00   5.08e-02   1.00e+00  3.00e+04        1    4.47e-03    7.31e-03
  Estimation errors of pose error, P_xyz, Q_xyzw
  Frame: 0:  0   0   0   0   0   0   0   
  Frame: 1:  1.079e-06   9.844e-07   -4.065e-07   -1.883e-06   -1.901e-06   -9.771e-07   4.182e-06   
  Frame: 2:  2.336e-06   2.307e-06   -9.579e-07   -2.807e-06   -2.348e-06   -1.065e-06   6.42e-06   
  Frame: 3:  2.272e-06   2.402e-06   -9.96e-07   -2.791e-06   -1.947e-06   -7.472e-07   6.532e-06   
  Frame: 4:  1.004e-06   1.107e-06   -4.582e-07   -1.851e-06   -1.098e-06   -3.416e-07   4.407e-06   
  Frame: 5:  0   0   0   0   0   0   0   
  
  Estimation errors of speedbias error, V_xyz, Ba_xyz, Bg_xyz
  Frame: 0:  0   0   0   0   0   0   0   0   0   
  Frame: 1:  7.897e-06   7.591e-06   -3.138e-06   -7.176e-09   -1.901e-08   -6.176e-09   8.277e-10   8.773e-11   -6.249e-10   
  Frame: 2:  3.532e-06   4.323e-06   -1.797e-06   -1.069e-08   -2.855e-08   -9.288e-09   1.434e-09   7.196e-11   -9.449e-10   
  Frame: 3:  -3.993e-06   -3.494e-06   1.474e-06   -1.061e-08   -2.857e-08   -9.303e-09   1.616e-09   -5.153e-12   -9.396e-10   
  Frame: 4:  -7.399e-06   -8.106e-06   3.365e-06   -7.014e-09   -1.904e-08   -6.197e-09   1.194e-09   -6.325e-11   -6.166e-10   
  Frame: 5:  0   0   0   0   0   0   0   0   0   
  
  last calib_error_params estimation: : 0.01218,0.01823,-0.02448,-5.024e-05,-0.0001062,4.789e-05,1
  leverarm errors (frame 0 is initial state)
  Frame 0:  -0.1, -0.15, 0.2;
  Frame 1:  -2.01e-05, -4.657e-05, 7.758e-06;
  Frame 2:  0.06663, 0.09989, -0.1334;
  Frame 3:  0.09993, 0.1498, -0.2001;
  Frame 4:  0.1065, 0.1597, -0.2135;
  misalignments (frame 0 is initial state)
  Frame 0: 0.1228
  Frame 1: 0.0004413
  Frame 2: 0.08124
  Frame 3: 0.1218
  Frame 4: 0.1297
  ```

  

