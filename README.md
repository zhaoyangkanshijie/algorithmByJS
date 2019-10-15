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
4. 感谢作者[杜少](https://www.cnblogs.com/dushao/p/6004883.html)、[凯尔宝宝](https://blog.csdn.net/xuyangxinlei/article/details/81062015)
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

## KMP算法(kmp.html)
1. 修改input值
3. 感谢作者[0giant](https://www.cnblogs.com/LUO77/p/5603893.html)
### 图例：
![KMP算法](kmp.gif)

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

* 快速排序的多种写法
    * 填充法：元素比较基准值，把元素值填入当前位置
    ```js
        let quickSort = (arr, l, r) => {
            let pivot, left = l, right = r;
            if (left < right) {//避免栈溢出风险
                pivot = arr[left];
                while (left != right) {
                    while (left < right && arr[right] > pivot) {
                        right--;
                    }
                    if (left < right) {
                        arr[left] = arr[right];
                        left++;
                    }
                    while (left < right && arr[left] < pivot) {
                        left++;
                    }
                    if (left < right) {
                        arr[right] = arr[left];
                        right--;
                    }
                }
                arr[left] = pivot;
                quickSort(arr, l, left - 1);
                quickSort(arr, left + 1, r);
            }
        }
    ```
    * 交换法：元素比较基准值左右均完成后，交换左右位置
    ```js
        let quickSort = (arr, l, r) => {
            if(l < r){
                var pivot = arr[l], left = l, right = r;
                while(left < right){
                    while(left < right && arr[right] >= pivot){
                        right--;
                    }
                    while (left < right && arr[left] <= pivot) {
                        left++;
                    }
                    if(left<right){
                        let tmp = arr[left];
                        arr[left] = arr[right];
                        arr[right] = tmp;
                    }
                }
                let tmp2 = arr[left];
                arr[left]  = arr[l];
                arr[l] = tmp2;

                quickSort(arr, l, left - 1);
                quickSort(arr, left + 1, r);
            }
        }
    ```
    * 非递归法：解决数据量大导致栈溢出的问题，因此把[left,right]保存到数组
    ```js
    let quickSort = function(num, left, right) {
        let list = [[left, right]]; // 将[left,right]存入数组中，类似于递归入栈
        while (list.length > 0) { // 若list不为空，循环弹出list最后一个数组进行快排
            let now = list.pop(); // 弹出list末尾。(也可用list.shift()取出list第一个数组，但在数据量较大时，这种方式效率较低)
            if (now[0] >= now[1]) { // 若左右指针相遇，待排序数组长度小宇1，则无需进行快排(注意不能写成now[0]==now[1]，这里now[0]是有可能大于now[1]的
                continue;
            }
            let i = now[0], j = now[1], flag = now[0]; // 以下与递归方法相同，请参考上面的递归详解
            while (i < j) {
                while (num[j] >= num[flag] && j > flag) j--;
                if (i >= j) {
                    break;
                }
                while (num[i] <= num[flag] && i < j) i++;
                let temp = num[flag];
                num[flag] = num[j];
                num[j] = num[i];
                num[i] = temp;
                flag = i;
            }
            list.push([now[0], flag - 1]); // 将flag左边数组作为待排序数组，只需将左右指针放入list即可。
            list.push([flag + 1, now[1]]); // 将flag右边数组作为待排序数组，只需将左右指针放入list即可。
        }
    }
    ```

* 任意基准：第一个数与随机一个数交换位置，再把第一个数作为主元，其余算法同理
* 三数(左中右)取中值作为主元：第一个数、中间数、末尾数取排第二大的数与第一个数交换位置，再把第一个数作为主元，其余算法同理
```js
let GetMid = (array, left, right) =>
{
	var mid = left + ((right - left) / 2);

	if (array[left] <= array[right])
	{
		if (array[mid] < array[left])
			return left;
		else if (array[mid] > array[right])
			return right;
		else
			return mid;
	}
	else
	{
		if (array[mid] > array[left])
			return left;
		else if (array[mid] < array[right])
			return right;
		else
			return mid;
	}

}
```
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
1. 思想

把数存入数组索引，遍历数组即完成排序

2. 复杂度
* 时间：O(n+k)
* 空间：O(n+k)

3. 稳定性

* 稳定

#### 桶排序
1. 概念

* 桶的个数：按需定义
* 桶的数据范围步长：(数组最大值-数组最小值)/桶个数
* 数映射到哪个桶：floor((当前数-数组最小值)/步长)

2. 思想

把数映射到每个桶中，再对每个桶内的数据进行排序，排序方法可选择插入排序，最后把桶拼接在一起

2. 复杂度
* 时间：最优O(n+k)，最差O(n^2)，平均O(n+k)
* 空间：O(n*k)

3. 稳定性

* 稳定(因为插入排序稳定)

#### 基数排序
1. 思想

以十进制为例，有0-9十个桶，把个位数为x的数放入第x个桶，序号由小到大收集桶的数据，其它位数重复以上操作(每次操作完成都能保证那一位数的较大值能排在后面)，直至最大位数排完

2. 操作
```js
let mod = 10;
let dev = 1;
for (let i = 0; i < maxDigit; i++ , dev *= 10, mod *= 10) {
    for (let j = 0; j < arr.length; j++) {
        let bucket = parseInt((arr[j] % mod) / dev);
        if (counter[bucket] == null) {
            counter[bucket] = [];
        }
        counter[bucket].push(arr[j]);
    }
    let pos = 0;
    for (let j = 0; j < counter.length; j++) {
        let value = null;
        if (counter[j] != null) {
            while ((value = counter[j].shift()) != null) {
                arr[pos++] = value;
            }
        }
    }
}
```

3. 复杂度
* 时间：O(d(n+r)) r为进制数(基数)，分配的时间复杂度为O（n）收集的的时间复杂度为O(radix)，分配和收集共需要distance趟

* 空间：O(n+r)

4. 稳定性

* 稳定

### 深度优先搜索
1. 思想

一条道路走到黑，走不通就回到上一个分叉点，换一条路走

2. 操作
* 建立邻接矩阵，1表示可直达，0表示不可直达
* 准备一个visit数组表示每个点是否访问
* 循环邻接矩阵，从第一个点开始，对遇到的每一个没访问过的点进行深度优先搜索，形成递归，递归条件结束为这个点没有下一个点或下一个点已经被访问，结束条件为所有点被访问

```C++
void DFS(int v)
{
    int n=vertexNum;//顶点数目
    if(v<0||v>=n) throw "位置出错";
    cout<<vertex[v]<<" ";//输出顶点v
    visited[v]=1;//被访问过
    for(int j=0;j<n;j++)
        if(visited[j]==0&&adj[v][j]==1)//没被访问过且存在边(v,j)
            DFS(j);
}
```

3. 复杂度
时间：O(n^2)

### 广度优先搜索
1. 思想

水波扩散

2. 操作
* 建立邻接矩阵，1表示可直达，0表示不可直达
* 准备一个visit数组表示每个点是否访问
* 准备一个队列来把新进来的数顶替旧的数
* 准备一个数组记录被顶替的数
* 循环邻接矩阵，从第一个点开始，进入队列，把第一个点取出放入数组，把第一个点的所有直连点放入队列，重复以上操作，直至所有点访问过或队列为空

```C++
void BFS(Graph G, void (*visit)(int v))
{
    int v = 0;
    //初始化访问标记的数组
    for (v = 0; v < G.vexnum; v++)
    {
        visited[v] = false;
    }
    //依次遍历整个图的结点
    for (v = 0; v < G.vexnum; v++)
    {
        //如果v尚未访问，则访问 v
        if  (!visited[v])
        {
            //把 v 顶点对应的数组下标处的元素置为真，代表已经访问了
            visited[v] = true;
            //然后v入队列，利用了队列的先进先出的性质
            q.push(v);
            //访问 v，打印处理
            cout << q.back() << " ";
            //队不为空时
            while (!q.empty())
            {
                //队头元素出队,并把这个出队的元素置为 u，类似层序遍历
                Graph *u = q.front();
                q.pop();
                //w为u的邻接顶点
                for (int w = FirstAdjVex(G, u); w >= 0; w = NextAdjVex(G,u,w))
                {
                    //w为u的尚未访问的邻接顶点
                    if (!visited[w])
                    {
                        visited[w] = true;
                        //然后 w 入队列，利用了队列的先进先出的性质
                        q.push(w);
                        //访问 w，打印处理
                        cout << q.back() << " ";
                    }
                }
            }
        }
    }
}
```
来源：[dashuai](https://www.cnblogs.com/kubixuesheng/p/4399705.html)

3. 复杂度
时间：O(n^2)

### 最小生成树算法prim
1. 思想

从第一点开始，寻找边最小的点连通为树，再从它们能直连到其它点中，寻找边最小的未访问过的点连通为树，直至所有点连在一起或所有点访问过

2. 操作
* 把图转化为邻接矩阵adj[][]
* visit数组记录每个点的访问情况
* lowcost数组记录记录每2个点间最小权值，初始化为第一个点到每个点的权值，不直连的记为infinate
* pos记录最短边下标
* 循环每一个点i，循环找出未访问过的最短边mindis(j)，点为j，标记j已访问，把j可直连的未访问过的点adj[j][x]与记录在案的每一个最小权值lowcost[x]比较，如果adj[j][x]较小，则刷新lowcost[x]
* 把每次mindis(j)相加可求总最小权值

```C++
#include <iostream>
#include <vector>
using namespace std;

//Prim算法实现
void prim_test()
{
    int n;
    cin >> n;
    vector<vector<int> > A(n, vector<int>(n));
    for(int i = 0; i < n ; ++i) {
        for(int j = 0; j < n; ++j) {
            cin >> A[i][j];
        }
    }

    int pos, minimum;
    int min_tree = 0;
    //lowcost数组记录每2个点间最小权值，visited数组标记某点是否已访问
    vector<int> visited, lowcost;
    for (int i = 0; i < n; ++i) {
        visited.push_back(0);    //初始化为0，表示都没加入
    }
    visited[0] = 1;   //最小生成树从第一个顶点开始
    for (int i = 0; i < n; ++i) {
        lowcost.push_back(A[0][i]);    //权值初始化为0
    }

    for (int i = 0; i < n; ++i) {    //枚举n个顶点
        minimum = max_int;
        for (int j = 0; j < n; ++j) {    //找到最小权边对应顶点
            if(!visited[j] && minimum > lowcost[j]) {
                minimum = lowcost[j];
                pos = j;
            }
        }
        if (minimum == max_int)    //如果min = max_int表示已经不再有点可以加入最小生成树中
            break;
        min_tree += minimum;
        visited[pos] = 1;     //加入最小生成树中
        for (int j = 0; j < n; ++j) {
            if(!visited[j] && lowcost[j] > A[pos][j]) lowcost[j] = A[pos][j];   //更新可更新边的权值
        }
    }

    cout << min_tree << endl;
}

int main(void)
{
    prim_test();

    return 0;
}
```
来源：[JoshuaMK](https://www.cnblogs.com/JoshuaMK/p/prim_kruskal.html)

### 最小生成树算法Kruskal

1. 思想

对所有权值进行从小到大排序，每次选取最小的权值，如果和已有点集构成环则跳过(通过并查集检查)，否则加到该点集中。

2. 操作
* 根据图建立类，记录图信息，点a，点b，ab权值,并按ab权值升序排序
* 初始化并查集father[i]=i
* 循环每一个点，寻找每一个点在并查集中的根，判断的条件为如果father[i]=i它就是根，否则就让i =father[i]，向上寻找，直到其相等
* 如果点同源，则跳过,否则a和b不同源，则father[b]=a，那么b就挂载在a下

```C++
#include <stdio.h>
#include <stdlib.h>
#define Max 50
typedef struct road *Road;
typedef struct road
{
	int a , b;
	int w;
}road;
 
typedef struct graph *Graph;
typedef struct graph
{
	int e , n;
	Road data;
}graph;
 
Graph initGraph(int m , int n)
{
	Graph g = (Graph)malloc(sizeof(graph));
	g->n = m;
	g->e = n;
	g->data = (Road)malloc(sizeof(road) * (g->e+1));
	return g;
}
 
void create(Graph g)
{
	int i;
	for(i = 1 ; i <= g->e ; i++)
	{
		int x , y, w;
		scanf("%d %d %d",&x,&y,&w);
		if(x < y)
		{
			g->data[i].a = x;
			g->data[i].b = y;
		}
		else
		{
			g->data[i].a = y;
			g->data[i].b = x;
		}
		g->data[i].w = w;
	}
}
 
int getRoot(int v[], int x)
{
	while(v[x] != x)
	{
		x = v[x];
	}
	return x;
}
 
void sort(Road data, int n)
{
	int i , j;
	for(i = 1 ; i <= n-1 ; i++)
	{
		for(j = 1 ; j <= n-i ; j++)
		{
			if(data[j].w > data[j+1].w)
			{
				road t = data[j];
				data[j] = data[j+1];
				data[j+1] = t;
			}
		}
	}
}
 
int Kruskal(Graph g)
{
	int sum = 0;
	//并查集
	int v[Max];
	int i;
	//init
	for(i = 1 ; i <= g->n ; i++)
	{
		v[i] = i;
	}
	sort(g->data , g->e);
	//main
	for(i = 1 ; i <= g->e ; i++)
	{
		int a , b;
		a = getRoot(v,g->data[i].a);
		b = getRoot(v,g->data[i].b);
		if(a != b)
		{
			v[a] = b;
			sum += g->data[i].w;
		}
	}
	return sum;
}
 
int main()
{
	int m , n , id = 1;
	while(scanf("%d %d",&m,&n) != EOF)
	{
		int r , i;
		Graph g = initGraph(m,n);
		create(g);
		r = Kruskal(g);
		printf("Case %d:%d\n",id++,r);
		free(g);
	}
	return 0;
}
```
来源：[mgsky1](https://blog.csdn.net/mgsky1/article/details/77840286)

### KMP算法
1. 思想
* 朴素算法
    子串在第一位与主串开始比较，在第j位与主串失配，把子串后移一位，继续重新比较。
    复杂度O(m*n)

* 改进算法
    失配时，不要浪费前j-1位匹配成功的资源，子串向前移动到子串前后缀重复的地方，如果重复后的子串和主串不匹配，则在不匹配的下一位重新比较。

2. 操作
* 求next数组(子串向前移动到子串前后缀重复的地方) 
```C++
public static int[] getNext(String ps) {
    char[] p = ps.toCharArray();
    int[] next = new int[p.length];
    next[0] = -1;
    int j = 0;
    int k = -1;
    while (j < p.length - 1) {
        if (k == -1 || p[j] == p[k]) {
            next[++j] = ++k;
        } else {
            k = next[k];
        }
    }
    return next;
}
```
* 求next数组(如果重复后的子串和主串不匹配，则在不匹配的下一位重新比较) 
```C++
public static int[] getNext(String ps) {
    char[] p = ps.toCharArray();
    int[] next = new int[p.length];
    next[0] = -1;
    int j = 0;
    int k = -1;
    while (j < p.length - 1) {
        if (k == -1 || p[j] == p[k]) {
            if (p[++j] == p[++k]) { // 当两个字符相等时要跳过
                next[j] = next[k];
            } else {
                next[j] = k;
            }
        } else {
            k = next[k];
        }
    }
    return next;
}
```
* KMP
```C++
public static int KMP(String ts, String ps) {
    char[] t = ts.toCharArray();
    char[] p = ps.toCharArray();
    int i = 0; // 主串的位置
    int j = 0; // 模式串的位置
    int[] next = getNext(ps);
    while (i < t.length && j < p.length) {
    if (j == -1 || t[i] == p[j]) { // 当j为-1时，要移动的是i，当然j也要归0
        i++;
        j++;
    } else {
        // i不需要回溯了
        // i = i - j + 1;
        j = next[j]; // j回到指定位置
    }
    }
    if (j == p.length) {
    return i - j;
    } else {
    return -1;
    }
}
```

来源：
1. [KMP算法&next数组总结](https://www.cnblogs.com/LUO77/p/5603893.html)
2. [[KMP算法]最简单通俗易懂求next数组的方法](https://blog.csdn.net/hi25779/article/details/89504487)
3. [（算法）通俗易懂的字符串匹配KMP算法及求next值算法](https://blog.csdn.net/qq_37969433/article/details/82947411)
4. [很详尽KMP算法（厉害）](https://www.cnblogs.com/ZuoAndFutureGirl/p/9028287.html)

### 二叉树
1. 储存方式
* 数组：按完全二叉树层次遍历1-n填入数组，在不完全的地方填null

    ["a", "b", "c", "d", "e", "f", null, "g", null, null, null, "h"]

* 链表：节点对象：值、左、右、（父）、插入左方法、插入右方法

来源：[二叉树的存储方式和遍历方式](https://blog.csdn.net/simplehap/article/details/63259845)

2. 节点位置关系

按数组关系

* 父：i，左：2i+1，右：2i+2
* 每层最左：2^i，每层最右：2^(i+1)-1

3. 遍历方法
* 前序遍历(深度优先搜索)：中左右
* 中序遍历：左中右
* 后序遍历：左右中
* 层序遍历(广度优先搜索)：队列

来源：[关于二叉树的前序、中序、后序三种遍历](https://blog.csdn.net/qq_33243189/article/details/80222629)

4. 代码示例
```js
//二叉树节点对象
function binaryTreeNode(data = null, parent = null, left = null, right = null) {
    this.data = data;
    this.parent = parent;
    this.left = left;
    this.right = right;
    this.appendLeft = function (node) {
        this.left = node;
        node.parent = this;
    }
    this.appendRight = function (node) {
        this.right = node;
        node.parent = this;
    }
}
//储存方式：数组转链表
function arrayBinaryTreeToLinkBinaryTree(arrayBinaryTree) {
    //console.log(arrayBinaryTree)
    var len = arrayBinaryTree.length;
    var root = null;
    var nodeArray = new Array(len).fill(null);
    //console.log(len,Math.floor(len / 2));
    //只需遍历一半即可生成整棵树
    for (var i = 0; i < Math.floor(len / 2); i++) {
        //console.log('i:' + i);
        if (arrayBinaryTree[i] != null) {
            if (nodeArray[i] == null) {
                nodeArray[i] = new binaryTreeNode({ key: arrayBinaryTree[i], value: i });
                //console.log('create node ' + arrayBinaryTree[i]);
            }
            //父子位置关系：i，2i+1,2i+2
            //console.log('2 * i + 1:' + (2 * i + 1) + ',len:'+len);
            if (2 * i + 1 <= len && arrayBinaryTree[2 * i + 1] != null) {
                if (nodeArray[2 * i + 1] == null) {
                    nodeArray[2 * i + 1] = new binaryTreeNode({ key: arrayBinaryTree[2 * i + 1], value: 2 * i + 1 });
                    //console.log('create node ' + arrayBinaryTree[2 * i + 1]);
                }
                nodeArray[i].appendLeft(nodeArray[2 * i + 1]);
                //console.log('node ' + nodeArray[i].data.key + ' append left node ' + arrayBinaryTree[2 * i + 1]);
            }
            //console.log('2 * i + 2:' + (2 * i + 2) + ',len:' + len);
            if (2 * i + 2 <= len && arrayBinaryTree[2 * i + 2] != null) {
                if (nodeArray[2 * i + 2] == null) {
                    nodeArray[2 * i + 2] = new binaryTreeNode({ key: arrayBinaryTree[2 * i + 2], value: 2 * i + 2 });
                    //console.log('create node ' + arrayBinaryTree[2 * i + 2]);
                }
                nodeArray[i].appendRight(nodeArray[2 * i + 2]);
                //console.log('node ' + nodeArray[i].data.key + ' append right node ' + arrayBinaryTree[2 * i + 2]);
            }
        }
        if (i == 0) {
            root = nodeArray[0];
            if (root == null) {
                return null;
            }
        }
    }
    //去除原数组null值，使储存空间不再连续
    nodeArray = nodeArray.filter(s => s);
    //console.log(nodeArray);
    return root;
}
//储存方式：链表转数组
function linkBinaryTreeToArrayBinaryTree(root) {
    //console.log('root:',root);
    var queue = [];
    var arrayBinaryTree = [];
    if (root != null) {
        queue.push(root);
        arrayBinaryTree.push(root.data.key);
    }
    else {
        return [];
    }
    //广度优先转换
    //console.log('queueInit:', queue);
    while (queue.length > 0) {
        //console.log('queue:',queue[0],queue.length);
        if (queue[0].left != null) {
            arrayBinaryTree.push(queue[0].left.data.key);
            //console.log('left:', queue[0].left);
            queue.push(queue[0].left);
        }
        else {
            arrayBinaryTree.push(null);
        }
        if (queue[0].right != null) {
            arrayBinaryTree.push(queue[0].right.data.key);
            //console.log('right:', queue[0].right);
            queue.push(queue[0].right);
        }
        else {
            arrayBinaryTree.push(null);
        }
        queue.shift();
        //console.log(arrayBinaryTree);
    }
    //console.log(arrayBinaryTree);
    //去除末尾没必要的null值
    var lastNotNull = -1;
    for (var len = arrayBinaryTree.length - 1; len >= 0; len--) {
        if (arrayBinaryTree[len] != null) {
            lastNotNull = len;
            //console.log(len);
            break;
        }
    }
    return arrayBinaryTree.slice(0, len+1);
}
//前序遍历
var preOrder = [];
function preOrderLoop(root) {
    if (root == null)
    {
        return;
    }
    //console.log(root.data.key);
    preOrder.push(root.data.key);
    preOrderLoop(root.left);
    preOrderLoop(root.right);
}
//中序遍历
var inOrder = [];
function inOrderLoop(root) {
    if (root == null) {
        return;
    }
    inOrderLoop(root.left);
    //console.log(root.data.key);
    inOrder.push(root.data.key);
    inOrderLoop(root.right);
}
//后序遍历
var postOrder = [];
function postOrderLoop(root) {
    if (root == null) {
        return;
    }
    postOrderLoop(root.left);
    postOrderLoop(root.right);
    //console.log(root.data.key);
    postOrder.push(root.data.key);
}
$(function () {
    var arrayTree = ['a', 'b', 'c', 'd', 'e', 'f', null, 'g', null, null, null, 'h'];
    var linktree = arrayBinaryTreeToLinkBinaryTree(arrayTree);
    console.log(linktree);

    preOrder = [];
    preOrderLoop(linktree);
    console.log(preOrder);

    inOrder = [];
    inOrderLoop(linktree);
    console.log(inOrder);
    
    postOrder = [];
    postOrderLoop(linktree);
    console.log(postOrder);

    var arrayTree2 = linkBinaryTreeToArrayBinaryTree(linktree);
    console.log(arrayTree2);
});
```