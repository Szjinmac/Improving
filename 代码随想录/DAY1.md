# DAY1

## 数组的概念

数组是存放在连续内存空间上的相同类型数据的集合，可以通过下标索引的方式获取下标下对应的数据

- 数组下标都从0开始
- 数组内存空间地址连续
- 数组的元素不能删除，只能覆盖



### 704.二分查找

- 循环可以继续的条件：`while (left<=right)`表示当循环只剩一个元素时接着判断
- 取中间数最好用`mid=left+(right-left)/2`防止发生整型溢出

#### Java

```java
class Solution {
    public int search(int[] nums, int target) {
        int len = nums.length;
        int left =0;
        int right = len-1;

        while(left<=right){
            int mid = left + (right-left)/2;
            if(nums[mid] == target){
                return mid;
            }else if(nums[mid]>target){
                right = mid - 1;
            }else{
                left = mid + 1;
            }
        }

        return -1;
    }
}
```



#### Python

```python
class Solution:
    def search(self, nums: List[int], target: int) -> int:
        left,right = 0,len(nums)-1

        while left <= right:
            mid = left+(right-left)//2

            if nums[mid]==target:
                return mid;
            elif nums[mid]>target:
                right = mid-1;
            else:
                left = mid + 1
        
        return -1
```





### 27.移除元素

```java
class Solution {
    public int removeElement(int[] nums, int val) {
        int slow = 0;
        

        for(int fast=0;fast<nums.length;fast++){
            if(nums[fast]!=val){
                swap(nums,slow,fast);
                slow+=1;
            }
        }

        return slow;

    }

    public void swap(int[] nums,int i,int j){
        int temp = nums[i];
        nums[i] = nums[j];
        nums[j] = temp;
    }
}
```

