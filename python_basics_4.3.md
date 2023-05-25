# Yandex handbook "Python Basics" answers

4.3. Рекурсия. Декораторы. Генераторы

A. Рекурсивный сумматор
```python
def recursive_sum(*args):
    if not args:
        return 0
    return args[0] + recursive_sum(*args[1:])   
```
B. Рекурсивный сумматор цифр
```python
def recursive_digit_sum(n):
    return n % 10 + recursive_digit_sum(n // 10) if n else 0
```
C. Многочлен N-ой степени
```python
def make_equation(*args):
    if len(args) == 1:
        return str(args[0])
    line = ') * x ' + ('- ' if args[-1] < 0 else '+ ') + str(args[-1])
    return '(' + make_equation(*args[:-1]) + line
```
D. Декор результата
```python
def answer(func):
    def wrap(*args, **kwargs):
        return f'Результат функции: {func(*args, **kwargs)}'
    return wrap
```
E. Накопление результата
```python
def result_accumulator(func):
    result = []

    def wrap(*args, method="accumulate"):
        result.append(func(*args))
        if method == "drop":
            temp = result.copy()
            result.clear()
            return temp
    return wrap
```
F. Сортировка слиянием
```python
def merge_sort(arr):
    n = len(arr)
    if n <= 1:
        return arr
    else:
        middle = int(len(arr) / 2)
        left = merge_sort(arr[:middle])
        right = merge_sort(arr[middle:])
        return merge(left, right)
        

def merge(left, right):
    result = []
    while len(left) > 0 and len(right) > 0:
        if left[0] <= right[0]:
            result.append(left[0])
            left = left[1:]
        else:
            result.append(right[0])
            right = right[1:]
    if len(left) > 0:
        result += left
    if len(right) > 0:
        result += right
    return result
```
G. Однотипность не порок
```python
def same_type(func):
    def wrapper(*args):
        if len({type(i) for i in args}) != 1:
            print("Обнаружены различные типы данных")
            return False
        return func(*args)
    return wrapper
```
H. Генератор Фибоначчи
```python
def fibonacci(n):
    n1, n2 = 0, 1
    for i in range(n):
        yield n1
        n1, n2 = n2, n1 + n2
```
I. Циклический генератор
```python
def cycle(line):
    while line:
        for i in line:
            yield i
```
J. "Выпрямление" списка
```python
def make_linear(arr):
    new_arr = []
    for i in arr:
        if isinstance(i, list):
            new_arr.extend(make_linear(i))
        else:
            new_arr.append(i)
    return new_arr
```
