# 1.Two Sum

题目：
Given an array of integers, return indices of the two numbers such that they add up to a specific target.

You may assume that each input would have exactly one solution.

Example:
Given nums = [2, 7, 11, 15], target = 9,

Because nums[0] + nums[1] = 2 + 7 = 9,
return [0, 1].

翻译：
给定一个整形数组和一个整数target，返回2个元素的下标，它们满足相加的和为target。
你可以假定每个输入，都会恰好有一个满足条件的返回结果。

Java版代码1（时间复杂度O(n)）：

```java
public class Solution {
    public int[] twoSum(int[] nums, int target) {
        Map<Integer,Integer> map=new HashMap<>();
        for(int i=0;i<nums.length;i++){
            Integer index=map.get(target-nums[i]);
            if(index==null){
                map.put(nums[i],i);
            }else{
                return new int[]{i,index};
            }
        }
        return new int[]{0,0};
    }
}
```



Java版代码2（时间复杂度O(n^2)）：(第一次的结果)

```java
public class Solution {
    public int[] twoSum(int[] nums, int target) {
        int[] result=new int[2];
        for(int i=0;i<nums.length-1;i++){
            for(int j=i+1;j<nums.length;j++){
                if(nums[i]+nums[j]==target){
                    return new int[]{i,j};
                }
            }
        }
        return result;
    }
}
```



# 2. 两数相加

给出两个 非空 的链表用来表示两个非负的整数。其中，它们各自的位数是按照 逆序 的方式存储的，并且它们的每个节点只能存储 一位 数字。

如果，我们将这两个数相加起来，则会返回一个新的链表来表示它们的和。

您可以假设除了数字 0 之外，这两个数都不会以 0 开头。

示例：

输入：(2 -> 4 -> 3) + (5 -> 6 -> 4)
输出：7 -> 0 -> 8
原因：342 + 465 = 807

第一次未答出来

```java
class Solution {
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        ListNode dead = new ListNode(0);
        ListNode p=l1, q=l2, curr = dead;
        int curry = 0;
        while(p!=null||q!=null){
            int x = (p==null)?0:p.val;
            int y = (q==null)?0:q.val;
            int sum = x + y + curry;
            curry = sum/10;
            curr.next  = new ListNode(sum%10);
            curr = curr.next;
            if(p!=null) p = p.next;
            if(q!=null) q = q.next;
        }
        if(curry!=0){
            curr.next = new ListNode(curry);
        }
        return dead.next;
    }
}
```



# 3. 无重复字符的最长子串

给定一个字符串，请你找出其中不含有重复字符的 最长子串 的长度。 

示例 1:

输入: "abcabcbb"
输出: 3 
解释: 因为无重复字符的最长子串是 "abc"，所以其长度为 3。
示例 2:

输入: "bbbbb"
输出: 1
解释: 因为无重复字符的最长子串是 "b"，所以其长度为 1。
示例 3:

输入: "pwwkew"
输出: 3
解释: 因为无重复字符的最长子串是 "wke"，所以其长度为 3。
     请注意，你的答案必须是 子串 的长度，"pwke" 是一个子序列，不是子串。

第一次的答案：

```java
class Solution {
    public int lengthOfLongestSubstring(String s) {
        char[] charArray = s.toCharArray();
        String str = "";
        Map<String, Integer> map = new HashMap<String, Integer>();
        int length = charArray.length;
        for(int i=0;i<length;i++){
            String next = Character.toString(charArray[i]);
            int index = str.indexOf(next);
            if(index == -1){
                str += next;
            }else{
                if(!map.containsKey(str))
                    map.put(str, str.length());
                str = str.substring(index+1) + next;
            }
            if(i>=length-1){
                if(!map.containsKey(str))
                    map.put(str, str.length());
            }
        }
        int result = 0;
        for(Map.Entry<String, Integer> smap: map.entrySet()){
            int slength = smap.getValue().intValue();
            if(result<slength)
                result = slength;
        }
        return result;
    }
}
```



第一次优化后的答案：时间消耗减少，空间消耗不变

```java
char[] charArray = s.toCharArray();
        String str = "";
        int length = charArray.length;
        int result = 0;
        for(int i=0;i<length;i++){
            String next = Character.toString(charArray[i]);
            int index = str.indexOf(next);
            if(index == -1){
                str += next;
            }else{
            	result = str.length()>result?str.length():result;
                str = str.substring(index+1) + next;
            }
            if(i>=length-1){
            	result = str.length()>result?str.length():result;
            }
        }
        return result;
```



官方答案：时间大幅减少，空间略微减少

```java
char[] charArray = s.toCharArray();
String str = "";
int length = charArray.length;
int result = 0;
for(int i=0;i<length;i++){
    String next = Character.toString(charArray[i]);
    int index = str.indexOf(next);
    if(index == -1){
        str += next;
    }else{
        result = str.length()>result?str.length():result;
        str = str.substring(index+1) + next;
    }
    if(i>=length-1){
        result = str.length()>result?str.length():result;
    }
}
return result;
```



# 4. 寻找两个有序数组的中位数

给定两个大小为 m 和 n 的有序数组 nums1 和 nums2。

请你找出这两个有序数组的中位数，并且要求算法的时间复杂度为 O(log(m + n))。

你可以假设 nums1 和 nums2 不会同时为空。

示例 1:

nums1 = [1, 3]
nums2 = [2]

则中位数是 2.0
示例 2:

nums1 = [1, 2]
nums2 = [3, 4]

则中位数是 (2 + 3)/2 = 2.5

第一次答案：

```java
class Solution {
    public double findMedianSortedArrays(int[] nums1, int[] nums2) {
        int len1 = nums1.length, len2 = nums2.length;
        if(len1 == 0)
            return (len2%2==0)?Double.valueOf(nums2[len2/2]+nums2[len2/2-1])/2:nums2[(len2-1)/2];
        if(len2 == 0)
            return (len1%2==0)?Double.valueOf(nums1[len1/2]+nums1[len1/2-1])/2:nums1[(len1-1)/2];
        List<Integer> all = new ArrayList<Integer>();
        int i, j;
        for(i = 0, j = 0;i<len1&&j<len2;){
            if(nums1[i]<nums2[j]){
                all.add(nums1[i++]);
            }else{
                all.add(nums2[j++]);
            }
        }
        while(i<len1){
            all.add(nums1[i++]);
        }
        while(j<len2){
            all.add(nums2[j++]);
        }
        int len = all.size();
        return (len%2==0)?Double.valueOf(all.get(len/2)+all.get(len/2-1))/2:all.get((len-1)/2);
    }
}
```