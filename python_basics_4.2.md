# Yandex handbook "Python Basics" answers

4.2. Позиционные и именованные аргументы. Функции высших порядков. Лямбда-функции

A. Генератор списков
```python
def make_list(length, value=0):
    return [value] * length   
```
B. Генератор матриц
```python
def make_matrix(size, value=0):
    if type(size) == int:
        return [[value for i in range(size)] for j in range(size)]
    else:
        return [[value for i in range(size[0])] for j in range(size[1])]
```
C. Функциональный нод 2.0
```python
def gcd(*args):
    a = list(args)
    while len(a) > 1:
        while a[1]:
            a[0], a[1] = a[1], a[0] % a[1]
        a.pop(1)
    return a[0]
```
D. Имя of the month 2.0
```python
def month(number, language='ru'):
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
E. Подготовка данных
```python
def to_string(*args, **kwargs):
    return kwargs.get("sep", " ").join([str(i) for i in args]) + kwargs.get("end", "\n")
```
F. Кофейня
```python
def order(*args):
    temp = in_stock
    GRADES = {
        "Эспрессо": {"coffee": 1},
        "Капучино": {"coffee": 1,
                     "milk": 3},
        "Макиато": {"coffee": 2,
                    "milk": 1},
        "Кофе по-венски": {"coffee": 1,
                           "cream": 2},
        "Латте Макиато": {"coffee": 1,
                          "milk": 2,
                          "cream": 1},
        "Кон Панна": {"coffee": 1,
                      "cream": 1},
    }
    for grade in args:
        for ingr in GRADES[grade]:
            if GRADES[grade].get(ingr, 0) > in_stock[ingr]:
                break
        else:
            for ingr in GRADES[grade]:
                in_stock[ingr] -= GRADES[grade][ingr]
            return grade
    if in_stock == temp:
        return "К сожалению, не можем предложить Вам напиток"
```
G. В эфире рубрика «Эксперименты»
```python
numbers = tuple()


def enter_results(*args):
    global numbers
    numbers += args


def get_sum():
    return round(sum(numbers[::2]), 2), round(sum(numbers[1::2]), 2)


def get_average():
    return round(2 * get_sum()[0] / len(numbers), 2), round(2 * get_sum()[1] / len(numbers), 2)
```
H. Длинная сортировка
```python
lambda x: (len(x), x.lower())
```
I. Чётная фильтрация
```python
lambda x: not sum(map(int, str(x))) % 2
```
J. Ключевой секрет
```python
def secret_replace(text, **kwargs):
    result = ''
    kwargs = {d: (v, 0) for d, v in kwargs.items()}
    for i in text:
        if i in kwargs:
            result += kwargs[i][0][kwargs[i][1] % len(kwargs[i][0])]
            kwargs[i] = kwargs[i][0], kwargs[i][1] + 1
        else:
            result += i
    return result
```
