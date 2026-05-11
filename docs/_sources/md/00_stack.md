# Stack (Tumpukan)

## Pengertian Stack

Stack adalah struktur data linier yang mengikuti prinsip **LIFO (Last In First Out)** atau **FILO (First In Last Out)**. Artinya, elemen yang masuk paling akhir akan dikeluarkan paling pertama. Analogi sederhana adalah tumpukan piring di dapur - piring yang diletakkan paling akhir akan diambil paling pertama.

## Karakteristik Stack

1. **LIFO Principle**: Elemen terakhir yang masuk adalah yang pertama keluar
2. **Sequential Access**: Akses hanya melalui satu ujung (top/puncak)
3. **Homogeneous**: Semua elemen bertipe data sama
4. **Dynamic Size**: Ukuran dapat bertambah atau berkurang

## Operasi Dasar Stack

### 1. Push

Menambahkan elemen baru ke puncak stack.

```python
def push(stack, element):
    stack.append(element)
```

**Kompleksitas**: O(1)

### 2. Pop

Menghapus dan mengembalikan elemen dari puncak stack.

```python
def pop(stack):
    if not is_empty(stack):
        return stack.pop()
    return None
```

**Kompleksitas**: O(1)

### 3. Peek

Melihat elemen puncak stack tanpa menghapusnya.

```python
def peek(stack):
    if not is_empty(stack):
        return stack[-1]
    return None
```

**Kompleksitas**: O(1)

### 4. isEmpty

Mengecek apakah stack kosong.

```python
def is_empty(stack):
    return len(stack) == 0
```

**Kompleksitas**: O(1)

### 5. Size

Mengetahui jumlah elemen dalam stack.

```python
def size(stack):
    return len(stack)
```

**Kompleksitas**: O(1)

## Implementasi Stack

### Menggunakan Array/List Python

```python
class Stack:
    def __init__(self):
        self.items = []

    def push(self, item):
        """Tambah elemen ke stack"""
        self.items.append(item)

    def pop(self):
        """Hapus dan kembalikan elemen top"""
        if not self.is_empty():
            return self.items.pop()
        return None

    def peek(self):
        """Lihat elemen top tanpa hapus"""
        if not self.is_empty():
            return self.items[-1]
        return None

    def is_empty(self):
        """Cek apakah stack kosong"""
        return len(self.items) == 0

    def size(self):
        """Kembalikan ukuran stack"""
        return len(self.items)

    def display(self):
        """Tampilkan semua elemen"""
        print("Stack:", self.items)
```

### Menggunakan Linked List

```python
class Node:
    def __init__(self, data):
        self.data = data
        self.next = None

class StackLL:
    def __init__(self):
        self.top = None

    def push(self, item):
        """Tambah elemen ke stack"""
        new_node = Node(item)
        new_node.next = self.top
        self.top = new_node

    def pop(self):
        """Hapus dan kembalikan elemen top"""
        if not self.is_empty():
            data = self.top.data
            self.top = self.top.next
            return data
        return None

    def peek(self):
        """Lihat elemen top"""
        if not self.is_empty():
            return self.top.data
        return None

    def is_empty(self):
        """Cek apakah stack kosong"""
        return self.top is None

    def display(self):
        """Tampilkan semua elemen"""
        current = self.top
        elements = []
        while current:
            elements.append(str(current.data))
            current = current.next
        print("Stack:", " <- ".join(elements))
```

## Aplikasi Stack

### 1. Undo/Redo Functionality

Setiap aksi disimpan dalam stack. Undo mengambil dari top stack.

```python
def undo_system():
    actions = Stack()
    actions.push("Tulis 'Hello'")
    actions.push("Tulis ' World'")
    actions.push("Format Bold")

    print("Undo:", actions.pop())  # Format Bold
    print("Undo:", actions.pop())  # Tulis ' World'
```

### 2. Browser History

Tombol back menyimpan history di stack.

