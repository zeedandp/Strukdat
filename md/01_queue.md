# Queue (Antrian)

## Pengertian Queue

Queue adalah struktur data linier yang mengikuti prinsip **FIFO (First In First Out)** atau **FCFS (First Come First Served)**. Artinya, elemen yang masuk paling awal akan dikeluarkan paling pertama. Analogi sederhana adalah antrian di kasir - orang yang antri paling awal akan dilayani paling awal.

## Karakteristik Queue

1. **FIFO Principle**: Elemen pertama yang masuk adalah yang pertama keluar
2. **Two-End Access**: Penambahan di belakang (rear), pengambilan di depan (front)
3. **Homogeneous**: Semua elemen bertipe data sama
4. **Dynamic Size**: Ukuran dapat berubah sesuai kebutuhan

## Operasi Dasar Queue

### 1. Enqueue

Menambahkan elemen baru ke belakang (rear) queue.

```python
def enqueue(queue, element):
    queue.append(element)
```

**Kompleksitas**: O(1)

### 2. Dequeue

Menghapus dan mengembalikan elemen dari depan (front) queue.

```python
def dequeue(queue):
    if not is_empty(queue):
        return queue.pop(0)  # Hapus dari indeks 0
    return None
```

**Kompleksitas**: O(n) - tidak efisien karena pergeseran elemen

### 3. Front/Peek

Melihat elemen di depan queue tanpa menghapusnya.

```python
def front(queue):
    if not is_empty(queue):
        return queue[0]
    return None
```

**Kompleksitas**: O(1)

### 4. Rear

Melihat elemen di belakang queue.

```python
def rear(queue):
    if not is_empty(queue):
        return queue[-1]
    return None
```

**Kompleksitas**: O(1)

### 5. isEmpty

Mengecek apakah queue kosong.

```python
def is_empty(queue):
    return len(queue) == 0
```

**Kompleksitas**: O(1)

### 6. Size

Mengetahui jumlah elemen dalam queue.

```python
def size(queue):
    return len(queue)
```

**Kompleksitas**: O(1)

## Implementasi Queue

### Menggunakan List Python (Simple Implementation)

```python
class Queue:
    def __init__(self):
        self.items = []

    def enqueue(self, item):
        """Tambah elemen ke belakang queue"""
        self.items.append(item)

    def dequeue(self):
        """Hapus dan kembalikan elemen depan"""
        if not self.is_empty():
            return self.items.pop(0)
        return None

    def front(self):
        """Lihat elemen depan"""
        if not self.is_empty():
            return self.items[0]
        return None

    def rear(self):
        """Lihat elemen belakang"""
        if not self.is_empty():
            return self.items[-1]
        return None

    def is_empty(self):
        """Cek apakah queue kosong"""
        return len(self.items) == 0

    def size(self):
        """Kembalikan ukuran queue"""
        return len(self.items)

    def display(self):
        """Tampilkan semua elemen"""
        print("Queue:", self.items)
```

### Menggunakan Collections.deque (Efisien)

```python
from collections import deque

class EfficientQueue:
    def __init__(self):
        self.items = deque()

    def enqueue(self, item):
        """Tambah elemen ke belakang"""
        self.items.append(item)

    def dequeue(self):
        """Hapus dan kembalikan elemen depan"""
        if not self.is_empty():
            return self.items.popleft()  # O(1) operation
        return None

    def front(self):
        """Lihat elemen depan"""
        if not self.is_empty():
            return self.items[0]
        return None

    def is_empty(self):
        """Cek apakah queue kosong"""
        return len(self.items) == 0

    def size(self):
        """Kembalikan ukuran queue"""
        return len(self.items)
```

### Menggunakan Linked List

```python
class Node:
    def __init__(self, data):
        self.data = data
        self.next = None

class QueueLL:
    def __init__(self):
        self.front_node = None
        self.rear_node = None

    def enqueue(self, item):
        """Tambah elemen ke belakang"""
        new_node = Node(item)
        if self.rear_node:
            self.rear_node.next = new_node
        self.rear_node = new_node

        if self.front_node is None:
            self.front_node = new_node

    def dequeue(self):
        """Hapus dan kembalikan elemen depan"""
        if self.is_empty():
            return None

        data = self.front_node.data
        self.front_node = self.front_node.next

        if self.front_node is None:
            self.rear_node = None

        return data

    def front(self):
        """Lihat elemen depan"""
        if not self.is_empty():
            return self.front_node.data
        return None

    def is_empty(self):
        """Cek apakah queue kosong"""
        return self.front_node is None

    def display(self):
        """Tampilkan semua elemen"""
        current = self.front_node
        elements = []
        while current:
            elements.append(str(current.data))
            current = current.next
        print("Queue:", " -> ".join(elements))
```

