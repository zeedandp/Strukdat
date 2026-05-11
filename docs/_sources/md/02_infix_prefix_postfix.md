# Infix, Prefix, dan Postfix Expressions

## Pengertian Notasi Ekspresi

Notasi ekspresi adalah cara untuk menuliskan operasi matematika. Ada tiga macam notasi yang umum digunakan dalam ilmu komputer:

1. **Infix**: Operasi ditulis di tengah operand (standar matematika)
2. **Prefix (Polish Notation)**: Operasi ditulis sebelum operand
3. **Postfix (Reverse Polish Notation)**: Operasi ditulis setelah operand

## 1. Infix Notation (Notasi Infix)

### Pengertian

Infix adalah notasi yang paling dikenal dan digunakan dalam matematika biasa. Operator ditulis di antara kedua operand.

### Format

```
operand1 operator operand2
```

### Contoh

```
2 + 3
5 * 4 - 2
(3 + 4) * 5
a + b * c
```

### Karakteristik

- Memerlukan tanda kurung untuk menentukan prioritas
- Memerlukan aturan prioritas operator (precedence)
- Memerlukan aturan asosiasi (associativity)
- Format yang paling mudah dipahami manusia

### Aturan Prioritas Operator (Precedence)

1. Kurung: `( )`
2. Eksponensial: `^` atau `**`
3. Perkalian & Pembagian: `*`, `/`, `%`
4. Penjumlahan & Pengurangan: `+`, `-`

### Aturan Asosiasi (Associativity)

- **Left-to-Right**: `+`, `-`, `*`, `/`, `%` (10 - 5 - 2 = 3)
- **Right-to-Left**: `^` (2 ^ 3 ^ 2 = 2 ^ 9 = 512)

## 2. Prefix Notation (Polish Notation)

### Pengertian

Prefix adalah notasi dimana operator ditulis sebelum kedua operand-nya. Dikembangkan oleh Jan Łukasiewicz.

### Format

```
operator operand1 operand2
```

### Contoh

```
+ 2 3                 → 2 + 3 = 5
- * 5 4 2            → (5 * 4) - 2 = 18
* + 3 4 5            → (3 + 4) * 5 = 35
+ * 2 3 / 8 4        → (2 * 3) + (8 / 4) = 8
```

### Karakteristik

- Tidak memerlukan tanda kurung
- Tidak memerlukan prioritas operator
- Lebih sulit dibaca oleh manusia
- Digunakan dalam beberapa bahasa pemrograman

### Evaluasi Prefix

Untuk mengevaluasi: scan dari **kanan ke kiri**

```
Algoritma:
1. Scan ekspresi dari kanan ke kiri
2. Jika operand, push ke stack
3. Jika operator, pop 2 operand, hitung, push hasil
4. Result ada di top stack
```

Contoh: `+ 2 * 3 4`

```
Scan dari kanan ke kiri:
4 → push 4, stack: [4]
3 → push 3, stack: [4, 3]
* → pop 3, pop 4, hitung 3*4=12, push 12, stack: [12]
2 → push 2, stack: [12, 2]
+ → pop 2, pop 12, hitung 2+12=14, push 14, stack: [14]

Hasil: 14
```

```python
def evaluate_prefix(expression):
    """Evaluasi prefix expression"""
    stack = []
    tokens = expression.split()

    # Scan dari kanan ke kiri
    for token in reversed(tokens):
        if token in ['+', '-', '*', '/', '^']:
            # Pop operand
            operand1 = stack.pop()
            operand2 = stack.pop()

            # Hitung
            if token == '+':
                result = operand1 + operand2
            elif token == '-':
                result = operand1 - operand2
            elif token == '*':
                result = operand1 * operand2
            elif token == '/':
                result = operand1 / operand2
            elif token == '^':
                result = operand1 ** operand2

            stack.append(result)
        else:
            stack.append(float(token))

    return stack[0]

# Contoh
print(evaluate_prefix("+ 2 * 3 4"))  # 14
print(evaluate_prefix("- * 5 4 2"))  # 18
```

## 3. Postfix Notation (Reverse Polish Notation)

### Pengertian

