# Yandex handbook "Python Basics" answers

3.1. Строки, кортежи, списки

A. Азбука
```python
for _ in range(int(input())):
    if (word := input())[0] not in 'абв':
        print('NO')
        break
else:
    print('YES')    
```
B. Кручу-верчу
```python
for i in input():
    print(i)
```
C. Анонс новости
```python
length = int(input())
for _ in range(int(input())):
    line = input()
    print(line[:length - 3].ljust(length, ".") if len(line) > length else line)
```
D. Очистка данных
```python
while (n := input()):
    if not n.endswith('@@@'):
        if n.startswith('##'):
            print(n[2:])
        else:
            print(n)
```
E. А роза упала на лапу Азора 4.0
```python
print('YES' if (line := input()) == line[::-1] else 'NO')
```
F. Зайка — 6
```python
counter = 0
for _ in range(int(input())):
    counter += input().count("зайка")
print(counter)
```
G. А и Б сидели на трубе
```python
print(sum(map(int, input().split())))
```
H. Зайка — 7
```python
for _ in range(int(input())):
    if "зайка" in (place := input()):
        print(place.index("зайка") + 1)
    else:
        print("Заек нет =(")
```
I. Без комментариев
```python
while (n := input()):
    if not n.startswith('#'):
        print(n[:(n.index('#') if '#' in n else len(n))])
```
J. Частотный анализ на минималках
```python
data = []
while (n := input()) != 'ФИНИШ':
    data.extend(n.lower().split())
max_count, data = 0, ''.join(data)
for symbol in set(data):
    max_count = max(max_count, data.count(symbol))
print(min([i for i in set(data) if data.count(i) == max_count]))
```
K. Найдётся всё
```python
headings = []
for _ in range(int(input())):
    headings.append(input())
word = input()
for heading in headings:
    if word.lower() in heading.lower():
        print(heading)
```
L. Меню питания
```python
order = ('Манная', 'Гречневая', 'Пшённая', 'Овсяная', 'Рисовая')
for i in range(int(input())):
    print(order[i % len(order)])
```
M. Массовое возведение в степень
```python
data = []
for _ in range(int(input())):
    data.append(int(input()))
number = int(input())
for i in data:
    print(i ** number)
```
N. Массовое возведение в степень 2.0
```python
data = list(map(int, input().split()))
number = int(input())
for i in data:
    print(i ** number, end=' ')
```
O. НОД 3.0
```python
numbers = list(map(int, input().split()))
a = numbers[0]
while len(numbers) > 1:
    b = numbers[1]
    while b:
        a, b = b, a % b
    numbers.pop(1)
print(a)
```
P. Анонс новости 2.0
```python
length, line = int(input()), []
for _ in range(int(input())):
    line.append(input())
for i in line:
    if length > 3:
        print(i[:length - 3] + "..." if len(i) >= length - 3 else (i + "..." if length == 4 else i))
        length -= len(i)
```
Q. А роза упала на лапу Азора 5.0
```python
line = ''.join(input().lower().split())
print('YES' if line == line[::-1] else 'NO')
```
R. RLE
```python
line = input()
temp_line, repeat = line[0], 1
for i in line[1:]:
    if i == temp_line:
        repeat += 1
    else:
        print(temp_line, repeat)
        temp_line, repeat = i, 1
print(temp_line, repeat)
```
S. Польский калькулятор
```python
data = list(input().split())
result = [int(data[0])]
for i in data[1:]:
    if i.isdigit():
        result.append(int(i))
    else:
        a = result.pop()
        exec("result[-1] " + i + "= a")
print(result[0])
```
T. Польский калькулятор — 2
```python
def factorial(n):
    return n * factorial(n - 1) if n > 1 else 1


data = list(input().split())
result = [int(data[0])]
for i in data[1:]:
    if i.isdigit():
        result.append(int(i))
    elif i == "/":
        a = result.pop()
        result[-1] //= a
    elif i == "~":
        result[-1] = -result[-1]
    elif i == "#":
        result.append(result[-1])
    elif i == "!":
        result[-1] = factorial(result[-1])
    elif i == "@":
        result.append(result.pop(-3))
    else:
        a = result.pop()
        exec("result[-1] " + i + "= a")
print(result[0])
```
