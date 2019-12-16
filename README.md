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
function mergeSort(arr) {
    if(arr.length < 2)
        return arr;

    let middle = Math.floor(arr.length / 2);
    let arrLeft = arr.slice(0, middle);
    let arrRight = arr.slice(middle);

    return merge(mergeSort(arrLeft), mergeSort(arrRight));

}

function merge(arrLeft, arrRight) {
    // 这里arrLeft和arrRight都是排好序的数组
    let i = 0;
    let j = 0;
    let newArr = [];
    while(i<arrLeft.length && j<arrRight.length) {
        if(arrLeft[i] < arrRight[j]) {
            newArr.push(arrLeft[i]);
            i++;
        } else {
            newArr.push(arrRight[j]);
            j++;
        }
    }

    if(i === arrLeft.length) {  //如果arrLeft已经遍历完，则直接把arrRight数组中剩余的元素放入newArr
        newArr = newArr.concat(arrRight.slice(j));
    } else {
        newArr = newArr.concat(arrLeft.slice(i));
    }
    return newArr;
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

```js
//修改上面的merge
function merge(arrLeft, arrRight) {
    let i = 0;
    let j = 0;
    let newArr = [];
    while(i<arrLeft.length && j<arrRight.length) {
        if(arrLeft[i] <= arrRight[j]) {//改为<=
            newArr.push(arrLeft[i]);
            i++;
        } else {
            newArr.push(arrRight[j]);
            for (var index = i; index < arrLeft.length; index++) {
                console.log('pairs:(' + arrLeft[index] + ',' + arrRight[j] + ')');
            }
            //此位置的逆序数对长度为：arrLeft.length - i
            //总逆序数对：把这里出现的逆序数对累加即可
            j++;
        }
    }

    if(i === arrLeft.length) {  //如果arrLeft已经遍历完，则直接把arrRight数组中剩余的元素放入newArr
        newArr = newArr.concat(arrRight.slice(j));
    } else {
        newArr = newArr.concat(arrLeft.slice(i));
    }
    return newArr;
}
```

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
    //从最后一个父节点开始排，一旦底层排好，上层则不会产生递归，复杂度O(n)
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
        heapify(arr, largest);//其子节点变父节点，再次调整，只需调整被改动的半边，复杂度O(log2 n)
    }
}

let swap = (arr, i, j) => {
    let temp = arr[i];
    arr[i] = arr[j];
    arr[j] = temp;
}

let heapSort = (arr) => {
    //初始化，i从最後一个父节点开始调整
    buildMaxHeap(arr);//复杂度O(n)
    //先将第一个元素和已经排好的元素前一位做交换，再从新调整(刚调整的元素之前的元素)，直到排序完毕
    for (let i = arr.length - 1; i > 0; i--) {//复杂度O(n)
        swap(arr, 0, i);
        len--;
        heapify(arr, 0);//从根节点开始递归，复杂度O(log2 n)
    }
    //总复杂度O(n+nlog2 n)->O(nlog2 n)
    return arr;
}
```

测试：
```js
let heapSort = (array) => {
        let len = array.length;
        buildMaxHeap(array);
        while(len>0){
            swap(array,0,len-1);
            len--;
            heapJustify(array,0,len);
        }
    }
    let buildMaxHeap = (array) => {
        let len = array.length;
        for(let i = Math.floor(len/2-1);i >= 0;i--){
            heapJustify(array,i,len);
        }
    }
    let heapJustify = (array,currentNodeIndex,subLength) => {
        let leftIndex = 2*currentNodeIndex+1;
        let rightIndex = 2*currentNodeIndex+2;
        let maxIndex = currentNodeIndex;
        if(leftIndex<subLength && array[leftIndex]>array[maxIndex]){
            maxIndex = leftIndex;
        }
        if(rightIndex<subLength && array[rightIndex]>array[maxIndex]){
            maxIndex = rightIndex;
        }
        if(maxIndex != currentNodeIndex){
            swap(array,maxIndex,currentNodeIndex);
            heapJustify(array,maxIndex,subLength);
        }
    }
    let swap = (array,i,j) => {
        let temp = array[i];
        array[i] = array[j];
        array[j] = temp;
    }
    $(()=>{
        let array = [5,1,2,3,4,6,7];
        //hj(array,0,array.length);//[5, 1, 2, 3, 4, 6, 7]
        //bmh(array);//[7, 4, 6, 3, 1, 5, 2]
        heapSort(array);//[1, 2, 3, 4, 5, 6, 7]
        console.log(array);
    });
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

### 动态规划
1. 思想

    * 找规律(数学归纳法)
        * 状态变量：哪些变量有递推关系 
        * 状态转移方程：上一个状态与下一个状态的关系
        * 边界条件
        * 优化：由前向后？由后向前？

