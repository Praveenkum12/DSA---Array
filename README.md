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
            int diff = sum - k;
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
### 10) Spiral Matrix
```
class Solution {
    public List<Integer> spiralOrder(int[][] arr) {
        List<Integer> list = new ArrayList<>();
        int n = arr.length;
        int m = arr[0].length;
        int top = 0, left = 0;
        int bottom = n-1, right = m-1;
        while(top<=bottom && left<=right){
            for(int i = left; i<=right; i++){
                list.add(arr[top][i]);
            }
            top++;
            for(int i = top; i<=bottom; i++){
                list.add(arr[i][right]);
            }
            right--;
            if(top<=bottom){
                for(int i=right; i>=left; i--){
                list.add(arr[bottom][i]);
                }
            }
            bottom--;
            if(left<=right){
                for(int i=bottom; i>=top; i--){
                list.add(arr[i][left]);
                }
            }
            left++;
        }
        return list;
    }
}
```
### 11) Count subarrays with given sum
```
class Solution {
    public int subarraySum(int[] arr, int k) {
        Map<Integer, Integer> map = new HashMap<>();
        int preSum = 0;
        int count = 0;
        map.put(0, 1);
        for(int el: arr){
            preSum += el;
            int diff = preSum - k;
            if(map.containsKey(diff)){
                count+=map.get(diff);
            }
            map.put(preSum, map.getOrDefault(preSum, 0)+1);
        }
        return count;
    }
}
```

