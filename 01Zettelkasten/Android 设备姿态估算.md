20250125
Status: #public-knowledge
Tags: 
aliases: 
# Android 设备姿态估算
计算设备的屏幕方向
通过计算设备的屏幕方向，您可以监测设备相对于地球参照系（具体为磁北极）的位置。以下代码展示了如何计算设备的屏幕方向：

```Kotlin
private lateinit var sensorManager: SensorManager
...
// Rotation matrix based on current readings from accelerometer and magnetometer.
val rotationMatrix = FloatArray (9)
SensorManager.getRotationMatrix (rotationMatrix, null, accelerometerReading, magnetometerReading)

// Express the updated rotation matrix as three orientation angles.
val orientationAngles = FloatArray (3)
SensorManager.getOrientation (rotationMatrix, orientationAngles)
```

系统使用设备的地磁场传感器和加速度计来计算屏幕方向的角度。通过使用这两个硬件传感器，系统可提供以下三个屏幕方向角度的数据：

**方位角**（绕 z 轴旋转的角度）。此为设备当前指南针方向与磁北向之间的角度。如果设备的上边缘面朝磁北向，则方位角为 0 度；如果上边缘朝南，则方位角为 180 度。与之类似，如果上边缘朝东，则方位角为 90 度；如果上边缘朝西，则方位角为 270 度。**【如果使用了这个角，那么加速度方向会和地球坐标系东南西北绑定】**
**俯仰角**（绕 x 轴旋转的角度）。此为平行于设备屏幕的平面与平行于地面的平面之间的角度。如果将设备与地面平行放置，且其下边缘最靠近您，同时将设备上边缘向地面倾斜，则俯仰角将变为正值。沿相反方向倾斜（将设备上边缘向远离地面的方向移动）将使俯仰角变为负值。值的范围为 -90 度到 90 度。
**倾侧角**（绕 y 轴旋转的角度）。此为垂直于设备屏幕的平面与垂直于地面的平面之间的角度。如果将设备与地面平行放置，且其下边缘最靠近您，同时将设备左边缘向地面倾斜，则侧倾角将变为正值。沿相反方向倾斜（将设备右边缘移向地面）将使侧倾角变为负值。值的范围为 -180 度到 180 度。

请注意，这些角度使用的坐标系与航空领域所用的坐标系（针对偏航、俯仰和侧倾）不同。在航空系统中，x 轴沿飞机的长边，从机尾到机头。

屏幕方向传感器通过处理来自加速度计和地磁场传感器的原始传感器数据来获取其数据。由于涉及繁重处理，屏幕方向传感器的准确度和精度会降低。具体而言，此传感器仅在侧倾角为 0 时才可靠。因此，Android 2.2（API 级别 8）已弃用屏幕方向传感器，Android 4.4 W（API 级别 20）已弃用屏幕方向传感器类型。我们建议不要使用来自屏幕方向传感器的原始数据，而是结合使用 getRotationMatrix () 方法和 getOrientation () 方法来计算屏幕方向值，如以下代码示例中所示。在此过程中，您可以使用 remapCoordinateSystem () 方法将屏幕方向值转换为应用的参照系。

```Kotlin
class SensorActivity : Activity(), SensorEventListener {

    private lateinit var sensorManager: SensorManager
    private val accelerometerReading = FloatArray(3)
    private val magnetometerReading = FloatArray(3)

    private val rotationMatrix = FloatArray(9)
    private val orientationAngles = FloatArray(3)

    public override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.main)
        sensorManager = getSystemService(Context.SENSOR_SERVICE) as SensorManager
    }

    override fun onAccuracyChanged(sensor: Sensor, accuracy: Int) {
        // Do something here if sensor accuracy changes.
        // You must implement this callback in your code.
    }

    override fun onResume() {
        super.onResume()

        // Get updates from the accelerometer and magnetometer at a constant rate.
        // To make batch operations more efficient and reduce power consumption,
        // provide support for delaying updates to the application.
        //
        // In this example, the sensor reporting delay is small enough such that
        // the application receives an update before the system checks the sensor
        // readings again.
        sensorManager.getDefaultSensor(Sensor.TYPE_ACCELEROMETER)?.also { accelerometer ->
            sensorManager.registerListener(
                    this,
                    accelerometer,
                    SensorManager.SENSOR_DELAY_NORMAL,
                    SensorManager.SENSOR_DELAY_UI
            )
        }
        sensorManager.getDefaultSensor(Sensor.TYPE_MAGNETIC_FIELD)?.also { magneticField ->
            sensorManager.registerListener(
                    this,
                    magneticField,
                    SensorManager.SENSOR_DELAY_NORMAL,
                    SensorManager.SENSOR_DELAY_UI
            )
        }
    }

    override fun onPause() {
        super.onPause()

        // Don't receive any more updates from either sensor.
        sensorManager.unregisterListener(this)
    }

    // Get readings from accelerometer and magnetometer. To simplify calculations,
    // consider storing these readings as unit vectors.
    override fun onSensorChanged(event: SensorEvent) {
        if (event.sensor.type == Sensor.TYPE_ACCELEROMETER) {
            System.arraycopy(event.values, 0, accelerometerReading, 0, accelerometerReading.size)
        } else if (event.sensor.type == Sensor.TYPE_MAGNETIC_FIELD) {
            System.arraycopy(event.values, 0, magnetometerReading, 0, magnetometerReading.size)
        }
    }

    // Compute the three orientation angles based on the most recent readings from
    // the device's accelerometer and magnetometer.
    fun updateOrientationAngles() {
        // Update rotation matrix, which is needed to update orientation angles.
        SensorManager.getRotationMatrix(
                rotationMatrix,
                null,
                accelerometerReading,
                magnetometerReading
        )

        // "rotationMatrix" now has up-to-date information.

        SensorManager.getOrientation(rotationMatrix, orientationAngles)

        // "orientationAngles" now has up-to-date information.
    }
}
```











---
# References
[位置传感器  \|  Sensors and location  \|  Android Developers](https://developer.android.google.cn/develop/sensors-and-location/sensors/sensors_position?hl=zh-cn)