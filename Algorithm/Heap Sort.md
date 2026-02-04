```
제목: Heap Sort

작성일: 2026.02.04
작성자: 최한영
분류: 정렬 알고리즘
```

## 개념
    힙 자료구조를 이용해 최대값(또는 최소값)을 반복적으로 꺼내 정렬하는 알고리즘

    * 정의: 완전 이진 트리구조인 힙을 이용한 정렬
    * 최악 O(n log n) 보장
    * 추가 배열 없이 정렬 가능(In-place)
    * 핵심 특징
        * 완전 이진 트리
        * Max Heap 사용(오름차순 정렬 시)
        * 불안정 정렬

> 완전 이진 트리: 

## 복잡도

* 평균 시간 복잡도: O(n log n)
* 공간 복잡도: O(1)

## 동작 원리
1. 배열을 Max Heap으로 만든다.
2. 루트(최댓값)를 마지막 원소와 교환한다.
3. 힙 크기를 1 줄인다.
4. 다시 Heapify(재배열)한다.
5. 반복

## 장단점
* 장점
    * 최악 O(n log n) 보장
    * 추가 메모리 거의 없음
    * 재귀 없이 구현
* 단점
    * 불안정 정렬
    * 캐시 효율이 좋지 않음
    * 평균적으로 퀵 정렬보다 느림

> 캐시 효율: CPU 캐시는 연속된 메모리 블록을 통째로 캐시에 가져오는데 이를 공간 지역성이라고 함

> 효율이 좋은 경우: 메모리에 있는 배열을 순서대로 접근
> 힙은 한 번에 접근하는 자신과 자식들의 인덱스가 선형이 아님 2 > (5 6)


## 예제 코드
```java
import java.util.Arrays;

public class HeapSort {

    public static void heapSort(int[] arr) {
        int n = arr.length;

        // 1️⃣ Max Heap 구성 (bottom-up)
        for (int i = n / 2 - 1; i >= 0; i--) {
            heapify(arr, n, i);
        }

        // 2️⃣ 하나씩 루트 제거
        for (int i = n - 1; i > 0; i--) {

            // 루트(최댓값)와 마지막 원소 교환
            swap(arr, 0, i);

            // heap 크기 줄이고 heapify
            heapify(arr, i, 0);
        }
    }

    private static void heapify(int[] arr, int n, int i) {
        int largest = i;
        int left = 2 * i + 1;
        int right = 2 * i + 2;

        if (left < n && arr[left] > arr[largest]) {
            largest = left;
        }

        if (right < n && arr[right] > arr[largest]) {
            largest = right;
        }

        if (largest != i) {
            swap(arr, i, largest);
            heapify(arr, n, largest);
        }
    }

    private static void swap(int[] arr, int i, int j) {
        int temp = arr[i];
        arr[i] = arr[j];
        arr[j] = temp;
    }

    public static void main(String[] args) {
        int[] arr = {5, 3, 8, 4, 2};

        heapSort(arr);

        System.out.println(Arrays.toString(arr));
    }
}


```