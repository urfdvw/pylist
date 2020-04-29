# 30-Day LeetCoding Challenge

## Week 1
- [136. Single Number](leet136.md)
    - `set()`基础。秒杀，就是记得把中文输入法关了。
- [202. Happy Number](leet202.md)
    - `set()`基础
    - 调用函数的时候记得不要忘了`self.`
    - `while`的开头和收尾， *目前好像没什么好的办法* 
- [53. Maximum Subarray](leet53.md)
    - cumsum 的应用
    - 秒杀，因为做过原题
    - 计算max和min的时候，注意要不要包括当前点
        - 如果包括就先update再计算
        - 如果不包括就先计算再update
- [283. Move Zeroes](leet283.md)
    - 同向快慢读写双指针
    - 虽然做过，不过还是死在了**读题**上
        - 题目要求保持先后顺序，结果我给反了过来
    - 其他挺简单的，仔细读题之后就秒杀了
- [122. Best Time to Buy and Sell Stock II](leet122.md)
    - simulation
    - 秒杀，好像都没什么可说的
- [49. Group Anagrams](leet49.md)
    - `dict()`的应用
    - 注意
        - string sort过之后是list
        - list不能作为dict的key
- [Counting Elements](leetw1ch7.md)
    - `set`基础运用
    - 没有漏出破绽，秒杀

## Week 2
- [876. Middle of the Linked List](leet876.md)
    - 倍速双指针
        - 注意快指针每循环移动一次，慢指针多个循环移动一次，这样不会出现越界太多的情况
        - 慢速指针在何时跟进可以用小的test case来特殊值法确定。用长度是 2 和 3 的linked list来尝试。
- [844. Backspace String Compare](leet844.md)
    - 不是很顺利的一题
    - 这个题有两个思路
        - simulation，模拟按键把字符串生成出来，然后比较
        - pointer，不生成出来，而是挪动指针逐个比较
        - 很明显时间复杂度一样都是O(n)，然而指针更省空间。但是写指针的时候我没写出来。
    - 本题目犯的常规错误
        - 引用函数忘了加 `self.`
    - 关于指针的教训
        - 不要把两个指针的循环条件同时放入，while循环的条件，否则会非常麻烦。而是要为两个指针单独写while循环
        - while循环的条件要是搞不清楚的话，就直接写`while True:`然后中间break，如果发现条件比较清楚的时候再放回正确的位置，如果不能的话就不改了。
            - 死循环不是一个好的style，实在不行可以换成for一个大数
        - 一个循环只做一件事，这个非常重要。做完就要continue或者break或者return。否则会糊粥。
            - **Style**: 多个if重叠的时候，可以在if之后加入注释，注明如果可以运行到注释这行，需要达到的条件。
- [155. Min Stack](leet155.md)
    - `stack`的进阶用法
    - 这个题因为有minimum所以让我想到了heap。而heap在pop的时候会非常之复杂。虽然trash list的策略确实可以AC，但是其实既浪费时间又浪费空间。
    - 常规错误
        - 不要把attribute和method起同一个名字
        - 用`a[0]`作为peek之前一定先判断list是否为空
        - 不要在某些语句的末尾加入无意义的冒号
            - 只要注意缩紧这个其实很容易避免
- [543. Diameter of Binary Tree](leet543.md)
    - DC on binary tree
    - 二叉树上的分治在检查的时候一定注意：
        - combine的时候有没有充分利用左右获得的答案
- [1046. Last Stone Weight](leet1046.md)
    - heap
    - heapify has no out put, heap operations are inline
    - max heap 的 负号位置
        - ```python
          h = [-s for s in stones]
          heapify(h)
          ```
        - push: `heappush(h, -x)`
        - pop:  `x = -heappop(h)`
        - peek: `-h[0]`
- [525. Contiguous Array](leet525.md)
    - cumsum 的应用
    - 注意 max 和 min 擂台的初始化
        - 根据题目要求，不一定要初始化到正负无穷
        - 比如这里 max 初始化到 0 就可以
- [Perform String Shifts](leetw2ch7.md)
    - circular shift
    - 看题，左右都能看反我也是服了

## week 3
- [238. Product of Array Except Self](leet238.md)
    - 双向 cumsum ，这里是product，不过和sum差别不大
    - 循环还是分开写， 可以更清楚一些