Postfix adalah notasi dimana operator ditulis setelah kedua operand-nya. Juga dikenal sebagai Reverse Polish Notation (RPN).

### Format

```
operand1 operand2 operator
```

### Contoh

```
2 3 +                 → 2 + 3 = 5
5 4 * 2 -            → (5 * 4) - 2 = 18
3 4 + 5 *            → (3 + 4) * 5 = 35
2 3 * 8 4 / +        → (2 * 3) + (8 / 4) = 8
```

### Karakteristik

- Tidak memerlukan tanda kurung
- Tidak memerlukan prioritas operator
- Lebih mudah dievaluasi komputer
- Lebih sulit dibaca oleh manusia
- Digunakan dalam kalkulator HP, Java Virtual Machine

### Evaluasi Postfix

Untuk mengevaluasi: scan dari **kiri ke kanan**

```
Algoritma:
1. Scan ekspresi dari kiri ke kanan
2. Jika operand, push ke stack
3. Jika operator, pop 2 operand, hitung, push hasil
4. Result ada di top stack
```

Contoh: `2 3 4 + *`

```
Scan dari kiri ke kanan:
2 → push 2, stack: [2]
3 → push 3, stack: [2, 3]
4 → push 4, stack: [2, 3, 4]
+ → pop 4, pop 3, hitung 3+4=7, push 7, stack: [2, 7]
* → pop 7, pop 2, hitung 2*7=14, push 14, stack: [14]

Hasil: 14
```

```python
def evaluate_postfix(expression):
    """Evaluasi postfix expression"""
    stack = []
    tokens = expression.split()

    # Scan dari kiri ke kanan
    for token in tokens:
        if token in ['+', '-', '*', '/', '^']:
            # Pop operand (urutan penting!)
            operand2 = stack.pop()
            operand1 = stack.pop()

            # Hitung
            if token == '+':
                result = operand1 + operand2
            elif token == '-':
                result = operand1 - operand2
            elif token == '*':
                result = operand1 * operand2
            elif token == '/':
                result = operand1 / operand2
            elif token == '^':
                result = operand1 ** operand2

            stack.append(result)
        else:
            stack.append(float(token))

    return stack[0]

# Contoh
print(evaluate_postfix("2 3 +"))              # 5
print(evaluate_postfix("5 4 * 2 -"))         # 18
print(evaluate_postfix("3 4 + 5 *"))         # 35
print(evaluate_postfix("2 3 * 8 4 / +"))     # 8
```

### Contoh Penuh: Input = A + (B - C) \* D

```
Langkah | Simbol | Stack | Output
--------|--------|-------|-------
1       | A      |       | A
2       | +      | +     | A
3       | (      | +(    | A
4       | B      | +(    | AB
5       | -      | +(-   | AB
6       | C      | +(-   | ABC
7       | )      | +     | ABC-
8       | *      | +*    | ABC-
9       | D      | +*    | ABC-D
10      | (end)  |       | ABC-D*+

Output Akhir: A B C - D * +
```

```python
def precedence(op):
    """Menentukan prioritas operator"""
    if op == '+' or op == '-':
        return 1
    if op == '*' or op == '/':
        return 2
    if op == '^':
        return 3
    return 0

def infToPostf(infix_expr):
    """Konversi infix ke postfix"""
    operand = ["A","B","C","D","E","F","G","H","I","J","K","L","M","N","O","P"]
    stk = []
    output = ""

    for char in infix_expr:
        if char == " ":
            continue

        # Jika operand
        if char in operand:
            output += char

        # Jika opening bracket
        elif char == '(':
            stk.append(char)

        # Jika closing bracket
        elif char == ')':
            while stk and stk[-1] != '(':
                output += stk.pop()
            if stk:
                stk.pop()  # Remove opening bracket

        # Jika operator
        else:
            while len(stk) > 0:
                top = stk[-1]
                if top == '(':
                    break
                if precedence(top) < precedence(char):
                    break
                output += stk.pop()
            stk.append(char)

    # Pop semua operator yang tersisa
    while len(stk) > 0:
        output += stk.pop()

    return output

# Contoh
print(infToPostf("A + (B - C) * D"))
# Output: ABC-D*+
```

