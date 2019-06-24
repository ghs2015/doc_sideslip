# B4 Correlation analysis

## 1. General states

### Side slip angle and others

[link](/home/xiang.zhang/gitRepo/sideslip/examples/plots/2019-06-21_13-50-27_body_and_vehicle_rate_bias_onesecsmth/sideslip)

[All plots](/home/xiang.zhang/gitRepo/sideslip/examples/plots/2019-06-21_16-13-00_vehicle_imu_frame_all_pose)

### Azimuth and roll



![1561052970645](/home/xiang.zhang/gitRepo/project/doc_sideslip/plots/1561052970645.png)



### Yaw rate and roll rate



![1561053486260](/home/xiang.zhang/gitRepo/project/doc_sideslip/plots/1561053486260.png)



#### Azimuth and pitch



![1561053042569](/home/xiang.zhang/gitRepo/project/doc_sideslip/plots/1561053042569.png)

### Yaw rate and pitch rate



![1561053385397](/home/xiang.zhang/gitRepo/project/doc_sideslip/plots/1561053385397.png)





#### Roll and pitch



![1561052997261](/home/xiang.zhang/gitRepo/project/doc_sideslip/plots/1561052997261.png)

### Pitch rate and roll rate

![1561053168354](/home/xiang.zhang/gitRepo/project/doc_sideslip/plots/1561053168354.png)





#### Azimuth and steering wheel angle

![1561052867084](/home/xiang.zhang/gitRepo/project/doc_sideslip/plots/1561052867084.png)

## 2. Gyro bias

### Factors involved: 

- IMU-to-Vehicle rotation angles.
- Synchronization, which is processed by sliding window averaging.

### Some questions:

- [x] Is the bias estimation stable during the straight and cornering condition?

  - relatively stable when moving straightly and 

  - significant change at the beginning and the end of the cornering

  ![1561151513886](/home/xiang.zhang/gitRepo/project/doc_sideslip/plots/1561151513886.png)

- [x] What is the short term bias estimation?

  - about `-0.01` given 1 second sliding window average.

- [x] What are bias of other two gyros?

  - Significant change **during** the cornering.

![1561159331121](/home/xiang.zhang/gitRepo/project/doc_sideslip/plots/1561159331121.png)

![1561159353433](/home/xiang.zhang/gitRepo/project/doc_sideslip/plots/1561159353433.png)

### a. Gyro bias and vehicle yaw rate bias estimation from NovAtel

![1561151758150](/home/xiang.zhang/gitRepo/project/doc_sideslip/plots/1561151758150.png)

![1561151770673](/home/xiang.zhang/gitRepo/project/doc_sideslip/plots/1561151770673.png)

![1561151778786](/home/xiang.zhang/gitRepo/project/doc_sideslip/plots/1561151778786.png)

![1561151788451](/home/xiang.zhang/gitRepo/project/doc_sideslip/plots/1561151788451.png)

### 

### c. Bias_yaw_rate_b and corrected vehicle pitch_rate, roll_rate, etc.

![1561152040707](/home/xiang.zhang/gitRepo/project/doc_sideslip/plots/1561152040707.png)

![1561152290706](/home/xiang.zhang/gitRepo/project/doc_sideslip/plots/1561152302718.png)



### d. Bias_yaw_rate_v and corrected vehicle pitch_rate, roll_rate, etc.

![1561152346297](/home/xiang.zhang/gitRepo/project/doc_sideslip/plots/1561152346297.png)

![1561152355677](/home/xiang.zhang/gitRepo/project/doc_sideslip/plots/1561152355677.png)

![1561152414070](/home/xiang.zhang/gitRepo/project/doc_sideslip/plots/1561152414070.png)

## 3. Worth a look



![1561076029179](/home/xiang.zhang/gitRepo/project/doc_sideslip/plots/1561076029179.png)

![1561076056654](/home/xiang.zhang/gitRepo/project/doc_sideslip/plots/1561076056654.png)



![1561076072653](/home/xiang.zhang/gitRepo/project/doc_sideslip/plots/1561076072653.png)

![1561076087270](/home/xiang.zhang/gitRepo/project/doc_sideslip/plots/1561076087270.png)



![1561076101073](/home/xiang.zhang/gitRepo/project/doc_sideslip/plots/1561076101073.png)

![1561076123650](/home/xiang.zhang/gitRepo/project/doc_sideslip/plots/1561076123650.png)

![1561076150864](/home/xiang.zhang/gitRepo/project/doc_sideslip/plots/1561076150864.png)

![1561076167205](/home/xiang.zhang/gitRepo/project/doc_sideslip/plots/1561076167205.png)



![1561076313753](/home/xiang.zhang/gitRepo/project/doc_sideslip/plots/1561076313753.png)



![1561076224673](/home/xiang.zhang/gitRepo/project/doc_sideslip/plots/1561076224673.png)

![1561076249436](/home/xiang.zhang/gitRepo/project/doc_sideslip/plots/1561076249436.png)



![1561076353102](/home/xiang.zhang/gitRepo/project/doc_sideslip/plots/1561076353102.png)

![1561076404053](/home/xiang.zhang/gitRepo/project/doc_sideslip/plots/1561076404053.png)



![1561076503702](/home/xiang.zhang/gitRepo/project/doc_sideslip/plots/1561076503702.png)





![1561076523181](/home/xiang.zhang/gitRepo/project/doc_sideslip/plots/1561076523181.png)



![1561076562287](/home/xiang.zhang/gitRepo/project/doc_sideslip/plots/1561076562287.png)

![1561076631520](/home/xiang.zhang/gitRepo/project/doc_sideslip/plots/1561076631520.png)





![1561076656548](/home/xiang.zhang/gitRepo/project/doc_sideslip/plots/1561076656548.png)

![1561076700209](/home/xiang.zhang/gitRepo/project/doc_sideslip/plots/1561076700209.png)