# Materi Hashing

## 1. Hashing : Close Address (Chaining)

### Pengertian

Close Address atau Chaining adalah metode pada hashing untuk menangani collision dengan cara menyimpan data yang memiliki index sama ke dalam sebuah list.

---

## Source Code CRUD Chaining

```python
# Membuat tabel hash
hash_table = [[] for _ in range(10)]

# Fungsi hash

def hash_function(key):
    return key % len(hash_table)

# CREATE / INSERT

def insert(key):
    index = hash_function(key)
    hash_table[index].append(key)
    print(f"Data {key} berhasil ditambahkan ke index {index}")

# READ / SEARCH

def search(key):
    index = hash_function(key)

    if key in hash_table[index]:
        print(f"Data {key} ditemukan di index {index}")
    else:
        print(f"Data {key} tidak ditemukan")

# UPDATE

def update(old_key, new_key):
    index = hash_function(old_key)

    if old_key in hash_table[index]:
        posisi = hash_table[index].index(old_key)
        hash_table[index][posisi] = new_key
        print(f"Data {old_key} berhasil diubah menjadi {new_key}")
    else:
        print("Data tidak ditemukan")

# DELETE

def delete(key):
    index = hash_function(key)

    if key in hash_table[index]:
        hash_table[index].remove(key)
        print(f"Data {key} berhasil dihapus")
    else:
        print("Data tidak ditemukan")

# DISPLAY

def display():
    print("\nIsi Hash Table")
    for i in range(len(hash_table)):
        print(i, "-->", hash_table[i])

# PROGRAM UTAMA
insert(15)
insert(25)
insert(35)
insert(20)
insert(30)

# Menampilkan isi hash

display()

# Search
search(25)
search(50)

# Update
update(25, 45)

# Delete
delete(35)

# Menampilkan isi akhir

display()
```

---

## Penjelasan Program

### Fungsi Hash

```python
key % len(hash_table)
```

Digunakan untuk menentukan index penyimpanan data.

Contoh:

```python
15 % 10 = 5
25 % 10 = 5
```

Karena hasilnya sama, maka terjadi collision.

---

## 2. Open Address

# A. Linear Probing

### Pengertian

Linear probing adalah metode collision handling dengan mencari index kosong berikutnya secara berurutan.

---

## Source Code Linear Probing

```python
size = 10
hash_table = [None] * size

# Fungsi hash

def hash_function(key):
    return key % size

# INSERT

def insert(key):
    index = hash_function(key)

    while hash_table[index] is not None:
        index = (index + 1) % size

    hash_table[index] = key
    print(f"Data {key} masuk ke index {index}")

# SEARCH

def search(key):
    index = hash_function(key)
    start = index

    while hash_table[index] is not None:
        if hash_table[index] == key:
            print(f"Data {key} ditemukan di index {index}")
            return

        index = (index + 1) % size

        if index == start:
            break

    print("Data tidak ditemukan")

# UPDATE

def update(old_key, new_key):
    index = hash_function(old_key)
    start = index

    while hash_table[index] is not None:
        if hash_table[index] == old_key:
            hash_table[index] = new_key
            print(f"Data {old_key} berhasil diubah menjadi {new_key}")
            return

        index = (index + 1) % size

        if index == start:
            break

    print("Data tidak ditemukan")

# DELETE

def delete(key):
    index = hash_function(key)
    start = index

    while hash_table[index] is not None:
        if hash_table[index] == key:
            hash_table[index] = None
            print(f"Data {key} berhasil dihapus")
            return

        index = (index + 1) % size

        if index == start:
            break

    print("Data tidak ditemukan")

# DISPLAY

def display():
    print("\nIsi Hash Table")
    for i in range(size):
        print(i, "-->", hash_table[i])

# TEST PROGRAM
insert(10)
insert(20)
insert(30)
insert(40)
insert(50)
insert(60)

# Collision
insert(70)

# Display

display()

# Search
search(40)

# Update
update(40, 99)

# Delete
delete(20)

# Display akhir

display()
```

---

# B. Quadratic Probing

### Pengertian

Quadratic probing menangani collision dengan lompatan kuadrat.

Rumus:

```python
(index + i^2) % size
```

---

## Source Code Quadratic Probing

```python
size = 10
hash_table = [None] * size

# Fungsi hash

def hash_function(key):
    return key % size

# INSERT

def insert(key):
    index = hash_function(key)
    i = 1

    while hash_table[index] is not None:
        index = (hash_function(key) + i**2) % size
        i += 1

    hash_table[index] = key
    print(f"Data {key} masuk ke index {index}")

# DISPLAY

def display():
    print("\nIsi Hash Table")
    for i in range(size):
        print(i, "-->", hash_table[i])

# TEST PROGRAM
insert(10)
insert(20)
insert(30)
insert(40)
insert(50)
insert(60)
insert(70)

# Collision
insert(80)
insert(90)

# Display

display()
```

---

# C. Load Factor < 1

### Pengertian

Load Factor adalah tingkat kepenuhan tabel hash.

Rumus:

```python
Load Factor = jumlah data / ukuran tabel
```

Jika hasil < 1 maka tabel belum penuh.

---

## Contoh Perhitungan

Ukuran tabel = 10

Jumlah data = 7

Maka:

```python
Load Factor = 7 / 10
             = 0.7
```

Karena 0.7 < 1 maka tabel belum penuh.

---

# Contoh Hash Table Penuh

```python
size = 5
hash_table = [None] * size

for i in range(size):
    hash_table[i] = i + 1

print(hash_table)
```

Output:

```python
[1, 2, 3, 4, 5]
```

Load Factor:

```python
5 / 5 = 1
```

Artinya tabel penuh.

---

# 3. Mid Square Method

## Pengertian

Mid Square Method adalah metode hashing dengan cara:

1. Mengkuadratkan key
2. Mengambil digit tengah
3. Menjadikan digit tengah sebagai index

---

## Source Code Mid Square Method

```python
size = 100

# Fungsi Mid Square

def mid_square_hash(key):
    kuadrat = key * key

    # ubah ke string
    kuadrat_str = str(kuadrat)

    # ambil digit tengah
    tengah = len(kuadrat_str) // 2

    if len(kuadrat_str) % 2 == 0:
        digit_tengah = kuadrat_str[tengah-1:tengah+1]
    else:
        digit_tengah = kuadrat_str[tengah]

    return int(digit_tengah) % size

# TEST
key = 123
index = mid_square_hash(key)

print("Key :", key)
print("Index Hash :", index)
```

---

## Contoh Perhitungan Mid Square

```python
123^2 = 15129
```

Digit tengah:

```python
1 5 1 2 9
    ^
```

Digit tengah = 1

Maka index = 1

---