[1. Two Sum](https://leetcode.com/problems/two-sum/)

### Idea

Using HashSet to record key value pair of index and its value, but notice the value should be placed on the key to better get the result of index as the result

### Implementation

```
class Solution {
    public int[] twoSum(int[] nums, int target) {
        int[] result = new int[2];
        Map<Integer, Integer> temp = new HashMap<>();
        for (int i = 0; i < nums.length; i++){
            if (temp.containsKey(target - nums[i])){
                result[0] =temp.get(target - nums[i]);
                result[1] = i;
                return result;
            }
            temp.put(nums[i],i);
        }
        return result;
    }
}
```
