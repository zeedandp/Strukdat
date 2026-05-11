# Sorting Algorithms (Algoritma Pengurutan)

## Pengertian Sorting

Sorting adalah proses mengatur kumpulan data dalam urutan tertentu (ascending atau descending). Sorting merupakan salah satu operasi fundamental dalam ilmu komputer yang banyak digunakan dalam aplikasi praktis.

## Pentingnya Sorting

1. **Pencarian Lebih Cepat**: Data terurut memungkinkan pencarian binary search yang lebih cepat
2. **Analisis Data**: Memudahkan interpretasi dan analisis data
3. **Presentasi**: Meningkatkan readability data
4. **Optimisasi**: Banyak algoritma memerlukan data yang terurut
5. **Aplikasi Praktis**: Digunakan di database, search engines, file systems

## Sorting 1: Bubble Sort

### Pengertian

Bubble Sort membandingkan elemen bersebelahan dan menukarnya jika urutan salah. Proses diulang hingga seluruh array terurut. Nilai terbesar "menggelembung" ke posisi akhirnya pada setiap iterasi.

### Algoritma

```
1. Mulai dari indeks 0
2. Bandingkan elemen i dengan i+1
3. Jika tidak sesuai urutan (arr[i] > arr[i+1]), tukar
4. Lanjut ke elemen berikutnya
5. Ulangi untuk setiap pass hingga tidak ada perubahan
6. Setelah setiap pass, elemen terbesar sudah pada posisinya
```

### Implementasi Python

#### 1. Bubble Sort Sederhana (Basic)

```python
def bubble_sort_simple(arr):
    """Bubble sort versi paling sederhana"""
    n = len(arr)

    for i in range(n):
        for j in range(n - 1):
            if arr[j] > arr[j + 1]:
                arr[j], arr[j + 1] = arr[j + 1], arr[j]

    return arr

# Test
arr = [64, 34, 25, 12]
print(bubble_sort_simple(arr))  # Output: [12, 25, 34, 64]
```

#### 2. Bubble Sort dengan Optimasi (Optimized)

```python
def bubble_sort(arr):
    """Bubble sort dengan early termination"""
    n = len(arr)

    for i in range(n):
        swapped = False

        # Compare adjacent elements
        for j in range(0, n - i - 1):
            if arr[j] > arr[j + 1]:
                # Swap
                arr[j], arr[j + 1] = arr[j + 1], arr[j]
                swapped = True

        # Jika tidak ada perubahan, array sudah terurut
        if not swapped:
            break

    return arr

# Test
arr = [64, 34, 25, 12, 22, 11, 90]
print(bubble_sort(arr))  # Output: [11, 12, 22, 25, 34, 64, 90]
```

#### 3. Bubble Sort Descending (Menurun)

```python
def bubble_sort_descending(arr):
    """Bubble sort descending (menurun)"""
    n = len(arr)

    for i in range(n):
        swapped = False

        for j in range(0, n - i - 1):
            if arr[j] < arr[j + 1]:  # Rubah ke < untuk descending
                arr[j], arr[j + 1] = arr[j + 1], arr[j]
                swapped = True

        if not swapped:
            break

    return arr

# Test
arr = [64, 34, 25, 12]
print(bubble_sort_descending(arr))  # Output: [64, 34, 25, 12]
```

#### 4. Bubble Sort dengan Custom Comparator

```python
def bubble_sort_custom(arr, reverse=False):
    """Bubble sort dengan parameter reverse"""
    n = len(arr)

    for i in range(n):
        swapped = False

        for j in range(0, n - i - 1):
            if reverse:
                condition = arr[j] < arr[j + 1]
            else:
                condition = arr[j] > arr[j + 1]

            if condition:
                arr[j], arr[j + 1] = arr[j + 1], arr[j]
                swapped = True

        if not swapped:
            break

    return arr

# Test
arr = [64, 34, 25, 12]
print(bubble_sort_custom(arr))           # [12, 25, 34, 64]
print(bubble_sort_custom(arr, True))     # [64, 34, 25, 12]
```

#### 5. Bubble Sort untuk Object/Dict

```python
def bubble_sort_objects(data, key=None):
    """Bubble sort untuk list of dictionaries"""
    n = len(data)

    for i in range(n):
        swapped = False

        for j in range(0, n - i - 1):
            if key:
                condition = data[j][key] > data[j + 1][key]
            else:
                condition = data[j] > data[j + 1]

            if condition:
                data[j], data[j + 1] = data[j + 1], data[j]
                swapped = True

        if not swapped:
            break

    return data

# Test
students = [
    {"name": "Alice", "score": 85},
    {"name": "Bob", "score": 92},
    {"name": "Charlie", "score": 78}
]

# Sort by score
result = bubble_sort_objects(students, key="score")
for student in result:
    print(f"{student['name']}: {student['score']}")
# Output: Charlie: 78, Alice: 85, Bob: 92
```

