#  TREE & PARSE TREE

---

## 1. Pengertian Tree

**Tree** adalah struktur data non-linear yang terdiri dari node (simpul) yang saling terhubung dalam bentuk hierarki.

Tree banyak digunakan dalam:
- Struktur folder
- Struktur organisasi
- Parsing bahasa pemrograman

###  Ciri-ciri Tree:
- Memiliki satu **root (akar)**
- Memiliki hubungan **parent-child**
- Tidak memiliki siklus (tidak loop)
- Bersifat hierarki

---

## 2. Terminologi pada Tree

| Istilah   | Penjelasan |
|----------|-----------|
| Root     | Node paling atas |
| Parent   | Node yang memiliki anak |
| Child    | Node turunan |
| Leaf     | Node tanpa anak |
| Subtree  | Bagian dari tree |

---

## 3. Struktur Tree

Contoh bentuk tree:

```
A
├── B
│   ├── D
│   └── E
└── C
```

---

## 4. Representasi Tree dalam Program

Tree biasanya direpresentasikan menggunakan class.

### Contoh (Python):

```python
class Node:
    def __init__(self, value):
        self.value = value
        self.children = []

    def add_child(self, child):
        self.children.append(child)
```

---

## 5. Menampilkan Tree

```python
def print_tree(node, level=0):
    print("  " * level + str(node.value))
    for child in node.children:
        print_tree(child, level + 1)

# contoh penggunaan
root = Node("A")
b = Node("B")
c = Node("C")
d = Node("D")
e = Node("E")

root.add_child(b)
root.add_child(c)
b.add_child(d)
b.add_child(e)

print_tree(root)
```

---

## 6. Traversal Tree

Traversal adalah cara mengunjungi semua node dalam tree.

### 🔹 Preorder
Root → Child

### 🔹 Inorder (Binary Tree)
Left → Root → Right

### 🔹 Postorder
Child → Root

---

## 7. Pengertian Parse Tree

**Parse Tree** adalah struktur tree yang digunakan untuk merepresentasikan ekspresi berdasarkan aturan grammar.

Digunakan dalam:
- Compiler
- Interpreter
- Parsing ekspresi matematika

---

## 8. Contoh Parse Tree

Ekspresi:
```
3 + 5
```

Parse Tree:
```
    +
   / \
  3   5
```

---

## 9. Komponen Parse Tree

- **Operator** → menjadi parent (node tengah)
- **Operand** → menjadi leaf (angka/variabel)

---

## 10. Konsep Token

**Token** adalah bagian kecil dari input yang diproses oleh parser.

Contoh:
```
"3 + 5"
```

Token:
```
["3", "+", "5"]
```

---

## 11. Proses Parsing

Parsing adalah proses membaca token satu per satu dan membangun tree.

### Langkah-langkah:
1. Membaca token
2. Menentukan node
3. Menentukan posisi (left/right)
4. Menyusun tree

---

## 12. Trace Parse Tree

**Trace parsing** adalah proses menampilkan langkah parsing secara detail.

### Contoh Trace:

```
Baca token: 3 → jadi left node
Baca token: + → jadi root
Baca token: 5 → jadi right node
```

---

## 13. Implementasi Parse Tree Sederhana

```python
class Node:
    def __init__(self, value):
        self.value = value
        self.left = None
        self.right = None

def parse_expression(tokens):
    print("Mulai parsing...")

    left = Node(tokens[0])
    print(f"Baca token: {tokens[0]} -> left node")

    operator = tokens[1]
    print(f"Baca token: {operator} -> root")

    right = Node(tokens[2])
    print(f"Baca token: {tokens[2]} -> right node")

    root = Node(operator)
    root.left = left
    root.right = right

    return root

def print_parse_tree(node, level=0):
    if node:
        print("  " * level + str(node.value))
        print_parse_tree(node.left, level + 1)
        print_parse_tree(node.right, level + 1)

# contoh penggunaan
expression = "3 + 5"
tokens = expression.split()

tree = parse_expression(tokens)

print("\nParse Tree:")
print_parse_tree(tree)
```

---

## 14. Output Program

```
Mulai parsing...
Baca token: 3 -> left node
Baca token: + -> root
Baca token: 5 -> right node

Parse Tree:
+
  3
  5
```

---

## 15. Kesimpulan

- Tree adalah struktur data berbentuk hierarki
- Parse tree digunakan untuk merepresentasikan struktur ekspresi
- Parsing membaca token dan membangun tree
- Trace parsing membantu memahami proses parsing secara detail

---
