### 최장 증가 수열 (LIS)란?
- 원소가 n개인 배열의 일부 원소를 골라내서 만든 부분 수열 중, 각 원소가 이전 원소보다 크다는 조건을 만족하고,
그 길이가 최대인 부분 수열을 최장 증가 부분 수열이라고 함.
- ex) [6,2,5,1,7,4,8,3] 이라는 배열이 있을 경우, LIS는 [2,5,7,9]이 됨

### 구현 방법 (시간복잡도)
1. DP : O(N^2)
2. Lower Bound: O(NlgN)

### 알고리즘 (DP)
아래에서 dp[i]는 i번째 인덱스에서 끝나는 최장 증가 부분 수열의 길이를 의미
```java
int arr[] = new int[]{6,2,5,1,7,4,8,3};
int dp[] = new int[arr.length];

for(int i=0; i<arr.length; i++){
    dp[i] = 1;
    for (int j=0;j<i;j++){
        if(arr[i]>arr[j]){
            dp[i] = Math.max(dp[i], dp[j]+1);
        }    
    }
}
```

### 알고리즘 설명 (DP)
- 배열 [6,2,5,1,7,4,8,3]이 초깃값
- i = 0 일때 dp[0] = 1이고 두번째 for문은 진입하지 않으므로 dp[0]=1
- i = 1 일때 dp[1] = 1이고 arr[0]>arr[1]이므로 두번째 for문 진입 X = > dp[1]=1
- i = 2 일때 dp[2] = 1이고 arr[0]>arr[2]이므로 dp[2] = 1, arr[1]<arr[2]이므로 dp[2] = max(dp[1]+1,dp[2]) => 2
- i = 3 일때 dp[3] = 1이고 이것보다 작은것이 앞에 없으므로 패스
- i = 4 일때 dp[4] = 1이고 arr[0]<arr[4] => dp[4] = 2, arr[1]<arr[4] => dp[4] = 2, arr[2]<arr[4] => dp[4]=3 ... dp[4]=3
- i = 5 일때 dp[5] = 1이고 arr[0]>arr[5] ... arr[1]<arr[5] => dp[5] = 2
- .....
- 결과 dp = [1,1,2,1,3,2,4,2]

### 알고리즘 (Lower Bound)
- DP 사용시 시간복잡도가 O(N^2)이므로 이것을 개선하기 위해 사용
- LIS의 형태를 유지하기 위해 주어진 배열의 인덱스를 하나씩 살펴보면서 그 숫자가 들어갈 위치를 이분탐색으로 탐색해서 넣는다.
- 이분 탐색의 경우 정확한 LIS가 아닌 LIS 길이를 구할 때 사용됨.

```java
private static int lowerBound(int[] arr, int value, int l, int r){
    while(l<r){
        int mid = (l+r)/2;
        if(value<=arr[mid]){
            r = mid;
        }else {
            l = mid + 1;
        }
    }
    return l;
}

public static void main(String[] args){
    int[] arr = new int[]{6, 2, 5, 1, 7, 4, 8, 3};
    int[] LIS = new int[arr.length];
    
    int cnt = 0;
    LIS[cnt++] = arr[0];
    for(int i=1;i<arr.length;i++){
        if (LIS[cnt - 1] < arr[i]) {
            LIS[cnt++] = arr[i];
        } else {
            int idx = lowerBound(LIS, arr[i], 0, cnt);
            LIS[idx] = arr[i];
        }
    }
}
```

### 알고리즘 설명 (LowerBound)
- 배열 [6,2,5,1,7,4,8,3]이 초깃값
- LIS[] 생성
- LIS[0] = 6
- i = 1 => 6 > 2 이므로 lowerBound() 호출하고 LIS[0] = 2로 바뀜
- i = 2 => 2 < 5 이므로 LIS[1] = 5
- i = 3 => 5 > 1 이므로 lowerBound() 호출하고 LIS[0] = 1로 바뀜
- i = 4 => 5 < 7 이므로 LIS[2] = 7
- i = 5 => 7 > 4 이므로 lowerBound() 호출하고 LIS[1] = 4로 바뀜
- i = 6 => 7 < 8 이므로 LIS[3] = 8
- i = 7 => 8 > 3 이므로 lowerBound() 호출하고 LIS[1] = 3로 바뀜
- 결과 LIS = [1,3,7,8]
- 결과적으로 가장 긴 LIS = 4