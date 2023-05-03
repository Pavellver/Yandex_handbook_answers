# Yandex handbook "Python Basics" answers

2.3. Циклы

A. Раз, два, три! Ёлочка, гори!
```python
while input() != 'Три!':
    print('Режим ожидания...')
print('Ёлочка, гори!')    
```
B. Зайка — 3
```python
counter = 0
while (x := input()) != 'Приехали!':
    if 'зайка' in x:
        counter += 1
print(counter)
```
C. Считалочка
```python
a, b = int(input()), int(input())
for i in range(a, b + 1):
    print(i, end=' ')
```
D. Считалочка 2.0
```python
a, b = int(input()), int(input())
if a < b:
    for i in range(a, b + 1):
        print(i, end=' ')
else:
    for i in range(a, b - 1, -1):
        print(i, end=' ')
```
E. Внимание! Акция!
```python
counter = 0
while (x := input()) != '0':
    if float(x) >= 500:
        counter += 0.9 * float(x)
    else:
        counter += float(x)
print(counter)
```
F. НОД
```python
a, b = int(input()), int(input())
while b:
    a, b = b, a % b
print(a)
```
G. НОК
```python
a, b = c, d = int(input()), int(input())
while b:
    a, b = b, a % b
print(c * d // a)
```
H. Излишняя автоматизация 2.0
```python
line, number = input(), int(input())
for _ in range(number):
    print(line)
```
I. Факториал
```python
a = int(input())
factorial = 1
for i in range(1, a + 1):
    factorial *= i
print(factorial)
```
J. Маршрут построен
```python
x, y = 0, 0
while (direction := input()) != 'СТОП':
    n = int(input())
    if direction == 'ВОСТОК':
        x += n
    elif direction == 'ЗАПАД':
        x -= n
    elif direction == 'СЕВЕР':
        y += n
    elif direction == 'ЮГ':
        y -= n
print(y, x, sep='\n')
```
K. Цифровая сумма
```python
print(sum(map(int, input())))
```
L. Сильная цифра
```python
print(max(map(int, input())))
```
M. Первому игроку приготовиться 2.0
```python
n, first = int(input()), input()
for _ in range(n - 1):
    first = min(first, input())
print(first)
```
N. Простая задача
```python
n = int(input())
i, result = 2, 'YES'
if n > 1:
    while n % i:
        if i > n ** 0.5:
            break
        i += 1
    else:
        result = 'NO'
else:
    result = 'NO'
print(result)
```
O. Зайка - 4
```python
counter = 0
for _ in range(int(input())):
    if 'зайка' in input():
        counter += 1
print(counter)
```
P. А роза упала на лапу Азора 2.0
```python
print('YES') if (x := input()) == x[::-1] else print('NO')
```
Q. Чётная чистота
```python
print(''.join(filter(lambda x: int(x) % 2, input())))
```
R. Простая задача 2.0
```python
n, result, i = int(input()), [], 1
if n < 2:
    print(n)
while n > 1:
    i += 1
    if not n % i:
        result.append(str(i))
        n //= i
        i = 1
else:
    print(' * '.join(result))
```
S. Игра в «Угадайку»
```python
begin, end = 1, 1001
print((begin + end) // 2)
while (x := input()) != 'Угадал!':
    if x == 'Меньше':
        end = (begin + end) // 2
        print((begin + end) // 2)
    elif x == 'Больше':
        begin = (begin + end) // 2
        print((begin + end) // 2)
print('=' * 35)
```
T. Хайпанём немножечко!
```python
result, hn1 = -1, 0
for i in range(int(input())):
    b = int(input())
    h, r, m = b % 256, (b // 256) % 256, b // 256 ** 2
    t = ((m + r + hn1) * 37) % 256
    if t != h or h > 99:
        result = i
        break
    hn1 = h
print(result)
```
