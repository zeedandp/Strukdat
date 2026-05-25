#  LINKED LIST (INSERT UNORDERED & ORDERED - PYTHON)

---

## 1. Konsep Dasar Linked List

Linked List adalah struktur data yang terdiri dari node-node:
- data → menyimpan nilai
- next → menunjuk ke node berikutnya

Contoh:
Head → 7 → 18 → 6 → None

---

## 2. Struktur Class

### Class Node

    class Node:
        def __init__(self, data):
            self.data = data
            self.next = None

Penjelasan:
- data → menyimpan nilai
- next → menunjuk ke node berikutnya

---

### Class LinkedList

    class LinkedList:
        def __init__(self):
            self.head = None

Penjelasan:
- head → node pertama

---

## 3. Method Dasar

### Append (Tambah di akhir)

    def append(self, data):
        new_node = Node(data)
        if not self.head:
            self.head = new_node
            return

        temp = self.head
        while temp.next:
            temp = temp.next
        temp.next = new_node

Penjelasan:
- Jika kosong → jadi head
- Jika tidak → traversal ke akhir

---

### Display

    def display(self):
        temp = self.head
        while temp:
            print(temp.data, end=" -> ")
            temp = temp.next
        print("None")

Output:
7 -> 18 -> 6 -> None

---

## 4. Insert Unordered

Konsep:
- Jika target ditemukan → sisipkan setelahnya
- Jika tidak → tambah di akhir

Code:

    def insert_unordered(self, target):
        temp = self.head

        while temp:
            if temp.data == target:
                new_node = Node(target)
                new_node.next = temp.next
                temp.next = new_node
                return
            temp = temp.next

        self.append(target)

---

Ilustrasi:

Jika ditemukan:
Head → 7 → 18 → 6 → None  
→ jadi  
Head → 7 → 18 → 18 → 6 → None  

Jika tidak ditemukan:
Head → 7 → 10 → 6 → None  
→ jadi  
Head → 7 → 10 → 6 → 18 → None  

---

## 5. Insert Ordered

Konsep:
- Digunakan untuk list terurut

Aturan:
1. Kosong → jadi head
2. Lebih kecil dari head → di depan
3. Selain itu → cari posisi

Code:

    def insert_ordered(self, data):
        new_node = Node(data)

        if not self.head or data < self.head.data:
            new_node.next = self.head
            self.head = new_node
            return

        temp = self.head

        while temp.next and temp.next.data < data:
            temp = temp.next

        new_node.next = temp.next
        temp.next = new_node

---

Ilustrasi:

Insert 7  → 7  
Insert 10 → 7 → 10  
Insert 6  → 6 → 7 → 10  
Insert 18 → 6 → 7 → 10 → 18  

---

## 6. Perbedaan

Unordered:
- Berdasarkan pencarian
- Bisa tambah di akhir

Ordered:
- Berdasarkan urutan
- Selalu di posisi yang benar

---

## 7. Program Lengkap

    class Node:
        def __init__(self, data):
            self.data = data
            self.next = None


    class LinkedList:
        def __init__(self):
            self.head = None

        def append(self, data):
            new_node = Node(data)
            if not self.head:
                self.head = new_node
                return

            temp = self.head
            while temp.next:
                temp = temp.next
            temp.next = new_node

        def display(self):
            temp = self.head
            while temp:
                print(temp.data, end=" -> ")
                temp = temp.next
            print("None")

        def insert_unordered(self, target):
            temp = self.head

            while temp:
                if temp.data == target:
                    new_node = Node(target)
                    new_node.next = temp.next
                    temp.next = new_node
                    return
                temp = temp.next

            self.append(target)

        def insert_ordered(self, data):
            new_node = Node(data)

            if not self.head or data < self.head.data:
                new_node.next = self.head
                self.head = new_node
                return

            temp = self.head

            while temp.next and temp.next.data < data:
                temp = temp.next

            new_node.next = temp.next
            temp.next = new_node


    # TEST
    ll = LinkedList()

    ll.append(7)
    ll.append(18)
    ll.append(6)

    print("Sebelum:")
    ll.display()

    ll.insert_unordered(18)

    print("Sesudah insert unordered:")
    ll.display()


    ll2 = LinkedList()
    ll2.insert_ordered(7)
    ll2.insert_ordered(10)
    ll2.insert_ordered(6)
    ll2.insert_ordered(18)

    print("\nOrdered list:")
    ll2.display()

---

## 8. Inti Penting

- Tidak ada index → pakai traversal
- Insert = manipulasi pointer
- Kunci:

    new_node.next = temp.next
    temp.next = new_node