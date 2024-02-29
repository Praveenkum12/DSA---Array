# DSA

Majority Element
java```
 public static int majorityElement(int[] arr) {
        int count = 0;
        int num = 0;
        int n = arr.length;
        for(int i = 0; i<arr.length; i++){
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