## Jenis-jenis Queue

### 1. Simple Queue (Linear Queue)

Queue biasa dengan operasi enqueue di rear dan dequeue di front.

### 2. Circular Queue

Queue yang terhubung melingkar, menghindari pemborosan ruang.

```python
class CircularQueue:
    def __init__(self, max_size):
        self.max_size = max_size
        self.items = [None] * max_size
        self.front = -1
        self.rear = -1

    def enqueue(self, item):
        """Tambah elemen dengan wrapping"""
        if self.is_full():
            return False

        if self.front == -1:
            self.front = 0

        self.rear = (self.rear + 1) % self.max_size
        self.items[self.rear] = item
        return True

    def dequeue(self):
        """Hapus elemen dengan wrapping"""
        if self.is_empty():
            return None

        data = self.items[self.front]
        self.items[self.front] = None

        if self.front == self.rear:
            self.front = -1
            self.rear = -1
        else:
            self.front = (self.front + 1) % self.max_size

        return data

    def is_empty(self):
        return self.front == -1

    def is_full(self):
        return (self.rear + 1) % self.max_size == self.front
```

### 3. Priority Queue

Setiap elemen memiliki prioritas, dequeue berdasarkan prioritas tertinggi.

```python
import heapq

class PriorityQueue:
    def __init__(self):
        self.items = []

    def enqueue(self, item, priority):
        """Tambah elemen dengan prioritas (lower = higher priority)"""
        heapq.heappush(self.items, (priority, item))

    def dequeue(self):
        """Hapus elemen dengan prioritas tertinggi"""
        if not self.is_empty():
            return heapq.heappop(self.items)[1]
        return None

    def is_empty(self):
        return len(self.items) == 0
```

### 4. Double Ended Queue (Deque)

Queue yang bisa enqueue/dequeue dari kedua ujung.

```python
class Deque:
    def __init__(self):
        self.items = deque()

    def add_front(self, item):
        """Tambah ke depan"""
        self.items.appendleft(item)

    def add_rear(self, item):
        """Tambah ke belakang"""
        self.items.append(item)

    def remove_front(self):
        """Hapus dari depan"""
        return self.items.popleft() if not self.is_empty() else None

    def remove_rear(self):
        """Hapus dari belakang"""
        return self.items.pop() if not self.is_empty() else None

    def is_empty(self):
        return len(self.items) == 0

    def size(self):
        return len(self.items)
```

## Aplikasi Queue

### 1. Proses Printer

Dokumen yang diprint antri didasarkan FIFO.

```python
def printer_queue_simulation():
    print_queue = EfficientQueue()

    # Dokumen masuk
    print_queue.enqueue("Document1.pdf")
    print_queue.enqueue("Document2.docx")
    print_queue.enqueue("Document3.jpg")

    # Proses printing
    while not print_queue.is_empty():
        doc = print_queue.dequeue()
        print(f"Printing: {doc}")
```

### 2. Customer Service Queue

Pelanggan dilayani berdasarkan FIFO.

```python
def customer_service():
    queue = EfficientQueue()

    # Pelanggan masuk
    queue.enqueue("Customer1")
    queue.enqueue("Customer2")
    queue.enqueue("Customer3")

    # Pelayanan
    service_time = 1
    while not queue.is_empty():
        customer = queue.dequeue()
        print(f"Melayani: {customer} (Time: {service_time}s)")
        service_time += 1
```

### 3. Breadth-First Search (BFS)

Queue digunakan untuk traversal graph/tree secara BFS.

```python
def bfs(graph, start):
    visited = set()
    queue = EfficientQueue()
    queue.enqueue(start)
    visited.add(start)

    while not queue.is_empty():
        node = queue.dequeue()
        print(node, end=" ")

        for neighbor in graph[node]:
            if neighbor not in visited:
                queue.enqueue(neighbor)
                visited.add(neighbor)

    print()
```