#### 6. Bubble Sort dengan Return Info (Debug)

```python
def bubble_sort_debug(arr):
    """Bubble sort dengan informasi detail"""
    n = len(arr)
    comparisons = 0
    swaps = 0
    passes = 0

    for i in range(n):
        passes += 1
        swapped = False

        for j in range(0, n - i - 1):
            comparisons += 1
            if arr[j] > arr[j + 1]:
                arr[j], arr[j + 1] = arr[j + 1], arr[j]
                swaps += 1
                swapped = True

        if not swapped:
            break

    return arr, {
        "comparisons": comparisons,
        "swaps": swaps,
        "passes": passes
    }

# Test
arr = [64, 34, 25, 12]
sorted_arr, info = bubble_sort_debug(arr)
print(f"Sorted: {sorted_arr}")
print(f"Info: {info}")
# Output: Sorted: [12, 25, 34, 64]
#         Info: {'comparisons': 6, 'swaps': 6, 'passes': 4}
```

### Contoh Proses (Array: [64, 34, 25, 12])

```
Pass 1:
Compare 64 & 34 -> 34, 64 (swap)
Compare 64 & 25 -> 25, 64 (swap)
Compare 64 & 12 -> 12, 64 (swap)
Result: [34, 25, 12, 64]

Pass 2:
Compare 34 & 25 -> 25, 34 (swap)
Compare 34 & 12 -> 12, 34 (swap)
Result: [25, 12, 34, 64]

Pass 3:
Compare 25 & 12 -> 12, 25 (swap)
Result: [12, 25, 34, 64]

Pass 4:
No swaps needed
Result: [12, 25, 34, 64] ✓ Sorted
```

### Kompleksitas

| Aspek            | Nilai                          |
| ---------------- | ------------------------------ |
| Best Case        | O(n) - array sudah terurut     |
| Average Case     | O(n²)                          |
| Worst Case       | O(n²) - array terurut terbalik |
| Space Complexity | O(1) - in-place                |

### Karakteristik

- **Stable**: ✓ (mempertahankan urutan elemen yang sama)
- **In-place**: ✓ (tidak perlu array tambahan)
- **Adaptif**: ✓ (lebih cepat jika data sudah terurut)
- **Simpler**: ✓ (mudah dipahami dan diimplementasikan)

### Keuntungan dan Kelemahan

**Keuntungan:**

- Implementasi sangat sederhana
- Tidak memerlukan ruang tambahan
- Stabil dan efisien untuk data kecil
- Bisa mendeteksi jika data sudah terurut

**Kelemahan:**

- Performa buruk untuk data besar (O(n²))
- Banyak operasi perbandingan dan penukaran
- Tidak cocok untuk dataset production

---

## Sorting 2: Selection Sort & Insertion Sort

### A. Selection Sort

#### Pengertian

Selection Sort membagi array menjadi dua bagian: sorted dan unsorted. Setiap iterasi memilih elemen terkecil dari bagian unsorted dan memindahkannya ke akhir bagian sorted.

#### Algoritma

```
1. Mulai dengan array yang belum terurut
2. Temukan elemen terkecil di array yang belum disort
3. Tukarkan dengan elemen pertama dari bagian unsorted
4. Pindahkan batas antara sorted dan unsorted ke kanan satu posisi
5. Ulangi sampai seluruh array terurut
```

#### Implementasi Python

##### 1. Selection Sort Sederhana

```python
def selection_sort_simple(arr):
    """Selection sort versi sederhana"""
    n = len(arr)

    for i in range(n):
        min_idx = i

        for j in range(i + 1, n):
            if arr[j] < arr[min_idx]:
                min_idx = j

        # Tukar
        arr[i], arr[min_idx] = arr[min_idx], arr[i]

    return arr

# Test
arr = [64, 34, 25, 12]
print(selection_sort_simple(arr))  # Output: [12, 25, 34, 64]
```

##### 2. Selection Sort dengan Tracking

