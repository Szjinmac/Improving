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



## 20.Valid Parentheses

```java
class Solution {
    public boolean isValid(String s) {
        Stack<Character> stack = new Stack();
        if(s.length()%2!=0) return false;

        for(char c:s.toCharArray()){
            if(c=='('||c=='{' || c=='['){
                stack.push(c);
            }else if(c==')' && !stack.isEmpty() && stack.peek()=='('){
                stack.pop();
            }else if(c==']' && !stack.isEmpty() && stack.peek()=='['){
                stack.pop();
            }else if(c=='}' && !stack.isEmpty() && stack.peek()=='{'){
                stack.pop();
            }else{
              //注意此处是为了判断"( [ } } ] )"这种情况
                return false;
            }
        }
        
        return stack.isEmpty();
    }
}
```



## 21. Merge Two Sorted Lists.     Easy

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public ListNode mergeTwoLists(ListNode list1, ListNode list2) {
        ListNode temp_node = new ListNode(0);
        ListNode current_node = temp_node;
        while(list1 !=null && list2!=null){
            if(list1.val<list2.val){
                current_node.next = list1;
                list1 = list1.next;
            }else{
                current_node.next = list2;
                list2 = list2.next;
            }

            current_node = current_node.next;
        }
        if(list1 != null){
            current_node.next = list1;
            list1 = list1.next;
        }
        if(list2 != null){
            current_node.next = list2;
            list2 = list2.next;
        }


        return temp_node.next;
    }
}
```



## 26.Remove Duplicates from Sorted Array    Easy

```java
class Solution {
    public int removeDuplicates(int[] nums) {
        int l = 1;
        for(int i=0; i<nums.length-1;i++){
            if(nums[i]!=nums[i+1]){
                nums[l] = nums[i+1];
                l++;
            }
        }
        return l;
    }

    
}
```



## 66.Plus One     Easy

```java
class Solution {
    public int[] plusOne(int[] digits) {
        for(int i = digits.length-1;i>=0;i--){
            if(digits[i]!=9){
                digits[i]++;

                return digits;
            }

            digits[i] = 0;
        }

        digits = new int[digits.length+1];
        digits[0] = 1;

        return digits;
    }
}
```



## 69.Sqrt(x) Easy

```java
class Solution {
    public int mySqrt(int x) {
        int l = 1;
        int r = x;

        while(l <= r){
            int mid = (l + r) / 2;

            if(x / mid == mid){
                return mid;
            } else if(mid > x / mid){
                r = mid - 1;
            } else {
                l = mid + 1;
            }
        }

        return r;
    }
}
```



## 70. Climbing Stairs     Easy

```java
//递归
class Solution {
    public int climbStairs(int n) {
        if(n==1) return 1;
        if(n==2) return 2;

        int[] a = new int[n];
        a[0] = 1;
        a[1] = 2; 

        for(int i=2;i<n;i++){
            a[i] = a[i-1]+a[i-2];
        }
        return a[n-1];
        
    }
}
```

## 88.Merge Sorted Array        Easy

```java
class Solution {
    public void merge(int[] nums1, int m, int[] nums2, int n) {
        int i=m-1;int j=n-1;
        while(i>=0&&j>=0){
            if(nums1[i]<=nums2[j]){
                nums1[i+j+1] = nums2[j];
                j--;
            }else{
                nums1[i+j+1] = nums1[i];
                
                i--;
            }
        }

        while(j>=0){
            nums1[j] = nums2[j];
            j--;
        }

        
        
        
    }
}
```

## 94.Binary Tree Inorder Traversal Easy

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {
    public List<Integer> inorderTraversal(TreeNode root) {
        List<Integer> res = new ArrayList<Integer>();
        Stack<TreeNode> stack = new Stack<TreeNode>();
        while(stack.size()>0 || root !=null){
            if(root!=null){
                stack.add(root);
                root = root.left;
            }else{
                TreeNode temp = stack.pop();
                res.add(temp.val);
                root = temp.right;
            }
        }

        return res;
    }
}
```

