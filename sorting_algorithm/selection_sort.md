# 选择排序

选择排序算法的实现思路有点类似插入排序，也分已排序区间和未排序区间。但是选择排序每次会从未排序区间中找到最小的元素，将其放到已排序区间的末尾。图示如下：

![选择排序](img/selection_sort.jpeg)

选择排序的PHP实现代码如下：

```php
<?php

/**
 * 选择排序算法实现
 */
function selection_sort($nums)
{
    if (count($nums) <= 1) {
        return $nums;
    }

    for ($i = 0; $i < count($nums); $i++) {
        $min= $i;
        for ($j = $i + 1; $j < count($nums); $j++) {
            if ($nums[$j] < $nums[$min]) {
                $min = $j;
            }
        }
        if ($min != $i) {
            $temp = $nums[$i];
            $nums[$i] = $nums[$min];
            $nums[$min] = $temp;
        }
    }

    return $nums;
}

$nums = [4, 5, 6, 3, 2, 1];
$nums = selection_sort($nums);
print_r($nums);
```

很显然，选择排序的时间复杂度也是 O(n^2)；由于不涉及额外的存储空间，所以是原地排序；由于涉及非相邻元素的位置交换，所以是不稳定的排序算法。

综合比较前面介绍的三个排序算法，时间复杂度都是一样的，也都是原地排序，但是选择排序是不稳定的排序算法，此外，插入排序和冒泡排序相比较，我们在将插入排序的时候讲到，插入排序只需要一条语句，而冒泡排序需要三条，在同等条件下，或者数据量很大的情况下，插入排序性能是要由于冒泡排序的，所以综合比较下来，三者的优先级是插入排序 > 冒泡排序 >> 选择排序。但是三者的时间复杂度都是 O(n^2)，数据量很大的情况下性能表现并不是很理想。