```python
def browser_history():
    history = Stack()
    history.push("google.com")
    history.push("github.com")
    history.push("stackoverflow.com")

    print("Back:", history.pop())  # stackoverflow.com
    print("Back:", history.pop())  # github.com
```

### 3. Function Call Stack

Bahasa pemrograman menggunakan stack untuk memanggil fungsi.

```python
def func_a():
    print("In func_a")
    func_b()

def func_b():
    print("In func_b")
    func_c()

def func_c():
    print("In func_c")

# Call stack: main -> func_a -> func_b -> func_c
```

### 4. Expression Evaluation & Conversion

- Konversi infix ke postfix
- Evaluasi postfix expression

```python
def evaluate_postfix(expression):
    stack = Stack()
    tokens = expression.split()

    for token in tokens:
        if token in ['+', '-', '*', '/']:
            b = stack.pop()
            a = stack.pop()
            if token == '+':
                result = a + b
            elif token == '-':
                result = a - b
            elif token == '*':
                result = a * b
            elif token == '/':
                result = a / b
            stack.push(result)
        else:
            stack.push(float(token))

    return stack.pop()

# Contoh: "5 3 +"
print(evaluate_postfix("5 3 +"))  # 8
```

### 5. Balanced Parentheses Checking

```python
def is_balanced(expression):
    stack = Stack()
    pairs = {')': '(', '}': '{', ']': '['}

    for char in expression:
        if char in '({[':
            stack.push(char)
        elif char in ')}]':
            if stack.is_empty() or stack.pop() != pairs[char]:
                return False

    return stack.is_empty()

print(is_balanced("((a+b)*c"))  # False
print(is_balanced("((a+b)*c)"))  # True
```

### 6. Depth-First Search (DFS)

Stack digunakan untuk traversal graph secara DFS.

```python
def dfs(graph, start):
    visited = set()
    stack = Stack()
    stack.push(start)

    while not stack.is_empty():
        node = stack.pop()
        if node not in visited:
            print(node, end=" ")
            visited.add(node)

            for neighbor in reversed(graph[node]):
                if neighbor not in visited:
                    stack.push(neighbor)
```

## Contoh Aplikasi: Konversi Desimal ke Biner

```python
def dec2bin(n):
    """Konversi bilangan desimal ke biner menggunakan Stack"""
    data = n
    s = stack()
    loopPush = ""
    loopPop = ""
    num = 0

    # Push semua sisa bagi ke stack
    while n > 0:
        num += 1
        push(s, n % 2)
        loopPush += f"\n{num}. Push stack with {s[-1]} --> {s}"
        n //= 2

    # Pop dari stack untuk mendapatkan biner
    result = ""
    while not isEmpty(s):
        num += 1
        result += str(pop(s))
        loopPop += f"{num}. Pop stack ---> {s}\n"

    return loopPush + "\n" + loopPop, f"Biner {data} = {result}"

# Contoh penggunaan
binary, process = dec2bin(57)
print(process)
print(binary)

# Output:
# 1. Push stack with 1 --> [1]
# 2. Push stack with 0 --> [1, 0]
# 3. Push stack with 0 --> [1, 0, 0]
# 4. Push stack with 1 --> [1, 0, 0, 1]
# 5. Push stack with 1 --> [1, 0, 0, 1, 1]
# 6. Push stack with 1 --> [1, 0, 0, 1, 1, 1]
# 7. Pop stack ---> [1, 0, 0, 1, 1]
# ...
# Biner 57 = 111001
```

## Contoh Aplikasi: Pengecekan Keseimbangan Kurung