# Array - HARD
### 1) Pascal Triangle
```
class Solution {
    public List<List<Integer>> generate(int n) {
        List<List<Integer>> list = new ArrayList<>();
        for(int i=1; i<=n; i++){
            list.add(nThRow(i));
        }
        return list;
    }

    private static List<Integer> nThRow(int n) {
        int ans = 1;
        List<Integer> list = new ArrayList<>();
        list.add(1);
        for(int i=1; i<n; i++){
            ans = ans * (n-i);
            ans = ans / i;
            list.add(ans);
        }

        return list;
    }
}
```
### 2) 	Majority Element (>N/3)
```
class Solution {
    public List<Integer> majorityElement(int[] arr) {
        List<Integer> list = new ArrayList<>();
        int el1 = 0, el2 = 0;
        int count1 = 0, count2 = 0;
        int n = arr.length;
        for(int i=0; i<n; i++){
            if(count1 == 0 && arr[i]!=el2){
                el1 = arr[i];
                count1++;
            }
            else if(count2 == 0 && arr[i]!=el1){
                el2 = arr[i];
                count2++;
            }
            else if(arr[i] == el1){
                count1++;
            }
            else if(arr[i] == el2){
                count2++;
            }
            else {
                count1--;
                count2--;
            }
        }

        count1 = 0;
        count2 = 0;

        for(int val: arr){
            if(val == el1){
                count1++;
            } else if(val == el2){
                count2++;
            }
        }

        if(count1 > n/3){
            list.add(el1);
        }
        if(count2 > n/3){
            list.add(el2);
        }
        return list;
    }
}
```
### 3) 3 Sum
```
class Solution {
    public List<List<Integer>> threeSum(int[] arr) {
       int n = arr.length;
        Arrays.sort(arr);
        Set<List<Integer>> set = new HashSet<>();
        for(int i=0; i<n; i++){
            int j = i+1;
            int k = n-1;
            while(j<k){
                int sum = arr[i]+arr[j]+arr[k];
                if(sum<0){
                    j++;
                }
                else if(sum>0){
                    k--;
                }
                else{
                    List<Integer> list = new ArrayList<>();
                    list.add(arr[i]);
                    list.add(arr[j]);
                    list.add(arr[k]);
                    set.add(list);
                    j++;
                    k--;
                    while(j<k && arr[j]==arr[j-1]) j++;
                    while(j<k && arr[k]==arr[k+1]) k--;
                }
            }
        }

        List<List<Integer>> ans = new ArrayList<>();
        for(List<Integer> lis: set){
            ans.add(lis);
        }
        return ans; 
    }
}
```
### 4) 4 Sum
```
public static  List<List<Integer>> fourSum(int[] arr, int target) {
        int n = arr.length;
        Arrays.sort(arr);
        Set<List<Integer>> set = new HashSet<>();
        for(int i=0; i<n; i++){
            if (i > 0 && (arr[i] == arr[i - 1])) continue;
            for(int j=i+1; j<n; j++){
                if (j > i + 1 && (arr[j] == arr[j - 1])) continue;
                int k = j+1;
                int l = n-1;
                while(k<l){
                    long sum = arr[i] + arr[j] + arr[k] + arr[l];
                    if(sum < target){
                        k++;
                    }
                    else if(sum > target){
                        l--;
                    }
                    else {
                        List<Integer> list = new ArrayList<>();
                        list.add(arr[i]);
                        list.add(arr[j]);
                        list.add(arr[k]);
                        list.add(arr[l]);
                        set.add(list);
                        k++;
                        l--;
                        while(k<l && arr[k]==arr[k-1]) k++;
                        while(k<l && arr[l]==arr[l+1]) l--;
                    }
                }
            }
        }

        List<List<Integer>> ans = new ArrayList<>();
        for(List<Integer> lis: set){
            ans.add(lis);
        }

        return ans;
    }
```
### 5) Count the number of subarrays with given xor K
```
public class Solution {
    public static int subarraysWithSumK(int []arr, int target) {
        int preSum = 0;
        int count = 0;
        int n = arr.length;
        Map<Integer, Integer> map = new HashMap<>();
        map.put(0,1);
        for(int i=0; i<n; i++){
            preSum ^= arr[i];
            int diff = preSum ^ target;
            if(map.containsKey(diff)){
                count += map.get(diff);
            }
            map.put(preSum, map.getOrDefault(preSum, 0)+1);
        }
        return count;
    }
}
```
### 6) Merge Intervals
```
class Solution {
    public int[][] merge(int[][] arr) {
        Arrays.sort(arr, new Comparator<int[]>() {
            public int compare(int[] a, int[] b) {
                return a[0] - b[0];
            }
        });
        int n = arr.length;
        List<int[]> list = new ArrayList<>();
        for(int i=0; i<n; i++){
            int[] tempInt = arr[i];
            int start = tempInt[0];
            int end = tempInt[1];
            int j = i+1;
            while(j<n && arr[j][0]<=end){
                if(arr[j][1] > end) end = arr[j][1];
                if(arr[j][0] < start) start = arr[j][0];
                j++;
            }
            tempInt[0] = start;
            tempInt[1] = end;
            list.add(tempInt);
            i = j-1;
        }
        int[][] ans = new int[list.size()][];
        int i = 0;
        for(int[] el: list){
            ans[i] = el;
            i++;
        }
        return ans;
    }
}
```
### 7) Merge Two sorted Arrays withoud extra space
```
public static void mergeTwoSortedArraysWithoutExtraSpace(long []arr1, long []arr2){
	int i= arr1.length - 1;
	int j= 0;
	
	while(i>0 && j<arr2.length && arr1[i] > arr2[j]){
	    long temp = arr1[i];
	    arr1[i] = arr2[j];
	    arr2[j] = temp;
	
	    i--;
	    j++;
	}
	
	Arrays.sort(arr1);
	Arrays.sort(arr2);
}
```
### 8) Finding repeated and missing number
```
public static int[] findMissingRepeatingNumbers(int []arr) {
        long sum = 0, sumSqr = 0;
        long n = arr.length;
        for(int val: arr){
            sum += (long)val;
            sumSqr += (long)val * (long)val;
        }
        long specSum = n * (n+1) / 2;
        long specSumSqr = n * (n+1) * (2 * n + 1) / 6;
        long eq1 = sum - specSum;
        long eq2 = (sumSqr - specSumSqr) / eq1;
        long x = (eq1 + eq2) / 2;
        long y = eq2  - x;
        int[] b = new int[2];
        b[0] = (int)x;
        b[1] = (int)y;
        return b;
}
```
### 9) Number of inversions
```
public class Solution {
    public static int numberOfInversions(int []arr, int n) {
        return mergeSort(arr, 0, n-1);
    }

    public static int mergeSort(int arr[], int low, int high){
        int count = 0;
        if(low == high){
            return count;
        }
        int mid = (low + high) / 2;
        count += mergeSort(arr, low, mid);
        count += mergeSort(arr, mid+1, high);
        return merg(arr, low, mid, high, count);
    }

    private static int merg(int[] arr, int low, int mid, int high, int count) {
        int i = low;
        int j = mid+1;
        List<Integer> list = new ArrayList<>();

        while(i<=mid && j<=high){
            if(arr[i] <= arr[j]){
                list.add(arr[i]);
                i++;
            }
            else {
                list.add(arr[j]);
                count += mid - i + 1;
                j++;
            }
        }

        while(i<=mid){
            list.add(arr[i]);
            i++;
        }

        while(j<=high){
            list.add(arr[j]);
            j++;
        }

        for (int x = low; x <= high; x++) {
            arr[x] = list.get(x - low);
        }

        return count;
    }
}
```
### 10) Reverse Pair - (Time: O(2n.logn))
```
public class Solution {
    public static int team(int []arr, int n){
        return mergeSort(arr, 0, n-1);
    }

     public static int mergeSort(int[] arr, int low, int high){
        int count =0;
        if(low == high){
            return 0;
        }
        int mid = (low + high) / 2;
        count += mergeSort(arr, low, mid);
        count += mergeSort(arr, mid+1, high);
        count += countPairs(arr, low, mid, high);
        merge(arr, low, mid, high);
        return count;
    }

    private static int countPairs(int[] arr, int low, int mid, int high){
        int right = mid+1;
        int count = 0;
        for(int i=low; i<=mid; i++){
            while(right <= high && arr[i] > 2*arr[right]){
                right++;
            }
            count += right - (mid+1);
        }
        return count;
    }

    public static void merge(int[] arr, int low, int mid, int high){
        int i = low;
        int j = mid+1;
        List<Integer> list = new ArrayList<>();
        while(i<=mid && j<=high){
            if(arr[i] <= arr[j]){
                list.add(arr[i]);
                i++;
            } else {
                list.add(arr[j]);
                j++;
            }
        }

        while(i<=mid){
            list.add(arr[i]);
            i++;
        }

        while(j<=high){
            list.add(arr[j]);
            j++;
        }

        for(int x=low; x<=high; x++){
            arr[x] = list.get(x - low);
        }
    }
}
```
### 11) Maximum Product Subarray
```
class Solution {
    public int maxProduct(int[] arr) {
        int max = Integer.MIN_VALUE;
        int prefix = 1, suffix = 1;
        int n = arr.length;
        for(int i=0; i<n; i++){
            prefix = prefix * arr[i];
            suffix = suffix * arr[n-i-1];

            max = Math.max(max, prefix);
            max = Math.max(max, suffix);

            if(prefix == 0){
                prefix = 1;
            }
            if(suffix == 0){
                suffix = 1;
            }
        }
        return max;
    }
}
```

