# Yandex handbook "Python Basics" answers

4.1. Функции. Области видимости. Передача параметров в функции

A. Функциональное приветствие
```python
def print_hello(name):
    print(f'Hello, {name}!')   
```
B. Функциональный НОД
```python
def gcd(a, b):
    while b:
        a, b = b, a % b
    return a
```
C. Длина числа
```python
def number_length(number):
    return len(str(abs(number)))
```
D. Копейка рубль бережёт
```python
def take_small(money):
    return [x for x in money if x < 100]
```
E. Виртуальный кликер
```python
count = 0


def click():
    global count
    count += 1

    
def get_count():
    return count
```
F. Странная игра
```python
total = 0


def move(player, number):
    global total
    if player == "Петя":
        total += number
    elif player == "Ваня":
        total -= number


def game_over():
    if total > 0:
        return "Петя"
    elif total < 0:
        return "Ваня"
    else:
        return "Ничья"
```
G. Максимальный максимум
```python
def max2D(matrix):
    return max(max(row) for row in matrix)
```
H. Числовое фрагментирование
```python
def fragments(numbers):
    if not numbers:
        return []

    result = []
    current = [numbers[0]]

    for num in numbers[1:]:
        if num > current[-1]:
            current.append(num)
        else:
            result.append(current)
            current = [num]

    result.append(current)
    return result
```
I. Имя of the month
```python
def month(number, language):
    MONTH = {
        'en': [
            'January', 'February', 'March',
            'April', 'May', 'June',
            'July', 'August', 'September',
            'October', 'November', 'December'
        ],
        'ru': [
            'Январь', 'Февраль', 'Март',
            'Апрель', 'Май', 'Июнь',
            'Июль', 'Август', 'Сентябрь',
            'Октябрь', 'Ноябрь', 'Декабрь'
        ]
    }
    return MONTH[language][number - 1]
```
J. Числовая строка
```python
def split_numbers(line):
    return tuple(map(int, line.split()))
```
K. Поиск гор
```python
def find_mountains(heights):
    mountains = []
    n = len(heights)
    for i in range(1, n-1):
        if heights[i] > heights[i-1] and heights[i] > heights[i+1]:
            mountains.append(i + 1)  # +1 for 1-based indexing
    return tuple(mountains)
```
L. Поиск гор 2
```python
def find_mountains(data):
    rows = len(data)
    cols = len(data[0]) if rows > 0 else 0
    mountains = []

    directions = [(-1, -1), (-1, 0), (-1, 1), (0, -1), (0, 1), (1, -1), (1, 0), (1, 1)]

    for i in range(1, rows - 1):
        for j in range(1, cols - 1):
            current = data[i][j]
            if all(current > data[i + di][j + dj] for di, dj in directions):
                mountains.append((i + 1, j + 1))  # 1-based indexing

    return tuple(mountains)
```
M. Модернизация системы вывода
```python
lst = []


def modern_print(string):
    print(string) if string not in lst else None
    lst.append(string)
```




N. Шахматный «обед»
```python
def can_eat(horse, shape):
    return abs(horse[0] - shape[0]) + abs(horse[1] - shape[1]) == 3
```
O. Слвоварная строка
```python
def get_dict(text):
    def convert_value(value):
        try:
            return int(value)
        except ValueError:
            try:
                return float(value)
            except ValueError:
                return value
    pairs = text.split(';')
    return {k: convert_value(v) for k, v in (pair.split('=') for pair in pairs)}
```
P. А роза упала на лапу Азора 7.0
```python
def is_palindrome(n):
    return str(n) == str(n)[::-1] if isinstance(n, int) else n == n[::-1]
```
Q. Простая задача 5.0
```python
def is_prime(n):
    for i in range(2, int(n**0.5) + 1):
        if not n % i:
            return False
    return n != 1
```
R. Слияние
```python
def merge(a, b):
    c = list(a) + list(b)
    n = len(c)
    for i in range(n):
        for j in range(0, n - i - 1):
            if c[j] > c[j + 1]:
                c[j], c[j + 1] = c[j + 1], c[j]
    return tuple(c)
```
S. Обмен содержимым
```python
def swap(a, b):
    a[:], b[:] = b[:], a[:]
```
T. Цезарю - Цезарева
```python
def roman(a, b):
    def to_roman(num):
        val = [
            (1000, "M"), (900, "CM"), (500, "D"), (400, "CD"),
            (100, "C"), (90, "XC"), (50, "L"), (40, "XL"),
            (10, "X"), (9, "IX"), (5, "V"), (4, "IV"), (1, "I")
        ]
        res = ""
        for v, symbol in val:
            while num >= v:
                res += symbol
                num -= v
        return res
    
    roman_a = to_roman(a)
    roman_b = to_roman(b)
    roman_sum = to_roman(a + b)
    
    return f"{roman_a} + {roman_b} = {roman_sum}"
```
