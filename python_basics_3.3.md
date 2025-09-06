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
L. Максимальное произведение
```python
max(x * y for x in numbers for y in numbers if x != y)
```
M. Словарный минимум
```python
min(data, key=lambda k: (sum(data[k]), k))
```
N. Поиск ошибок
```python
{key for key, values in data.items() if len(values) != len(set(values))}
```
O. Буквенная статистика
```python
{ch.lower(): text.lower().count(ch.lower()) for ch in set(text) if ch.isalpha()}
```
P. RLE наоборот
```python
''.join([ch * count for ch, count in rle])
```
Q. Таблица умножения 2.0
```python
[[i * j for j in range(1, n + 1)] for i in range(1, n + 1)]
```
R. Делители
```python
{num: [d for d in range(1, num + 1) if num % d == 0] for num in numbers}
```
S. Простое множество
```python
{num for num in numbers if num > 1 and all(num % div != 0 for div in range(2, int(num**0.5) + 1))}
```
T. Обобщение
```python
{
    tuple(sorted((w1, w2)))
    for i, w1 in enumerate(text.split())
    for w2 in text.split()[i + 1:]
    if len(set(w1) & set(w2)) >= 3
}
```