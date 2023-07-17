# DAY5



```java
'A' - 'A' == 0
'B' - 'A' == 1
'C' - 'A' == 2
```

- map是映射，元素是键-值对，关键字起到索引作用，值表示与索引相关联的数值
- set是集合，每个元素只包含一个关键字
- set不允许修改元素的值，map允许修改value不允许修改key值

## 242.有效的字母异位词



```java
class Solution {
    public boolean isAnagram(String s, String t) {
        if(s.length()!=t.length()){
            return false;
        }

        int[] alpha = new int[26];

        for(int i=0;i<s.length();i++){
            alpha[s.charAt(i)-'a']++;
            alpha[t.charAt(i)-'a']--;
        }

        for(int i=0;i<26;i++){
            if(alpha[i]!=0)return false;
        }

        return true;

    }
}
```



## 349.两个数组的交集

```java
class Solution {
    public int[] intersection(int[] nums1, int[] nums2) {
        HashSet<Integer> set = new HashSet<>();

        for(int i =0 ;i < nums1.length;i++){
            set.add(nums1[i]);
        }

        HashSet<Integer> list = new HashSet<>();

        for(int i=0;i<nums2.length;i++){
            if(set.contains(nums2[i])){
                list.add(nums2[i]);
            }
        }

        return list.stream().mapToInt(x->x).toArray();

    }
}                 
```



## 202.快乐数

```java
class Solution {
    public boolean isHappy(int n) {
        Set<Integer> seen = new HashSet<>();
        while(n!=1 && !seen.contains(n)){
            seen.add(n);
            n = getNext(n);
        }

        return n==1;
    }

    private int getNext(int n){
        int sum = 0;
        while(n>0){
            int temp = n%10;
            sum+=temp*temp;
            n = n/10;
        }

        return sum;
    }
}
```



## 1.两数之和

```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        HashMap<Integer,Integer>  map = new HashMap<Integer,Integer>();
        for(int i=0;i<nums.length;i++){
            if(map.containsKey(target-nums[i])){
                return new int[]{map.get(target-nums[i]),i};
            }

            map.put(nums[i],i);
        }

        return new int[0];
    }
}
```

