# 1. STM32开发
## 1.1. IMU型号
InvenSense公司的ICM-20602，现在被日本TDK公司收购
## 1.2. 特性
    1.陀螺仪 Gyroscope specification
![](_v_images/1541139710_11923.png)

    2. 加速度计 Accelerometer 
![](_v_images/1541139822_21486.png)

## 1.3. 芯片坐标系
![](_v_images/1541142317_11250.png)

## 1.4. 电路图
![](_v_images/1541140067_1511.png)

## 1.5. 通信接口
采用SPI接口，因为STM32系列的MCU的I2C有使用上的bug。
![](_v_images/1541140309_16507.png)

## 1.6. STM323F4应用
![](_v_images/1541143896_11878.png)

## ICM20602参数设置
### 采样频率
![](_v_images/1541399078_30508.png)