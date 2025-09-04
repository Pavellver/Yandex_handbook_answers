# Yandex handbook "Python Basics" answers

3.3. Списочные выражения. Модель памяти для типов языка Python

A. Список квадратов
```python
[number ** 2 for number in range(a, b + 1)]   
```
B. Список квадратов 2
```python
[number**2 for number in range(a, b + (1 if a < b else -1), 1 if a < b else -1)]
```
C. Основы фильтрации
```python
[num for num in range(a, b + 1) if num % d == 0]
```
D. Множество нечетных чисел
```python
{number for number in numbers if number % 2}
```
E. Множество всех полных квадратов
```python
{number for number in numbers if number in [i ** 2 for i in range(1, int(max(numbers) ** 0.5 + 1))]}
```
F. Длины всех слов
```python
[len(word) for word in sentence.split()]
```
G. Цифровая выжимка
```python
''.join([ch for ch in text if ch.isdigit()])
```
H. Аббревиатура
```python
''.join(word[0] for word in string.split()).upper()
```
I. Преобразование в строку
```python
' - '.join(str(i) for i in sorted(set(numbers)))
```
J. Огласите список
```python
[word for word in words.split() if sum(ch.lower() in 'аяуюоёэеиыaeiouy' for ch in word) >= 3]
```
K. Выявление уникальности
```python
{num for num in numbers if numbers.count(num) == 1}
```