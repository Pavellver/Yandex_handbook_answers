# Yandex handbook "Python Basics" answers

6.1. Модули math и numpy

A. Математика — круто, но это не точно
```python
import math as m

x = float(input())
a = m.log(m.pow(x, 3 / 16), 32)
b = m.pow(x, m.cos((m.pi * x) / (2 * m.e)))
c = m.pow(m.sin(x / m.pi), 2)
print(a + b - c)   
```
B. Потоковый НОД
```python
from math import gcd
from sys import stdin

for i in stdin:
    print(gcd(*map(int, i.split())))
```
C. Есть варианты?
```python
from math import comb

n, m = map(int, input().split())
print(comb(n, m) * m // n, comb(n, m))
```
D. Среднее не арифметическое
```python
import math as m

numbers = list(map(float, input().split()))
print(m.pow(m.prod(numbers), 1 / len(numbers)))
```
E. Шаг навстречу
```python
from math import dist, cos, sin

deca_x, deca_y = map(float, input().split())
pola_r, pola_f = map(float, input().split())
pola_x = pola_r * cos(pola_f)
pola_y = pola_r * sin(pola_f)
print(dist((deca_x, deca_y), (pola_x, pola_y)))
```
F. Матрица умножения
```python
import numpy as np


def multiplication_matrix(n):
    matrix = np.arange(1, n + 1)
    return matrix * matrix[:, None]
```
G. Шахматная подготовка
```python
import numpy as np


def make_board(num):
    matrix = np.indices((num, num)).sum(axis=0) % 2
    return np.array(np.rot90(matrix), dtype='int8')
```
H. Числовая змейка 3.0
```python
import numpy as np


def snake(m, n, direction='H'):
    matrix = np.zeros((n, m), dtype=np.int16)
    num = 1
    if direction == 'H':
        for i in range(n):
            if not i % 2:
                matrix[i] = np.arange(num, num + m)
            else:
                matrix[i] = np.arange(num + m - 1, num - 1, -1)
            num += m
    else:
        for j in range(m):
            if not j % 2:
                matrix[:, j] = np.arange(num, num + n)
            else:
                matrix[:, j] = np.arange(num + n - 1, num - 1, -1)
            num += n
    return matrix
```
I. Вращение
```python
import numpy as np


def rotate(matrix, angle):
    return np.rot90(matrix, (360 - angle) // 90)
```
J. Лесенка
```python
import numpy as np


def stairs(vector):
    n = len(vector)
    matrix = np.zeros((n, n), dtype=int)
    for i in range(n):
        matrix[i] = np.roll(vector, i)
    return matrix
```
