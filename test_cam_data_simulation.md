### TODO

- [x] Validate the camera simulation data.

  - [x] checklist

    - [x] get_ctm_ecef2ned

    - [x] get_transformation_error

    - [x] `sim_cam_data` noisy cam pose misalign ignored. (fixed by should not affect ref cam)

    - [x] gt cam pose should not have calibration offset and misalignment, `fixed`

    - [x] `scipy Q from quaternion ` assignment order is wrong, should be `x,y,z,w`, fixed

      Now the result is close to calibration result. But still a bit of abnormal.

    - [x] change to use the ref cam instead of noisy cam data. changed. Much closer.

    - [x] The problem may be related to the way of add imu2cam angles, use addition or rotation?? May not. Have another idea.

    - [x] The calibration error is in proportion to the speed! Maybe one of position is not updated! Fixed. In the `c++` source code.

    - [x] The hard-coded calibration parameters confused the order of roll, pitch, yaw. Fixed.

### Bugs?

#### Derived and defined calibration parameters are inconsistent.

- The Euler angles of calibration looks normal.



#### Records

```python
# use overlap camera data, looks normal, except the Q's sign
p_b2c_derived_b [0. 0. 0.]
p_b2c_def_b [0. 0. 0.]
q_b2c_derived [ 0.  0.  0. -1.]
q_b2c_def [0. 0. 0. 1.]
(array([0., 0., 0.]), 0.0)

# TODO, abnormal!!
use gt cam data
p_b2c_derived_b [ 2.82415668  1.13002953 -1.92880616]
p_b2c_def_b [ 2.1  -1.35  1.8 ]

q_b2c_derived [ 0.00432494  0.0044014   0.00870728 -0.99994305]
q_b2c_def [ 0.00476861 -0.0078726   0.00388912  0.99995008]

(array([-0.72415668, -2.48002953,  3.72880616]), 0.015918889935101495)
```

Fixed quaternion assignment order in the test script.

```python
use overlap cam data
p_b2c_derived_b [0. 0. 0.]
p_cam_b_def [0. 0. 0.]
q_b2c_derived [ 0.  0.  0. -1.]
q_b2c_def [0. 0. 0. 1.]
error:  (array([0., 0., 0.]), 1.1102230246251565e-16)
    
use gt cam data
p_b2c_derived_b [ 2.82415668 -1.13002953  1.92880616]
p_cam_b_def [ 2.  -1.5  2. ]

q_b2c_derived [ 0.00870724 -0.0044014  -0.00432497 -0.99994305]
q_b2c_def [ 0.00432503 -0.00874541  0.00432503  0.99994305]

error:  (array([-0.82415668, -0.36997047,  0.07119384]), 0.01851157988177816)
```

Used ground truth cam data.

```python
p_b2c_derived_b [0. 0. 0.]
p_cam_b_def [0. 0. 0.]
q_b2c_derived [ 0.  0.  0. -1.]
q_b2c_def [0. 0. 0. 1.]
error:  (array([0., 0., 0.]), 1.1102230246251565e-16)
    
use gt cam data
p_b2c_derived_b [ 2.60000531 -1.50000265  2.00000022]  # x axis 0.6 offset
p_cam_b_def [ 2.  -1.5  2. ]

q_b2c_derived [ 0.00870722 -0.00440138 -0.00432495 -0.99994305]
q_b2c_def [ 0.00432503 -0.00874541  0.00432503  0.99994305]
error:  (array([-6.00005312e-01,  2.64677341e-06, -2.16632783e-07]), 0.01851154693532489)  # rotation looks abnormal, 1 deg
```

Fixed using first key frame cam data instead of every key frame.

```python
Press ENTER or type command to continue
use overlap cam data
p_b2c_derived_b [0. 0. 0.]
p_cam_b_def [0. 0. 0.]
q_b2c_derived [ 0.  0.  0. -1.]
q_b2c_def [0. 0. 0. 1.]
error:  (array([0., 0., 0.]), 2.220446049250313e-16)

use gt cam data
p_b2c_derived_b [ 1.99999899 -1.50000268  2.        ]
p_cam_b_def [ 2.  -1.5  2. ]
q_b2c_derived [ 0.00870722 -0.00440134 -0.00432495 -0.99994305]
q_b2c_def [ 0.00432503 -0.00874541  0.00432503  0.99994305]
error:  (array([ 1.00622407e-06,  2.67508761e-06, -9.90882043e-10]), 0.018511513255719765)  # distance between Quaternions are still abnormal
```

Fixed the reading order of pitch, roll, yaw to rotation angle x, y, z

```
use overlap cam data
p_b2c_derived_b [0. 0. 0.]
p_cam_b_def [0. 0. 0.]
q_b2c_derived [ 0.  0.  0. -1.]
q_b2c_def [0. 0. 0. 1.]
error:  (array([0., 0., 0.]), 2.220446049250313e-16)


use gt cam data
p_b2c_derived_b [ 1.99999899 -1.50000268  2.        ]
p_cam_b_def [ 2.  -1.5  2. ]
q_b2c_derived [ 0.00870722 -0.00440134 -0.00432495 -0.99994305]
q_b2c_def [-0.00870733  0.00440118  0.00432503  0.99994305]
error:  (array([ 1.00622407e-06,  2.67508761e-06, -9.90882043e-10]), 2.0919641505927826e-07)

```

