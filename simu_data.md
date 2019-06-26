## Simu-1: A simple circle motion profile

#### 1. IMU

``` python
    # IMU model, according to STIM300 used by NovAtel                               
    imu_err = {
               'gyro_b': np.array([0.01, 0.01, 0.01]) * D2R,     
               'gyro_arw': np.array([0.15, 0.15, 0.15]) * D2R/60,  
               'gyro_b_stability': np.array([0.3, 0.3, 0.3]) * D2R/3600,  
               'gyro_b_corr': np.array([100.0, 100.0, 100.0]), 
               'accel_b': np.array([4e-4, 4e-4, 4e-4]),  # follow high accuracy acc
               'accel_vrw': np.array([2.5e-5, 2.5e-5, 2.5e-5]) / 60,
               'accel_b_stability': np.array([4e-4, 4e-4, 4e-4]),                        'accel_b_corr': np.array([100.0, 100.0, 100.0])
               }  
```

#### 2. Motion profile

![1561505629146](/home/xiang.zhang/gitRepo/project/doc_sideslip/plots/1561505629146.png)

#### 3. Plots

![1561505695409](/home/xiang.zhang/gitRepo/project/doc_sideslip/plots/1561505695409.png)

![1561505783545](/home/xiang.zhang/gitRepo/project/doc_sideslip/plots/1561505783545.png)

![1561505869329](/home/xiang.zhang/gitRepo/project/doc_sideslip/plots/1561505869329.png)

![1561505930872](/home/xiang.zhang/gitRepo/project/doc_sideslip/plots/1561505930872.png)

![1561505951052](/home/xiang.zhang/gitRepo/project/doc_sideslip/plots/1561505951052.png)

![1561505977174](/home/xiang.zhang/gitRepo/project/doc_sideslip/plots/1561505977174.png)

#### 4. Statistics

``` python

Sample frequency of IMU: [fs] = 125.0 Hz
Reference frame: 0
Simulation time duration: 390.0 s
Simulation runs: 1

------------------------------------------------------------
Simulation results are saved to /home/xiang.zhang/gitRepo/gnss-ins-sim/demo_saved_data/2019-06-25-16-27-15
The following results are saved:
        time: sample time
        ref_pos: true LLA pos in the navigation frame
        ref_vel: true vel in the body frame
        ref_att_euler: true attitude (Euler angles, ZYX)
        ref_accel: true accel in the body frame
        ref_gyro: true angular velocity in the body frame
        accel: accel measurements
        gyro: gyro measurements
        pos: simulation position from algo
        att_euler: simulation attitude (Euler, ZYX)  from algo
        vel: simulation velocity from algo
        ref_att_quat: true attitude (quaternion)
        att_quat: simulation attitude (quaternion)  from algo

------------------------------------------------------------
The following are error statistics.
-----------statistics for simulation position from algo (in units of ['deg', 'deg', 'm'])
        --Max error: [1.15060776e-01 1.03006949e-01 1.25321446e+03]
        --Avg error: [ 1.15060776e-01 -1.03006949e-01 -1.25321446e+03]
        --Std of error: [0. 0. 0.]

-----------statistics for simulation attitude (Euler, ZYX)  from algo (in units of ['deg', 'deg', 'deg'])
        --Max error: [132.02377177   0.81144294   2.27268687]
        --Avg error: [-132.02377177    0.81144294    2.27268687]
        --Std of error: [0. 0. 0.]

-----------statistics for simulation velocity from algo (in units of ['m/s', 'm/s', 'm/s'])
        --Max error: [53.20970605 76.24952627  0.26149887]
        --Avg error: [-53.20970605  76.24952627  -0.26149887]
        --Std of error: [0. 0. 0.]

```



### Simu-2: Two laps

#### Motion profile

![1561508229429](/home/xiang.zhang/gitRepo/project/doc_sideslip/plots/1561508229429.png)

#### Plots

![1561508358918](/home/xiang.zhang/gitRepo/project/doc_sideslip/plots/1561508358918.png)



![1561508376120](/home/xiang.zhang/gitRepo/project/doc_sideslip/plots/1561508376120.png)

![1561508635924](/home/xiang.zhang/gitRepo/project/doc_sideslip/plots/1561508635924.png)



![1561508765687](/home/xiang.zhang/gitRepo/project/doc_sideslip/plots/1561508765687.png)

![1561508809237](/home/xiang.zhang/gitRepo/project/doc_sideslip/plots/1561508809237.png)

#### Statistics
``` python
------------------------------------------------------------
Sample frequency of IMU: [fs] = 125.0 Hz
Reference frame: 0
Simulation time duration: 480.0 s
Simulation runs: 1

------------------------------------------------------------
Simulation results are saved to /home/xiang.zhang/gitRepo/gnss-ins-sim/demo_saved_data/2019-06-25-17-09-22
The following results are saved:
        time: sample time
        ref_pos: true LLA pos in the navigation frame
        ref_vel: true vel in the body frame
        ref_att_euler: true attitude (Euler angles, ZYX)
        ref_accel: true accel in the body frame
        ref_gyro: true angular velocity in the body frame
        accel: accel measurements
        gyro: gyro measurements
        pos: simulation position from algo
        vel: simulation velocity from algo
        att_euler: simulation attitude (Euler, ZYX)  from algo
        ref_att_quat: true attitude (quaternion)
        att_quat: simulation attitude (quaternion)  from algo

------------------------------------------------------------
The following are error statistics.
-----------statistics for simulation position from algo (in units of ['deg', 'deg', 'm'])
        --Max error: [1.77823015e-01 1.84534769e-01 1.65537692e+03]
        --Avg error: [ 1.77823015e-01 -1.84534769e-01 -1.65537692e+03]
        --Std of error: [0. 0. 0.]

-----------statistics for simulation velocity from algo (in units of ['m/s', 'm/s', 'm/s'])
        --Max error: [ 67.93422452 114.31255687   0.93035783]
        --Avg error: [-67.93422452 114.31255687  -0.93035783]
        --Std of error: [0. 0. 0.]

-----------statistics for simulation attitude (Euler, ZYX)  from algo (in units of ['deg', 'deg', 'deg'])
        --Max error: [132.05139063   0.98920871   2.7397607 ]
        --Avg error: [-132.05139063    0.98920871    2.7397607 ]
        --Std of error: [0. 0. 0.]
```