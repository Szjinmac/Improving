# DAY6

## 454.四数相加2

```java
class Solution {
    public int fourSumCount(int[] nums1, int[] nums2, int[] nums3, int[] nums4) {
        Map<Integer, Integer> map = new HashMap<>();
        int res = 0;

        for(int i=0;i<nums1.length;i++){
            for(int j=0;j<nums2.length;j++){
                int sumAB = nums1[i]+nums2[j];
                if(map.containsKey(sumAB)) map.put(sumAB,map.get(sumAB)+1);
                else map.put(sumAB,1);
            }
        }

        for(int i=0;i<nums3.length;i++){
            for(int j=0;j<nums4.length;j++){
                int sumCD = -(nums3[i]+nums4[j]);
                if(map.containsKey(sumCD)) res += map.get(sumCD);
            }
        }

        return res;
    }
}
```



## 383.赎金信

```java
class Solution {
    public boolean canConstruct(String ransomNote, String magazine) {
        if(ransomNote.length()>magazine.length()){
            return false;
        }

        int[] cnt = new int[26];

        for(char c:magazine.toCharArray()){
            cnt[c-'a']++;
        }

        for(char c:ransomNote.toCharArray()){
            cnt[c-'a'] -- ;
            if(cnt[c-'a']<0){
                return false;
            }

        }


        return true;
    }
}
```



## 15.三数之和

```java
class Solution {
    public List<List<Integer>> threeSum(int[] nums) {
        //排序
        Arrays.sort(nums);
        List<List<Integer>> res = new ArrayList<>();

        for(int k=0;k<nums.length-2;k++){
            //如果nums[k]大于0，那后面的也大于0
            if(nums[k]>0) break;
            //去重
            if(k>0&&nums[k] == nums[k-1]) continue;
            int i = k+1,j=nums.length-1;
            while(i<j){
                int sum = nums[k]+nums[i]+nums[j];
                if(sum<0){
                    while(i<j && nums[i]==nums[++i]);
                }else if(sum>0){
                    while(i<j && nums[j] == nums[--j]);
                }else{
                    res.add(new ArrayList<Integer>(Arrays.asList(nums[k], nums[i], nums[j])));
                    while(i < j && nums[i] == nums[++i]);
                    while(i < j && nums[j] == nums[--j]);


                }
            }
        }

        return res;
    }
}
```