### Contoh Implementasi Lengkap

```python
def stack():
    s = []
    return s

def push(s, data):
    s.append(data)

def pop(s):
    return s.pop()

def peek(s):
    return s[-1]

def isEmpty(s):
    return s == []

def precedence(op):
    if op == '+' or op == '-':
        return 1
    if op == '*' or op == '/':
        return 2
    if op == '^':
        return 3
    return 0

def infixToPostfix(infix):
    """Konversi infix ke postfix dengan proses detail"""
    operand = ["A","B","C","D","E","F","G","H","I","J","K","L","M","N","O","P"]
    stk = stack()
    res = ""
    steps = []
    step_num = 0

    for i in infix:
        if i == " ":
            continue

        if i in operand:
            res += i
            step_num += 1
            steps.append(f"{step_num}. Operand '{i}': Output = {res}, Stack = {stk}")

        elif i == '(':
            push(stk, i)
            step_num += 1
            steps.append(f"{step_num}. Opening bracket '(': Output = {res}, Stack = {stk}")

        elif i == ')':
            while len(stk) > 0 and stk[-1] != '(':
                res += pop(stk)
            if stk:
                pop(stk)  # Remove '('
            step_num += 1
            steps.append(f"{step_num}. Closing bracket ')': Output = {res}, Stack = {stk}")

        else:  # Operator
            while len(stk) > 0:
                top = stk[-1]
                if top == '(':
                    break
                if precedence(top) < precedence(i):
                    break
                res += pop(stk)
            push(stk, i)
            step_num += 1
            steps.append(f"{step_num}. Operator '{i}': Output = {res}, Stack = {stk}")

    while len(stk) > 0:
        res += pop(stk)

    return res, steps

# Contoh penggunaan
result, steps = infixToPostfix("A + (B - C) * D")
print("=== Proses Konversi ===")
for step in steps:
    print(step)
print(f"\nHasil Akhir: {result}")
```

## Konversi Infix ke Postfix

**Algoritma (Shunting Yard)**

```
1. Siapkan output queue dan operator stack
2. Scan infix dari kiri ke kanan
3. Jika operand, tambah ke output queue
4. Jika operator:
   - Selama ada operator di stack dengan precedence >= operator saat ini
     dan associativity left-to-right, pop dan tambah ke output queue
   - Push operator saat ini ke stack
5. Jika '(', push ke stack
6. Jika ')':
   - Pop dan tambah ke output queue sampai menemukan '('
   - Pop '(' (jangan tambah ke output)
7. Pop semua sisa operator di stack ke output queue
```

```python
def infix_to_postfix(infix):
    """Konversi infix ke postfix menggunakan Shunting Yard"""
    precedence = {'+': 1, '-': 1, '*': 2, '/': 2, '^': 3}
    right_associative = {'^'}  # Right-associative operators

    output_queue = []
    operator_stack = []
    tokens = infix.split()

    for token in tokens:
        if token not in ['+', '-', '*', '/', '^', '(', ')']:
            # Operand
            output_queue.append(token)

        elif token in precedence:
            # Operator
            while (operator_stack and
                   operator_stack[-1] != '(' and
                   operator_stack[-1] in precedence):

                top_precedence = precedence[operator_stack[-1]]
                curr_precedence = precedence[token]

                if token in right_associative:
                    if top_precedence > curr_precedence:
                        output_queue.append(operator_stack.pop())
                    else:
                        break
                else:
                    if top_precedence >= curr_precedence:
                        output_queue.append(operator_stack.pop())
                    else:
                        break

            operator_stack.append(token)

        elif token == '(':
            operator_stack.append(token)

        elif token == ')':
            while operator_stack and operator_stack[-1] != '(':
                output_queue.append(operator_stack.pop())
            if operator_stack:
                operator_stack.pop()  # Remove '('

    # Pop sisa operator
    while operator_stack:
        output_queue.append(operator_stack.pop())

    return ' '.join(output_queue)

# Contoh
print(infix_to_postfix("3 + 4 * 5"))      # 3 4 5 * +
print(infix_to_postfix("( 3 + 4 ) * 5"))  # 3 4 + 5 *
print(infix_to_postfix("10 + 2 * 6"))     # 10 2 6 * +
```

