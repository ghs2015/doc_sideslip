# Requirements
- [ ] Simulate 10 laps of data given median IMU accuracy.
- Confirm the correctness of the output of gyroscopes and accelerometers.
- Confirm the gravity calculation is location dependent.
- Given that roll and pitch of camera observations have `0,1 degree` error, check the estimation error of azimuth.
- Make the simulated motion profile as real as possible. The detailed requirement needs to determine, such as steering angle oscillation effect.
- Confirm the reference frame consistent with the true condition or not.

# Sensor model
## IMU data
- Sensor model
- Motion plan
## Camera

# Motion profile

# Naviation algorithm simulation

# Performance analysis

# Implementation and deploy

# New algorithm prototyping and validation
## Sensor fusion with cameras

## Sensor fusion with GNSS

## Side slip angle error estimation


# Reference
https://github.com/Aceinna/gnss-ins-sim

# To-do
- [x] Finish the readme of Aceinna/gnss-ins-sim
- [ ] Analyze the weird curves of side slip plots.
- [ ] Find out the code converting IMU spec to simulated output.
