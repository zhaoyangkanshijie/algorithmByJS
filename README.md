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

* 时间：最优O(nlog2n)，最差O(n^2)，平均O(nlog2n)
* 空间：最优O(logn)每一次都平分数组的情况，最差O(n)退化为冒泡排序的情况

4. 稳定性

* 不稳定

5. 优化

* 任意基准：第一个数与随机一个数交换位置，再把第一个数作为主元
* 三数(左中右)取中值作为主元
* 数组长度小到指定长度，用插入排序

#### 冒泡排序
1. 思想

相邻元素两两对比，把较大数放后面

2. 操作
```js
for (let i = 0; i < len; i++) {
    for (let j = 0; j < len - 1 - i; j++) {
        if (arr[j] > arr[j+1]) {        //相邻元素两两对比
            let temp = arr[j+1];        //元素交换
            arr[j+1] = arr[j];
            arr[j] = temp;
        }
    }
}
```

3. 复杂度
* 时间：最优O(n)，最差O(n^2)，平均O(n^2)
* 空间：O(1)

4. 稳定性

* 稳定

#### 选择排序
1. 思想

随着索引移动，不断寻找最小的数，与索引处元素交换

2. 操作
```js
for (let i = 0; i < len - 1; i++) {
    minIndex = i;
    for (let j = i + 1; j < len; j++) {
        if (arr[j] < arr[minIndex]) {     //寻找最小的数
            minIndex = j;                 //将最小数的索引保存
        }
    }
    temp = arr[i];
    arr[i] = arr[minIndex];
    arr[minIndex] = temp;
}
```

3. 复杂度
* 时间：最优O(n)，最差O(n^2)，平均O(n^2)
* 空间：O(1)

4. 稳定性

* 不稳定

#### 插入排序
1. 思想

有一个已经有序的数据序列，要求在这个已经排好的数据序列中插入一个数，但要求插入后此数据序列仍然有序

2. 操作
```js
for (let i = 1; i < len; i++) {
    preIndex = i - 1;
    current = arr[i];
    while (preIndex >= 0 && arr[preIndex] > current) {
        arr[preIndex + 1] = arr[preIndex];
        preIndex--;
    }
    arr[preIndex + 1] = current;
}
```

3. 复杂度
* 时间：最优O(n)，最差O(n^2)，平均O(n^2)
* 空间：O(1)

4. 稳定性

* 稳定

#### 希尔排序
1. 思想

递减间隔分组插入排序

2. 操作
```js
while(gap>=1){  
    for(let i =gap;i<arr.length;i++){  
        let j,temp=arr[i];  
        for(j=i-gap;j>=0&&temp<arr[j];j=j-gap){  
            arr[j+gap]=arr[j];  
        }  
        arr[j+gap]=temp;  
    }  
    gap=Math.floor(gap/2);  
}
```

3. 复杂度
* 时间：最优O(nlog2n)，最差O(n^2)，平均O(n^1.5)
* 空间：O(1)

4. 稳定性

* 不稳定

#### 归并排序
1. 思想

相当于二叉树，每个根节点表示一个数，两两归并排序到其上一个节点，直到根节点完全排好

2. 操作
```js
let mergeSort = (arr) => {//采用自上而下的递归方法
    // 设置终止的条件，
    if (arr.length < 2) {
        return arr;
    }
    //设立中间值
    let middle = parseInt(arr.length / 2);
    //第1个和middle个之间为左子列
    let left = arr.slice(0, middle);
    //第middle+1到最后为右子列
    let right = arr.slice(middle);
    if (left == "undefined" && right == "undefined") {
        return false;
    }
    return merge(mergeSort(left), mergeSort(right));
}

let merge = (left, right) => {
    let result = [];

    while (left.length && right.length) {
        if (left[0] <= right[0]) {
            //把left的左子树推出一个，然后push进result数组里
            result.push(left.shift());
        } else {
            //把right的右子树推出一个，然后push进result数组里
            result.push(right.shift());
        }
    }
    //经过上面一次循环，只能左子列或右子列一个不为空，或者都为空
    while (left.length) {
        result.push(left.shift());
    }
    while (right.length) {
        result.push(right.shift());
    }
    return result;
}
```