### B. Infix ke Prefix

**Algoritma**
Reverse infix → Reverse ( ) → Swap ( ) → Convert to Postfix → Reverse

```python
def infix_to_prefix(infix):
    """Konversi infix ke prefix"""
    # 1. Reverse infix
    tokens = infix.split()
    reversed_infix = ' '.join(reversed(tokens))

    # 2. Reverse (swap) parenthesis
    reversed_infix = reversed_infix.replace('(', 'TEMP')
    reversed_infix = reversed_infix.replace(')', '(')
    reversed_infix = reversed_infix.replace('TEMP', ')')

    # 3. Konversi ke postfix
    postfix = infix_to_postfix(reversed_infix)

    # 4. Reverse kembali
    tokens = postfix.split()
    prefix = ' '.join(reversed(tokens))

    return prefix

# Contoh
print(infix_to_prefix("3 + 4 * 5"))      # * + 3 4 5
print(infix_to_prefix("( 3 + 4 ) * 5"))  # * + 3 4 5
```

### C. Postfix ke Infix

```python
def postfix_to_infix(postfix):
    """Konversi postfix ke infix"""
    stack = []
    tokens = postfix.split()

    for token in tokens:
        if token in ['+', '-', '*', '/', '^']:
            # Pop 2 operand
            b = stack.pop()
            a = stack.pop()
            # Push result dengan infix format
            infix_expr = f"( {a} {token} {b} )"
            stack.append(infix_expr)
        else:
            stack.append(token)

    return stack[0]

# Contoh
print(postfix_to_infix("3 4 5 * +"))      # ( 3 ( 4 5 * ) )
print(postfix_to_infix("3 4 + 5 *"))     # ( ( 3 4 + ) 5 * )
```

### D. Prefix ke Infix

```python
def prefix_to_infix(prefix):
    """Konversi prefix ke infix"""
    stack = []
    tokens = prefix.split()

    # Scan dari kanan ke kiri
    for token in reversed(tokens):
        if token in ['+', '-', '*', '/', '^']:
            # Pop 2 operand
            a = stack.pop()
            b = stack.pop()
            # Push result dengan infix format
            infix_expr = f"( {a} {token} {b} )"
            stack.append(infix_expr)
        else:
            stack.append(token)

    return stack[0]

# Contoh
print(prefix_to_infix("+ 3 * 4 5"))      # ( 3 ( 4 5 * ) )
print(prefix_to_infix("* + 3 4 5"))     # ( ( 3 4 + ) 5 * )
```

## Tabel Perbandingan

| Aspek             | Infix        | Prefix                 | Postfix             |
| ----------------- | ------------ | ---------------------- | ------------------- |
| Readability       | Sangat mudah | Sulit                  | Sulit               |
| Precedence        | Diperlukan   | Tidak                  | Tidak               |
| Parenthesis       | Diperlukan   | Tidak                  | Tidak               |
| Evaluasi Manual   | Sulit        | Medium                 | Mudah               |
| Evaluasi Komputer | Sulit        | Medium                 | Mudah               |
| Digunakan di      | Matematika   | Fungsional Programming | RPN Kalkulator, JVM |

## Aplikasi Praktis

### 1. Kalkulator RPN (Postfix)

```python
def rpn_calculator():
    """Simulasi kalkulator RPN"""
    stack = []

    print("=== RPN Calculator ===")
    print("Masukkan operand atau operator (atau 'q' untuk keluar)")

    while True:
        inp = input(">> ")

        if inp.lower() == 'q':
            break

        if inp in ['+', '-', '*', '/']:
            if len(stack) < 2:
                print("Error: Operand tidak cukup")
                continue

            b = stack.pop()
            a = stack.pop()

            if inp == '+':
                result = a + b
            elif inp == '-':
                result = a - b
            elif inp == '*':
                result = a * b
            elif inp == '/':
                result = a / b

            stack.append(result)
            print(f"Result: {result}, Stack: {stack}")
        else:
            try:
                stack.append(float(inp))
                print(f"Stack: {stack}")
            except:
                print("Invalid input")

# Jalankan: rpn_calculator()
```