### 4. Round Robin Scheduling dalam OS

Process scheduling di sistem operasi.

```python
def round_robin_scheduling(processes, time_slice):
    queue = EfficientQueue()

    for process in processes:
        queue.enqueue(process)

    current_time = 0

    while not queue.is_empty():
        process = queue.dequeue()
        execute_time = min(process['burst_time'], time_slice)

        print(f"Waktu {current_time}-{current_time + execute_time}: {process['name']}")
        current_time += execute_time

        process['burst_time'] -= execute_time

        if process['burst_time'] > 0:
            queue.enqueue(process)
        else:
            print(f"  {process['name']} selesai")
```

### 5. Level Order Traversal Tree

```python
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

def level_order_traversal(root):
    if not root:
        return

    queue = EfficientQueue()
    queue.enqueue(root)

    while not queue.is_empty():
        node = queue.dequeue()
        print(node.val, end=" ")

        if node.left:
            queue.enqueue(node.left)
        if node.right:
            queue.enqueue(node.right)
```

### 6. Server Request Processing

Antrian request yang diterima server.

```python
def server_request_processing():
    request_queue = PriorityQueue()

    # Menerima request dengan prioritas
    request_queue.enqueue("Simple Query", priority=3)
    request_queue.enqueue("File Upload", priority=1)
    request_queue.enqueue("Database Update", priority=2)

    # Proses berdasarkan prioritas
    while not request_queue.is_empty():
        request = request_queue.dequeue()
        print(f"Processing: {request}")
```

## Contoh Implementasi Lengkap

```python
# Program: Simulasi Antrian Minimarket

from collections import deque

class Cashier:
    def __init__(self, name):
        self.name = name
        self.queue = deque()

    def add_customer(self, customer):
        self.queue.append(customer)
        print(f"{customer} bergabung di antrian {self.name}")

    def serve_customer(self):
        if self.queue:
            customer = self.queue.popleft()
            print(f"{self.name} melayani {customer}")
            return customer
        else:
            print(f"{self.name} sedang menganggur")
            return None

    def queue_length(self):
        return len(self.queue)

# Simulasi
cashier1 = Cashier("Kasir 1")
cashier2 = Cashier("Kasir 2")

# Pelanggan masuk
cashier1.add_customer("Pelanggan A")
cashier1.add_customer("Pelanggan B")
cashier2.add_customer("Pelanggan C")
cashier1.add_customer("Pelanggan D")

print("\n--- Mulai Pelayanan ---")
cashier1.serve_customer()
cashier2.serve_customer()
cashier1.serve_customer()
cashier2.serve_customer()

print(f"\nSisa antrian Kasir 1: {cashier1.queue_length()}")
print(f"Sisa antrian Kasir 2: {cashier2.queue_length()}")
```

## Kompleksitas Queue

| Operasi | Array (List) | Deque | Linked List |
| ------- | ------------ | ----- | ----------- |
| Enqueue | O(1)         | O(1)  | O(1)        |
| Dequeue | O(n)         | O(1)  | O(1)        |
| Front   | O(1)         | O(1)  | O(1)        |
| Search  | O(n)         | O(n)  | O(n)        |
| Space   | O(n)         | O(n)  | O(n)        |

**Rekomendasi**: Gunakan `collections.deque` untuk implementasi yang efisien!

## Keuntungan dan Kelemahan

### Keuntungan

- Model real-world yang natural (antrian)
- Operasi O(1) untuk enqueue dan dequeue (dengan deque)
- Mudah diimplementasikan
- Cocok untuk scheduling dan buffering

### Kelemahan

- Akses terbatas hanya di depan dan belakang
- Tidak bisa akses elemen tengah
- Dequeue dari list biasa adalah O(n)
- Tidak cocok untuk pencarian random

## Kesimpulan

Queue adalah struktur data yang sangat penting dalam sistem computing. Dengan FIFO principle-nya, queue memungkinkan penyelesaian berbagai masalah praktis seperti job scheduling, customer service, dan graph traversal. Untuk implementasi yang efisien, gunakan `collections.deque` daripada list biasa.
