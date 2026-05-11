# Searching (Pencarian)

Searching (Pencarian) adalah proses fundamental dalam ilmu komputer untuk menemukan elemen tertentu di dalam sekumpulan data. Koleksi data tersebut bisa berupa array, list, tree, atau struktur data lainnya. Terdapat tiga algoritma pencarian utama yang akan dibahas: **Sequential Search**, **Binary Search**, dan **Hashing**.

---

## 1. Sequential Search (Linear Search)

### Pengertian

Sequential Search atau Linear Search adalah algoritma pencarian paling sederhana. Data yang dicari dibandingkan satu per satu dengan setiap elemen dalam list, mulai dari indeks pertama hingga indeks terakhir, hingga data ditemukan atau seluruh list telah ditelusuri.

### Cara Kerja

```
Data: [10, 50, 30, 70, 80, 20, 90, 40]
Cari: 30

Langkah 1: Bandingkan 10 dengan 30 → tidak sama
Langkah 2: Bandingkan 50 dengan 30 → tidak sama
Langkah 3: Bandingkan 30 dengan 30 → DITEMUKAN di indeks 2 ✓
```

### Implementasi Python

```python
def sequential_search(arr, target):
    for i in range(len(arr)):
        if arr[i] == target:
            return i   # kembalikan indeks jika ditemukan
    return -1          # kembalikan -1 jika tidak ditemukan

# Contoh penggunaan
arr = [10, 50, 30, 70, 80]
print(sequential_search(arr, 30))   # Output: 2
print(sequential_search(arr, 99))   # Output: -1
```

### Kompleksitas

| Aspek            | Nilai                                         |
| ---------------- | --------------------------------------------- |
| Best Case        | O(1) - data ada di posisi pertama             |
| Average Case     | O(n)                                          |
| Worst Case       | O(n) - data di posisi terakhir atau tidak ada |
| Space Complexity | O(1)                                          |

### Karakteristik

- Bekerja pada data **tidak terurut** maupun terurut
- Tidak memerlukan pre-processing data
- Cocok untuk dataset kecil

---

## 2. Binary Search

### Pengertian

Binary Search bekerja pada **array yang sudah terurut**. Pencarian dilakukan dengan membagi list menjadi dua grup, lalu membandingkan data yang dicari dengan elemen di indeks tengah. Jika data lebih besar dari nilai tengah, pencarian dilanjutkan hanya di grup kanan; jika lebih kecil, di grup kiri. Proses ini diulang hingga data ditemukan.

### Cara Kerja

```
Data (terurut): [2, 5, 8, 12, 16, 23, 38, 56, 72, 91]
Cari: 23

Iterasi 1: Mid = indeks 4 → nilai 16. 23 > 16 → cari di kanan
Iterasi 2: Mid = indeks 7 → nilai 56. 23 < 56 → cari di kiri
Iterasi 3: Mid = indeks 5 → nilai 23. 23 == 23 → DITEMUKAN ✓
```

### Implementasi Python

```python
def binary_search(arr, target):
    low = 0
    high = len(arr) - 1

    while low <= high:
        mid = (low + high) // 2

        if arr[mid] == target:
            return mid          # ditemukan
        elif arr[mid] < target:
            low = mid + 1       # cari di bagian kanan
        else:
            high = mid - 1      # cari di bagian kiri

    return -1   # tidak ditemukan

# Contoh penggunaan
arr = [2, 5, 8, 12, 16, 23, 38, 56, 72, 91]
print(binary_search(arr, 23))   # Output: 5
print(binary_search(arr, 10))   # Output: -1
```

### Kompleksitas

| Aspek            | Nilai                              |
| ---------------- | ---------------------------------- |
| Best Case        | O(1) - data tepat di posisi tengah |
| Average Case     | O(log n)                           |
| Worst Case       | O(log n)                           |
| Space Complexity | O(1) iteratif / O(log n) rekursif  |

### Karakteristik

- Hanya bekerja pada data **terurut**
- Jauh lebih cepat dari Sequential Search untuk data besar
- Setiap iterasi memangkas setengah ruang pencarian

---

## 3. Hashing

### Pengertian

