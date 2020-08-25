# 记忆化搜索

要点
- 一道题可以用DC的DFS来完成。
- 搜索的分支有重复所以有可能（基本上）要超时
- 这时候只要在DC的函数上加上对结果的记忆即可

从DC到Dict记忆到lru_cache请看[这里](misc/mem_dfs.md)

# Example
- [109. Triangle](lint109.md)
- [107. Word Break](lint107.md)
- [582. Word Break II](lint582.md)
- [683. Word Break III](lint683.md)
- [192. Wildcard Matching](lint192.md)
- [154. Regular Expression Matching](lint154.md)
- [110. Minimum Path Sum](lint110.md)
- [64. Minimum Path Sum](leet64.md)
- [111. Climbing Stairs](lint111.md)
- [114. Unique Paths](lint114.md)
- [115. Unique Paths II](lint115.md)
- [76. Longest Increasing Subsequence](lint67.md)
- [1143. Longest Common Subsequence](leet1143.md)
- [221. Maximal Square](leet221.md)
- [983. Minimum Cost For Tickets](leet983.md)