```python
def selection_sort(arr):
    """Selection sort"""
    n = len(arr)

    for i in range(n):
        # Cari elemen minimum dari posisi i ke akhir
        min_idx = i
        for j in range(i + 1, n):
            if arr[j] < arr[min_idx]:
                min_idx = j

        # Tukar elemen ke posisi i
        if i != min_idx:
            arr[i], arr[min_idx] = arr[min_idx], arr[i]

    return arr

# Test
arr = [64, 34, 25, 12, 22, 11, 90]
print(selection_sort(arr))  # Output: [11, 12, 22, 25, 34, 64, 90]
```

##### 3. Selection Sort Descending

```python
def selection_sort_descending(arr):
    """Selection sort descending"""
    n = len(arr)

    for i in range(n):
        max_idx = i  # Cari MAKSIMUM bukan minimum

        for j in range(i + 1, n):
            if arr[j] > arr[max_idx]:  # Ubah ke >
                max_idx = j

        arr[i], arr[max_idx] = arr[max_idx], arr[i]

    return arr

# Test
arr = [64, 34, 25, 12]
print(selection_sort_descending(arr))  # Output: [64, 34, 25, 12]
```

##### 4. Selection Sort dengan Debug Info

```python
def selection_sort_debug(arr):
    """Selection sort dengan tracking"""
    n = len(arr)
    comparisons = 0
    swaps = 0
    steps = []

    for i in range(n):
        min_idx = i

        for j in range(i + 1, n):
            comparisons += 1
            if arr[j] < arr[min_idx]:
                min_idx = j

        if i != min_idx:
            arr[i], arr[min_idx] = arr[min_idx], arr[i]
            swaps += 1
            steps.append(f"Swap position {i} and {min_idx}: {arr}")

    return arr, {
        "comparisons": comparisons,
        "swaps": swaps,
        "steps": steps
    }

# Test
arr = [64, 34, 25, 12]
sorted_arr, info = selection_sort_debug(arr.copy())
print(f"Sorted: {sorted_arr}")
print(f"Swaps: {info['swaps']}")
for step in info['steps']:
    print(f"  {step}")
```

##### 5. Selection Sort untuk Object

```python
def selection_sort_objects(data, key=None, reverse=False):
    """Selection sort untuk list of dictionaries"""
    n = len(data)

    for i in range(n):
        extremum_idx = i

        for j in range(i + 1, n):
            if key:
                val_extremum = data[extremum_idx][key]
                val_j = data[j][key]
            else:
                val_extremum = data[extremum_idx]
                val_j = data[j]

            if reverse:
                condition = val_j > val_extremum
            else:
                condition = val_j < val_extremum

            if condition:
                extremum_idx = j

        data[i], data[extremum_idx] = data[extremum_idx], data[i]

    return data

# Test
students = [
    {"name": "Alice", "score": 85},
    {"name": "Bob", "score": 92},
    {"name": "Charlie", "score": 78}
]

result = selection_sort_objects(students, key="score")
for s in result:
    print(f"{s['name']}: {s['score']}")
```

##### 6. Selection Sort dengan Custom Comparator

```python
class Student:
    def __init__(self, name, score):
        self.name = name
        self.score = score

    def __repr__(self):
        return f"{self.name}({self.score})"

def selection_sort_class(arr, compare=None):
    """Selection sort dengan custom comparator"""
    n = len(arr)

    for i in range(n):
        min_idx = i

        for j in range(i + 1, n):
            if compare:
                if compare(arr[j], arr[min_idx]):
                    min_idx = j
            else:
                if arr[j] < arr[min_idx]:
                    min_idx = j

        arr[i], arr[min_idx] = arr[min_idx], arr[i]

    return arr

# Test
students = [
    Student("Alice", 85),
    Student("Bob", 92),
    Student("Charlie", 78)
]

# Sort by score
result = selection_sort_class(students, lambda a, b: a.score < b.score)
print(result)  # [Charlie(78), Alice(85), Bob(92)]
#### Contoh Proses (Array: [64, 34, 25, 12])

```

Pass 1: Min = 12 (index 3)
Tukar dengan 64: [12, 34, 25, 64]

Pass 2: Min = 25 (index 2)
Tukar dengan 34: [12, 25, 34, 64]

Pass 3: Min = 34 (index 2)
Tidak perlu tukar: [12, 25, 34, 64]

Pass 4: Done
Result: [12, 25, 34, 64] ✓ Sorted

