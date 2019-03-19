



![image-20190316161136123](https://ws3.sinaimg.cn/large/006tKfTcgy1g14pbybwf0j31bq0u0n0z.jpg)

###排序算法比较

| 算法             | 稳定性 | 时间复杂度                   | 空间复杂度 | 备注                     |
| ---------------- | ------ | ---------------------------- | ---------- | ------------------------ |
| 选择排序         | ×      | N^2                          | 1          |                          |
| 冒泡排序         | √      | N^2                          | 1          |                          |
| 插入排序         | √      | N ~ N^2                      | 1          | 时间复杂度和初始顺序有关 |
| 希尔排序         | ×      | N 的若干倍乘于递增序列的长度 | 1          | 改进版插入排序           |
| 快速排序         | ×      | NlogN                        | logN       |                          |
| 三向切分快速排序 | ×      | N ~ NlogN                    | logN       | 适用于有大量重复主键     |
| 归并排序         | √      | NlogN                        | N          |                          |
| 堆排序           | ×      | NlogN                        | 1          | 无法利用局部性原理       |

**快速排序是最快的通用排序算法**，它的内循环的指令很少，**而且它还能利用缓存，因为它总是顺序地访问数据**。它的运行时间近似为 ~cNlogN，这里的 c 比其它线性对数级别的排序算法都要小。

###常见数据结构操作比较

![image-20190316155712039](/Users/allentian/Library/Application Support/typora-user-images/image-20190316155712039.png)

###堆得不同实现及其操作

![image-20190316160842529](/Users/allentian/Library/Application Support/typora-user-images/image-20190316160842529.png)

### 计数排序（简化版的桶排序）

**时间复杂度**：O(M+N)

**缺点**：不适用于浮点数，不适用于数组最小值和最大值相差过大的情况

计数排序需要根据原始数列的取值范围，创建一个统计数组，**用来统计原始数列中每一个可能的整数值所出现的次数**。

原始数列中的整数值，和统计数组的下标是一一对应的，**以数列的最小值作为偏移量，最大值-最小值作为数组长度（节约空间）**。比如原始数列的最小值是90， 那么整数95对应的统计数组下标就是 95-90 = 5。

#### 改进版计数排序

![image-20190319105655287](/Users/allentian/Library/Application Support/typora-user-images/image-20190319105655287.png)

![image-20190319105741873](/Users/allentian/Library/Application Support/typora-user-images/image-20190319105741873.png)

![image-20190319105828876](/Users/allentian/Library/Application Support/typora-user-images/image-20190319105828876.png)

### 桶排序

**桶元素分布均匀**：当n=m，时间复杂度可以达到O(n)

**桶元素分布极不均匀**：退化成O(nlogn)，相当于全在一个桶里排序，且还浪费了很多桶空间

1.得到数列的最大值和最小值，并算出差值d

2.初始化桶

3.遍历原始数组，将每个元素放入桶中

1. **`int num = (int)((array[i] - min)  * (bucketNum-1) / d);`**
2. `        bucketList.get(num).add(array[i]);`

4.**对每个桶内部进行排序（内部可以用Collections.sort()//JDK底层采用了归并排序或归并的优化版本）**

5**.输出全部元素**

![image-20190319110449005](/Users/allentian/Library/Application Support/typora-user-images/image-20190319110449005.png)

### 快速排序的指针移动顺序问题

**如果pivot选择数组最左边元素，则一定是right指针先左移，找小于pivot的，left指针再右移找大于pivot**

**这个移动顺序是为什么**：

选择的是最左边元素作为pivot，而最后希望得到的是左边小于pivot，右边大于pivot

且pivot的位置就是right==left的位置，**那么要求这个位置的数一定要是小于pivot的（因为要和pivot交换）**

而如果先移动left的话，那么最后碰撞就可能会是两种情况

1. left碰撞到**上一轮已交换后的right位置**，**但上一轮交换后right指向的大于pivot！！！**
2. right碰撞到**这一轮的未交换前left位置，但这一轮未交换前left指向的是大于pivot！！！**

所以，以上两种情况都会**导致大于pivot的数和pivot交换，同时pivot又是数组最左元素，即大于pivot元素被交换到了左数组，显然发生了错误**

### 红黑树

**五个性质**

1. 每个结点要么是红的要么是黑的。  
2. 根结点是黑的。  
3. 每个叶结点（叶结点即指树尾端NIL指针或NULL结点）都是黑的。  
4. 如果一个结点是红的，那么它的两个儿子都是黑的。  
5.  对于任意结点而言，其到叶结点树尾端NIL指针的每条路径都包含相同数目的黑结点。 

![image-20190317122147640](https://ws4.sinaimg.cn/large/006tKfTcgy1g15ob5jf9ej31340gcjut.jpg)