## 101.Symmetric Tree     Easy

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {
    public boolean isSymmetric(TreeNode root) {
        if(root==null){
            return true;
        }

        return dfs(root.left,root.right);
        
    }

    boolean dfs(TreeNode left,TreeNode right){
        if(left==null&&right==null){
            return true;
        }
        if(left==null || right==null){
            return false;
        }
        if(left.val!=right.val){
            return false;
        }

        return dfs(left.right,right.left)&&dfs(left.left, right.right);
    }
}
```



## 104.Maximum depth of binary tree     Easy

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {
    //递归
    public int maxDepth(TreeNode root) {
        if(root==null){
            return 0;
        }else{
            int left = maxDepth(root.left);
            int right = maxDepth(root.right);

            return Math.max(left,right)+1;
        }


    }
}
```



## 二分法查找算法中的应用范围

### 在有序数组中进行查找一个数(二分下标)

数组具有随机访问的特性，由于数组在内存中==连续存放==，因此我们可以通过数组的下标快速地访问到这个元素。如果数组存放在链表中，访问一个元素我们都得通过遍历，有遍历的功夫我们早就找到了这个元素，因此，在链表中不适合使用二分法。

### 在整数范围内查找一个整数(二分答案)

如果我们要找的是一个整数，并且我们知道这个整数的范围，那么我们就可以使用二分查找算法，逐渐缩小整数的范围。

### 二分法的两种思路

1. 在循环体中查找元素
2. 在循环体中排除目标元素一定不存在发区间

#### 循环可以继续的条件

`while(left<=right)`表示在区间里只剩下一个元素的时候，我们还需要继续查找

#### 取中间数的代码

取中间数的代码`int mid=(left+right)/2`,严格意义上是有bug的，这是因为在left和right很大的时候，`left+right`有可能会发在整形溢出，这个时候推荐的写法是：

`int mid=left + (right-left)/2 `



### 二分法另外一种思路

在循环体中排除目标元素一定不存在的区间。`while left<right`表示当`left=right`时退出循环。注意使用这个思路需要向上取整数，`int mid = left + (rignt-left+1)/2`,否则可能出现死循环。

## 704.Binary Search    Easy [数组] [二分查找]

```java
class Solution {
    public int search(int[] nums, int target) {
        int left = 0;
        int right = nums.length -1 ;

        while(left<=right){
            int mid = left+(right-left)/2;
            if(nums[mid]==target){
                return mid;
            }else if(nums[mid]>target){
                right = mid-1;
            }else{
                left = mid+1;
            }
        }   

        return -1;
    }
}

public class Solution {
  
    // 「力扣」第 704 题：二分查找

    public int search(int[] nums, int target) {
        int len = nums.length;

        int left = 0;
        int right = len - 1;
        // 目标元素可能存在在区间 [left, right]
        while (left < right) {
            int mid = left + (right - left) / 2;
            if (nums[mid] < target) {
                // 下一轮搜索区间是 [mid + 1, right]
                left = mid + 1;
            } else {
                // 下一轮搜索区间是 [left, mid]
                right = mid;
            }
        }

        if (nums[left] == target) {
            return left;
        }
        return -1;
    }
}

public class Solution {
  
    // 「力扣」第 704 题：二分查找

    public int search(int[] nums, int target) {
        int len = nums.length;

        int left = 0;
        int right = len - 1;
        while (left < right) {
            int mid = left + (right - left + 1) / 2;
            if (nums[mid] > target) {
                // 下一轮搜索区间是 [left, mid - 1]
                right = mid - 1;
            } else {
                // 下一轮搜索区间是 [mid, right]
                left = mid;
            }
        }

        if (nums[left] == target) {
            return left;
        }
        return -1;
    }
}

```



## 374.Guess Number Higher or Lower ==Easy== [数组] [二分法]