Hashing adalah algoritma pencarian ketiga yang bahkan lebih cepat dari Binary Search. Pencarian akan lebih cepat lagi jika semua data terletak tepat di tempatnya masing-masing, sehingga pencarian hanya memerlukan **satu kali** proses perbandingan saja.

Di dalam algoritma hashing terdapat beberapa istilah dasar:

- **Hash Table** - struktur penyimpanan data yang dirancang untuk memudahkan pencarian. Di Python, tipe data `list` dapat digunakan untuk merepresentasikan hash table.
- **Slot** - posisi (indeks) pada hash table sebagai tempat penyimpanan setiap data. Nilai slot adalah integer mulai dari `0` sampai `n`.
- **Hash Function** - fungsi yang memetakan data ke slot di dalam hash table.

### Fungsi Hash (Hash Function)

Hash function memegang peranan penting dalam algoritma hashing. Fungsi ini menerima nilai data sebagai parameter dan mengembalikan nilai integer (nilai hash) yang merepresentasikan nomor slot.

Contoh hash function paling sederhana adalah **Remainder Function** (fungsi modulus):

```
hash(data) = data % ukuran_tabel
```

Contoh perhitungan dengan ukuran tabel 11:

| Data | Nilai Hash (data % 11) |
| ---- | ---------------------- |
| 54   | 10                     |
| 26   | 4                      |
| 93   | 5                      |
| 17   | 6                      |
| 77   | 0                      |
| 31   | 9                      |

Hasil penempatan dalam hash table:

```
Slot:  [  0  |  1  |  2  |  3  |  4  |  5  |  6  |  7  |  8  |  9  | 10  ]
Data:  [ 77  | None| None| None|  26 |  93 |  17 | None| None|  31 |  54 ]
```

**Load Factor** hash table dihitung dengan:

```
λ = jumlahData / ukuranTabel = 6 / 11 ≈ 0.54
```

### Implementasi Python

```python
def remainderFunction(data, num):
    return data % num

def createHashTable(num):
    return ['none'] * num

def putData(data, table):
    for item in data:
        ind = remainderFunction(item, len(table))
        table[ind] = item
    return table

def searchHash(data, table):
    hashVal = remainderFunction(data, len(table))
    return data == table[hashVal]

# Contoh penggunaan
a = [54, 26, 93, 17, 77, 31]
hashTable = createHashTable(11)
hashTable = putData(a, hashTable)

print(hashTable)
# [77, 'none', 'none', 'none', 26, 93, 17, 'none', 'none', 31, 54]

print(searchHash(93, hashTable))   # Output: True
print(searchHash(99, hashTable))   # Output: False
```

### Hash Function untuk String

Jika data berupa string, nilai hash dapat diperoleh dari jumlah nilai ASCII setiap karakter penyusunnya menggunakan fungsi `ord()`:

```python
def strVal(strData):
    temp = 0
    for i in range(len(strData)):
        temp = temp + ord(strData[i])
    return temp

print(strVal('indonesia'))
```

Namun fungsi ini menghasilkan nilai yang sama untuk **anagram** (misalnya `'dia'` dan `'adi'`). Untuk mengatasinya, tambahkan bobot berdasarkan posisi karakter:

```python
def strValWeighted(strData):
    temp = 0
    for i in range(len(strData)):
        temp = temp + ord(strData[i]) * i   # bobot = posisi karakter
    return temp

# 'adi': a*0 + d*1 + i*2 → berbeda dengan 'dia': d*0 + i*1 + a*2
```

---

## 4. Penanganan _Collision_

### Pengertian Collision

Collision (tabrakan) terjadi ketika dua data yang berbeda menghasilkan nilai hash yang sama, sehingga keduanya menunjuk ke slot yang sama. Contoh: data `44` memiliki hash `44 % 11 = 0`, padahal slot 0 sudah ditempati oleh data `77`.

Untuk meminimalkan collision, diperlukan **perfect hash function**, yaitu fungsi hash yang memetakan setiap data ke slot yang unik.

Salah satu contoh perfect hash function adalah **Mid-Square Method**: kuadratkan nilai data, lalu ambil digit bagian tengah, kemudian hitung modulus dengan ukuran tabel.

