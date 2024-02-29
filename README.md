# Array - MEDIUM

### Longest Subarray With Sum K (without negative numbers)
```
 public static int longestSubarrayWithSumK(int []arr, long target) {
        int n = arr.length;
        int max = Integer.MIN_VALUE;
        int j = 0;
        long sum = 0;
        for(int i=0; i<n; i++){
            sum+=arr[i];
            while(j<n && sum>target){
                sum-=arr[j];
                j++;
            }
            if(sum == target){
                int temp = i - j + 1;
                if(temp > max){
                    max = temp;
                }
            }
        }
        return max;
    }
```

### Longest Subarray With Sum K (with negative numbers)
```
 public static int getLongestSubarray(int []arr, int k) {
        Map<Integer, Integer> map = new HashMap<>();
        int n = arr.length;
        int maxLen = 0;
        int sum = 0;
        for(int i =0; i<n; i++){
            sum += arr[i];
            if(sum == k){
                maxLen = Math.max(maxLen, i+1);
            }
            int diff = sum - k;1
            if(map.containsKey(diff)){
                int temp = i - map.get(diff);
                maxLen = Math.max(maxLen, temp);
            }
            if(!map.containsKey(sum)){
                map.put(sum, i);
            }
        }
        return maxLen;
    }
```

### 2 Sum Problem
```
 public static String twoSum(int n, int []arr, int target) {
        Arrays.sort(arr);
        int left = 0, right = n - 1;
        while (left < right) {
            int sum = arr[left] + arr[right];
            if (sum == target) {
                return "YES";
            } else if (sum < target) left++;
            else right--;
        }
        return "NO";
    }
```

###  Sort An Array of 0s, 1s and 2s
```
 public static void sortArray(ArrayList<Integer> arr, int n) {
        int low = 0, mid = 0, high = n-1;
        for(int i=0; i<n; i++){
            if(arr.get(mid) == 0){
                swap(arr, mid, low);
                mid++;
                low++;
            }
            else if(arr.get(mid) == 1){
                mid++;
            }
            else {
                swap(arr, mid, high);
                high--;
            }
        }
    }

    static void swap(ArrayList<Integer> arr, int a, int b){
        int temp = arr.get(a);
        arr.set(a, arr.get(b));
        arr.set(b, temp);
    }
```

### Majority Element (>n/2 times) - Moores's voting algorithm 
```
 public static int majorityElement(int[] arr) {
        int count = 0;
        int num = 0;
        int n = arr.length;
        for(int i = 0; i<n; i++){
            if(count == 0){
                count++;
                num = arr[i];
            }
            else if(arr[i] == num) {
                count++;
            }
            else if(arr[i] != num){
                count--;
            }
        }
        count = 0;
        for(int i=0; i<n; i++){
        if(arr[i] == num)  count++;
        }
        if(count > n/2){
            return num;
        }
        return -1;
    }
```
