+++
author = "Ymmald"
title = "Introduction to linear algebra"
date = "2022-12-11"
description = "学习线性代数的过程中感觉比较重要的内容"

+++

# MIT 线性代数课程的笔记


## 矩阵乘法

### 将矩阵的初等变换和矩阵乘法相联系    
以矩阵诠释消元变化    
左乘是行变换，右乘是列变换    

### 矩阵乘法的其他解释方式     
将结果看作第一个矩阵中列向量按照第二个矩阵进行线性排列       
或看作第二个矩阵中的行向量按照第一个矩阵进行线性排列的结果     

### 矩阵乘法的五种运算方式    
- 常规方法     
- 第一个矩阵列向量的线性组合
- 第二个矩阵行向量的线性组合
- 第一个矩阵的列乘以第二个矩阵的行
- 分块乘法

## 逆矩阵

### 逆矩阵  
方阵的左逆等于右逆（其实就相当于AB=E中的A和B可以互换位置）   

### 方阵不可逆的解释    
行/列向量中，有一行/列未做出贡献，不能完全构成单位矩阵中的向量     
Ax = 0有非零解时（其实就相当与A的行列式等于0），方阵不可逆     

### 求解逆矩阵的方法    
拆成列向量的形式，再求解线性方程组    
增广矩阵的变换（解释：A的逆乘以增广矩阵，将增广矩阵分块来看）      

- $ ABB^{-1}A^{-1} = E $ 
    
- $AA^{-1} = I$   
 两边取转置       
  $ (A^{-1})^T(A)^T = I $
->二者互为转置，转置和逆两种运算对于单个矩阵来说可以颠倒     
$ (A^T)^{-1}=(A^{-1})^T $

## 消元：正确认识矩阵的概念


### 数学符号的含义
L：下三角矩阵     
U：上三角矩阵


### 消元的顺序
 *$ E_{32}E_{21} $*     
*是相对右侧向量而来的变化，要计算E，要看他们对右侧向量的叠加效果*    
*先做第二行的变换再做第三行的变换，第二行的会影响第三行的……    
$E_{21}会影响E_{32}$    
挪到右边去就没有这个影响了……（顺序会倒过来)     
从下面的行开始做消元*

EA=U      
A=LU：如果不存在行变换，消元乘数可以直接写入L中            
     
消元时左乘E，对A进行行初等变换->对U进行行初等变换

***操作数？？           
$ 大概是n^2+(n-1)^2+(n-2)^2+···+1^2 $***             

***$1/3n^3 (对n2积分)$***     
***如果在右侧加上常数向量b，则还需要再进行n^2次操作
微积分考虑连续状态下对求和，但线性代数是离散的***

### 数学名词的含义
置换矩阵：逆与转置相等

## 向量空间
### 子空间
- 三维空间中，任意穿过原点的平面构成子空间    
- 任意穿过原点的直线也构成子空间
- 一个平面与一条直线的并集不是子空间（加法不封闭）
- 一个平面与一条直线的交集是子空间 
- 任意两个子空间的交集也依然是子空间
- 向量空间必须满足的条件：加法封闭和数乘封闭
- 零向量是个特殊的向量空间 

### 两种构筑子空间的方法：
- 从几个向量，通过线性组合
- 在一个方程组中，通过让x满足特定条件（齐次线性方程组）

## 求解线性方程组
- Ax = b有解，当且仅当b是A的各列向量的线性组合    
- 即b属于A的列空间     
- A列的个数n等于未知数的个数     
- A行的个数m等于方程的个数      
- 当b是零向量时，x是子空间，否则不是（否则不能穿过原点）       


### 矩阵的秩r
自由变量：任意选取自由变量的值，再求解其他的       
特解（特定的解）：自由向量赋值为0、1    
有n-r个自由变量     
行阶梯形矩阵



