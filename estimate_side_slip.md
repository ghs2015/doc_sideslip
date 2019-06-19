



## Asumptions

- Method to check the side slip angle estimation is valid or normal.
  - Positively correlated with the **steering wheel angle** and **yaw rate** when on the **EVEN surface**.
    - Around zero when moving straightly.
    - With same the symbol as the steering wheel angle.
- The track ground is sufficiently accurate when moving in the free way.
- The side slip angle estimation depends on the azimuth estimation.
  - Azimuth estimation is derived from IMU gyro measurements and current position, velocity, and attitude.
- Some observations show there are big difference (2 degree) between corrected yaw rate and raw yaw rate, although they are in difference frames. However, some plots under this condition still show reasonable side slip estimation by (azimuth - track ground).
  - **Guess**: The estimated bias is fixed for yaw rate. The confidence of yaw rate is low. The azimuth is estimated by fusion which is not severely affected by very the low yaw rate.

## To check

- [x] The side slip angle estimation of the returning segment NO.2 is obvious or not.

  About 0.1 degree, which is similar to NO.2 returning.

- [x] The insignificant side slip angle estimation is because the uneven road surface, which can be observed by roll and pitch??

  - [x] When even road surface (relatively stable roll and pitch), slip angle estimation intensity?

    0.1 degree.

  - [x] When uneven, slip angle estimation intensity?

    0.4 degree.

## Side slip estimation

### Road Segment NO.1

![1560965905085](/home/xiang.zhang/gitRepo/project/doc_sideslip/plots/1560965905085.png)

### Road Segment NO. 2

![1560817877339](/home/xiang.zhang/.config/Typora/typora-user-images/1560817877339.png)

### Observations

#### Some plots

The oscillation of steering wheel angle may be related to estimated side slip results??



![1560819379425](/home/xiang.zhang/.config/Typora/typora-user-images/1560819379425.png)

![1560819463173](/home/xiang.zhang/.config/Typora/typora-user-images/1560819463173.png)



![1560819512045](/home/xiang.zhang/.config/Typora/typora-user-images/1560819512045.png)

![1560819529634](/home/xiang.zhang/.config/Typora/typora-user-images/1560819529634.png)

###  Side slip angle observations 

(Use degree unit for angles.)

#### From curves.

- The corrected yaw rate is very low when cornering but in proportion to the decoded raw yaw rate.

#### B2

![1560898419546](/home/xiang.zhang/.config/Typora/typora-user-images/1560898419546.png)



![1560898518313](/home/xiang.zhang/.config/Typora/typora-user-images/1560898518313.png)



![1560904840837](/home/xiang.zhang/gitRepo/project/doc_sideslip/plots/1560905143353.png)

- The trend of side slip angle and steering wheel angle may be worth noticing as a estimation of side slip performance.

![1560905665406](/home/xiang.zhang/gitRepo/project/doc_sideslip/plots/1560905665406.png)



![1560905697902](/home/xiang.zhang/gitRepo/project/doc_sideslip/plots/1560905697902.png)





#### B3

![1560905792779](/home/xiang.zhang/gitRepo/project/doc_sideslip/plots/1560905792779.png)

![1560905803867](/home/xiang.zhang/gitRepo/project/doc_sideslip/plots/1560905803867.png)



![1560905821051](/home/xiang.zhang/gitRepo/project/doc_sideslip/1560905821051.png)

![1560905831466](/home/xiang.zhang/gitRepo/project/doc_sideslip/plots/1560905831466.png)



#### b4

![1560905939430](/home/xiang.zhang/gitRepo/project/doc_sideslip/plots/1560905939430.png)





![1560905970186](/home/xiang.zhang/gitRepo/project/doc_sideslip/plots/1560905970186.png)



![1560906025244](/home/xiang.zhang/gitRepo/project/doc_sideslip/plots/1560906025244.png)

![1560906033022](/home/xiang.zhang/gitRepo/project/doc_sideslip/plots/1560906033022.png)



![1560906064117](/home/xiang.zhang/gitRepo/project/doc_sideslip/plots/1560906064117.png)

![1560906070831](/home/xiang.zhang/gitRepo/project/doc_sideslip/plots/1560906070831.png)



![1560906122717](/home/xiang.zhang/gitRepo/project/doc_sideslip/plots/1560906122717.png)

![1560906129907](/home/xiang.zhang/gitRepo/project/doc_sideslip/plots/1560906129907.png)



- When the correlation between side slip and azimuth, track ground is low. May because there are frequent or heavy steering wheel angle changes.

![1560906258371](/home/xiang.zhang/gitRepo/project/doc_sideslip/plots/1560906258371.png)



![1560906270497](/home/xiang.zhang/gitRepo/project/doc_sideslip/plots/1560906270497.png)









































#### **From correlations.**

- The `corrected yaw rate` changes exactly with `decoded raw IMU` yaw rate. Sown from the correlation between the two is within [0.97, 1.00]. Also these two variables change in proportion with steering wheel angle.
- `side slip angle` correlates with `pitch`, `roll`, and `azimuth`, but not stably correlated.
- `Track ground` is tightly correlated with `azimuth`.

## To-do:

- [x] Select cornering (lat, lon) range and corresponding straight range.
- [x] Generate tuned results.
- [x] Plot.
	- [x] jjjsteering angle
- [x] save plots
- [x] Statistically analyze.
	- [x] Covariance 
		- fixed sideslip and steering angle.
		- fixed sideslip and yaw rate.
		- yaw rate and  steering angle
- [x] test with more vehicles.
- [x] Test with more road segments.
  - [x] Add road segment NO.2 
  - [x] Plot two straight segments preceding and following the corners.
- [x] plot additional variables
	- [x] Add plots of roll, pitch.
	- [x] Add plots of yaw rate bias estimation (yaw rate std).
- [x] Draw assumptions about side-slip performance evaluation.
- [ ] Analyze the reason of insignificant (returning) side-slip. 
  - [x] interaction with decoded raw IMU yaw rate
  - [x] with roll, pitch
  - [ ] see raw roll rate and pitch rate??
- [ ] Solutions?
  - [ ] Improve current algorithm?
  - [ ] Use a separate  yaw (or plus attitude) estimation based on short-term gyro outputs.
