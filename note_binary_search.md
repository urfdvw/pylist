# Binary search

## 模板和要点
- Find target index: find any/first/last target in the list
    -   ```python
        # corner cases
        # init boundaries
        while(low + 1 < up):
            # while up and low are not next to each other
            mid = int(low + (up - low)/2)
            if(nums[mid] == target):
            elif(nums[mid] > target):
            else:  # (nums[mid] < target)
        # check wether up or low
        # if not found
        ```
    - 要點
        - 相邻即退出
            - while(low + 1 < up):
        - mid = (low - up)/2 + low
        - 比较的三种情况==, >, <
            - 全部都是 = mid
            - 情况 ==
                - 如果求any position，可以返回
                - 如果求first，up = min
                - 剩下一种你猜
            - 情况 target < list[mid]
                - up = mid
            - 剩下一种你猜
        - 判断到底返回up还是low
            - 顺序可能有讲究

- Binary search by condition: find any/first/last element in list that
    - 要點：
        - list的前后两半分别满足与不满足**某个条件**
        - 找到满足和不满足**分界**的地方
        - 判断只有两项，及满足or不满足
        - 返回时候不用check，因为up和low的propertie不变，所以可以知道该返回哪个。
        - 注意要返回的是index还是element，都有可能

- 缩小有解范围的大小
    - 要點：
        - 要寻找***any***解的位置
        - 可以通过两界的性质判区间内是否有解
        
- 按结果搜索
    - 要點
        - 题目要求的函数是一个复杂过程，let's call it backward process
        - 但是其逆过程是一个简单过程，let's call it forward process
        - 题目要求的函数输入输出都是scaler，且是一个单调函数。
        - 目前猜测，这类问题都可以转换为binary search by condition问题
        
## Examples
- Find target index: find any/first/last target in the list
    - [457. Classical Binary Search](lint457.md)
    - [14. First Position of Target](lint14.md),
    - [458. Last Position of Target](lint458.md),
    - [447. Search in a Big Sorted Array](lint447.md)
    - [460. Find K Closest Elements](lint460.md)
- Binary search by condition: find any/first/last element in list that
    - [74. First Bad Version](lint74.md),
    - [159. Find Minimum in Rotated Sorted Array](lint159.md)
    - [585. Maximum Number in Mountain Sequence](lint585.md)
    - [4. Ugly Number II](lint4.md)
    - [1008. Construct Binary Search Tree from Preorder Traversal](leet1008.md)
    - [Leftmost Column with at Least a One](leetw3.md)
- 缩小有解范围的大小
    - [75. Find Peak Element](lint75.md)
    - [62. Search in Rotated Sorted Array](lint62.md)
    - [33. Search in Rotated Sorted Array](leet33.md)
- 按结果搜索
    - [141. Sqrt(x)](lint141.md),
    - [183. Wood Cut](lint183.md),
    - [437. Copy Books](lint437.md)

## MISC
- 如果明确要求olog(n)，一定是二分法
- 除了明显是递归的题，能不递归就不递归
- ["bisect" package examples](misc/bisect.md)