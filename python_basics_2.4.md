# Yandex handbook "Python Basics" answers

2.4. Вложенные циклы

A. Таблица умножения
```python
for i in range(1, (x := int(input())) + 1):
    for j in range(1, x + 1):
        if j < x:
            print(i * j, end=' ')
        else:
            print(i * j)    
```
B. Не таблица умножения
```python
for i in range(1, (x := int(input())) + 1):
    for j in range(1, x + 1):
        print(f'{j} * {i} = {i * j}')
```
C. Новогоднее настроение
```python
for z in range(1, x := int(input()) + 1):
    if z in (sum(range(i)) for i in range(x)):
        print(z)
    else:
        print(z, end=' ')
```
D. Суммарная сумма
```python
summ = 0
for _ in range(int(input())):
    summ += sum(map(int, list(input())))
print(summ)
```
E. Зайка — 5
```python
counter, temp = 0, 0
for _ in range(int(input())):
    while (x := input()) != 'ВСЁ':
        if x == 'зайка':
            temp += 1
    if temp:
        counter += 1
        temp = 0
print(counter)
```
F. НОД 2.0
```python
n, a = int(input()), int(input())
for _ in range(n - 1):
    b = int(input())
    while b:
        a, b = b, a % b
print(a)
```
G. На старт! Внимание! Марш!
```python
for i in range(int(input())):
    for j in range(3 + i, 0, -1):
        print(f'До старта {j} секунд(ы)')
    print(f'Старт {i + 1}!!!')
```
H. Максимальная сумма
```python
name, summ = '', 0
for _ in range(int(input())):
    temp_name, temp_summ = input(), sum(map(int, input()))
    if temp_summ >= summ:
        name, summ = temp_name, temp_summ
print(name)
```
I. Большое число
```python
number = ''
for _ in range(int(input())):
    number += max(input())
print(number)
```
J. Мы делили апельсин
```python
for i in range(1, (n := int(input())) - 1):
    if i == 1:
        print('А Б В')
    for j in range(1, n - i):
        print(f'{i} {j} {n - i - j}')
```
K. Простая задача 3.0
```python
counter = 0
for i in range(int(input())):
    j = 2
    if (n := int(input())) > 1:
        counter += 1
        if n == 2:
            counter += 1
        while n % j:
            if j > n ** 0.5:
                break
            j += 1
        else:
            counter -= 1
print(counter)
```
L. Числовой прямоугольник
```python
n, k = int(input()), int(input())
width = len(str(n * k))
for i in range(1, n + 1):
    for j in range(k * (i - 1) + 1, k * i + 1):
        if j == k * i:
            print(str(j).rjust(width, ' '))
        else:
            print(str(j).rjust(width, ' '), end=' ')
```
M. Числовой прямоугольник 2.0
```python
n, k = int(input()), int(input())
width = len(str(n * k))
for i in range(1, n + 1):
    for j in range(i, i + n * (k - 1) + 1, n):
        if j == i + n * (k - 1):
            print(str(j).rjust(width, ' '))
        else:
            print(str(j).rjust(width, ' '), end=' ')
```
N. Числовая змейка
```python
n, k = int(input()), int(input())
width = len(str(n * k))
for i in range(1, n + 1):
    if i % 2:
        for j in range(k * (i - 1) + 1, k * i + 1):
            if j == k * i:
                print(str(j).rjust(width, ' '))
            else:
                print(str(j).rjust(width, ' '), end=' ')
    else:
        for j in range(k * i, k * (i - 1), -1):
            if j == k * (i - 1) + 1:
                print(str(j).rjust(width, ' '))
            else:
                print(str(j).rjust(width, ' '), end=' ')
```
O. Числовая змейка 2.0
```python
n, k = int(input()), int(input())
width = len(str(n * k))
for i in range(1, n + 1):
    for j in range(k):
        if not j % 2 and j != k - 1:
            print(str(i + 2 * n * (j // 2)).rjust(width, ' '), end=' ')
        elif not j % 2 and j == k - 1:
            print(str(i + 2 * n * (j // 2)).rjust(width, ' '))
        elif j % 2 and j != k - 1:
            print(str(2 * n * (j // 2 + 1) - (i - 1)).rjust(width, ' '), end=' ')
        else:
            print(str(2 * n * (j // 2 + 1) - (i - 1)).rjust(width, ' '))
```
P. Редизайн таблицы умножения
```python
a, b = int(input()), int(input())
for i in range(1, a + 1):
    for j in range(1, a + 1):
        if j != a:
            print(f'{(str(i * j) + " " if b % 2 else str(i * j)).center(b)}|', end='')
        else:
            print(f'{(str(i * j) + " " if b % 2 else str(i * j)).center(b)}')
    if i * j != a * a:
        print(f'{"-"* ((b + 1) * a - 1)}')
```
Q. А роза упала на лапу Азора 3.0
```python
counter = 0
for _ in range(int(input())):
    if (n := input()) == n[::-1]:
        counter += 1
print(counter)
```
R. Новогоднее настроение 2.0
```python
g, lengths = '', [0]
for j in range(1, (x := int(input())) + 1):
    g += str(j) + ' '
    if j in (sum(range(i)) for i in range(j + 2)):
        lengths.append(len(g) - 1)
        g = ''
lengths.append(len(g) - 1)
d = 1
for z in range(1, x + 1):
    if z - 1 in (sum(range(i)) for i in range(z + 2)):
        print(f"{' ' * ((max(lengths) - lengths[d]) // 2)}{z}", end=' ' if z != 1 else '\n')
        d += 1
    else:
        print(z, end='\n' if z in (sum(range(i)) for i in range(z + 2)) else ' ')
```
S. Числовой квадрат
```python
for i in range(n := int(input())):
    for j in range(n):
        d = str(min(i, j, n - i - 1, n - j - 1) + 1)
        print(d.rjust(len(str((n + 1) // 2)), ' '), end=' ' if j < n - 1 else '\n')
print('=' * 35)
```
T. Математическая выгода
```python
def convert_from_base_to_base(num, from_base=10, to_base=10):
    n = int(num, from_base) if isinstance(num, str) else num
    alphabet = "0123456789ABCDEFGHIJKLMNOPQRSTUVWXYZ"
    result = ""
    while n > 0:
        n, m = divmod(n, to_base)
        result += alphabet[m]
    return result[::-1]


number = input()
max_benefit, best_base = 0, 0
for base in range(2, 11):
    if (digits_sum := sum(map(int, convert_from_base_to_base(number, 10, base)))) > max_benefit:
        best_base = base
        max_benefit = digits_sum
print(best_base)
```
