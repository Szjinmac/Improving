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

