# 插入排序

插入排序的原理是：我们将数组中的数据分为两个区间，已排序区间和未排序区间。初始已排序区间只有一个元素，就是数组的第一个元素。插入算法的核心思想是取未排序区间中的元素，在已排序区间中找到合适的插入位置将其插入，并保证已排序区间数据一直有序。重复这个过程，直到未排序区间中元素为空，算法结束。如下图所示：

![插入排序](img/insertion_sort.png)

插入排序也比较简单，实现代码如下：

```php
<?php
    
/**
 * 插入排序实现函数（PHP）
 * @param $nums
 * @return mixed
 */
function insertion_sort($nums) {
    if (count($nums) <= 1) {
        return $nums;
    }

    for ($i = 0; $i < count($nums); $i++) {
        $value = $nums[$i];
        $j = $i - 1;
        for (; $j >= 0; $j--) {
            if ($nums[$j] > $value) {
                $nums[$j+1] = $nums[$j];
            } else {
                break;
            }
        }
        $nums[$j+1] = $value;
    }

    return $nums;
}

$nums = [4, 5, 6, 3, 2, 1];
$nums = insertion_sort($nums);
print_r($nums);
```

插入排序需要两个嵌套的循环，时间复杂度是O(n^2)；没有额外的存储空间，是原地排序算法；不涉及相等元素位置交换，是稳定的排序算法。

插入排序的时间复杂度和冒泡排序一样，也不是很理想，但是插入排序不涉及数据交换，从更细粒度来区分，性能要略优于冒泡排序。