## 第二周 - 2021-11-28


##### 题目：(1)子域名访问计数
##### 链接：https://leetcode-cn.com/problems/subdomain-visit-count/
##### 语言：Python
```python
class Solution:
    def subdomainVisits(self, cpdomains: List[str]) -> List[str]:
        # 1.从后向前扫描域名段；
        # 2.条件：检查子段是否存在于域名，使用哈希表去重和统计；
        # 3:边界：j>=0

        # 时间复杂度：O(n^2)
        
        m = {}
        for cpdomain in cpdomains:
            count, domain = cpdomain.split(" ")
            domainFields = domain.split(".")
            count, j = int(count), len(domainFields) - 1
            while j >= 0:
                suffixDomain = ".".join(domainFields[j:])
                if suffixDomain in m.keys(): m[suffixDomain] += count 
                else: m[suffixDomain] = count
                j -= 1

        return ["{} {}".format(v, k) for k, v in m.items()]

```
<br>


##### 题目：(2)和为 K 的子数组
##### 链接：https://leetcode-cn.com/problems/subarray-sum-equals-k/
##### 语言：Go
```go
func subarraySum(nums []int, k int) int {
    // 1.将原数组转换为前缀来求值；
    // 2.查找与之匹配的 k 值；

    // 时间复杂度：O(n) + O(n^2)

    n := len(nums)
    s := make([]int, n+1)
    s[0] = 0
    for i := 1; i <= n; i++ { s[i] = s[i-1] + nums[i-1] }
    
    ans := 0
    // O(n^2)
    for i := 0; i < n; i++ {
        for j := i; j < n; j++ {
            if s[j+1] - s[i] == k {
                ans += 1
            }
        }
    }
    return ans
}

```
<br>


