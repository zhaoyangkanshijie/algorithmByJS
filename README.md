# algorithmByJS

## 最短路径算法dijkstra(shortestPath.html)
### 运行方式
1. 自动生成随机数或手动输入数
2. 点击"start"，再点击起始方格，点击"end"，再点击结束方格，来定义起始和结束位置。
3. 点击"shortestPath"，会画出最短路径。方格数字表示经过这格的距离，数字越大，距离越大。
4. 点击"clear"会清除路线，然后可重新定义起始和结束位置。
### 图例：
![最短路径](shortestPath.gif)

## 排序算法(sort.html)
### 运行方式
1. 自动生成随机数或手动输入数
2. 点击其中一种排序算法，对数字进行排序
3. 点击"reset"重置数据
4. 感谢作者[杜少](https://www.cnblogs.com/dushao/p/6004883.html)
### 图例：
![最短路径](sort.gif)

## 深度优先搜索(dfs.html)
### 运行方式
1. 设置格子长款个数，绘制表格
2. 点击格子设置和取消障碍
3. 点击"搜索路径"进行搜索
4. 感谢作者[zwseaman](https://blog.csdn.net/zwseaman/article/details/7592855)
### 图例：
![最短路径](dfs.gif)

## 最小生成树算法prim(prim.html)
1. 点击"start"自动寻找出路
2. 点击"reset"重置迷宫
3. 感谢作者[欧阳蒜苗](https://blog.csdn.net/scargtt/article/details/71078275)
### 图例：
![最短路径](prim.gif)

## 算法简介
### 最短路径算法dijkstra
* 准备信息
1. 一共有vertex个点
2. 起始点为第a个点，结束点为第b个点
3. 把问题模型转化为：点与点之间距离的邻接矩阵adj[][]
4. 记录起点到每个顶点的最短路径的信息数组dis[]
5. 信息数组dis[]的每项信息对象msg，path文字记录起始点到每个点，value记录这段路径的距离，visit记录是否已经访问
6. 定义最远距离为infinate

* 邻接矩阵初始化(问题模型转化)
1. 全部初始化为infinate
2. 自身到自身距离为0，对角线为0
3. 计算点到点的距离，非直连点距离记为infinate

* 初始化信息数组
1. 记录path为“va-->vi”
2. 根据adj[a][i]记录value
3. visit除自身点为true以外，其余全为false

* 计算过程
1. a找出最近直连点x，路径为pathAX

具体操作为循环每一个**没访问过**的**直连**点，比较dis[i]得出最小值，并获得序号x，标记x已经访问

2. x找出最近直连点y，路径为pathXY，如果有路径pathAX + pathXY < pathAY，则更新pathAY距离

具体操作为循环每一个**没访问过**的**直连**点，如果dis[x] + adj[x][i] < dis[i]，更新dis[i]信息

3. 循环以上过程，即每一个点，使得信息数组填充完备，其中dis[b]包含最短路径信息

* 更多操作
1. 可打印最短距离，经过的路径信息等

* 思考
1. 最短路径是 1维寻找最小数 的2维版本
2. 1维寻找最小数可实现排序，路径也可以进行排序
3. 3维的最短路径，只需计算出周围8个点的路径，坐标计算变为3维，其余思想不变

### 排序算法
#### 快速排序
1. 思想

记录第一个数，通过调整数组，先不管排序，比它小的放左边，比它大的放右边，以它为切割点，分割成2个数组，重复以上操作，直到不可分割出数组

2. 操作

* 如何扫描？

```js
while (i != j) {
    while (i < j && arr[j] > temp) {//从右往左扫描到一个小于temp的元素
        j--;
    }
    if (i < j) {
        arr[i] = arr[j];//把j的元素放在i的位置上（temp的左边）
        i++;//i右移一位
    }
    while (i < j && arr[i] < temp) {//从左往右扫描找到一个大于temp的元素
        i++;
    }
    if (i < j) {
        arr[j] = arr[i];//把i的元素放在j的位置上(temp的右边)
        j--;
    }
}
arr[i] = temp;//将temp放在最终位置
```

* 结束条件(持续条件)

左索引大于等于右索引(左索引小于右索引)

3. 复杂度

* 时间：最优O(nlogn)，最差O(n^2)，平均O(nlogn)
* 空间：最优O(logn)每一次都平分数组的情况，最差O(n)退化为冒泡排序的情况

4. 稳定性

* 不稳定

5. 优化

* 任意基准：第一个数与随机一个数交换位置，再把第一个数作为主元
* 三数(左中右)取中值作为主元
* 数组长度小到指定长度，用插入排序

#### 冒泡排序


#### 选择排序


#### 插入排序


#### 希尔排序


#### 归并排序


#### 堆排序


#### 计数排序


#### 桶排序


#### 基数排序


### 深度优先搜索

### 最小生成树算法prim