3. 操作

* 细节排序方法

对比左右两个有序序列，只需比较两边第一个元素，把较小的取出并放入新数组，使归并数组有序

* 结束递归条件

数组长度为1(二叉树分到根节点)

4. 复杂度
* 时间：最优O(nlog2n)，最差O(nlog2n)，平均O(nlog2n)
* 空间：O(n)

5. 稳定性

* 稳定

6. 优化

* TimSort

检测序列中的天然有序子段，若检测到严格降序子段则翻转序列为升序子段，在最好情况下无论升序还是降序都可以使时间复杂度降至为O(n)

* 原地归并

原本需要一个辅助数组，所以归并排序的空间复杂度是O(n)，优化后可以进行原地排序，额外空间为O(1)。

核心思想是“交换两段相邻内存块”。

具体操作：起始左右索引为各自的第一个元素，比较两边索引，不产生逆序，则两边索引向前走，否则，把右边产生逆序的数据段插入到左边索引之前，直到其中一个数组遍历完成。

![原地归并](mergeSortOpt.png)

7. 其它应用

* 逆序数对

#### 堆排序
1. 概念

堆实际上是一个完全二叉树，并且其左右子节点都不大于父节点（父节点大于子节点）
最大堆是父节点>左节点>右节点

父节点索引为i，其左子节点索引为2i+1，其右子节点索引为2i+2

最后一个父节点的索引为floor(length/2-1)

2. 思想

从后往前遍历一次每个父节点来构造堆(父节点>子节点)，遍历后根节点(0)一定是最大的数，与最后一个节点(length-1)交换位置，数组长度-1，接下来的操作不影响最后一个元素，重复以上操作。

3. 操作

```js
let len;    //因为声明的多个函数都需要数据长度，所以把len设置成为全局变量

let buildMaxHeap = (arr) => {   //建立大顶堆
    len = arr.length;
    for (let i = Math.floor(len / 2 - 1); i >= 0; i--) {
        heapify(arr, i);
    }
}

let heapify = (arr, i) => {     //堆调整
    let left = 2 * i + 1,//左节点
        right = 2 * i + 2,//右节点
        largest = i;//父节点

    if (left < len && arr[left] > arr[largest]) {
        largest = left;
    }

    if (right < len && arr[right] > arr[largest]) {
        largest = right;
    }

    if (largest != i) {
        swap(arr, i, largest);
        heapify(arr, largest);//其子节点变父节点，再次调整
    }
}

let swap = (arr, i, j) => {
    let temp = arr[i];
    arr[i] = arr[j];
    arr[j] = temp;
}

let heapSort = (arr) => {
    //初始化，i从最後一个父节点开始调整
    buildMaxHeap(arr);
    //先将第一个元素和已经排好的元素前一位做交换，再从新调整(刚调整的元素之前的元素)，直到排序完毕
    for (let i = arr.length - 1; i > 0; i--) {
        swap(arr, 0, i);
        len--;
        heapify(arr, 0);//从根节点开始递归
    }
    return arr;
}
```

* 处理数组越界

在堆调整时，需要判断左右节点索引是否超过要处理的长度

* 初始化和重复操作

初始化建立堆，使父节点>子节点，后形成循环过程：交换数值，长度减一，根节点调整堆(由于堆性质，每次比较3个数，即可把最大数调至父节点，无需考虑子孙节点比父节点大)。

* 为什么不一开始就每次建立堆，交换，然后长度减一？

这样做和选择排序，每次找到最大数，放到最后的操作一样了

4. 复杂度
* 时间：初始化堆O(n)，调整堆(nlog2n)，总体O(nlog2n)
* 空间：O(1)

5. 稳定性

* 不稳定

#### 计数排序


#### 桶排序


#### 基数排序


### 深度优先搜索

### 最小生成树算法prim
