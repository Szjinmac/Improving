# LeetCode题解

## 1.Two Sum 		Easy

### 我的解法  暴力解法

```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        for(int i=0;i<nums.length;i++){
            for(int j=i+1;j<nums.length;j++){
                if(nums[i]+nums[j]==target){
                    return new int[]{i,j};
                }
            }
        }

        return new int[] {};
    }
}


//时间复杂度 o(n^2)
//空间复杂度 o(1)
```



### 其他解法  使用哈希表(可能是最优解)

```java
import java.util.HashMap;
import java.util.Map;
 
class Solution {
    public int[] twoSum(int[] nums, int target) {
        Map<Integer, Integer> numToIndex = new HashMap<>();
        for (int i = 0; i < nums.length; i++) {
          
            if (numToIndex.containsKey(target - nums[i])) {
                return new int[] {numToIndex.get(target - nums[i]), i};
            }
          //注意使用nums[i]作为key更简单，不能与if语句交换先后顺序
            numToIndex.put(nums[i], i);
        }
        return new int[] {};
    }
}

//时间复杂度 o(n)
//空间复杂度 o(n)
```



### Python

```python
#暴力解法
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        for i in range(len(nums)):
            for j in range(i + 1, len(nums)):
                if nums[i] + nums[j] == target:
                    return [i, j]
        return []
      

#哈希表
def twoSum(self, nums: List[int], target: int) -> List[int]:
        numToIndex = {}
        for i in range(len(nums)):
            if target - nums[i] in numToIndex:
                return [numToIndex[target - nums[i]], i]
            numToIndex[nums[i]] = i
        return []
```

