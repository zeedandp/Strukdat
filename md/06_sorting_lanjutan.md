# Materi Sorting

## Program Menghitung Waktu Sorting

Program berikut digunakan untuk membandingkan waktu sorting:

* Bubble Sort
* Selection Sort
* Insertion Sort
* Merge Sort
* Quick Sort

Dengan jumlah data:

* 100
* 200
* 300
* 400
* 500

---

## Source Code Sorting

```python
import random
import time

# Bubble Sort

def bubble_sort(arr):
    data = arr.copy()

    for i in range(len(data)):
        for j in range(0, len(data)-i-1):
            if data[j] > data[j+1]:
                data[j], data[j+1] = data[j+1], data[j]

    return data

# Selection Sort

def selection_sort(arr):
    data = arr.copy()

    for i in range(len(data)):
        min_idx = i

        for j in range(i+1, len(data)):
            if data[j] < data[min_idx]:
                min_idx = j

        data[i], data[min_idx] = data[min_idx], data[i]

    return data

# Insertion Sort

def insertion_sort(arr):
    data = arr.copy()

    for i in range(1, len(data)):
        key = data[i]
        j = i - 1

        while j >= 0 and key < data[j]:
            data[j + 1] = data[j]
            j -= 1

        data[j + 1] = key

    return data

# Merge Sort

def merge_sort(arr):
    if len(arr) <= 1:
        return arr

    mid = len(arr) // 2

    left = merge_sort(arr[:mid])
    right = merge_sort(arr[mid:])

    result = []
    i = j = 0

    while i < len(left) and j < len(right):
        if left[i] < right[j]:
            result.append(left[i])
            i += 1
        else:
            result.append(right[j])
            j += 1

    result.extend(left[i:])
    result.extend(right[j:])

    return result

# Quick Sort

def quick_sort(arr):
    if len(arr) <= 1:
        return arr

    pivot = arr[len(arr)//2]

    left = [x for x in arr if x < pivot]
    middle = [x for x in arr if x == pivot]
    right = [x for x in arr if x > pivot]

    return quick_sort(left) + middle + quick_sort(right)

# Pengujian waktu
sizes = [100, 200, 300, 400, 500]

for size in sizes:
    data = [random.randint(1, 1000) for _ in range(size)]

    print(f"\nJumlah Data : {size}")

    # Bubble Sort
    start = time.time()
    bubble_sort(data)
    end = time.time()
    print("Bubble Sort :", end-start, "detik")

    # Selection Sort
    start = time.time()
    selection_sort(data)
    end = time.time()
    print("Selection Sort :", end-start, "detik")

    # Insertion Sort
    start = time.time()
    insertion_sort(data)
    end = time.time()
    print("Insertion Sort :", end-start, "detik")

    # Merge Sort
    start = time.time()
    merge_sort(data)
    end = time.time()
    print("Merge Sort :", end-start, "detik")

    # Quick Sort
    start = time.time()
    quick_sort(data)
    end = time.time()
    print("Quick Sort :", end-start, "detik")
```

---