2. 样例

    * 来源：[力扣（LeetCode）](https://leetcode-cn.com)

    *  最长上升子序列

        ```txt
        输入: [10,9,2,5,3,7,101,18]
        输出: 4 
        解释: 最长的上升子序列是 [2,3,7,101]，它的长度是 4。

        返回长度，尽可能输出其中一种可能的序列。
        动态规划的时间复杂度为 O(n2) 。
        ```

        普通动态规划
        ```js
        let lis = (nums) => {
            let len = nums.length;
            if(len == 0) return 0;
            let dp = new Array(len).fill(1);
            let pos = [];
            let res = 0;
            //i表示最新的一位数
            for(let i=0;i<nums.length;i++){
                //j表示i前面的所有数
                for(let j=0;j<i;j++){
                //找出i前比i小的位置的最长递增子序列的最大值（找到以nums[i]结尾的最长递增子序列），虽然此处不一定是整个数组中的最大值
                    if(nums[j]<nums[i]){//改变运算符可变型为最长不减子序列，最长下降子序列等
                        dp[i] = Math.max(dp[i],dp[j]+1);//状态转移方程
                    }
                }
                //找出整个数组中的最大值
                //res = Math.max(res,dp[i]);
                if(res < dp[i]){
                    res = dp[i];
                    pos.push(nums[i]);//储存序列，用于输出
                }
            }
            console.log(nums,dp,pos);
            //[1, 2, 3, 4, 5, 3, 6, 4, 5]
            //[1, 3, 6, 7, 9, 10]
            return res;
        }

        $(()=>{
            let numbers = [1,3,6,7,9,4,10,5,6];
            console.log(lis(numbers));//6
        })
        ```

        抽牌二分查找，改进时间复杂度为O(n log n)
        ```js
        let lis = (nums) => {
            let top = new Array(nums.length);
            let piles = 0;// 牌堆数初始化为 0
            for (let i = 0; i < nums.length; i++) {
                let poker = nums[i];// 要处理的扑克牌
                //二分查找:决定新来的牌插入哪一个牌堆(插入到刚好比这牌大的牌堆中)
                //牌堆顶：1 2 3 4 5 6 7 8 -> 新牌：3
                //1 2 3 4
                //3 4
                //4
                //牌堆顶：1 2 3 3 5 6 7 8 -> 替换

                //牌堆顶：1 2 3 3 5 6 7 8 -> 新牌：9
                //5 6 7 8
                //7 8
                //8
                //牌堆顶：1 2 3 3 5 6 7 8 9 -> 新建
                let left = 0, right = piles;
                while (left < right) {
                    let mid = parseInt((left + right) / 2);
                    if (top[mid] >= poker) {
                        right = mid;
                    } 
                    else {
                        left = mid + 1;
                    } 
                }
                console.log("left:"+left,"piles:"+piles)
                if (left == piles) piles++;// 没找到合适的牌堆，新建一堆
                top[left] = poker;// 把这张牌放到牌堆顶
                console.log("poker top",top)
            }
            return piles;//最后牌堆数即为最长递增子序列长度
        }
        ```

        题目升级变型：俄罗斯套娃信封问题
        ```txt
        给定一些标记了宽度和高度的信封，宽度和高度以整数对形式 (w, h) 出现。当另一个信封的宽度和高度都比这个信封大的时候，这个信封就可以放进另一个信封里，如同俄罗斯套娃一样。

        请计算最多能有多少个信封能组成一组“俄罗斯套娃”信封（即可以把一个信封放到另一个信封里面）。

        说明:
        不允许旋转信封。

        输入: envelopes = [[5,4],[6,4],[6,7],[2,3]]
        输出: 3 
        解释: 最多信封的个数为 3, 组合为: [2,3] => [5,4] => [6,7]。
        ```

        ```js
        let maxEnvelopes = (envelopes) => {
            //先按第0位顺序排序，再按第一位逆序排序，根据第一位求最长递增子序列
            envelopes = envelopes.sort((a,b)=>{
                console.log(a,b);//a是第二个数,b是第一个数
                console.log((a[0]<b[0])||(a[0]==b[0]&&a[1]>b[1]));
                if((a[0]<b[0])||(a[0]==b[0]&&a[1]>b[1])){
                    return -1;
                }
                else{
                    return 1;
                }
            });
            console.log(envelopes);
            let numbers = envelopes.map((value,index,arr)=>{
                return value[1];
            });
            console.log(numbers);
            return lis(numbers);//见上面
        }
        $(()=>{
            let envelopes = [[5,4],[6,4],[6,7],[2,3]];
            console.log(maxEnvelopes(envelopes));
        });
        ```

### 滑动窗口
* 算法识别与思想

    一个数组中，对一些连续数据的操作，形成窗口

1. 样例1

    * 来源：[力扣（LeetCode）](https://leetcode-cn.com)

    * 和为K的子数组
    ```txt
    给定一个整数数组和一个整数 k，你需要找到该数组中和为 k 的连续的子数组的个数,并输出所有子数组。

    示例:
    输入:nums = [1,1,1], k = 2
    输出: 2 , [1,1] 与 [1,1] 为两种不同的情况。
    说明 :
    数组的长度为 [1, 20,000]。
    数组中元素的范围是 [-1000, 1000] ，且整数 k 的范围是 [-1e7, 1e7]。
    ```

    二重循环
    ```js
    let subarraySum = (nums, k) => {
        let count = 0;
        let position = [];
        for(let start = 0;start < nums.length;start++){
            let sum = 0;
            for(let end = start;end < nums.length;end++){
                sum += nums[end];
                if(sum == k){
                    count++;
                    position.push({
                        'start': start,
                        'end': end
                    });
                }
            }
        }
        console.log(position);
        return count;
    };
    $(()=>{
        let nums = [3,4,7,2,-3,1,4,2];
        let k = 7;
        console.log(subarraySum(nums,k))
        //0: {start: 0, end: 1}
        //1: {start: 2, end: 2}
        //2: {start: 2, end: 5}
        //3: {start: 5, end: 7}
        //4
    })
    ```

    哈希表
    ```js
    let subarraySum = (nums, k) => {
        let hashmap = [{
            'position': [0],
            'count': 1
        }];
        let sum = 0,count = 0;
        for(let i = 0;i < nums.length;i++){
            sum += nums[i];
            if(!hashmap[sum]){
                hashmap[sum] = {
                    'position': [i],
                    'count': 1
                }
            }
            else{
                hashmap[sum].position.push(i);
                hashmap[sum].count++;
            }
            if(hashmap[sum-k]){
                count += hashmap[sum-k].count;
            }
        }
        console.log(hashmap);
        return count;
    };
    $(()=>{
        let nums = [3,4,7,2,-3,1,4,2];
        let k = 7;
        console.log(subarraySum(nums,k))
        // 0: {position: Array(1), count: 1}
        // 3: {position: Array(1), count: 1}
        // 7: {position: Array(1), count: 1}
        // 13: {position: Array(1), count: 1}
        // 14: {position: Array(2), count: 2}
        // 16: {position: Array(1), count: 1}
        // 18: {position: Array(1), count: 1}
        // 20: {position: Array(1), count: 1}
        // 4
    })
    ```

### 快慢指针
* 算法识别与思想

    判断链表成环等单向追及问题，来源于龟兔赛跑，快的再次追及慢的，表示成环。

1. 判断链表成环
```js
class ListNode{
    constructor(val){
        this.val = val;
        this.next = null;
    }
}
let hasCycle = (head) => {
    if (head == null || head.next == null) {
        return false;
    }
    let slow = head;
    let fast = head.next;
    while (slow != fast) {
        if (fast == null || fast.next == null) {
            return false;
        }
        slow = slow.next;
        fast = fast.next.next;
    }
    return true;
}
$(()=>{
    let head = new ListNode(1);
    let node1 = new ListNode(2);
    let node2 = new ListNode(3);
    let node3 = new ListNode(4);
    let node4 = new ListNode(5);
    head.next = node1;
    node1.next = node2;
    node2.next = node3;
    node3.next = node4;
    //node4.next = node1;
    console.log(hasCycle(head));
});
```

2. 判断链表回文
```js
class ListNode{
    constructor(val){
        this.val = val;
        this.next = null;
    }
}
let isPalindrome = (head) => {
    if(head == null || head.next == null) {
        return true;
    }
    let slow = head, fast = head;
    let current = head, previous = null;
    while(fast != null && fast.next != null) {//翻转一半链表，记录中间位置
        current = slow;//当前位置指向下一位，结束时current会去到中间位置（奇偶情况都满足），指向为反向，即翻转一半链表
        slow = slow.next;//结束时slow会去到中间位置，指向为正向
        fast = fast.next.next;
        current.next = previous;//当前节点的下一节点为已翻转的子链表
        previous = current;//记录当前节点位置
    }
    if(fast != null) {//节点为奇数时，后半段的起始位置，位于中间节点的下一位
        slow = slow.next;
    }
    while(current != null && slow != null) {//从中间开始向外扩散，对比正反链表每一位值是否一样
        if(current.val != slow.val) {
            return false;
        }
        current = current.next;
        slow = slow.next;
    }
    return true;
}
let head = new ListNode(1);
    let a = new ListNode(2);
    let b = new ListNode(3);
    let c = new ListNode(2);
    let d = new ListNode(1);
    head.next = a;
    a.next = b;
    b.next = c;
    c.next = d;
    console.log(isPalindrome(head));
```

### 双指针
* 算法识别与思想

    一个数组中，对不连续数据或单个数据的操作，两指针左右移动，直到满足条件，如相遇、到达边界等。

1. 样例1

    * 来源：[力扣（LeetCode）](https://leetcode-cn.com)

    * 两数之和
    ```txt
    给定一个整数数组 nums 和一个目标值 target，在该数组中找出和为目标值的那 两个 整数，并返回他们的数组下标。
    不能重复利用这个数组中同样的元素。

    示例:

    给定 nums = [2, 7, 11, 15], target = 9

    因为 nums[0] + nums[1] = 2 + 7 = 9
    所以返回 [0, 1]
    ```

    二重指针循环
    ```js
    let twoSum = (nums, target) => {
        let len = nums.length;
        for(let previous = 0;previous < len;previous++){
            for(let next = previous+1;next < len;next++){
                if(nums[previous]+nums[next]==target){
                    return [previous,next];
                }
            }
        }
    }
    $(()=>{
        let nums = [2, 7, 11, 15], target = 9;
        console.log(twoSum(nums, target));
    });
    ```

    哈希表
    ```js
    let twoSum = (nums, target) => {
        let len = nums.length;
        let hashmap = [];
        for(let i = 0;i < len;i++){
            if(hashmap[target-nums[i]] >= 0 && hashmap[target-nums[i]] < len){
                return [hashmap[target-nums[i]],i];
            }
            hashmap[nums[i]] = i;
        }
    }
    $(()=>{
        let nums = [2, 7, 11, 15], target = 9;
        console.log(twoSum(nums, target));
    });
    ```

2. 样例2

    * 来源：[力扣（LeetCode）](https://leetcode-cn.com)

    * 三数之和
    ```txt
    给定一个包含 n 个整数的数组 nums 和一个目标值 target，判断 nums 中是否存在三个元素 a，b，c ，使得 a + b + c = target ？找出所有满足条件且不重复的三元组。

    注意：不可以包含重复的三元组。

    例如, 给定数组 nums = [-1, 0, 1, 2, -1, -4]，target = 0

    满足要求的三元组集合为：
    [
        [-1, 0, 1],
        [-1, -1, 2]
    ]
    ```

    排序+双指针
    ```js
    let threeSum = function(nums,target) {
        let ans = [];
        const len = nums.length;
        if(nums == null || len < 3) return ans;
        nums.sort((a, b) => a - b); // 排序O(nlog2n)
        for (let i = 0; i < len - 2 ; i++) {//O(n2)
            if(i > 0 && nums[i] == nums[i-1]) continue; // 去重
            if(nums[i]+nums[i+1]+nums[i+2] > target) continue;//和尽可能小的数相加，过大则不适合
            if(nums[i]+nums[len-1]+nums[len-2] < target) continue;//和尽可能大的数相加，过小则不适合
            let L = i+1;//下一个数
            let R = len-1;//最后一个数
            while(L < R){
                const sum = nums[i] + nums[L] + nums[R];
                if(sum == target){
                    ans.push([nums[i],nums[L],nums[R]]);
                    while (L<R && nums[L] == nums[L+1]) L++; // 去重
                    while (L<R && nums[R] == nums[R-1]) R--; // 去重
                    L++;
                    R--;
                }
                else if (sum < target) L++;
                else if (sum > target) R--;
            }
        }
        return ans;
    };
    $(()=>{
        let nums = [-1, 0, 1, 2, -1, -4 ,0 ,0];
        let target = 0;
        console.log(threeSum(nums,target));
    });
    ```

* 样例3

    * 来源：[力扣（LeetCode）](https://leetcode-cn.com)

    * 四数之和
    ```txt
    给定一个包含 n 个整数的数组 nums 和一个目标值 target，判断 nums 中是否存在四个元素 a，b，c 和 d ，a + b + c + d = target ？找出所有满足条件且不重复的四元组。

    注意：不可以包含重复的四元组。

    示例：

    给定数组 nums = [1, 0, -1, 0, -2, 2]，和 target = 0。

    满足要求的四元组集合为：
    [
        [-1,  0, 0, 1],
        [-2, -1, 1, 2],
        [-2,  0, 0, 2]
    ]
    ```

    排序+化简+双指针
    ```js
    let fourSum = function(nums,target) {
        let ans = [];
        const len = nums.length;
        if(nums == null || len < 4) return ans;
        nums.sort((a, b) => a - b); // 排序O(nlog2n)
        for (let i = 0; i < len - 3 ; i++) {//O(n)
            if(i > 0 && nums[i] == nums[i-1]) continue; // 去重
            // 先直接和其它三个数可能的最小值相加，还是过大就说明这个i不合适
            if (nums[i]+nums[i+1]+nums[i+2]+nums[i+3] > target) continue;
            // 与其它三个数可能的最大值相加，还是过小就继续下个循环
            if (nums[i]+nums[len-1]+nums[len-2]+nums[len-3] < target)  continue;
            //化简为三数之和
            const target2 = target - nums[i];
            const nums2 = nums.slice(i+1);
            for(let arr of threeSum(nums2,target2)){//O(n2)
                let array = JSON.parse(JSON.stringify(arr));
                array.unshift(nums[i]);
                ans.push(array);
            }
        }
        return ans;
    };
    let threeSum = function(nums,target) {
        let ans = [];
        const len = nums.length;
        if(nums == null || len < 3) return ans;
        //nums.sort((a, b) => a - b); // 已经有序，无需再排
        for (let i = 0; i < len - 2 ; i++) {
            if(i > 0 && nums[i] == nums[i-1]) continue; // 去重
            if(nums[i]+nums[i+1]+nums[i+2] > target) continue;//和尽可能小的数相加，过大则不适合
            if(nums[i]+nums[len-1]+nums[len-2] < target) continue;//和尽可能大的数相加，过小则不适合
            let L = i+1;//下一个数
            let R = len-1;//最后一个数
            while(L < R){
                const sum = nums[i] + nums[L] + nums[R];
                if(sum == target){
                    ans.push([nums[i],nums[L],nums[R]]);
                    while (L<R && nums[L] == nums[L+1]) L++; // 去重
                    while (L<R && nums[R] == nums[R-1]) R--; // 去重
                    L++;
                    R--;
                }
                else if (sum < target) L++;
                else if (sum > target) R--;
            }
        }
        return ans;
    };
    $(()=>{
        let nums = [1, 0, -1, 0, -2, 2];
        let target = 0;
        console.log(fourSum(nums,target));
    });
    ```

### 区间合并
* 算法识别与思想

    产生没有交集的空间

* 样例

    * 来源：[力扣（LeetCode）](https://leetcode-cn.com)

    * 合并区间
    ```txt
    给出一个区间的集合，请合并所有重叠的区间。

    示例 1:

    输入: [[1,3],[2,6],[8,10],[15,18]]
    输出: [[1,6],[8,10],[15,18]]
    解释: 区间 [1,3] 和 [2,6] 重叠, 将它们合并为 [1,6].
    ```

    首数字排序+合并
    ```js
    let merge = function(intervals) {
        let result = [];
        let len = intervals.length;
        if(len == 0){
            return [];
        }
        if(len == 1){
            return intervals;
        }
        intervals.sort((a,b) => a[0] - b[0]);//对第一位进行升序排列
        let i = 0;
        while(i < len){
            let currentLeft = intervals[i][0];
            let currentRight = intervals[i][1];
            //对于[a,b],[c,d]，如果b>=c，则合并为[a,max(b,d)]
            while(i < len - 1 && intervals[i+1][0] <= currentRight){
                i++;
                currentRight = Math.max(intervals[i][1],currentRight);
            }
            result.push([currentLeft,currentRight]);
            i++;
        }
        return result;
    };
    $(()=>{
        let intervals = [[1,3],[2,6],[8,10],[15,18]];
        let intervals2 = [[1,4],[4,5]];
        let intervals3 = [[1,9],[2,5],[19,20],[10,11],[12,20],[0,3],[0,1],[0,2]];
        console.log(merge(intervals3));//[[0, 9],[10, 11],[12, 20]]
    });
    ```

### 原地链表翻转
* 算法识别与思想

    每次摘取当前链表头部，反向连接

1. 单向链表翻转
```js
class ListNode{
    constructor(val){
        this.val = val;
        this.next = null;
    }
}
let reverseLinkList = (head) => {
    let previous = null;
    let current = head;
    while (current != null) {
        let next = current.next;//将下一个节点位置保存起来 2(next)-3-4-5 3(next)-4-5 ...
        current.next = previous;//当前节点的下一节点为已翻转的子链表：null 1-null 2-1-null ...
        previous = current;//记录当前节点位置 1(previous)-null 2(previous)-1-null ...
        current = next;//记录当前位置位于下一节点 2(current)-3-4-5 3(current)-4-5 ...
    }
    return previous;
}
$(()=>{
    let head = new ListNode(1);
    let a = new ListNode(2);
    let b = new ListNode(3);
    let c = new ListNode(4);
    let d = new ListNode(5);
    head.next = a;
    a.next = b;
    b.next = c;
    c.next = d;
    console.log(reverseLinkList(head));
});
```

2. 单向链表每k个元素进行翻转
```js
class ListNode{
    constructor(val){
        this.val = val;
        this.next = null;
    }
}
let reverseKGroup = (head, k) => {
    let dummy = new ListNode(0);
    dummy.next = head;

    let pre = dummy;
    let end = dummy;

    while (end.next != null) {
        for (let i = 0; i < k && end != null; i++) end = end.next;//把end移到每一组的最后一位
        if (end == null) break;
        let start = pre.next;
        let next = end.next;
        end.next = null;//断开end的后续连接
        pre.next = reverseLinkList(start);//设置每组头部指向这组翻转的链表
        start.next = next;//原本组的头部变为尾部，尾部连接上end的下一位
        pre = start;//设置遍历位置到达这组的末尾位置
        end = pre;
    }
    return dummy.next;//返回改变后链表的头部
};
let reverseLinkList = (head) => {
    let previous = null;
    let current = head;
    while (current != null) {
        let next = current.next;//将下一个节点位置保存起来 2(next)-3-4-5 3(next)-4-5 ...
        current.next = previous;//当前节点的下一节点为已翻转的子链表：null 1-null 2-1-null ...
        previous = current;//记录当前节点位置 1(previous)-null 2(previous)-1-null ...
        current = next;//记录当前位置位于下一节点 2(current)-3-4-5 3(current)-4-5 ...
    }
    return previous;
}
$(()=>{
    let head = new ListNode(1);
    let a = new ListNode(2);
    let b = new ListNode(3);
    let c = new ListNode(4);
    let d = new ListNode(5);
    head.next = a;
    a.next = b;
    b.next = c;
    c.next = d;
    let group = 2;
    console.log(reverseKGroup(head,group));
});
```

### 循环排序
* 算法识别与思想

    处理数组中的数值限定在一定区间的问题，寻找丢失的/重复的/最小的元素，使用索引作为哈希键值，脏环境处理的方法。

1. 样例1

    * 来源：[力扣（LeetCode）](https://leetcode-cn.com)

    * 寻找重复数
    ```txt
    给定一个包含 n + 1 个整数的数组 nums，其数字都在 1 到 n 之间（包括 1 和 n），可知至少存在一个重复的整数。假设只有一个重复的整数，找出这个重复的数。

    输入: [1,3,4,2,2]
    输出: 2
    ```

    排序遍历和哈希表统计略过，看循环检测（哈希数组下标-链表成环-快慢指针）
    ```js
    findDuplicate(nums) {
        //[1,3,5,2,2,4]
        //1->3->2(1)->5->4->2(2)
        let slow = nums[0];
        let fast = nums[0];
        do {//找到链表成环的起始位置5
            slow = nums[slow];
            fast = nums[nums[fast]];
        } while (slow != fast);


        let ptr1 = nums[0];
        let ptr2 = slow;
        while (ptr1 != ptr2) {//找到链表成环的重复数
            ptr1 = nums[ptr1];
            ptr2 = nums[ptr2];
        }

        return ptr1;
    }
    ```

2. 样例2

    * 来源：[力扣（LeetCode）](https://leetcode-cn.com)

    * 缺失数字
    ```txt
    给定一个包含 0, 1, 2, ..., n 中 n 个数的序列，找出 0 .. n 中没有出现在序列中的那个数。

    输入: [3,0,1]
    输出: 2
    ```

    排序遍历
    ```js
    let missingNumber = (nums) => {
        nums.sort((a,b)=>a-b);
        for(let i = 0;i < nums.length;i++){
            if(nums[i] != i){
                return i;
            }
        }
        return nums.length;
    }
    ```

    哈希表或桶排序遍历
    ```js
    let missingNumber = (nums) => {
        let arr = new Array(nums.length).fill(0);
        for(let i = 0;i < nums.length;i++){
            arr[nums[i]]++;
        }
        for(let i = 0;i < arr.length;i++){
            if(arr[i]==0){
                return i;
            }
        }
        return nums.length;
    }
    ```

    位运算
    ```js
    let missingNumber = (nums) => {
        let missing = nums.length;
        for (let i = 0; i < nums.length; i++) {
            missing ^= i ^ nums[i];
        }
        return missing;
    }
    ```

    脑筋急转弯：公式求和再减掉所有数
    ```js
    let missingNumber = (nums) => {
        let len = nums.length;
        let total = len * (len + 1) / 2;
        for(let i = 0;i < len;i++){
            total -= nums[i];
        }
        if(total >= 0){
            return total;
        }
        else{
            return len;
        }
    }
    ```
    

3. 样例3

    * 来源：[力扣（LeetCode）](https://leetcode-cn.com)

    * 寻找重复数
    ```txt
    给定一个未排序的整数数组，找出其中没有出现的最小的正整数。

    输入: [1,2,0]
    输出: 3
    输入: [3,4,-1,1]
    输出: 2
    输入: [7,8,9,11,12]
    输出: 1
    ```

    脏环境哈希，正负表示访问情况，绝对值表示原值
    ```js
    let firstMissingPositive = (nums) => {
        let len = nums.length;

        //下面需要用通过变负数的方式看数组下标是否被访问，所以先排除下标为1的情况
        let hasOne = false;
        for (let i = 0; i < len; i++){
            if (nums[i] == 1) {
                hasOne = true;
                break;
            }
        }
        if (!hasOne){
            return 1;
        }
        if (len == 1){
            return 2;
        }

        //把小于1和大于数组长度的数变为1
        for (let i = 0; i < len; i++){
            if ((nums[i] < 1) || (nums[i] > len)){
                nums[i] = 1;
            }
        }

        //某一位的值为负数，表示访问过，并且其绝对值即为原值
        for (let i = 0; i < len; i++) {
            let a = Math.abs(nums[i]);
            if (a == len){//把值为len的数放到0位
                nums[0] = - Math.abs(nums[0]);
            }
            else{//把哈希位置的数变为负数，表示访问过
                nums[a] = - Math.abs(nums[a]);
            }
        }

        //从1号位开始，后面出现的第一个正数，即为缺失的数字
        for (let i = 1; i < len; i++) {
            if (nums[i] > 0){
                return i;
            }
        }
        //1号位后的全被访问过，但0号位未访问过，即为数组长度的数字
        if (nums[0] > 0){
            return len;
        }
        //全部都访问过，即为数组长度的数字+1
        return len + 1;
    };
    ```

### 双堆类型
* 算法识别与思想

    需要把数字分成两队的问题，一边最大堆找最大元素，一边最小堆找最小元素，也可求中位数，使用优先队列（先进最大数先出，如医院急诊室排队）

    ```txt
    设计一个支持以下两种操作的数据结构：

    void addNum(int num) - 从数据流中添加一个整数到数据结构中。
    double findMedian() - 返回目前所有元素的中位数。

    示例：

    addNum(1)
    addNum(2)
    findMedian() -> 1.5
    addNum(3) 
    findMedian() -> 2
    ```

    优先队列（最大堆，最小堆）
    ```js
    class PriorityQueue{
        //-1从小到大，1从大到小
        constructor(compare = 1){
            this.data = [];
            this.compare = compare;
        }
        push(number){
            if(this.compare == 1){
                if(this.data.length == 0){
                    this.data.push(number);
                }
                else{
                    let low = 0;
                    let high = this.data.length - 1;
                    let mid = 0;
                    while(low < high){
                        mid = low + parseInt((high - low) / 2);
                        if(this.data[mid] > number){
                            low = mid + 1;
                        }
                        else{
                            high = mid;
                        }
                    }
                    mid = low + parseInt((high - low) / 2);
                    if(this.data[mid] > number){
                        this.data.splice(mid+1,0,number);
                    }
                    else{
                        this.data.splice(mid,0,number);
                    }
                }
            }
            else{
                if(this.data.length == 0){
                    this.data.push(number);
                }
                else{
                    let low = 0;
                    let high = this.data.length - 1;
                    let mid = 0;
                    while(low < high){
                        mid = low + parseInt((high - low) / 2);
                        if(this.data[mid] > number){
                            high = mid;
                        }
                        else{
                            low = mid + 1;
                        }
                    }
                    mid = low + parseInt((high - low) / 2);
                    if(this.data[mid] < number){
                        this.data.splice(mid+1,0,number);
                    }
                    else{
                        this.data.splice(mid,0,number);
                    }
                }
            }
        }
        pop(){
            let index = this.topIndex();
            if(index != -1){
                let tmp = this.data[index];
                this.data.splice(index,1);
                return tmp;
            }
            else{
                return null;
            }
        }
        topIndex(){
            return this.data.length > 0 ? 0 : -1;
        }
        top(){
            let index = this.topIndex();
            if(index != -1){
                return this.data[index];
            }
            else{
                return null;
            }
        }
        shift(){
            let index = this.bottomIndex();
            if(index != -1){
                let tmp = this.data[index];
                this.data.splice(index,1);
                return tmp;
            }
            else{
                return null;
            }
        }
        bottomIndex(){
            return this.data.length > 0 ? this.data.length - 1 : -1;
        }
        bottom(){
            let index = this.bottomIndex();
            if(index != -1){
                return this.data[index];
            }
            else{
                return null;
            }
        }
        size() {
            return this.data.length;
        }
        toString(){
            return this.data.toString();
        }
    }
    class MedianFinder{
        constructor(){
            this.maxHeap = new PriorityQueue(1);
            this.minHeap = new PriorityQueue(-1);
        }
        addNum(num){
            if (this.maxHeap.size() == 0 || num < this.minHeap.top()) {
                this.maxHeap.push(num);
                if (this.maxHeap.size() > this.minHeap.size() + 1) {
                    this.minHeap.push(this.maxHeap.pop());
                }
            }
            else {
                this.minHeap.push(num);
                if (this.minHeap.size() > this.maxHeap.size()) {
                    this.maxHeap.push(this.minHeap.pop());
                }
                if(this.maxHeap.top() > this.minHeap.bottom()){
                    this.minHeap.push(this.maxHeap.pop());
                    this.maxHeap.push(this.minHeap.pop());
                }
            }
        }
        findMedian(){
            // console.log('----------------------------')
            // console.log('max:',this.maxHeap.toString())
            // console.log('min:',this.minHeap.toString())
            // console.log(this.maxHeap.size(),this.minHeap.size(),this.maxHeap.top(),this.minHeap.top())
            // console.log('----------------------------')
            if (this.maxHeap.size() > this.minHeap.size()) {
                return this.maxHeap.top();
            }
            else{
                return 0.5 * (this.minHeap.top() + this.maxHeap.top());
            }
        }
    };
    $(()=>{
        // var a = new PriorityQueue();
        // a.push(41);
        // console.log(a.toString());
        // a.push(35);
        // console.log(a.toString());
        // a.push(2);
        // console.log(a.toString());
        // a.push(4);
        // console.log(a.toString());
        // a.push(5);
        // console.log(a.toString());
        // console.log(a.pop());
        // console.log(a.toString());
        // console.log(a.shift());
        // console.log(a.toString());
        // -------------------------
        var obj = new MedianFinder();
        obj.addNum(41);
        console.log(obj.findMedian());
        obj.addNum(35);
        console.log(obj.findMedian());
        obj.addNum(62);
        console.log(obj.findMedian());
        obj.addNum(4);
        console.log(obj.findMedian());
        obj.addNum(97);
        console.log(obj.findMedian());
        obj.addNum(108);
        console.log(obj.findMedian());
    })
    
    // ---------------------------
    // Adding number 41
    // MaxHeap lo: [41]
    // MinHeap hi: []
    // Median is 41
    // =======================
    // Adding number 35
    // MaxHeap lo: [35]
    // MinHeap hi: [41]
    // Median is 38
    // =======================
    // Adding number 62
    // MaxHeap lo: [41, 35]
    // MinHeap hi: [62]
    // Median is 41
    // =======================
    // Adding number 4
    // MaxHeap lo: [35, 4]
    // MinHeap hi: [41, 62]
    // Median is 38
    // =======================
    // Adding number 97
    // MaxHeap lo: [41, 35, 4]
    // MinHeap hi: [62, 97]
    // Median is 41
    // =======================
    // Adding number 108
    // MaxHeap lo: [41, 35, 4]
    // MinHeap hi: [62, 97, 108]
    // Median is 51.5
    ```

### 子集问题
* 算法识别与思想

    BFS处理数字的排列组合问题，或使用回溯算法和dfs，实际上排列组合问题可转化为树状结构，先固定第一个条件，下面会出现n-1个条件，固定第二个条件会出现n-2个条件，如此类推。

    ```txt
    给定一个整数数组 nums，返回该数组所有可能的不重复子集（幂集）。
    输入: nums = [1,2,3]
    输出:
    [
      [3],
      [1],
      [2],
      [1,2,3],
      [1,3],
      [2,3],
      [1,2],
      []
    ]
    ```

    BFS
    ```js
    let twoDimensionUnique = (arr) => {
        let set = new Set();
        let res = arr.slice(0);
        for(let i = 0;i < res.length;i++){
            set.add(res[i].toString());
        }
        res = [];
        for(let value of set){
            res.push(Array.from(value.split(',').map(item=>parseInt(item)).filter(x=>!isNaN(x))));
        }
        return res;
    }
    let subsets = (nums) => {
        let res = [[]];
        nums.sort((a,b)=>a-b);
        for(let i = 0;i < nums.length;i++){
            let cnt = res.length;
            for(let j = 0;j < cnt;j++){
                let tmp = JSON.parse(JSON.stringify(res[j]));
                tmp.push(nums[i]);
                res.push(tmp);
            }
        }
        return twoDimensionUnique(res);
    };
    let nums = [1,2,3]
    console.log(subsets(nums))
    ```

    回溯(DFS)
    ```js
    let twoDimensionUnique = (arr) => {
        let set = new Set();
        let res = arr.slice(0);
        for(let i = 0;i < res.length;i++){
            set.add(res[i].toString());
        }
        res = [];
        for(let value of set){
            res.push(Array.from(value.split(',').map(item=>parseInt(item)).filter(x=>!isNaN(x))));
        }
        return res;
    }
    let subsets = (nums) => {
        let res = [];
        nums.sort((a,b)=>a-b);
        traceback(nums, [], 0);

        function traceback(arr, tmp, start) {
            console.log('-------------------')
            console.log('data1',arr,tmp,start)
            res.push(tmp.slice(0));//需要深复制
            console.log('res',res)
            for (let i = start; i < arr.length; i++) {
                if (i > start && nums[i] == nums[i - 1]) {
                    continue;
                }
                tmp.push(nums[i]);
                console.log('data2',arr,tmp,i)
                traceback(arr, tmp, i + 1);
                tmp.pop();
                console.log('data3',arr,tmp,i)
            }
        }
        
        return twoDimensionUnique(res);
        //固定[]为树的根节点，下面有分叉1,2,3，再下面有(12,123,13),(23)
        //遍历树可以得到[ [], [ 1 ], [ 1, 2 ], [ 1, 2, 3 ], [ 1, 3 ], [ 2 ], [ 2, 3 ], [ 3 ] ]
        // -------------------
        // data1 [ 1, 2, 3 ] [] 0
        // res [ [] ]
        // data2 [ 1, 2, 3 ] [ 1 ] 0
        // -------------------
        // data1 [ 1, 2, 3 ] [ 1 ] 1
        // res [ [], [ 1 ] ]
        // data2 [ 1, 2, 3 ] [ 1, 2 ] 1
        // -------------------
        // data1 [ 1, 2, 3 ] [ 1, 2 ] 2
        // res [ [], [ 1 ], [ 1, 2 ] ]
        // data2 [ 1, 2, 3 ] [ 1, 2, 3 ] 2
        // -------------------
        // data1 [ 1, 2, 3 ] [ 1, 2, 3 ] 3
        // res [ [], [ 1 ], [ 1, 2 ], [ 1, 2, 3 ] ]
        // data3 [ 1, 2, 3 ] [ 1, 2 ] 2
        // data3 [ 1, 2, 3 ] [ 1 ] 1
        // data2 [ 1, 2, 3 ] [ 1, 3 ] 2
        // -------------------
        // data1 [ 1, 2, 3 ] [ 1, 3 ] 3
        // res [ [], [ 1 ], [ 1, 2 ], [ 1, 2, 3 ], [ 1, 3 ] ]
        // data3 [ 1, 2, 3 ] [ 1 ] 2
        // data3 [ 1, 2, 3 ] [] 0
        // data2 [ 1, 2, 3 ] [ 2 ] 1
        // -------------------
        // data1 [ 1, 2, 3 ] [ 2 ] 2
        // res [ [], [ 1 ], [ 1, 2 ], [ 1, 2, 3 ], [ 1, 3 ], [ 2 ] ]
        // data2 [ 1, 2, 3 ] [ 2, 3 ] 2
        // -------------------
        // data1 [ 1, 2, 3 ] [ 2, 3 ] 3
        // res [ [], [ 1 ], [ 1, 2 ], [ 1, 2, 3 ], [ 1, 3 ], [ 2 ], [ 2, 3 ] ]
        // data3 [ 1, 2, 3 ] [ 2 ] 2
        // data3 [ 1, 2, 3 ] [] 1
        // data2 [ 1, 2, 3 ] [ 3 ] 2
        // -------------------
        // data1 [ 1, 2, 3 ] [ 3 ] 3
        // res [ [], [ 1 ], [ 1, 2 ], [ 1, 2, 3 ], [ 1, 3 ], [ 2 ], [ 2, 3 ], [ 3 ] ]
        // data3 [ 1, 2, 3 ] [] 2
        // [ [], [ 1 ], [ 1, 2 ], [ 1, 2, 3 ], [ 1, 3 ], [ 2 ], [ 2, 3 ], [ 3 ] ]
    };
    let nums = [1,2,3]
    console.log(subsets(nums))
    ```

### 二分变种
* 算法识别与思想

    对于排序好的数组、链表、矩阵，进行二分搜索、插入

    ```js
    let binarySearch1 = (nums, key) => {//查找中间与key相等的元素
        let left = 0, right = nums.length - 1;
        while (left <= right) {
            let m = left + parseInt((right - left) / 2);
            if (nums[m] == key) {
                return m;
            } else if (nums[m] > key) {
                right = m - 1;
            } else {
                left = m + 1;
            }
        }
        return -1;
    }
    let binarySearch2 = (nums, key) => {//查找第一个与key相等的元素
        let left = 0, right = nums.length - 1;
        while (left < right) {
            let m = left + parseInt((right - left) / 2);
            if (nums[m] < key) {
                left = m + 1;
            } else {
                right = m;
            }
        }
        if(nums[left] != key){
            return -1;
        }
        return left;
    }
    let binarySearch3 = (nums, key) => {//查找最后一个与key相等的元素
        let left = 0, right = nums.length - 1;
        while (left < right) {
            let m = left + parseInt((right - left) / 2);
            if (m == left) {
                break;
            }
            if (nums[m] <= key) {
                left = m;
            } else {
                right = m - 1;
            }
        }
        if(nums[right] != key){
            return -1;
        }
        return right;
    }
    let binarySearch4 = (nums, key) => {//查找第一个大于key的元素(上确界)
        let left = 0, right = nums.length - 1;
        while (left < right) {
            let m = left + parseInt((right - left) / 2);
            if (m == left) {
                break;
            }
            if (nums[m] <= key) {
                left = m;
            } else {
                right = m;
            }
        }
        if(nums[right] <= key){
            return -1;
        }
        return right;
    }
    let binarySearch5 = (nums, key) => {//查找最后一个小于key的元素(下确界)
        let left = 0, right = nums.length - 1;
        while (left < right) {
            let m = left + parseInt((right - left) / 2);
            if (m == left) {
                break;
            }
            if (nums[m] < key) {
                left = m;
            } else {
                right = m - 1;
            }
        }
        if(nums[right] >= key){
            return -1;
        }
        return right;
    }
    let nums = [1,2,2,2,2,2,2,3,4,5];
    let key = 2;
    console.log(binarySearch1(nums,key))// 4
    console.log(binarySearch2(nums,key))// 1
    console.log(binarySearch3(nums,key))// 6
    console.log(binarySearch4(nums,key))// 7
    console.log(binarySearch5(nums,key))// 0
    ```

### 前K个系列
* 算法识别与思想

    求解最大/最小/最频繁的K个元素，统计排序

    ```txt
    给一非空的单词列表，返回前 k 个出现次数最多的单词。

    返回的答案应该按单词出现频率由高到低排序。如果不同的单词有相同出现频率，按字母顺序排序。

    输入: ["i", "love", "leetcode", "i", "love", "coding"], k = 2
    输出: ["i", "love"]
    解析: "i" 和 "love" 为出现次数最多的两个单词，均为2次。
    注意，按字母顺序 "i" 在 "love" 之前。。
    ```

    字典统计+二重排序
    ```js
    let dictionary = new Array();
    let topKFrequent = (words, k) => {
        //let dictionary = new Array();
        for(let i = 0;i < words.length;i++){
            if(!dictionary[words[i]]){
                dictionary[words[i]] = 1;
            }
            else{
                dictionary[words[i]]++;
            }
        }
        //console.log(dictionary)
        let result = Object.keys(dictionary).sort((a,b)=>{
            if(dictionary[a] == dictionary[b]){
                if(a > b){
                    return 1;
                }
                else{
                    return -1;
                }
            }
            return dictionary[b] - dictionary[a];
        });
        for(let value of result){
            console.log(value,dictionary[value])
        }
        return result.slice(0,k);
    };
    let words = ["rmrypv","zgsedk","jlmetsplg","wnfbo","hnnftqf","bxlr","sviavwoxss","jdbgvc","zddeno","rxgw","hnnftqf","hdmvplne","rlmdt","jlmetsplg","ous","rmrypv","fwxulnpit","dmhuq","rxgw","ledleb","bxlr","indbvb","ckqqibnx","cub","ijww","ehd","hfhlfqzkcn","sviavwoxss","rxgw","bxjxpfp","mgqj","oic","ptk","fwxulnpit","ijww","sviavwoxss","bgfvfa","zfkgsudxq","alkq","dmhuq","zddeno","rxgw","zgsedk","amarxpg","bgfvfa","wnfbo","sviavwoxss","sviavwoxss","alkq","nmclxk","zgsedk","bwowfvira","ous","bxlr","zddeno","rxgw","ous","wnfbo","rmrypv","sviavwoxss","ehd","zgsedk","jlmetsplg","abxvhyehv","ledleb","wnfbo","bgfvfa","bwowfvira","amarxpg","wnfbo","bwowfvira","dmhuq","ouy","bxlr","rxgw","oic","hnnftqf","ledleb","rlmdt","oldainprua","ous","ckqqibnx","dmhuq","hnnftqf","oic","jlmetsplg","ppn","amarxpg","jlgfgwb","bxlr","bwowfvira","hdmvplne","oic","ledleb","bwowfvira","oic","ptk","dmhuq","abxvhyehv","ckqqibnx","indbvb","ypzfk","rmrypv","bxjxpfp","amarxpg","dmhuq","sviavwoxss","bwowfvira","zfkgsudxq","wnfbo","rxgw","jxkvrmajri","cub","abxvhyehv","bwowfvira","indbvb","ehd","ckqqibnx","oic","ptk","hnnftqf","ouy","oic","zgsedk","abxvhyehv","ypzfk","ptk","sviavwoxss","rmrypv","oic","ous","abxvhyehv","hnnftqf","hfhlfqzkcn","ledleb","cub","ppn","zddeno","indbvb","oic","jlmetsplg","ouy","bwowfvira","bklij","gucayxp","zfkgsudxq","hfhlfqzkcn","zddeno","ledleb","zfkgsudxq","hnnftqf","bgfvfa","jlmetsplg","indbvb","ehd","wnfbo","hnnftqf","rlmdt","bxlr","indbvb","jdbgvc","jlmetsplg","cub","jlgfgwb","ypzfk","indbvb","dmhuq","jlmetsplg","zgsedk","rmrypv","cub","rxgw","ledleb","rxgw","sviavwoxss","ckqqibnx","hdmvplne","dmhuq","wnfbo","jlmetsplg","bxlr","zfkgsudxq","bxjxpfp","ledleb","indbvb","ckqqibnx","ous","ckqqibnx","cub","ous","abxvhyehv","bxlr","hfhlfqzkcn","hfhlfqzkcn","oic","ten","amarxpg","indbvb","cub","alkq","alkq","sviavwoxss","indbvb","bwowfvira","ledleb"];
    let k = 41;
    let arr = topKFrequent(words,k)
    console.log(arr);
    ```

### K路归并
* 算法识别与思想

    处理k个排好序的数据问题

### 拓扑排序
* 算法识别与思想

    寻找一种线性的顺序，这些元素之间具有依懒性，使用有向无环图