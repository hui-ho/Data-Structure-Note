# 二分查找的变形版本（下）

二分查找的第三个变形版本：**在给定排序序列中查找第一个大于等于给定值的元素**。思路还是和之前两个变形版本类似，当 $mid 已经是最左边的元素，或者 $mid 的前一个元素值小于给定查询值，则 $mid 对应元素即为满足条件的元素，否则继续往前查找。

```php
<?php

/**
 * 二分查找变形版：查找第一个大于等于给定值的元素（数组中包含重复数据）
 */
function binary_search($nums, $num)
{
    if (count($nums) <= 1) {
        return 0;
    }
    return binary_search_internal($nums, $num, 0, count($nums) - 1);
}

function binary_search_internal($nums, $num, $low, $high)
{
    if ($low > $high) {
        return -1;
    }

    $mid = floor(($low + $high) / 2);
    if ($num <= $nums[$mid]) {
        if ($mid == 0 || $nums[$mid - 1] < $num) {
            return $mid;
        } else {
            return binary_search_internal($nums, $num, $low, $mid - 1);
        }
    } elseif ($num > $nums[$mid]) {
        return binary_search_internal($nums, $num, $mid + 1, $high);
    }
}

$nums = [1, 2, 3, 3, 4, 5, 6];
$index = binary_search($nums, 3);
print $index;
```

最后要讨论的一个二分查找的变形版本：**在给定序列中查找最后一个小于等于给定值的元素**。这次的判断节点变成了 $nums[$mid] <= $num，其中 $num 是待查找的元素值，当 $mid 已经是最后一个元素索引，或者 $mid 的后一个元素值大于 $num 则当前 $mid 对应元素就是要查找的元素，否则要继续往后查找。

```php
<?php
    
/**
 * 二分查找变形版：查找最后一个小于等于给定值的元素（数组中包含重复数据）
 */
function binary_search($nums, $num)
{
    if (count($nums) <= 1) {
        return 0;
    }
    return binary_search_internal($nums, $num, 0, count($nums) - 1);
}

function binary_search_internal($nums, $num, $low, $high)
{
    if ($low > $high) {
        return -1;
    }

    $mid = floor(($low + $high) / 2);
    if ($num >= $nums[$mid]) {
        if ($mid == count($nums) - 1 || $nums[$mid + 1] > $num) {
            return $mid;
        } else {
            return binary_search_internal($nums, $num, $mid + 1, $high);
        }
    } elseif ($num < $nums[$mid]) {
        return binary_search_internal($nums, $num, $low, $mid - 1);
    }
}

$nums = [1, 2, 3, 3, 4, 5, 6];
$index = binary_search($nums, 3);
print $index;
```