```

#### Kompleksitas

| Aspek            | Nilai           |
| ---------------- | --------------- |
| Best Case        | O(n²)           |
| Average Case     | O(n²)           |
| Worst Case       | O(n²)           |
| Space Complexity | O(1) - in-place |

#### Karakteristik

- **Stable**: ✗ (bisa mengubah urutan elemen yang sama)
- **In-place**: ✓ (tidak perlu array tambahan)
- **Adaptif**: ✗ (selalu O(n²) regardless data)
- **Jumlah swap minimal**: ✓ (hanya O(n) swaps)

#### Keuntungan dan Kelemahan

**Keuntungan:**

- Jumlah penukaran minimal (O(n))
- Sederhana untuk diimplementasikan
- Performa konsisten
- Efisien untuk memory writes

**Kelemahan:**

- Performa buruk untuk data besar (O(n²))
- Tidak stabil
- Harus check seluruh array pada setiap iterasi

---

### B. Insertion Sort

#### Pengertian

Insertion Sort membangun array sorted satu elemen pada satu waktu. Mirip dengan cara mengurutkan kartu di tangan - kita ambil kartu satu per satu dan sisipkan pada posisi yang benar.

#### Algoritma

```

1. Mulai dari elemen kedua (index 1)
2. Simpan elemen saat ini sebagai key
3. Bandingkan dengan elemen sebelumnya
4. Geser elemen yang lebih besar ke kanan
5. Sisipkan key di posisi yang benar
6. Ulangi untuk semua elemen

````

#### Implementasi Python

##### 1. Insertion Sort Sederhana

```python
def insertion_sort_simple(arr):
    """Insertion sort versi sederhana"""
    for i in range(1, len(arr)):
        key = arr[i]
        j = i - 1

        while j >= 0 and arr[j] > key:
            arr[j + 1] = arr[j]
            j -= 1

        arr[j + 1] = key

    return arr

# Test
arr = [64, 34, 25, 12]
print(insertion_sort_simple(arr))  # Output: [12, 25, 34, 64]
````

##### 2. Insertion Sort Standar

```python
def insertion_sort(arr):
    """Insertion sort"""
    n = len(arr)

    for i in range(1, n):
        key = arr[i]  # Elemen yang akan diinsert
        j = i - 1

        # Geser elemen yang lebih besar ke kanan
        while j >= 0 and arr[j] > key:
            arr[j + 1] = arr[j]
            j -= 1

        # Insert key pada posisi yang benar
        arr[j + 1] = key

    return arr

# Test
arr = [64, 34, 25, 12, 22, 11, 90]
print(insertion_sort(arr))  # Output: [11, 12, 22, 25, 34, 64, 90]
```

##### 3. Insertion Sort Descending

```python
def insertion_sort_descending(arr):
    """Insertion sort descending"""
    n = len(arr)

    for i in range(1, n):
        key = arr[i]
        j = i - 1

        while j >= 0 and arr[j] < key:  # Ubah ke <
            arr[j + 1] = arr[j]
            j -= 1

        arr[j + 1] = key

    return arr

# Test
arr = [64, 34, 25, 12]
print(insertion_sort_descending(arr))  # Output: [64, 34, 25, 12]
```

##### 4. Insertion Sort dengan Debug

```python
def insertion_sort_debug(arr):
    """Insertion sort dengan tracking detail"""
    n = len(arr)
    comparisons = 0
    shifts = 0
    steps = []

    for i in range(1, n):
        key = arr[i]
        j = i - 1
        steps.append(f"Insert key={key} at position {i}")

        while j >= 0 and arr[j] > key:
            comparisons += 1
            arr[j + 1] = arr[j]
            shifts += 1
            j -= 1
            steps.append(f"  Shift: {arr}")

        arr[j + 1] = key
        steps.append(f"  Place key: {arr}")

    return arr, {
        "comparisons": comparisons,
        "shifts": shifts,
        "steps": steps
    }

# Test
arr = [64, 34, 25, 12]
sorted_arr, info = insertion_sort_debug(arr.copy())
print(f"Sorted: {sorted_arr}")
print(f"Comparisons: {info['comparisons']}, Shifts: {info['shifts']}")
```

##### 5. Insertion Sort untuk String

```python
def insertion_sort_strings(arr, reverse=False):
    """Insertion sort untuk string array"""
    n = len(arr)

    for i in range(1, n):
        key = arr[i]
        j = i - 1

        if reverse:
            while j >= 0 and arr[j] < key:
                arr[j + 1] = arr[j]
                j -= 1
        else:
            while j >= 0 and arr[j] > key:
                arr[j + 1] = arr[j]
                j -= 1

        arr[j + 1] = key

    return arr

