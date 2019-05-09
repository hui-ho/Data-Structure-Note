# 特殊的线性结构：栈

栈又叫堆栈，是限定只能在一端进行插入和删除操作的线性表，并且满足后进先出（LIFO）的特点。我们把允许插入和删除的一端叫做栈顶，另一个端叫做栈底，不含任何数据的栈叫做空栈。

栈支持通过数组/链表实现，通过数组实现的通常叫做顺序栈，通过链表实现的叫做链栈。下面简单演示下如何在 PHP 中通过数组实现一个简单的顺序栈：

```php
<?php

/**
 * 通过 PHP 数组实现简单的顺序栈
 */
class SimpleStack {

    private $_stack = [];
    private $_size = 0;

    public function __construct($size = 10)
    {
        $this->_size = $size;
    }

    // 获取栈顶元素
    public function pop()
    {
        // 空栈
        if (count($this->_stack) == 0) {
            return false;
        }
        return array_pop($this->_stack);
    }

    // 推送元素到栈顶
    public function push($value)
    {
        // 满栈
        if (count($this->_stack) == $this->_size) {
            return false;
        }
        array_push($this->_stack, $value);
        return true;
    }

    public function isEmpty()
    {
        // 是否是空栈
        return current($this->_stack) == false;
    }

    public function size()
    {
        return count($this->_size);
    }
}

$stack = new SimpleStack(15);
var_dump($stack->isEmpty());  # true
$stack->push(111);
$stack->push('梁非凡');
var_dump($stack->pop());  # 梁非凡
var_dump($stack->size());  # 1
```

堆栈在日常开发和软件使用中，应用非常广泛，比如我们的浏览器前进、倒退功能，编辑器/IDE 中的撤销、取消撤销功能，程序代码中的函数调用、递归、四则运算等等，都是基于堆栈这种数据结构来实现的，就连著名的 stackoverflow 网站也是取「栈溢出」，需要求教之意。
