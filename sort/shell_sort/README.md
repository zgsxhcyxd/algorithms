# 希尔排序

## 排序过程

希尔排序是插入排序的优化版本，同属于**插入类排序**。优化：插入排序只能比较相邻元素，大距离移动元素开销大，比如 `[1, 2, 3, 4, 0]` 中把 0 挪到第一位就需要交换四次。

希尔排序是将跨步的分组进行组内排序，使数组在大体上基本有序（小元素在前，大元素在后），当步长减少到 1 时无序元素将极少。“步长” 是希尔排序的特性。

```shell
shell_sort $ go run main.go
[UNSORTED]:  [4 1 3 0 2]
[DEBUG step]:  2
[DEBUG]:  [3 1 4 0 2]	# 4 3 -> 3 4
[DEBUG]:  [3 0 4 1 2]	# 1 0 -> 0 1
[DEBUG]:  [2 0 3 1 4]	# 4 2 -> 2 4	# 2 3 4 与 0 1 均有序
[DEBUG step]:  1
[DEBUG]:  [0 2 3 1 4]	# 2 0 -> 0 2
[DEBUG]:  [0 2 3 1 4]	
[DEBUG]:  [0 1 2 3 4]	# 2 3 1 -> 1 2 3
[DEBUG]:  [0 1 2 3 4]	# step == 0 排序完毕
[SORTED]:  [0 1 2 3 4]
```



## 排序效果

![3](http://p7f8yck57.bkt.clouddn.com/2018-06-13-150820.gif)



## 复杂度

### 时间复杂度

希尔排序的时间复杂度与步长的选取有关。如果步长为 1 直接进行排序，此时希尔排序与插入排序无异，复杂度为 **O(N^2)**。最好的步长是 Sedgewick 提出的，参考讨论：[fastest-gap-sequence-for-shell-sort](https://stackoverflow.com/questions/2539545/fastest-gap-sequence-for-shell-sort)

一般来说时间复杂度为：**O(Nlog2N)** 级别

### 空间复杂度

无需过多辅助空间，空间复杂度为 **O(1)**

### 稳定性

相同的元素如果分到不同分组，则相对顺序可能会变，是不稳定的。如

```shell
[5, 3, 3, 7]	# 选取步长为 4 / 2 = 2
[3,  , 5,  ]	# 5 3 -> 3 5
[ , 3,  , 7]	# 3 7 -> 3 7 
```

排序完毕，可看到两个 3  的顺序发生了变化。



## 使用场景

若初始步长不是 1，希尔排序就比插入排序快，选取适当步长效率更高。和插入排序一样，适用于小数据量、或基本有序的大数据量集合，实际上因为效率常常会使用快排代替希尔排序。