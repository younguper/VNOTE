# 1. JacobiSVD
# 2. 2.旋转向量

```
// 绕Ｚ轴旋转９０度的旋转矩阵
Matrix3d R_Z1 = AngleAxisd(M_PI/2,Vector3d(0,0,1)).matrix();
```
# 3. 数据类型
## 3.1. 定义

1. Eigen中所有矩阵的创建方式
```
// Eigen 中所有向量和矩阵都是Eigen::Matrix，它是一个模板类。它的前三个参数为：数据类型，行，列
// 声明一个2*3的float矩阵
Eigen::Matrix<float, 2, 3> matrix_23;
```
2. 同时，Eigen 通过 typedef 提供了许多内置类型，不过底层仍是Eigen::Matrix．

```
    // 例如 Vector3d 实质上是 Eigen::Matrix<double, 3, 1>，即三维向量
    Eigen::Vector3d v_3d;
	// 这是一样的
    Eigen::Matrix<float,3,1> vd_3d;

    // Matrix3d 实质上是 Eigen::Matrix<double, 3, 3>
    Eigen::Matrix3d matrix_33 = Eigen::Matrix3d::Zero(); //初始化为零
```
3. 如果不确定矩阵大小，可以使用动态大小的矩阵
```
    Eigen::Matrix< double, Eigen::Dynamic, Eigen::Dynamic > matrix_dynamic;
    // 更简单的
    Eigen::MatrixXd matrix_x;
```
*重点关注对象：Matrix3f, Matrix4f, Matrix3d, and Matrix4d.*

## 3.2. 初始化
```
// 输入数据（初始化）
matrix_23 << 1, 2, 3, 4, 5, 6;
```
另外，Eigen提供实用程序函数来初始化矩阵
```
// Set each coefficient to a uniform random value in the range [ -1 , 1]
A = Matrix3f :: Random () ;
// Set B to the identity matrix
B = Matrix4d :: Identity () ;
// Set all elements to zero
A = Matrix3f :: Zero () ;
// Set all elements to ones
A = Matrix3f :: Ones () ;
// Set all elements to a constant value
B = Matrix4d :: Constant (4.5) ;
```

## 3.3. 格式转换
但是在Eigen里你不能混合两种不同类型的矩阵，像这样是错的，即使是单精度和双精度的浮点数之间
```
Eigen::Matrix<float, 2, 3> matrix_23;
Eigen::Matrix<double, 2, 1> result_wrong_type = matrix_23 * v_3d;
// 应该显式转换
Eigen::Matrix<double, 2, 1> result = matrix_23.cast<double>() * v_3d;
cout << result << endl;
```
## 3.4. 矩阵操作
### 3.4.1. 基本操作

```
matrix_33 = Eigen::Matrix3d::Random();      // 随机数矩阵
cout << matrix_33 << endl << endl;

cout << matrix_33.transpose() << endl;      // 转置
cout << matrix_33.sum() << endl;            // 各元素和
cout << matrix_33.trace() << endl;          // 迹
cout << 10*matrix_33 << endl;               // 数乘
cout << matrix_33.inverse() << endl;        // 逆
cout << matrix_33.determinant() << endl;    // 行列式

```
### 3.4.2. 点乘和叉乘
```
Eigen::Vector3d v(1, 2, 3);
Eigen::Vector3d w(0, 1, 2);
double vDotw = v.dot(w); // dot product of two vectors
Eigen::Vector3d vCrossw = v.cross(w); // cross product of two vectors
```
### 3.4.3. 矩阵元素操作
```
 Eigen::MatrixXd A = Eigen::MatrixXd::Random(7, 9);
  std::cout << "The element at fourth row and 7the column is " << A(3, 6) << std::endl;
  Eigen::MatrixXd B = A.block(1, 2, 3, 3);
  std::cout << "Take sub-matrix whose upper left corner is A(1, 2)" << std::endl << B << std::endl;

  Eigen::VectorXd a = A.col(1); // take the second column of A
  Eigen::VectorXd b = B.row(0); // take the first row of B

  Eigen::VectorXd c = a.head(3);// take the first three elements of a
  Eigen::VectorXd d = b.tail(2);// take the last two elements of b
```
## 3.5. 四元数
```
 Eigen::Quaterniond q(2, 0, 1, -3); 
  std::cout << "This quaternion consists of a scalar " << q.w() << " and a vector " << std::endl << q.vec() << std::endl;
  q.normalize();
  std::cout << "To represent rotation, we need to normalize it such that its length is " << q.norm() << std::endl;

  Eigen::Vector3d v(1, 2, -1);
  Eigen::Quaterniond p;
  p.w() = 0;
  p.vec() = v;
  Eigen::Quaterniond rotatedP = q * p * q.inverse(); 
  Eigen::Vector3d rotatedV = rotatedP.vec();
  std::cout << "We can now use it to rotate a vector " << std::endl << v << " to " << std::endl << rotatedV << std::endl;

  Eigen::Matrix3d R = q.toRotationMatrix(); // convert a quaternion to a 3x3 rotation matrix
  std::cout << "Compare with the result using an rotation matrix " << std::endl << R * v << std::endl;

  Eigen::Quaterniond a = Eigen::Quterniond::Identity();
  Eigen::Quaterniond b = Eigen::Quterniond::Identity();
  Eigen::Quaterniond c; // Adding two quaternion as two 4x1 vectors is not supported by the EIgen API. That is, c = a + b is not allowed. We have to do this in a hard way

  c.w() = a.w() + b.w();
  c.x() = a.x() + b.x();
  c.y() = a.y() + b.y();
  c.z() = a.z() + b.z();
 
```