```
Contoh: data = 35
35² = 1225
Ambil digit tengah: '22'
hash = 22 % 11 = 0
```

### Metode Penanganan Collision

#### a) Linear Probing

Jika terjadi collision di slot tertentu, cari slot kosong berikutnya satu per satu secara linear mulai dari posisi collision.

```python
def linearProbing(ind, hashTable, data):
    count = ind
    found = False

    while count != ind - 1 and not found:
        if hashTable[count] == 'none':
            found = True
            hashTable[count] = data
        else:
            count = count + 1
            if count == len(hashTable) - 1:
                count = 0

    return hashTable

def putDataWithProbing(a, hashTable):
    for item in a:
        ind = remainderFunction(item, len(hashTable))
        if hashTable[ind] == 'none':
            hashTable[ind] = item
        else:
            hashTable = linearProbing(ind, hashTable, item)
    return hashTable

# Contoh: menambahkan 44, 55, 20 ke data awal
a = [54, 26, 93, 17, 77, 31, 44, 55, 20]
hashTable = createHashTable(11)
hashTable = putDataWithProbing(a, hashTable)
print(hashTable)
```

#### b) Quadratic Probing

Berbeda dengan linear probing yang maju satu per satu, quadratic probing mencari slot dengan menambahkan posisi collision dengan nilai: **1, 3, 5, 7, 9, ...**

```
Slot hasil hash: 0 (collision)
Coba: 0+1 = 1
Coba: 1+3 = 4  (jika masih collision)
Coba: 4+5 = 9  (jika masih collision)
```

Hasil hash table dengan quadratic probing untuk data `[54, 26, 93, 17, 77, 31, 44, 55, 20]`:

```
Slot:  [  0  |  1  |  2  |  3  |  4  |  5  |  6  |  7  |  8  |  9  | 10  ]
Data:  [ 77  |  44 |  20 |  55 |  26 |  93 |  17 | None| None|  31 |  54 ]
```

#### c) Chaining

Pada metode Chaining, setiap slot tidak hanya menyimpan satu data, tetapi bisa menyimpan **beberapa data sekaligus** dalam bentuk linked list atau list bertingkat.

```python
def createChainHashTable(num):
    return [[] for _ in range(num)]

def putDataChaining(data, table):
    for item in data:
        ind = remainderFunction(item, len(table))
        table[ind].append(item)
    return table

def searchChaining(data, table):
    ind = remainderFunction(data, len(table))
    return data in table[ind]

# Contoh penggunaan
a = [54, 26, 93, 17, 77, 31, 44, 55, 20]
chainTable = createChainHashTable(11)
chainTable = putDataChaining(a, chainTable)

print(searchChaining(44, chainTable))   # Output: True
```

Ilustrasi struktur Chaining:

```
Slot 0:  [77] → [44] → [55]
Slot 4:  [26]
Slot 5:  [93]
Slot 6:  [17]
Slot 9:  [31] → [20]
Slot 10: [54]
```

---

## Perbandingan Algoritma Searching

| Algoritma         | Kondisi Data        | Best Case | Worst Case | Space |
| ----------------- | ------------------- | --------- | ---------- | ----- |
| Sequential Search | Tidak harus terurut | O(1)      | O(n)       | O(1)  |
| Binary Search     | Harus terurut       | O(1)      | O(log n)   | O(1)  |
| Hashing           | Tidak harus terurut | O(1)      | O(1)\*     | O(n)  |

> \*Hashing mencapai O(1) jika tidak ada collision. Dengan collision handling, performa bisa menurun tergantung metode yang digunakan.

### Kapan Menggunakan?

| Situasi                                    | Algoritma yang Tepat          |
| ------------------------------------------ | ----------------------------- |
| Data tidak terurut, dataset kecil          | Sequential Search             |
| Data sudah terurut, pencarian berulang     | Binary Search                 |
| Kecepatan pencarian adalah prioritas utama | Hashing                       |
| Data dinamis (sering insert/delete)        | Hashing dengan Chaining       |
| Memory terbatas                            | Sequential atau Binary Search |
