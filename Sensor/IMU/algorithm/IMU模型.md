# 1. IMU模型
## 1.1. gyro的误差模型
$$
\omega_m^B=S_g\omega^B+b_g+n_g+s_{ga}a^B
$$
其中$b_g$为bias偏差，$n_g$为高斯白噪声，$S_g$为尺度因子，$s_{ga}$为g-灵敏度，即加速度对角速度的影响
为了对以上四种误差有更直观的认识，请看下图：
![](_v_images/20190711103821833_1506252631.png)
## 1.2. accel的误差模型
$$
a_m^B=R_{BG}S_a(a^G-g^G)+b_a+n_a
$$