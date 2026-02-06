```
Title: Quick Sort

Date: 2026.02.04
Author: 최한영
Category: 정렬 알고리즘
```

## 개념
    기준값(Pivot)을 정해서 작은 값과 큰 값을 나누는 정렬

    * 정의: Pivot을 기준으로 배열을 분할하며 정렬하는 분할 정복 알고리즘
    * 평균적으로 매우 빠름
    * 추가 메모리를 거의 사용하지 않음
    * 핵심 특징
        * 평균 O(n log n)
        * 최악 O(n²)
        * In-place 정렬 가능
        * 불안정 정렬


> In-place 정렬: 추가적인 메모리 공간을 사용하지 않고 입력받은 배열 안에서 요소들의 위치를 직접 바꿔서 정렬하는 방식
> 메모리가 부족한 임베디드 등에서 유리


## 복잡도

* 평균 시간 복잡도: O(n log n)
* 최악 시간 복잡도: O(n²)
* 공간 복잡도: O(log n)(재귀 스택)

## 동작 원리
1. Pivot 선택
2. Pivot보다 작은 값은 왼쪽
3. Pivot보다 큰 값은 오른쪽
4. 좌우를 재귀적으로 반복

## 장단점
* 장점
  * 평균적으로 가장 빠른 정렬
  * 추가 배열이 필요 없음
  * 캐시 친화적
  
* 단점
  * 최악 O(n²)
  * 안정 정렬 아님
  * pivot 선택에 따라 성능 크게 영향

## 예제 코드
```java
import java.util.Arrays;

public class QuickSort {

    public static void quickSort(int[] arr, int left, int right) {
        if (left >= right) return;

        int pivotIndex = partition(arr, left, right);

        quickSort(arr, left, pivotIndex - 1);
        quickSort(arr, pivotIndex + 1, right);
    }

    private static int partition(int[] arr, int left, int right) {

        int pivot = arr[right];   // 마지막 원소를 pivot
        int i = left - 1;

        for (int j = left; j < right; j++) {
            if (arr[j] <= pivot) {
                i++;
                swap(arr, i, j);
            }
        }

        swap(arr, i + 1, right);
        return i + 1;
    }

    private static void swap(int[] arr, int i, int j) {
        int temp = arr[i];
        arr[i] = arr[j];
        arr[j] = temp;
    }

    public static void main(String[] args) {
        int[] arr = {5, 3, 8, 4, 2};

        quickSort(arr, 0, arr.length - 1);

        System.out.println(Arrays.toString(arr));
    }
}

```