```java
/** 
 * Forward declaration of guess API.
 * @param  num   your guess
 * @return 	     -1 if num is higher than the picked number
 *			      1 if num is lower than the picked number
 *               otherwise return 0
 * int guess(int num);
 */

public class Solution extends GuessGame {
    public int guessNumber(int n) {
        int left = 1;
        int right = n;

        while(left<=right){
            int mid = left+(right-left)/2;
            if(guess(mid)==0){
                return mid;
            }
            else if(guess(mid)==-1){
                right = mid-1; 
            }else{
                left = mid+1;
            }
        }

        return -1;
    }
}
```



## 35.Search Insert Position  ==Medium== [二分法]

```java
public class Solution {

    public int searchInsert(int[] nums, int target) {
        int len = nums.length;
        // 题目没有说输入数组的长度可能为 0，因此需要做特殊判断
        if (len == 0) {
            return 0;
        }

        if (nums[len - 1] < target) {
            return len;
        }
        int left = 0;
        int right = len - 1;

        // 在区间 [left, right] 查找插入元素的位置
        while (left < right) {
            int mid = left + (right - left) / 2;
            if (nums[mid] < target){
                // 下一轮搜索的区间是 [mid + 1, right]
                left = mid + 1;
            } else {
                // 下一轮搜索的区间是 [left, mid]
                right = mid;
            }
        }
        // 由于程序走到这里 [left, right] 里一定存在插入元素的位置
        // 且退出循环的时候一定有 left == right 成立，因此返回 left 或者 right 均可
        return left;
    }
}

```



## 34. Find First and Last Position of Element in Sorted Array   ==Medium== [二分法放弃]

```java
class Solution {
    public int[] searchRange(int[] nums, int target) {
        int len = nums.length;
        if(len==0){
            return new int[]{-1,-1};
        }

        int firstPosition = searchFirstPosition(nums,target);
        if(firstPosition == -1){
            return new int[]{-1,-1};
        }

        int lastPosition = searchLastPosition(nums,target);

        return new int[]{firstPosition,lastPosition};

    }

    private int searchFirstPosition(int[] nums , int target){
        int left = 0;
        int right = nums.length-1;

        while(left < right){
            int mid = left+(right-left)/2;
            if(nums[mid]<target){
                left = mid+1;
            }else{
                right = mid;
            }
        }

        if(nums[left]==target){
            return left;
        }else{
            return -1;
        }
    }

    private int searchLastPosition(int[] nums , int target){
        int left = 0;
        int right = nums.length-1;

        while(left < right){
            int mid = left+(right-left+1)/2;
            if(nums[mid]>target){
                right = mid-1;
            }else{
                left = mid;
            }
        }

        return left;
    }
}
```



## 153.Find Minimum in Rotated Sorted Array ==medium== [数组] [二分法]



```java
//使用二分法，如果nums[mid]<nums[right]说明最小值一定在左半部分，反之，最小值在右半部分
class Solution {
    public int findMin(int[] nums) {
        int left = 0;
        int right = nums.length - 1;

        while(left<right){
            int mid =left+(right-left)/2;
            if(nums[mid]<nums[right]){
                right = mid;
            }else{
                left = mid+1;
            }
        }

        return nums[left];
    }
}
```



## 154.Find Minimum in Rotated Sorted Array II ==hard== [数组] [二分法]

```java
//与153题类似，只不过nums[mid] = nums[right]时，需要right-1来进行去重
class Solution {
    public int findMin(int[] nums) {
        int left = 0;
        int right = nums.length - 1;

        while(left<right){
            int mid = left+(right-left)/2;
            if(nums[mid]<nums[right]){
                right = mid;
            }else if(nums[mid] == nums[right]){
                right = right-1;
            }else{
                left = mid+1;
            }
                
            
        }

        return nums[left];
    }
}
```





## 33.Search in Rotated Sorted Array ==Medium== [二分法]

