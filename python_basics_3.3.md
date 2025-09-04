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
F. Буквенная статистика
```python
{letter: text.lower().count(letter) for letter in text.lower() if letter.isalpha()}
```
G. Делители
```python
{number: [i for i in range(1, number + 1) if not number % i] for number in numbers}
```
H. Аббревиатура
```python
''.join(word[0] for word in string.split()).upper()
```
I. Преобразование в строку
```python
' - '.join(str(i) for i in sorted(set(numbers)))
```
J. RLE наоборот
```python
''.join(i * j for i, j in rle)
```
