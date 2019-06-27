### Simulation

#### 1. IMU model

```python
    # IMU model, according to STIM300 used by NovAtel                                                                                                                                                                             
    imu_err = {                                                                                                                                                                                                                    
               'gyro_b': np.array([0.01, 0.01, 0.01]),                                                                                                                                                                             
               'gyro_arw': np.array([0.15, 0.15, 0.15]),                                                                                                                                                                           
               'gyro_b_stability': np.array([0.3, 0.3, 0.3]),                                                                                                                                                                      
               'gyro_b_corr': np.array([100.0, 100.0, 100.0]),                                                                                                                                                                     
               'accel_b': np.array([4.0e-4, 4.0e-4, 4.0e-4]),  # follow high accuracy acc                                                                                                                                          
               'accel_vrw': np.array([2.5e-5, 2.5e-5, 2.5e-5]),                                                                                                                                                                    
               'accel_b_stability': np.array([4e-4, 4e-4, 4e-4]),                                                                                                                                                                  
               'accel_b_corr': np.array([100.0, 100.0, 100.0])                                                                                                                                                                     
              }
```



#### 2. Motion profile

![1561666799338](/home/xiang.zhang/gitRepo/project/doc_sideslip/plots/1561666799338.png)



#### 3. Statistics

```python
------------------------------------------------------------
Sample frequency of IMU: [fs] = 125.0 Hz
Reference frame: 0
Simulation time duration: 480.0 s
Simulation runs: 1

------------------------------------------------------------
Simulation results are saved to /home/xiang.zhang/gitRepo/gnss-ins-sim/demo_saved_data/2019-06-27-12-21-30
The following results are saved:
        time: sample time
        ref_pos: true LLA pos in the navigation frame
        ref_vel: true vel in the body frame
        ref_att_euler: true attitude (Euler angles, ZYX)
        ref_accel: true accel in the body frame
        ref_gyro: true angular velocity in the body frame
        accel: accel measurements
        gyro: gyro measurements
        att_euler: simulation attitude (Euler, ZYX)  from algo
        pos: simulation position from algo
        vel: simulation velocity from algo
        ref_att_quat: true attitude (quaternion)
        att_quat: simulation attitude (quaternion)  from algo

------------------------------------------------------------
The following are error statistics.
-----------statistics for simulation attitude (Euler, ZYX)  from algo (in units of ['deg', 'deg', 'deg'])
        --Max error: [0.36725186 0.29685345 0.09155358]
        --Avg error: [-0.36725186  0.29685345  0.09155358]
        --Std of error: [0. 0. 0.]

-----------statistics for simulation position from algo (in units of ['deg', 'deg', 'm'])
        --Max error: [4.47011018e-03 1.40983403e-02 2.83864161e+01]
        --Avg error: [ 4.47011018e-03 -1.40983403e-02 -2.83864161e+01]
        --Std of error: [0. 0. 0.]

-----------statistics for simulation velocity from algo (in units of ['m/s', 'm/s', 'm/s'])
        --Max error: [2.71104866 6.26605209 0.21218976]
        --Avg error: [-2.71104866 -6.26605209  0.21218976]
        --Std of error: [0. 0. 0.]
```



#### 4. Plots

![1561667189022](/home/xiang.zhang/gitRepo/project/doc_sideslip/plots/1561667189022.png)

![1561667212281](/home/xiang.zhang/gitRepo/project/doc_sideslip/plots/1561667212281.png)



![1561667311758](/home/xiang.zhang/gitRepo/project/doc_sideslip/plots/1561667311758.png)



#### 5. Simulation validation

##### 5.1 Euler angle and angular rate

![1561667388949](/home/xiang.zhang/gitRepo/project/doc_sideslip/plots/1561667388949.png)

![1561667429180](/home/xiang.zhang/gitRepo/project/doc_sideslip/plots/1561667429180.png)



##### 5.2 Velocity and acceleration

###### 5.2.1 Ground truth

![1561667474207](/home/xiang.zhang/gitRepo/project/doc_sideslip/plots/1561667474207.png)

###### 5.2.2 Simulated

![1561667521238](/home/xiang.zhang/gitRepo/project/doc_sideslip/plots/1561667521238.png)

###### 5.2.3 Proof related to body frame acceleration error [1]

![1561667913121](/home/xiang.zhang/gitRepo/project/doc_sideslip/plots/1561667913121.png)

##### ![1561667957506](/home/xiang.zhang/gitRepo/project/doc_sideslip/plots/1561667957506.png)

[1] Strapdown Inertial Navigation Technology - 2nd Edition David H. Titterton and John L. Weston