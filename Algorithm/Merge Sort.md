```
제목: Merge Sort

작성일: 2026.02.04
작성자: 최한영
분류: 정렬 알고리즘
```
## 개념
    배열을 반으로 계속 나눈 뒤, 정렬하면서 다시 합치는 알고리즘

    * 정의: 분할 정복 기반의 정렬 알고리즘
    * O(n log n)을 보장하는 안정적인 정렬이 필요할 때 사용
    * 사용되는 상황: 대용량 데이터 정렬, 안정 정렬이 필요한 경우
    * 특징: 
        * 재귀
        * 안정 정렬 (Stable Sort)
        * 추가 메모리 필요


> 안정 정렬: 중복된 키값을 가진 요소들이 정렬 후에도 입력되었을 때 상대적인 순서를 그대로 유지 (삽입, 병합, 버블)

> 불안정 정렬: 중복된 키값을 가진 요소들의 상대적인 순서가 뒤바뀔 수 있음 (퀵, 선택, 힙)



## 복잡도

* 시간 복잡도: O(n log n)
* 공간 복잡도: O(n)


## 동작 원리

* 배열을 절반으로 나눈다.
* 더 이상 나눌 수 없을 때까지 재귀 호출한다.
* 두 배열을 비교하면서 정렬하여 병합한다.

## 장단점
* 장점
    * 항상 O(n log n) 보장
    * 안정 정렬
    * 큰 데이터에 적합
* 단점
    * 추가 메모리 필요O(n)
    * 재귀 호출로 인한 스택 사용

## 예제 코드

```java
import java.util.Arrays;

public class MergeSort {

    public static void mergeSort(int[] arr, int left, int right) {
        if (left >= right) return;

        int mid = (left + right) / 2;

        mergeSort(arr, left, mid);
        mergeSort(arr, mid + 1, right);

        merge(arr, left, mid, right);
    }

    public static void merge(int[] arr, int left, int mid, int right) {

        int[] temp = new int[right - left + 1];

        int i = left;       // 왼쪽 배열 시작
        int j = mid + 1;    // 오른쪽 배열 시작
        int k = 0;

        while (i <= mid && j <= right) {
            if (arr[i] <= arr[j]) {
                temp[k++] = arr[i++];
            } else {
                temp[k++] = arr[j++];
            }
        }

        while (i <= mid) {
            temp[k++] = arr[i++];
        }

        while (j <= right) {
            temp[k++] = arr[j++];
        }

        for (int t = 0; t < temp.length; t++) {
            arr[left + t] = temp[t];
        }
    }

    public static void main(String[] args) {
        int[] arr = {5, 3, 8, 4, 2};

        mergeSort(arr, 0, arr.length - 1);

        System.out.println(Arrays.toString(arr));
    }
}
```


