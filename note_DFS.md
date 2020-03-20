# 用DFS找到全部答案的题目

## Divide and Conquer 的思路
- `dc` function should have the same parameter defination as the original problem
- `s` is a parameter defining the sacle of the problem. Different problem should be defined by different length of string `s`
- main logic is to combine the answers gathered from different branches
- recursion exit is defined when there are not enough length to make branches
- recursion exit returns are hard coded
```python
def question(self, s):
    return self.dc(s)
    # return self.dc(s)[0] # if have multiple returns

def dc(self, s):
    # if catch the end
    if is_end(s):
        return hard_code_answer

    # get answer of all branches
    ans_list = []
    for b in branch:
        ans_list.append(self.dc(s - b))

    # combine ans lists
    ans = combine(ans_list)

    return ans #, ans1, ans2 ...
```

## Traverse 的思路
- 尝试所有的答案，每次尝试一个。
- 3 basic parameters
    - s: scope of the (sub)problem
    - cur: current attempt
    - ans: all completed attempt
- retursion body
```python
def question(self, s):
    ans = []
    cur = []
    self.traverse(s, cur, ans)
    return ans

def traverse(scope, cur, ans):
    if complete:
        ans.append(deep_copy(cur))
        return

    for step in step_candidates:
        if possible(step):
            cur.append(step)
            self.traverse(scope - step, cur, ans)
            cur.pop()
    return
```


## 循环的思路
严格意义上这个算不上是DFS，而是BFS。这些题目的特征如下：
- 是一个寻找全部答案的题目
- 最终答案是多个大小相等的元素构成的
- 每个元素有几个选项，所有选项之间相互不干涉

## Examples of DC and Traverse
- DC, Traverse
    - [680. Split String](lint680.md)
- DC, Traverse, Iteration
    - 17
    - [425. Letter Combinations of a Phone Number](lint425.md)
## MISC
- DC 比 Traverse 花费的空间大，因为answer list作为return在函数之间传递。所以DC也慢。