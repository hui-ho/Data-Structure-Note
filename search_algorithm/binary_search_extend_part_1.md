# 二分查找的变形版本（上）

符合标准的二分查找条件的序列一般是比较理想的情况，如果要查找的元素在序列中有多个怎么办？所以二分查找的第一个常见的变形版本，就是**在一个给定排序序列中查找第一个等于给定值的元素**。

```php
<?php

function binary_search($nums, $num)
{
    return binary_search_internal($nums, $num, 0, count($nums) - 1);
}

function binary_search_internal($nums, $num, $low, $high)
{
    if ($low > $high) {
        return -1;
    }

    $mid = floor(($low + $high) / 2);
    if ($num > $nums[$mid]) {
        return binary_search_internal($nums, $num, $mid + 1, $high);
    } elseif ($num < $nums[$mid]) {
        return binary_search_internal($nums, $num, $low, $mid - 1);
    } else {
        if ($mid == 0 || $nums[$mid-1] != $num) {
            return $mid;
        } else {
            return binary_search_internal($nums, $num, $low, $mid - 1);
        }
    }
}

$nums = [1, 2, 3, 4, 5, 6];
$index = binary_search($nums, 5);
print $index;
```

既然有第一个等于给定值的查询，自然就有最后一个等于给定值的查询，这就是二分查找的第二个变形版本：**在给定已排序序列中查找最后一个等于给定值的元素**。实现逻辑和上面类似，只需要改动 $num == $nums[$mid] 时的处理逻辑，只是这时的条件变成了 $mid 位置到了序列的最右边，不能再往后了，或者索引大于 $mid 的后一个元素值不等于带查找元素，才返回 $mid，否则，还要继续往后找。

```php
function binary_search_internal($nums, $num, $low, $high)
{
    if ($low > $high) {
        return -1;
    }

    $mid = floor(($low + $high) / 2);
    if ($num < $nums[$mid]) {
        return binary_search_internal($nums, $num, $low, $mid - 1);
    } elseif ($num > $nums[$mid]) {
        return binary_search_internal($nums, $num, $mid + 1, $high);
    } else {
        if ($mid == count($nums) - 1 || $nums[$mid + 1] != $num) {
            return $mid;
        } else {
            return binary_search_internal($nums, $num, $mid + 1, $high);
        }
    }
}
```