```java
class Solution {
    public int search(int[] nums, int target) {
        //首先使用二分法找到最小值
        int l = 0;
        int r = nums.length-1;
        while(l < r){
            int mid = l+(r-l)/2;
            if(nums[mid]>nums[r]){
                l = mid+1;
            }else{
                r = mid;
            }
        }

        int left = find(nums,target,0,l);
        int right = find(nums,target,l,nums.length-1);

        if(left==-1){
           return right==-1?-1:right;
        }else{
            return left;
        }


    }

    public int find(int[] nums,int target,int l,int r){
        

        while(l<=r){
            int mid = l+(r-l)/2;
            if(nums[mid]>target){
                r = mid-1;
            }else if(nums[mid]<target){
                l = mid+1;
            }else{
                return mid;
            }
        }

        return -1;
    }
}
```



## 81.Search in Rotated Sorted Array II ==Medium== [二分法]

```java
class Solution {
    public boolean search(int[] nums, int t) {
        int n = nums.length;
        int l = 0, r = n - 1;
        // 恢复二段性
        while (l < r && nums[0] == nums[r]) r--;

        // 第一次二分，找旋转点
        while (l < r) {
            int mid = l + r + 1 >> 1;
            if (nums[mid] >= nums[0]) {
                l = mid;
            } else {
                r = mid - 1;
            }
        }
        
        int idx = n;
        if (nums[r] >= nums[0] && r + 1 < n) idx = r + 1;

        // 第二次二分，找目标值
        int ans = find(nums, 0, idx - 1, t);
        if (ans != -1) return true;
        ans = find(nums, idx, n - 1, t);
        return ans != -1;
    }
    int find(int[] nums, int l, int r, int t) {
        while (l < r) {
            int mid = l + r >> 1;
            if (nums[mid] >= t) {
                r = mid;
            } else {
                l = mid + 1;
            }
        }
        return nums[r] == t ? r : -1;
    }
}


```



## 278. First Bad Version  ==Easy== [二分法]

```java
/* The isBadVersion API is defined in the parent class VersionControl.
      boolean isBadVersion(int version); */

public class Solution extends VersionControl {
    public int firstBadVersion(int n) {
        int left=1; 
        int right=n;
        while(left<=right){
            int mid = left+(right-left)/2;
            if(isBadVersion(mid)==false){
                left = mid+1;
            }else{
                if(isBadVersion(mid-1)==false){
                    return mid;
                }else{
                    right = mid-1;
                }
            }
        }
        return left;
    }
}
```



## 852.Peak Index in a Mountain Array ==Medium== [二分法]

```java
class Solution {
    public int peakIndexInMountainArray(int[] arr) {
        int left = 0;
        int right = arr.length-1;
		//注意这里使用排除二分法，left<right
        
        while(left<right){
            int mid = left+(right-left)/2;
            if(arr[mid]<arr[mid+1]){
                left = mid+1;
            }else{
                right = mid;
            }
        }

        return left;
    }
}
```



## 1095.Find in Mountain Array ==Hard==[二分法]

```java
/**
 * // This is MountainArray's API interface.
 * // You should not implement it, or speculate about its implementation
 * interface MountainArray {
 *     public int get(int index) {}
 *     public int length() {}
 * }
 */
 
class Solution {
    public int findInMountainArray(int target, MountainArray mountainArr) {
        //首先使用二分法找出最大值
        int left = 0;
        int right = mountainArr.length()-1;
        while(left<right){
            int mid = left+(right-left)/2;

            if(mountainArr.get(mid)<mountainArr.get(mid+1)){
                left = mid+1;
            }else{
                right = mid;
            }
        }

        int max = left;
        //左边的目标值
        int leftnum = findtarget(target,mountainArr,0,left);
        //右边的目标
        int rightnum = findtargetright(target,mountainArr,left,mountainArr.length()-1);

        if(leftnum==-1){
            return rightnum==-1?-1:rightnum;
        }else{
            return leftnum==-1?-1:leftnum;
        }
    }

    public int findtarget(int target,MountainArray mountainArr,int left,int right){
        while(left<=right){
            int mid = left+(right-left)/2;
            if(mountainArr.get(mid)>target){
                right = mid -1;
            }else if(mountainArr.get(mid)<target){
                left = mid+1;
            }else{
                return mid;
            }
        }

        return -1;
    }

     public int findtargetright(int target,MountainArray mountainArr,int left,int right){
        while(left<=right){
            int mid = left+(right-left)/2;
            if(mountainArr.get(mid)>target){
                left  = mid + 1;
            }else if(mountainArr.get(mid)<target){
                right = mid - 1;
            }else{
                return mid;
            }
        }

        return -1;
    }
}
```