### Ax = b方程组有解
- b在A的列向量构成的向量空间里
- 如果A的行向量的线性组合等于0向量，那么b的同样的线性组合等于0（没有贡献的方程不能与其他方程有冲突）

### 求解非齐次线性方程组
1. 寻找特解：将所有自由变量设为0       
1. 加上任意令空间的向量

### 子空间的维数
可以任意选取的自由向量个数，n - r


### r与方程组的关系
*m表示行，n表示列*
1. r = n < m时，方程组有唯一解或者无解
2. r = m < n时，方程组一定有无穷多个解，自由变量n - r个
3. r = m = n时，方程组有唯一解
1. r < m 或r < n 时，方程组无解或者有无穷多个解

*向量组中如果包含零向量，则不可能线性无关*

### 列向量线性相关性和自由变量个数的关系
- 如果矩阵的列线性无关，则 r =  n <= m，没有自由变量       
- 如果矩阵的列线性相关，则 r < n ，有自由变量 

*向量组生成一个向量空间
这个向量空间包含这个向量组的所有线性组合*

## 向量的基
### 向量的一组基
- 线性无关
- 生成整个空间

*矩阵的秩 -> 主向量的个数 -> 向量空间的维数*

## 四个子空间及其基本关系
- C(A)，A的列空间 in $R^m$ (维数为r)
- N(A)，A的null space in $R^n$ （维数为n - r)
- $C(A^T)$，A的行空间（转置为列空间） in $R^n$ （维数为r）
- $N(A^T)$，A的左零空间  in $R^m$  (维数为m - r)

### 行变换不会对行空间产生影响，但会影响列空间
A -> R（经过行变换）    
R中含有主元的行可作为一组基向量

### 对左零空间的解释
$A^Ty = 0$      
$y^TA = 0$   
一个行向量乘以A得到零向量

### 求解左零空间
#### 高斯-若尔当消元法
$(A|I) -> (I|A^T)$    
右侧单位矩阵将左侧矩阵A的变换记录了下来    
$(A|I) -> (R|E)$     
EI = E     
EA = R    
左侧的E中包含能让A的行向量线性组合为0向量的线性组合方式  

### R
行最简形矩阵

## 矩阵空间
对于矩阵加法封闭、数乘封闭

### 矩阵空间的子空间
3*3矩阵空间：维度9
- 上三角矩阵：维度6
- 对称矩阵：维度6
- 上三角对称矩阵->对角矩阵：维度3
- 上三角矩阵或对称矩阵：**不是子空间**     
*上三角矩阵和对称矩阵任意线性组合可得到整个$R^{3*3}$矩阵的向量空间*

***两个子矩阵空间的维度之和等于他们并集和交集的维度之和***

### 子空间与零空间
$v_1+v_2+v_3+v_4 = 0$构成子空间     
与A = （1， 1， 1，1）的零空间等价    
**$r_A = 1$，零空间的维度为3，则子空间是三维的**

***仅由零点组成的空间是一维的***


## 拓扑结构与矩阵
用矩阵描述实际问题（电流为例）    
m表示连线的个数，n表示节点的个数
### Ax=0
x表示节点（等势点）
- 以A来对x（点）做运算
- 以结果向量表示电势差           
***E=Ax, E表示电势差***

### 基尔霍夫电流定律（KCL）
$A^Ty = 0$      
y表示电流    
- 以$A^T$来对y做运算
- 以结果向量表示各个节点的合电流
- 结果等于0向量，说明各个节点的流入等于流出     
***$A^T$y = f, f表示外部电流源###


***欧姆定律x = Cy***

### 树
没有形成回路的图（行向量线性无关）     

### 欧拉公式
用线性代数证明欧拉公式     
***相互无关的回路数目($dim N(A^T)$) = 边的数目(m) - (节点数目(n) - 1)***    
***相互线性无关的回路数目+节点数目-边的数目 = 1***     
***#nodes-#edges+#loops=1***



