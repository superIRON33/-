首先是对于排序以及算法得一个相关概述，如下：
1. 稳定排序：如果 a 原本在 b 的前面，且 a == b，排序之后 a 仍然在 b 的前面，则为稳定排序。
2. 非稳定排序：如果 a 原本在 b 的前面，且 a == b，排序之后 a 可能不在 b 的前面，则为非稳定排序。
3. 原地排序：原地排序就是指在排序过程中不申请多余的存储空间，只利用原来存储待排数据的存储空间进行比较和交换的数据排序。
4. 非原地排序：需要利用额外的数组来辅助排序。
5. 时间复杂度：一个算法执行所消耗的时间。
6. 空间复杂度：运行完一个算法所需的内存大小。
7. 下面开始我对于排序的归纳与总结：
# 选择排序
排序过程：
1. 首先，找到数组中最小的元素，然后将它和数组的第一个元素交换位置(如果第一个元素就是最小元素那么它就和自己交换)。
2. 其次，在剩下的元素中找到最小的元素，将它与数组的第二个元素交换位置。
3. 如此往复，直到将整个数组排序。这种方法就叫选择排序。
- 时间复杂度为**O(n2)**，空间复杂度为**O(1)**
- 属于**原地排序**
- 属于**非稳定排序**
# 冒泡排序
排序过程
1. 把第一个元素与第二个元素比较，如果第一个比第二个大，则交换他们的位置。接着继续比较第二个与第三个元素，如果第二个比第三个大，则交换他们的位置….
2. 我们对每一对相邻元素作同样的工作，从开始第一对到结尾的最后一对，这样一趟比较交换下来之后，排在最右的元素就会是最大的数。
3. 除去最右的元素，我们对剩余的元素做同样的工作，如此重复下去，直到排序完成。
- 时间复杂度为**O(n2)**，空间复杂度为**O(1)**
- 属于**原地排序**
- 属于**稳定排序**
# 插入排序
排序过程：
1. 从数组第2个元素开始抽取元素。
2. 把它与左边第一个元素比较，如果左边第一个元素大于它，就继续与左边下一个元素比较下去，直到遇到小于它的元素，然后插到这个元素的右边。
3. 继续选取第3，4，….n个元素,重复步骤 2 ，选择适当的位置插入，知道第n个元素，完成排序。
- 算法时间复杂度为**O(n2)**，空间复杂度为**O(1)**
- 属于**原地排序**
- 属于**稳定排序**
# 希尔排序
排序思想：希尔排序可以说是**插入排序的一种变种**。无论是插入排序还是冒泡排序，如果数组的最大值刚好是在第一位，要将它挪到正确的位置就需要 n - 1 次移动。当原数组的一个元素如果距离它正确的位置很远的话，需要与相邻元素交换多次才能到达正确的位置，这样效率较低。希尔排序就是插入排序排序的一种简单改进，交换不相邻的元素以对数组的局部进行排序，以此来提升效率。
排序过程：
1. 先让数组中任意间隔为 h 的元素有序，刚开始 h 的大小可以是 h = n / 2
2. 接着让 h = n / 4，让 h 一直缩小，相当于不断增大步长，当 h = 1 时，也就是此时数组中任意间隔为1的元素有序，此时的数组就是有序的了。
- 时间复杂度为**O(nlogn)**，空间复杂度：**O(1)**
- 属于非稳定排序
- 属于原地排序
# 归并排序
排序思想：将一个大的无序数组有序，我们可以把大的数组分成两个，然后对这两个数组分别进行排序，之后在把这两个数组合并成一个有序的数组。由于两个小的数组都是有序的，所以在合并的时候是很快的。

注意：在一个归并排序中，可以将总的数组中n个元素分成**logn个层次**，每个层次的合并保持在**O(n)**的复杂度，那么最后的算法时间复杂度为**O(nlogn)**

排序过程：
1. 通过递归的方式将大的数组一直分割，直到数组的大小为 1，此时只有一个元素，那么该数组就是有序的了
2. 再把两个数组大小为1的合并成一个大小为2的，再把两个大小为2的合并成4的 …
3. 直到全部小的数组合并起来。
- 时间复杂度为**O(nlogn)**，空间复杂度为**O(n)**
- 属于**稳定排序**
- 属于**非原地排序**
可以分别通过递归或者迭代实现归并排序，代码中有MergeSort和MergeSort2
# 快速排序
排序思路：
首先我们来看总体的排序过程
1. 比如说将一个数组中的第一个元素作为主元，之后，采用双指针的思想，让 i = left + 1（此处最外层left即为0），让 j = right
2. 之后 i 和 j 向数组中间进行移动，如果 arr[i] >= 主元，那么i停止，同理如果 arr[j] <= 主元，那么 j 停止，此时将 arr[i] 与 arr[j] 进行交换，然后继续这样的过程直到 **i >= j**
3. 这时，除了主元，在 arr[j] 之前的元素都将小于等于主元，在 arr[j] 之后的元素都将大于等于主元
4. 此时将 arr[j] 和主元进行交换，就能看到满意的情况，主元左边元素均小于主元，右边元素都大于主元
5. 这个时候就可以采用**分治**的思想，对于主元的左右两部分数组再**分别递归**地进行上述过程
6. 当数组元素只有一个或者零个时，那么数组整体就是有序的了。
**注意**:
1. 快排中最核心的部分就是划分的partition过程，而且是需要借助外部空间的
2. 快速排序中partition时主元的选取可以是任意的，不一定必须是第一个元素为主元，可以选取第一个或者最后一个，也可以利用random随机生成介于0到数组长度之间的一个整数作为主元索引，将对应元素作为主元

- 时间复杂度为**O(nlogn)**，空间复杂度为**O(logn)**
- 属于非稳定排序
- 属于原地排序

补充：
1. 当选定第一个元素为主元时，当数组基本有序时，每次只会对主元一边的数组进行分割，这样，分割次数会边多，而算法的时间复杂度会退化为**O(n2)**，但是当对主元进行随机选取的时候，就不一样了，它的时间复杂度的期望值就是**O(logn)**了，但是注意，只是期望，就是说快速排序退化成**O(n2)**复杂度的概率就很低了，上面的代码在这方面也可以进行优化
2. 当一个数组中，有很多重复元素，partition操作都容易将数组划分为极度不平衡的两部分，即使我们的主元选择得很合适，这时候复杂度也会退化为**O(n2)**的复杂度，上面的是已经进行优化过的版本
3. 当然，提到了上面的问题，对于大量重复元素存在于数组中的情况，还可以进行三路快速排序，将整个数组划分为**小于主元**，**等于主元**，**大于主元**三部分区域

# 堆排序
堆排序：堆排序就是把堆顶的元素与最后一个元素交换，交换之后破坏了堆的特性，我们再把堆中剩余的元素再次构成一个大顶堆，然后再把堆顶元素与最后第二个元素交换….如此往复下去，等到剩余的元素只有一个的时候，此时的数组就是有序的了。
- 堆排序的时间复杂度为**O(nlogn)**，空间复杂度为O(1)
- 属于非稳定排序
- 属于原地排序