# CS4222 Assignment 3


## Group 20 Members
CHEU WEE LOON   A0097836L   
GOH JIAQUAN     A0097722X   
QUEK JUN JIE    A0098816M


## Summary
We made changes to the following methods:
- initSensors()
- startSensing()
- onSensorChanged()
- detectShootingDirectionAndRegion()

In initSensors(), we get a rotation vector sensor:
```
rotationSensor = sensorManager.getDefaultSensor(Sensor.TYPE_ROTATION_VECTOR);
```

In startSensing(), we register a listener for the rotation vector sensor:
```
sensorManager.registerListener(this, rotationSensor, SensorManager.SENSOR_DELAY_GAME);
```

In onSensorChanged(), we add a handler for rotation vector event:
```
... else if (event.sensor.getType() == Sensor.TYPE_ROTATION_VECTOR) {
    detectShootingDirectionAndRegion(event);
}
```
In detectShootingDirectionAndRegion(), we get rotation matrix from vector and use .getOrientation() get the Euler's angles then we extract out the azimuth:
```
float[] rotationMatrix = new float[16];
SensorManager.getRotationMatrixFromVector(rotationMatrix, event.values);

float[] orientationValues = new float[3];
SensorManager.getOrientation(rotationMatrix, orientationValues);

double azimuth = Math.toDegrees(orientationValues[0]);
...
```