# Test
words = ["zebra", "apple", "mango", "banana"]
print(insertion_sort_strings(words))         # [apple, banana, mango, zebra]
print(insertion_sort_strings(words, True))   # [zebra, mango, banana, apple]
```

##### 6. Insertion Sort untuk Object

```python
def insertion_sort_objects(data, key=None, reverse=False):
    """Insertion sort untuk list of dictionaries"""
    n = len(data)

    for i in range(1, n):
        curr = data[i]
        j = i - 1

        while j >= 0:
            if key:
                compare_val = data[j][key]
                curr_val = curr[key]
            else:
                compare_val = data[j]
                curr_val = curr

            if reverse:
                condition = compare_val < curr_val
            else:
                condition = compare_val > curr_val

            if condition:
                data[j + 1] = data[j]
                j -= 1
            else:
                break

        data[j + 1] = curr

    return data

# Test
students = [
    {"name": "Alice", "score": 85},
    {"name": "Bob", "score": 92},
    {"name": "Charlie", "score": 78}
]

result = insertion_sort_objects(students, key="score")
for s in result:
    print(f"{s['name']}: {s['score']}")
# Output: Charlie: 78, Alice: 85, Bob: 92
```

##### 7. Insertion Sort dengan Binary Search (Kompleks)

```python
def binary_search(arr, key, start, end):
    """Cari posisi insert menggunakan binary search"""
    if start == end:
        return start if arr[start] > key else start + 1

    if start > end:
        return start

    mid = (start + end) // 2

    if arr[mid] < key:
        return binary_search(arr, key, mid + 1, end)
    elif arr[mid] > key:
        return binary_search(arr, key, start, mid - 1)
    else:
        return mid

def insertion_sort_binary(arr):
    """Insertion sort dengan binary search untuk menemukan posisi"""
    n = len(arr)

    for i in range(1, n):
        key = arr[i]

        # Cari posisi dengan binary search
        pos = binary_search(arr, key, 0, i - 1)

        # Geser elemen
        for j in range(i - 1, pos - 1, -1):
            arr[j + 1] = arr[j]

        arr[pos] = key

    return arr

# Test
arr = [64, 34, 25, 12, 22]
print(insertion_sort_binary(arr))  # Output: [12, 22, 25, 34, 64]
```

##### 8. Insertion Sort Hybrid (Multiple Keys)

```python
def insertion_sort_multi_key(data, keys):
    """Insertion sort dengan multiple keys (tuple comparison)"""
    n = len(data)

    for i in range(1, n):
        key = data[i]
        j = i - 1

        while j >= 0:
            # Bandingkan multiple keys
            compare = tuple(key.get(k) for k in keys)
            current = tuple(data[j].get(k) for k in keys)

            if current > compare:
                data[j + 1] = data[j]
                j -= 1
            else:
                break

        data[j + 1] = key

    return data

# Test
students = [
    {"dept": "CS", "year": 3, "name": "Alice"},
    {"dept": "CS", "year": 2, "name": "Bob"},
    {"dept": "EE", "year": 3, "name": "Charlie"},
    {"dept": "CS", "year": 3, "name": "David"}
]

result = insertion_sort_multi_key(students, ["dept", "year", "name"])
for s in result:
    print(f"{s['dept']} Year {s['year']}: {s['name']}")
#### Contoh Proses (Array: [64, 34, 25, 12])