```python
def parenthesesCheck(expression):
    """Cek penempatan kurung dalam operasi matematika"""
    s = stack()
    check = True
    proc = ""
    err = ""
    num = 0
    numErr = 0

    for i in expression:
        # Jika opening bracket
        if i == "(" or i == "[" or i == "{":
            num += 1
            push(s, i)
            proc += f"{num}. Push stack with {i} --> {s}\n"

        # Jika closing bracket
        elif i == ")" or i == "]" or i == "}":
            num += 1
            if isEmpty(s):
                check = False
                proc += f"{num}. Pop stack --> {s}\n"
            else:
                chk = pop(s)
                proc += f"{num}. Pop stack --> {s}\n"

                # Cek kecocokan bracket
                if chk == "(" and i != ")":
                    numErr += 1
                    err += f"{numErr}. Kurung buka '{chk}' tidak cocok dengan kurung tutup '{i}'\n"
                    check = False
                if chk == "[" and i != "]":
                    numErr += 1
                    err += f"{numErr}. Kurung buka '{chk}' tidak cocok dengan kurung tutup '{i}'\n"
                    check = False
                if chk == "{" and i != "}":
                    numErr += 1
                    err += f"{numErr}. Kurung buka '{chk}' tidak cocok dengan kurung tutup '{i}'\n"
                    check = False

    # Stack harus kosong jika seimbang
    if not isEmpty(s):
        check = False
        err += f"Kurung buka tidak tertutup!\n"

    return check, "Proses cek:\n" + proc, "Error:\n" + err

# Contoh penggunaan
result, proses, error = parenthesesCheck("([4+5]/[9+8]*(3+2))")
print(result)
print(proses)
print(error)

# Output:
# True
# Proses cek:
# 1. Push stack with ( --> ['(']
# 2. Push stack with [ --> ['(', '[']
# 3. Pop stack --> ['(']
# 4. Push stack with [ --> ['(', '[']
# 5. Pop stack --> ['(']
# 6. Push stack with ( --> ['(', '(']
# 7. Pop stack --> ['(']
# 8. Pop stack --> []
# Error:
```

## Contoh Implementasi Lengkap

```python
# Program: Tower of Hanoi menggunakan Stack
class StackDisplay:
    def __init__(self, name):
        self.name = name
        self.items = []

    def push(self, item):
        self.items.append(item)

    def pop(self):
        return self.items.pop() if self.items else None

    def display(self):
        print(f"{self.name}: {self.items}")

def hanoi(n, source, destination, auxiliary):
    if n == 1:
        disk = source.pop()
        destination.push(disk)
        print(f"Pindahkan disk {disk} dari {source.name} ke {destination.name}")
        source.display()
        destination.display()
        print()
    else:
        hanoi(n-1, source, auxiliary, destination)
        disk = source.pop()
        destination.push(disk)
        print(f"Pindahkan disk {disk} dari {source.name} ke {destination.name}")
        source.display()
        destination.display()
        print()
        hanoi(n-1, auxiliary, destination, source)

# Jalankan Tower of Hanoi
rod_a = StackDisplay("Rod A")
rod_b = StackDisplay("Rod B")
rod_c = StackDisplay("Rod C")

# Inisialisasi dengan 3 disk
for i in range(3, 0, -1):
    rod_a.push(i)

print("=== Tower of Hanoi dengan 3 Disk ===")
hanoi(3, rod_a, rod_c, rod_b)
```

## Kompleksitas Stack

| Operasi | Array | Linked List |
| ------- | ----- | ----------- |
| Push    | O(1)  | O(1)        |
| Pop     | O(1)  | O(1)        |
| Peek    | O(1)  | O(1)        |
| Search  | O(n)  | O(n)        |
| Space   | O(n)  | O(n)        |

## Keuntungan dan Kelemahan

### Keuntungan

- Operasi yang simpel dan cepat
- Menggunakan memori secara efisien
- Cocok untuk masalah rekursi
- Implementasi mudah

### Kelemahan

- Akses terbatas hanya di puncak
- Tidak bisa akses elemen tengah
- Tidak cocok untuk pencarian elemen tertentu
- Ukuran terbatas jika menggunakan array statis

## Kesimpulan

Stack adalah struktur data fundamental yang sangat berguna dalam berbagai aplikasi pemrograman. Dengan LIFO principle-nya, stack memungkinkan penyelesaian berbagai masalah dengan elegan, mulai dari undo/redo, browser history, hingga evaluasi ekspresi dan graph traversal.
