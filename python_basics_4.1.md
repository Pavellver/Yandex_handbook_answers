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
D. Имя of the month
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
E. Числовая строка
```python
def split_numbers(line):
    return tuple(map(int, line.split()))
```
F. Модернизация системы вывода
```python
lst = []


def modern_print(string):
    print(string) if string not in lst else None
    lst.append(string)
```
G. Шахматный «обед»
```python
def can_eat(horse, shape):
    return abs(horse[0] - shape[0]) + abs(horse[1] - shape[1]) == 3
```
H. А роза упала на лапу Азора 7.0
```python
def is_palindrome(n):
	return str(n) == str(n)[::-1] if type(n) == int else n == n[::-1]
```
I. Простая задача 5.0
```python
def is_prime(n):
    for i in range(2, int(n**0.5) + 1):
        if not n % i:
            return False
    return n != 1
```
J. Слияние
```python
def merge(a, b):
    c = list(a) + list(b)
    c.sort()
    return tuple(c)
```
