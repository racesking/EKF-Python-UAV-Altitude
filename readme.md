# EKF (Extended Kalman Filter) in Python for UAV altitude determination

This repository contains an implementation of an EKF (Extended Kalman Filter) in Python. The purpose of this implementation is to provide a way to estimate the orientation of a sensor using gyrometer, accelerometer, and magnetometer data.

## Overview

The gyrometer data alone is insufficient because it will eventually drift away from its original reference point over time. Furthermore, there is no way for the gyrometer to know the actual orientation after a certain period of time due to a lack of reference points. In order to alleviate these problems, we are going to use the accelerometer to provide a reference vector that is pointing downwards (gravity), and a magnetometer to provide another vector pointing in the magnetic north direction. With these 2 reference vectors, the orientation of the sensor will be fully defined thus we can use them as a reference to counter the drift of the gyrometer.

## Kalman Filter States

In order to use the Kalman Filter, we first have to define the states that we want to use. This implementation defines a state vector that includes the roll, pitch, and yaw angles, as well as their respective rate of change. 

## Accelerometer Data

The acceleration measured by the accelerometer module can be calculated if we know the acceleration of the body in the world frame, and the orientation of the body. Our reference vector is going to be the gravity vector, and we know that this vector will always point downwards in the world frame. Therefore, if we know the orientation of the body, we can predict the acceleration that the accelerometer is going to measure. This is all based on the assumption that external forces are negligible thus the only force that acts on the body is the gravitational force.

## Magnetometer Data

The magnetometer provides us with a vector that is always pointing to the magnetic North. This vector changes (elevation of the vector changes depending on the altitude) over the surface of the Earth thus we will need a map of the vectors if we want a reference vector that works across the globe. However, in this project, we will be assuming that the change in the North reference vector is negligible since the sensor will not be moving around much (probably only within the room).

The magnetometer actually gives a 3 directional reference vector instead of a simple North heading in 2 dimensions. Due to this, there are some complications that arise. In this project, we assume that the accelerometer is accurate in providing the reference vector in the vertical plane, and the magnetometer data is accurate in providing the reference vector in the horizontal place. As a result of this, we remove 1 dimension from the magnetometer reference vector.

## Dependencies

- Python 3.x
- numpy
- matplotlib

## Usage

Clone the repository and run the `main.py` file. The script will read data from a CSV file located in the `data` folder and plot the estimated orientation using the EKF. The script also generates a log file containing the estimated orientation and sensor data. 

This repository also includes the an Arduino code for reading sensor data in the ExtractSensorData folder.

Feel free to modify the script to use your own sensor data. 

## Conclusion

The EKF implementation provides a way to estimate the orientation of a sensor using gyrometer, accelerometer, and magnetometer data. The implementation can be used as a starting point for more advanced sensor fusion projects.