```

Initial: [64, 34, 25, 12]
Sorted: [64] Unsorted: [34, 25, 12]

i=1: key=34
34 < 64, geser 64 ke kanan
Result: [34, 64, 25, 12]
Sorted: [34, 64]

i=2: key=25
25 < 64, geser 64 ke kanan
25 < 34, geser 34 ke kanan
Result: [25, 34, 64, 12]
Sorted: [25, 34, 64]

i=3: key=12
12 < 64, geser 64 ke kanan
12 < 34, geser 34 ke kanan
12 < 25, geser 25 ke kanan
Result: [12, 25, 34, 64]
Sorted: [12, 25, 34, 64] ✓

````

#### Kompleksitas

| Aspek            | Nilai                          |
| ---------------- | ------------------------------ |
| Best Case        | O(n) - array sudah terurut     |
| Average Case     | O(n²)                          |
| Worst Case       | O(n²) - array terurut terbalik |
| Space Complexity | O(1) - in-place                |

#### Karakteristik

- **Stable**: ✓ (mempertahankan urutan elemen yang sama)
- **In-place**: ✓ (tidak perlu array tambahan)
- **Adaptif**: ✓ (lebih cepat jika data sudah terurut, O(n))
- **Online**: ✓ (bisa mengurutkan data seiring diterimanya)

#### Keuntungan dan Kelemahan

**Keuntungan:**

- Sangat efisien untuk data kecil atau semi-terurut
- Stabil dan in-place
- Sederhana untuk diimplementasikan
- Baik untuk array yang hampir terurut
- Cocok untuk digunakan dalam Timsort hybrid sort

**Kelemahan:**

- Performa buruk untuk data besar (O(n²))
- Banyak pergeseran elemen

---

## Perbandingan Ketiga Algoritma

### Kompleksitas

| Algoritma      | Best  | Average | Worst | Space |
| -------------- | ----- | ------- | ----- | ----- |
| Bubble Sort    | O(n)  | O(n²)   | O(n²) | O(1)  |
| Selection Sort | O(n²) | O(n²)   | O(n²) | O(1)  |
| Insertion Sort | O(n)  | O(n²)   | O(n²) | O(1)  |

### Karakteristik

| Algoritma      | Stable | In-place | Adaptif | Jumlah Swap |
| -------------- | ------ | -------- | ------- | ----------- |
| Bubble Sort    | ✓      | ✓        | ✓       | Banyak      |
| Selection Sort | ✗      | ✓        | ✗       | Minimal     |
| Insertion Sort | ✓      | ✓        | ✓       | Medium      |

### Kapan Menggunakan?

| Situasi                  | Algoritma                       |
| ------------------------ | ------------------------------- |
| Data kecil (≤ 50 elemen) | Insertion Sort > Bubble Sort    |
| Data hampir terurut      | Insertion Sort                  |
| Data acak                | Selection Sort (minimal swap)   |
| Perlu stabil             | Bubble Sort atau Insertion Sort |
| Perlu minimal swap       | Selection Sort                  |
| Learning purpose         | Bubble Sort                     |

---

## Contoh Program Lengkap & Aplikasi Praktis

### 1. Sorting dengan Debug & Visualisasi

```python
def bubble_sort_debug(arr):
    """Bubble sort dengan debugging info"""
    n = len(arr)
    print(f"Array awal: {arr}\n")

    for i in range(n):
        print(f"Pass {i+1}:")
        swapped = False

        for j in range(0, n - i - 1):
            if arr[j] > arr[j + 1]:
                arr[j], arr[j + 1] = arr[j + 1], arr[j]
                swapped = True
                print(f"  Swap {arr[j+1]} dan {arr[j]}: {arr}")

        if not swapped:
            print("  No swaps - array sudah terurut!")
            break
        else:
            print(f"  State: {arr}\n")

    return arr

def selection_sort_debug(arr):
    """Selection sort dengan debugging info"""
    n = len(arr)
    print(f"Array awal: {arr}\n")

    for i in range(n):
        min_idx = i
        for j in range(i + 1, n):
            if arr[j] < arr[min_idx]:
                min_idx = j

        if i != min_idx:
            arr[i], arr[min_idx] = arr[min_idx], arr[i]
            print(f"Pass {i+1}: Swap {arr[min_idx]} dengan {arr[i]}")

        print(f"  State: {arr}\n")

    return arr

def insertion_sort_debug(arr):
    """Insertion sort dengan debugging info"""
    n = len(arr)
    print(f"Array awal: {arr}\n")

    for i in range(1, n):
        key = arr[i]
        j = i - 1
        print(f"Iterasi {i}: Insert {key}")

        while j >= 0 and arr[j] > key:
            arr[j + 1] = arr[j]
            j -= 1

        arr[j + 1] = key
        print(f"  State: {arr}\n")

    return arr

# Test Bubble Sort
print("=== BUBBLE SORT ===")
arr1 = [64, 34, 25, 12]
bubble_sort_debug(arr1)

print("\n=== SELECTION SORT ===")
arr2 = [64, 34, 25, 12]
selection_sort_debug(arr2)

print("\n=== INSERTION SORT ===")
arr3 = [64, 34, 25, 12]
insertion_sort_debug(arr3)
````

### 2. Aplikasi: Sorting Nilai Siswa

