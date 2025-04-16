# Lecture 9 Sorting

# Bubble sort

**Bubble sort** repeatedly goes through the list, compares each adjacent pair, and swaps them if they are in the wrong order. 重复遍历数组，比较相邻两个元素，顺序不对则交

After each pass, the largest/smallest unsorted element "bubbles up" to its correct position at the end.

```java
for (int k = 1; k < list.length; k++) {
  for (int i = 0; i < list.length - k; i++) {
    if (list[i] > list[i + 1]) {
      // swap list[i] and list[i+1]
    }
  }
}
```

## Bubble Sort Optimization

If the list is already sorted or nearly sorted([1,2,3,4]), a regular bubble sort still performs unnecessary passes.

**Optimization**: Use a boolean flag `needNextPass`​. If no swap occurs during a pass, stop early.

```java
boolean needNextPass = true;
for (int k = 1; k < list.length && needNextPass; k++) {
  needNextPass = false;
  for (int i = 0; i < list.length - k; i++) {
    if (list[i] > list[i + 1]) {
      // swap
      needNextPass = true;
    }
  }
}
```

对于 `[1,2,3,4]`​，第一轮遍历没有任何交换，`needNextPass = false`​，排序提前结束。

## Bubble Sort Analysis

**Best case**

* The bubble sort algorithm needs just the **first pass** to determine the array is already sorted.
* During this first pass, it performs `n - 1`​ comparisons (each pair of adjacent elements)

  ‍
* So the **best-case time complexity is O(n)** .

.**Worst case**

Example: Initial list:`[5, 4, 3, 2, 1]`​

* **Pass 1:**  `[5, 4, 3, 2, 1] → [4, 3, 2, 1, 5]`​  
  → 4 comparisons (5 compared with 4, 3, 2, 1)
* **Pass 2:**  `[4, 3, 2, 1, 5] → [3, 2, 1, 4, 5]`​  
  → 3 comparisons
* **Pass 3:**  `[3, 2, 1, 4, 5] → [2, 1, 3, 4, 5]`​  
  → 2 comparisons
* **Pass 4:**  `[2, 1, 3, 4, 5] → [1, 2, 3, 4, 5]`​  
  → 1 comparison

🔢 Total comparisons: **4 + 3 + 2 + 1**  **=**  **10**

🧮 In general, for `n`​ elements, the worst-case comparison count is:

$$
(n - 1) + (n - 2) + ... + 2 + 1 = n(n - 1) / 2
$$

📌 Therefore, **worst-case time complexity is O(n²)** .

```java
public class BubbleSort {

    public static void bubbleSort(int[] list) {
        boolean needNextPass = true;

        for (int k = 1; k < list.length && needNextPass; k++) {
            // Array may be sorted and next pass not needed
            needNextPass = false;

            // Perform the kth pass
            for (int i = 0; i < list.length - k; i++) {
                if (list[i] > list[i + 1]) {
                    int temp = list[i];
                    list[i] = list[i + 1];
                    list[i + 1] = temp;

                    needNextPass = true; // Next pass still needed
                }
            }
        }
    }

    public static void main(String[] args) {
        int size = 100000;
        int[] a = new int[size];

        randomInitiate(a);

        long startTime = System.currentTimeMillis();
        bubbleSort(a);
        long endTime = System.currentTimeMillis();

        System.out.println((endTime - startTime) + "ms");
    }

    private static void randomInitiate(int[] a) {
        for (int i = 0; i < a.length; i++)
            a[i] = (int) (Math.random() * a.length);
    }
}

```

‍