## 4.Median of Two Sorted Arrays ==Hard== [二分法]不太会

```java
public class Solution {

    public double findMedianSortedArrays(int[] nums1, int[] nums2) {
        if (nums1.length > nums2.length) {
            int[] temp = nums1;
            nums1 = nums2;
            nums2 = temp;
        }

        int m = nums1.length;
        int n = nums2.length;

        // 分割线左边的所有元素需要满足的个数 m + (n - m + 1) / 2;
        int totalLeft = (m + n + 1) / 2;

        // 在 nums1 的区间 [0, m] 里查找恰当的分割线，
        // 使得 nums1[i - 1] <= nums2[j] && nums2[j - 1] <= nums1[i]
        int left = 0;
        int right = m;

        while (left < right) {
            int i = left + (right - left + 1) / 2;
            int j = totalLeft - i;
            if (nums1[i - 1] > nums2[j]) {
                // 下一轮搜索的区间 [left, i - 1]
                right = i - 1;
            } else {
                // 下一轮搜索的区间 [i, right]
                left = i;
            }
        }

        int i = left;
        int j = totalLeft - i;

        int nums1LeftMax = i == 0 ? Integer.MIN_VALUE : nums1[i - 1];
        int nums1RightMin = i == m ? Integer.MAX_VALUE : nums1[i];
        int nums2LeftMax = j == 0 ? Integer.MIN_VALUE : nums2[j - 1];
        int nums2RightMin = j == n ? Integer.MAX_VALUE : nums2[j];

        if (((m + n) % 2) == 1) {
            return Math.max(nums1LeftMax, nums2LeftMax);
        } else {
            return (double) ((Math.max(nums1LeftMax, nums2LeftMax) + Math.min(nums1RightMin, nums2RightMin))) / 2;
        }
    }
}

作者：liweiwei1419
链接：https://leetcode.cn/problems/median-of-two-sorted-arrays/solutions/15086/he-bing-yi-hou-zhao-gui-bing-guo-cheng-zhong-zhao-/
来源：力扣（LeetCode）
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。
```



## 287. Find the Duplicate Number ==Medium== [二分法]

```java
class Solution {
    public int findDuplicate(int[] nums) {
        int left = 1;
        int right = nums.length-1;

        while(left < right){
            int mid = left+(right-left)/2;
            int count = 0;

            for(int num:nums){
                if(num<=mid){
                    count+=1;
                }
            }

            if(count>mid){
                right = mid;
            }else{
                left = mid+1;
            }
        }
        return left;
    }
}
```



## 1300. Sum of Mutated Array Closest to Target ==Medium== [二分法]



```java
class Solution {
    public int findBestValue(int[] arr, int target) {
        int left = 0;
        int right = 0;
        //找到最大值
        for(int num:arr){
            right =Math.max(right,num);
        }

        while(left<right){
            int mid =left+(right-left)/2;
            int sum = calculatesum(arr,mid);
            if(sum<target){
                left = mid+1;
            }else{
                right = mid;
            }
        }

        int sum1 = calculatesum(arr,left);
        int sum2 = calculatesum(arr,left-1);
        if (target - sum1 <= sum2 - target) {
            return left - 1;
        }
        return left;


    }

    private int calculatesum(int[] arr,int value){
        int sum = 0;
        for(int num:arr){
            sum+=Math.min(num,value);
        }

        return sum;
    }
}

```



## 875.Koko Eating Bananas ==Medium== 二分法