### 2. Expression Evaluator

```python
def evaluate_expression(expr, notation='infix'):
    """Evaluasi ekspresi dalam berbagai notasi"""
    if notation == 'infix':
        # Konversi ke postfix terlebih dahulu
        postfix = infix_to_postfix(expr)
        return evaluate_postfix(postfix)
    elif notation == 'prefix':
        return evaluate_prefix(expr)
    elif notation == 'postfix':
        return evaluate_postfix(expr)
    else:
        return None

# Contoh
print(evaluate_expression("3 + 4 * 5", 'infix'))      # 23
print(evaluate_expression("+ 3 * 4 5", 'prefix'))     # 23
print(evaluate_expression("3 4 5 * +", 'postfix'))    # 23
```

## Contoh Implementasi Lengkap

```python
# Program: Expression Converter & Evaluator

class ExpressionProcessor:
    def __init__(self):
        self.precedence = {'+': 1, '-': 1, '*': 2, '/': 2, '^': 3}
        self.right_associative = {'^'}

    def infix_to_postfix(self, infix):
        """Konversi infix ke postfix"""
        output_queue = []
        operator_stack = []
        tokens = infix.split()

        for token in tokens:
            if token not in ['+', '-', '*', '/', '^', '(', ')']:
                output_queue.append(token)
            elif token in self.precedence:
                while (operator_stack and
                       operator_stack[-1] != '(' and
                       operator_stack[-1] in self.precedence):
                    top_prec = self.precedence[operator_stack[-1]]
                    curr_prec = self.precedence[token]

                    if token in self.right_associative:
                        if top_prec > curr_prec:
                            output_queue.append(operator_stack.pop())
                        else:
                            break
                    else:
                        if top_prec >= curr_prec:
                            output_queue.append(operator_stack.pop())
                        else:
                            break

                operator_stack.append(token)
            elif token == '(':
                operator_stack.append(token)
            elif token == ')':
                while operator_stack and operator_stack[-1] != '(':
                    output_queue.append(operator_stack.pop())
                if operator_stack:
                    operator_stack.pop()

        while operator_stack:
            output_queue.append(operator_stack.pop())

        return ' '.join(output_queue)

    def evaluate_postfix(self, postfix):
        """Evaluasi postfix expression"""
        stack = []
        tokens = postfix.split()

        for token in tokens:
            if token in ['+', '-', '*', '/', '^']:
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
                elif token == '^':
                    result = a ** b

                stack.append(result)
            else:
                stack.append(float(token))

        return stack[0]

    def evaluate_infix(self, infix):
        """Evaluasi infix expression"""
        postfix = self.infix_to_postfix(infix)
        return self.evaluate_postfix(postfix)

# Contoh penggunaan
processor = ExpressionProcessor()

# Test
print("=== Expression Processor ===")
print(f"Infix: 3 + 4 * 5")
postfix = processor.infix_to_postfix("3 + 4 * 5")
print(f"Postfix: {postfix}")
print(f"Result: {processor.evaluate_infix('3 + 4 * 5')}")

print(f"\nInfix: ( 3 + 4 ) * 5")
postfix = processor.infix_to_postfix("( 3 + 4 ) * 5")
print(f"Postfix: {postfix}")
print(f"Result: {processor.evaluate_infix('( 3 + 4 ) * 5')}")

print(f"\nInfix: 10 + 2 * 6 - 3")
postfix = processor.infix_to_postfix("10 + 2 * 6 - 3")
print(f"Postfix: {postfix}")
print(f"Result: {processor.evaluate_infix('10 + 2 * 6 - 3')}")
```

## Kesimpulan

Pemahaman tentang infix, prefix, dan postfix expressions sangat penting dalam ilmu komputer:

1. **Infix**: Format standar untuk manusia, memerlukan parser yang kompleks
2. **Postfix**: Format ideal untuk komputer, mudah dievaluasi dengan stack
3. **Prefix**: Format unik, digunakan dalam functional programming

Stack memainkan peran krusial dalam konversi dan evaluasi ekspresi ini, menegaskan pentingnya struktur data dalam pemecahan masalah komputasi.
