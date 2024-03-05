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

### 1) 2 Sum Problem
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

###  2) Sort An Array of 0s, 1s and 2s
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

### 3) Majority Element (>n/2 times) - Moores's voting algorithm 
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

### 4) Maximum Subarray Sum - (Kadane's Algorithm)
```
public static long maxSubarraySum(int[] arr, int n) {
	long max = 0;
        long sum = 0;
        if(n == 0) return max;

        for(int i=0; i<n; i++){
            sum += arr[i];
            if(sum > max){
                max = Math.max(sum, max);
            }
            if(sum<0){
                sum = 0;
            }
        }
        return max;
}
```

### 5) Best time to buy and sell stock
```
public static int bestTimeToBuyAndSellStock(int []prices) {
        int minPrice = Integer.MAX_VALUE;
        int max = 0;
        int n = prices.length;
        for(int i = 0; i<n; i++){
            if(prices[i] < minPrice){
                minPrice = prices[i];
            }
            max = Math.max(max, prices[i]-minPrice);
        }
        return max;
    }
```

### 5) Rearrage Numbers
```
public int[] rearrangeArray(int[] arr) {
        int[] newArr = new int[arr.length];
        int pos = 0;
        int neg = 1;
        int n = arr.length;
        for(int i = 0; i<n; i++){
            if(arr[i] > 0){
                newArr[pos] = arr[i];
                pos += 2;
            } else {
                newArr[neg] = arr[i];
                neg += 2;
            }
        }
	return newArr;
}
```

### 6) Next Permutation
```
public void nextPermutation(int[] arr) {
        int index = -1;
        int n = arr.length;
        for(int i = n-2; i>=0; i--){
            if(arr[i] < arr[i+1]){
                index = i;
                break;
            }
        }

        if(index == -1) {
            for(int i = 0; i<n/2; i++){
                int temp = arr[i];
                arr[i] = arr[n-i-1];
                arr[n-i-1] = temp;
            }
            return;
        }

        for(int i =n-1; i>=0; i--){
            if(arr[i] > arr[index]){
                int temp = arr[i];
                arr[i] = arr[index];
                arr[index] = temp;
                break;
            }
        }

        int start = index+1;
        int end = n - 1;
        int total = start + end;
        for(int i= start; i<=total/2; i++){
            int temp = arr[i];
            arr[i] = arr[total-i];
            arr[total-i] = temp;
        }
    }
```

### 7) Longest Consecutive Sequence
```
    public int longestConsecutive(int[] arr) {
        int longest = 1;
        if(arr.length == 0){
            return 0;
        }
        Set<Integer> set = new TreeSet<>();
        for(int val: arr){
            set.add(val);
        }

        for (int it : set) {
            if (!set.contains(it - 1)) {
                int cnt = 1;
                int x = it;
                while (set.contains(x + 1)) {
                    x = x + 1;
                    cnt = cnt + 1;
                }
                longest = Math.max(longest, cnt);
            }
        }
        return longest;
    }
```
### 8) Set Matrix Zero
###### Better approach
```
    public void setZeroes(int[][] matrix) {
        int n = matrix.length;
        int m = matrix[0].length;

        int[] row = new int[n];
        int[] col = new int[m];

        for(int i=0; i<n; i++){
            for(int j = 0; j<m; j++){
                if(matrix[i][j]==0){
                    row[i] = 1;
                    col[j] = 1;
                }
            }
        }

        for(int i=0; i<n; i++){
            for(int j=0; j<m; j++){
                if(row[i] == 1 || col[j] == 1){
                    matrix[i][j] = 0;
                }
            }
        }
    }
```
###### Optimised approach - avoided extra spaces, but better approach is better in compare to time complexity
```
public void setZeroes(int[][] matrix) {
        int n = matrix.length;
        int m = matrix[0].length;
        int col0 = matrix[0][0];
        for(int i=0; i<n; i++){
            for(int j=0; j<m; j++){
                if(matrix[i][j] == 0){
                    matrix[i][0] = 0;
                    if(j == 0){
                        col0 = 0;
                    } else{
                        matrix[0][j] = 0;
                    }
                }
            }
        }

        for(int i=1; i<n; i++){
            for(int j=1; j<m; j++){
                if(matrix[0][j] == 0 || matrix[i][0] == 0){
                    matrix[i][j] = 0;
                }
            }
        }

        if(matrix[0][0] == 0){
            for(int j=1; j<m; j++){
                matrix[0][j] = 0;
            }
        }

        if(col0 == 0){
            for(int i=0; i<n; i++){
                matrix[i][0] = 0;
            }
        }

        for(int i=0; i<n; i++){
            for(int j = 0; j<m; j++){
                System.out.print(matrix[i][j]);
            }
            System.out.println();
        }
    }
```
### 9) Rotate 90deg
###### Brute-force approach - using extra space here
```
public void rotate(int[][] matrix) {
        int n = matrix.length;
        int[][] arr = new int[n][n];
        for(int i=0; i<n; i++){
            for(int j=0; j<n; j++){
                arr[j][n-i-1] = matrix[i][j];
            }
        }

        for(int i =0; i<n; i++){
            for(int j = 0; j<n; j++){
                matrix[i][j] = arr[i][j]; 
            }
        }
    }
```
###### Optimised approach - avoided
```
public void rotate(int[][] matrix) {
        int n = matrix.length;
        for(int i=0; i<n; i++){
            for(int j= i; j<n; j++){
                int temp = matrix[i][j];
                matrix[i][j] = matrix[j][i];
                matrix[j][i] = temp;
            }
        }

        for(int i=0; i<n; i++){
            for(int j=0; j<n; j++){
                System.out.print(matrix[i][j]);
            }
            System.out.println();
        }

        for(int i=0; i<n; i++){
            for(int j=0; j<n/2; j++){
                int temp = matrix[i][j];
                matrix[i][j] = matrix[i][n-1-j];
                matrix[i][n-1-j] = temp;
            }
        }
    }
```