```python
class StudentGradeManager:
    def __init__(self):
        self.students = []

    def add_student(self, name, score):
        """Tambah siswa"""
        self.students.append({"name": name, "score": score})

    def sort_by_score_ascending(self):
        """Sort nilai ascending (terendah ke tertinggi)"""
        return insertion_sort_objects(
            self.students.copy(),
            key="score",
            reverse=False
        )

    def sort_by_score_descending(self):
        """Sort nilai descending (tertinggi ke terendah)"""
        return insertion_sort_objects(
            self.students.copy(),
            key="score",
            reverse=True
        )

    def sort_by_name(self):
        """Sort berdasarkan nama (alphabetical)"""
        arr = self.students.copy()
        n = len(arr)

        for i in range(1, n):
            key = arr[i]
            j = i - 1

            while j >= 0 and arr[j]["name"] > key["name"]:
                arr[j + 1] = arr[j]
                j -= 1

            arr[j + 1] = key

        return arr

    def display_ranking(self):
        """Tampilkan ranking siswa"""
        sorted_students = self.sort_by_score_descending()

        print("=== RANKING SISWA ===")
        for idx, student in enumerate(sorted_students, 1):
            print(f"{idx}. {student['name']}: {student['score']}")

# Penggunaan
manager = StudentGradeManager()
manager.add_student("Alice", 85)
manager.add_student("Bob", 92)
manager.add_student("Charlie", 78)
manager.add_student("David", 88)

manager.display_ranking()
# Output:
# === RANKING SISWA ===
# 1. Bob: 92
# 2. David: 88
# 3. Alice: 85
# 4. Charlie: 78
```

### 3. Aplikasi: Sorting Transaksi

```python
class TransactionSorter:
    @staticmethod
    def sort_by_amount(transactions, reverse=False):
        """Sort transaksi berdasarkan jumlah"""
        n = len(transactions)

        for i in range(1, n):
            key = transactions[i]
            j = i - 1

            while j >= 0:
                if reverse:
                    condition = transactions[j]["amount"] < key["amount"]
                else:
                    condition = transactions[j]["amount"] > key["amount"]

                if condition:
                    transactions[j + 1] = transactions[j]
                    j -= 1
                else:
                    break

            transactions[j + 1] = key

        return transactions

    @staticmethod
    def sort_by_date(transactions):
        """Sort transaksi berdasarkan tanggal"""
        n = len(transactions)

        for i in range(1, n):
            key = transactions[i]
            j = i - 1

            while j >= 0 and transactions[j]["date"] > key["date"]:
                transactions[j + 1] = transactions[j]
                j -= 1

            transactions[j + 1] = key

        return transactions

# Penggunaan
transactions = [
    {"date": "2026-04-03", "amount": 500000},
    {"date": "2026-04-01", "amount": 1000000},
    {"date": "2026-04-02", "amount": 250000},
]

# Sort by amount
sorted_amt = TransactionSorter.sort_by_amount(transactions.copy(), True)
print("Sort by Amount (Descending):")
for t in sorted_amt:
    print(f"  {t['date']}: Rp {t['amount']:,}")

# Sort by date
sorted_date = TransactionSorter.sort_by_date(transactions.copy())
print("\nSort by Date:")
for t in sorted_date:
    print(f"  {t['date']}: Rp {t['amount']:,}")
```

### 4. Aplikasi: Benchmark Sorting Algorithms

```python
import time

class SortingBenchmark:
    @staticmethod
    def benchmark_sorting(arr, sort_func, name):
        """Mulai waktu eksekusi sorting"""
        arr_copy = arr.copy()

        start = time.time()
        sort_func(arr_copy)
        end = time.time()

        elapsed = (end - start) * 1000  # Convert to milliseconds

        return {
            "algorithm": name,
            "time_ms": elapsed,
            "sorted": arr_copy
        }

    @staticmethod
    def compare_algorithms(arr):
        """Bandingkan semua algoritma"""
        algorithms = [
            (bubble_sort, "Bubble Sort"),
            (selection_sort, "Selection Sort"),
            (insertion_sort, "Insertion Sort")
        ]

        print(f"Array size: {len(arr)}\n")
        results = []

        for func, name in algorithms:
            result = SortingBenchmark.benchmark_sorting(arr, func, name)
            results.append(result)
            print(f"{name}: {result['time_ms']:.4f} ms")

        # Cari tercepat
        fastest = min(results, key=lambda x: x['time_ms'])
        print(f"\nFastest: {fastest['algorithm']} ({fastest['time_ms']:.4f} ms)")

        return results

# Test dengan array random
import random
random_arr = [random.randint(1, 1000) for _ in range(100)]

print("=== SORTING ALGORITHM COMPARISON ===\n")
SortingBenchmark.compare_algorithms(random_arr)
```

### 5. Aplikasi: Multi-Level Sorting