```java
class Solution {
    public int minEatingSpeed(int[] piles, int h) {
        //首先找到堆中的最大值
        int max = 0;
        for(int num:piles){
            max = max>num?max:num;
        }

        int left = 1;
        int right = max;

        while(left<right){
            int mid = left+(right-left)/2;
            int time = 0;

            for(int num:piles){
                
                int hour=(mid+num-1)/mid;
                time +=hour;
            }

            if(time>h){
                left=mid+1;
            }else{
                right = mid;
            }

        }

        return left;
        
    }
}
```

## 410.Split Array Largest Sum ==hard== [二分法]

```java
class Solution {
    public int splitArray(int[] nums, int k) {
        int max = 0;
        int sum = 0;

        //子数组各自和的最大值
        for(int num:nums){
            max = Math.max(max,num);
            sum+=num;
        }

        int left = max;
        int right = sum;

        while(left<right){
            int mid = left+(right-left)/2;

            int splits = split(nums,mid);
            if(splits>k){
                left = mid+1;
            }else{
                right = mid;
            }
        }

        return left;

    }

   

    private int split(int[] nums,int maxIntervalSum){
        int splits = 1;
        int currentSum = 0;
        //当前区间的和
        for(int num:nums){
            if(currentSum + num>maxIntervalSum){
                currentSum = 0;
                splits++;
            }

            currentSum+=num;
        }

        return splits;
    }

    

```



## 1011.Capacity To Ship Packages Within D Days ==hard== [二分法]

```java
class Solution {
    public int shipWithinDays(int[] weights, int days) {
        int max = 0;
        int sum = 0;

        for(int weight:weights){
            max = Math.max(max,weight);
            sum+=weight;
        }

        int left = max;
        int right = sum;

        while(left<right){
            int mid = left+(right-left)/2;
            int day = split(weights,mid);

            if(day>days){
                left = mid+1;

            }else{
                right = mid;
            }
        }

        return left;

    }

    private int split(int[] weights, int max){
        int days = 1;
        int currentSum = 0;

        for(int weight:weights){
            if(currentSum+weight>max){
                currentSum = 0;
                days+=1;
            }

            currentSum+=weight;
        }

        return days;
    }
}
```





## LCP12.小张刷题计划

```java
class Solution {
    public int minTime(int[] time, int m) {
        int left = 0;
        int right = Integer.MAX_VALUE;
        while(left <= right) {
            int mid = left + (right - left) / 2;
            //如果这个时间限制可以在规定天数里面完成刷题计划
            if(check(time, mid, m)) {
                //向左缩小查找范围
                right = mid - 1;
            }else {
                //反之 向右缩小查找范围
                left = mid + 1;
            }
        }
        return left;
    }

    boolean check(int[] time, int target, int m) {
        int maxTime = 0;
        int total = 0;
        //如果第一天就都做完了
        //后续代码不会将days进行递增 应该初始化为1
        int days = 1;
        //是否使用过了场外援助
        boolean helper = true;
        for(int i = 0; i < time.length; i++) {
            //维护花费时间最长的题目
            maxTime = Math.max(maxTime, time[i]);
            //累加这一天的总做题时间
            total += time[i];
            //如果超过当天做题时间限制了
            if(total > target) {
                //如果未使用过场外援助
                if(helper) {
                    //减去耗时最多的题目
                    total -= maxTime;
                    helper = false;
                }else {
                    //超时并且使用过场外援助
                    //得从下一天重新开始了
                    days++;
                    //刷新场外援助
                    helper = true;
                    //当天最大值刷新
                    maxTime = 0;
                    //总计时间刷新
                    total = 0;
                    //最重要的一点也很容易遗忘
                    //这道没有时间做的题目留到下一天重新开始做
                    i--;
                }
            }
        }
        return m >= days;
    }
}

作者：Paddi-Yan
链接：https://leetcode.cn/problems/xiao-zhang-shua-ti-ji-hua/solutions/1402270/lcp-12-by-lyyprogrammer-wy2f/
来源：力扣（LeetCode）
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。
```

