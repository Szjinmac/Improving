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



## 13.Roman to Integer

### 我的解法 暴力解法

```java
public int romanToInt(String s) {
        Map<Character,Integer> map = new HashMap<Character,Integer>();
        map.put('I',1);
        map.put('V',5);
        map.put('X',10);
        map.put('L',50);
        map.put('C',100);
        map.put('D',500);
        map.put('M',1000);

        s=s.replace("CM","DCCCC");
        s=s.replace("CD","CCCC");
        s=s.replace("XC","LXXXX");
        s=s.replace("XL","XXXX");
        s=s.replace("IX","VIIII");
        s=s.replace("IV","IIII");

        

        int result = 0;
        for (Character ch:s.toCharArray()){
            result+=map.get(ch);
        }

        return result;
    }

//时间复杂度 o(n)
//空间复杂度 o(1)
```

#### Python

```python
def romanToInt(self, s: str) -> int:
        translations = {
            "I": 1,
            "V": 5,
            "X": 10,
            "L": 50,
            "C": 100,
            "D": 500,
            "M": 1000
        }
        number = 0
        s = s.replace("IV", "IIII").replace("IX", "VIIII")
        s = s.replace("XL", "XXXX").replace("XC", "LXXXX")
        s = s.replace("CD", "CCCC").replace("CM", "DCCCC")
        for char in s:
            number += translations[char]
        return number
```



## 14.Longest Common Prefix		Easy

```java
public String longestCommonPrefix(String[] strs) {
        if(strs.length == 0){
            return "";
        }
				//先把数组的第一个字符串当作结果，如果不存在就去掉结果的最后一个字符接着循环
        String prefix = strs[0];
        for(int i=1;i<strs.length;i++){
            while(strs[i].indexOf(prefix)!=0){
                prefix = prefix.substring(0,prefix.length()-1);
              	if (prefix.isEmpty()) return "";
            }
        }

        return prefix;
        
    }

//时间复杂度 o(n)
//空间复杂度 o(1)
```



### python

```python
class Solution:
    def longestCommonPrefix(self, strs: List[str]) -> str: # strs = ["flower","flow","flight"]
        short = min(strs, key=len) # short = "flow"
        for item in strs: # When item = "flight"
            while len(short) > 0:
                if item.startswith(short): # during loop 1 condition fails, during loop 2 condition fails, during loop 3 "flight" startswith fl is True
                    break
                else:
                    short = short[:-1] # during loop 1 short = flo, during loop 2 short = fl
        return short
```



## 35.Search Insert Position

### 暴力解法

```java
class Solution {
    public int searchInsert(int[] nums, int target) {
        for(int i=0;i<nums.length;i++){
            if(nums[i]==target || nums[i]>target){
                return i;
            }
        }

        return nums.length;
    }

}

//时间复杂度 o(n)
//空间复杂度 o(1)
```



### 二分法

```java
class Solution {
    public int searchInsert(int[] nums, int target) {
         int lo = 0, hi = nums.length - 1;

        while (lo <= hi) {
            int mid = lo + (hi - lo) / 2;

            if (target < nums[mid]) hi = mid - 1;
            else if (target > nums[mid]) lo = mid + 1;
            else return mid;
        }

        return lo;
    }
}
```