```python
def sort_by_multiple_fields(data, fields):
    """Sort data dengan multiple fields (priority-based)"""
    n = len(data)

    for i in range(1, n):
        key = data[i]
        j = i - 1

        # Compare menggunakan multiple fields
        while j >= 0:
            should_swap = False

            for field in fields:
                key_val = key.get(field)
                curr_val = data[j].get(field)

                if curr_val > key_val:
                    should_swap = True
                    break
                elif curr_val < key_val:
                    break

            if should_swap:
                data[j + 1] = data[j]
                j -= 1
            else:
                break

        data[j + 1] = key

    return data

# Test
employees = [
    {"dept": "IT", "salary": 50000, "name": "Alice"},
    {"dept": "IT", "salary": 55000, "name": "Bob"},
    {"dept": "HR", "salary": 45000, "name": "Charlie"},
    {"dept": "IT", "salary": 50000, "name": "David"},
]

# Sort by department first, then by salary, then by name
sorted_emp = sort_by_multiple_fields(
    employees.copy(),
    ["dept", "salary", "name"]
)

print("=== SORTED EMPLOYEES ===")
for emp in sorted_emp:
    print(f"{emp['dept']}: {emp['name']} (${emp['salary']})")
```

### 6. Aplikasi: Real-time Leaderboard

```python
class Leaderboard:
    def __init__(self):
        self.players = []

    def add_player(self, name, score):
        """Tambah pemain dengan score"""
        self.players.append({"name": name, "score": score})
        self._update_leaderboard()

    def update_score(self, name, new_score):
        """Update score pemain"""
        for player in self.players:
            if player["name"] == name:
                player["score"] = new_score
                break
        self._update_leaderboard()

    def _update_leaderboard(self):
        """Sort leaderboard"""
        n = len(self.players)

        for i in range(1, n):
            key = self.players[i]
            j = i - 1

            while j >= 0 and self.players[j]["score"] < key["score"]:
                self.players[j + 1] = self.players[j]
                j -= 1

            self.players[j + 1] = key

    def display(self, top_n=None):
        """Tampilkan leaderboard"""
        display_players = self.players[:top_n] if top_n else self.players

        print("=== LEADERBOARD ===")
        for idx, player in enumerate(display_players, 1):
            print(f"{idx}. {player['name']}: {player['score']} pts")

# Test
leaderboard = Leaderboard()
leaderboard.add_player("Player1", 100)
leaderboard.add_player("Player2", 250)
leaderboard.add_player("Player3", 150)
leaderboard.add_player("Player4", 200)

leaderboard.display()
# Output:
# === LEADERBOARD ===
# 1. Player2: 250 pts
# 2. Player4: 200 pts
# 3. Player3: 150 pts
# 4. Player1: 100 pts
```

### 7. Aplikasi: Event Scheduler

```python
class EventScheduler:
    def __init__(self):
        self.events = []

    def add_event(self, name, date, time):
        """Tambah event"""
        self.events.append({"name": name, "date": date, "time": time})

    def sort_by_date(self):
        """Sort event berdasarkan tanggal dan waktu"""
        n = len(self.events)

        for i in range(1, n):
            key = self.events[i]
            j = i - 1

            while j >= 0:
                curr_date = self.events[j]["date"]
                curr_time = self.events[j]["time"]
                key_date = key["date"]
                key_time = key["time"]

                # Compare date first, then time
                if (curr_date > key_date) or \
                   (curr_date == key_date and curr_time > key_time):
                    self.events[j + 1] = self.events[j]
                    j -= 1
                else:
                    break

            self.events[j + 1] = key

        return self.events

    def display_schedule(self):
        """Tampilkan jadwal event"""
        sorted_events = self.sort_by_date()

        print("=== EVENT SCHEDULE ===")
        for event in sorted_events:
            print(f"{event['date']} {event['time']}: {event['name']}")

# Test
scheduler = EventScheduler()
scheduler.add_event("Meeting", "2026-04-09", "14:00")
scheduler.add_event("Lunch", "2026-04-09", "12:00")
scheduler.add_event("Presentation", "2026-04-10", "09:00")
scheduler.add_event("Workshop", "2026-04-09", "16:00")

scheduler.display_schedule()
# Output:
# === EVENT SCHEDULE ===
# 2026-04-09 12:00: Lunch
# 2026-04-09 14:00: Meeting
# 2026-04-09 16:00: Workshop
# 2026-04-10 09:00: Presentation
```

---

## Kesimpulan

Ketiga algoritma sorting ini adalah dasar dalam ilmu komputer:

1. **Bubble Sort**: Mudah dipahami, cocok untuk pembelajaran, performa buruk untuk data besar
2. **Selection Sort**: Jumlah swap minimal, performa konsisten O(n²)
3. **Insertion Sort**: Paling efisien di antara ketiganya untuk data kecil/semi-terurut

Untuk dataset production yang besar, digunakan algoritma lebih canggih seperti Merge Sort, Quick Sort, atau Hybrid Sort (Timsort, Introsort).

```

```
