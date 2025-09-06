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
    if isinstance(size, int):
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
F. Арифметический помощник
```python
def get_operator(op):
    import operator
    return {
        '+': operator.add,
        '-': operator.sub,
        '*': operator.mul,
        '//': operator.floordiv,
        '**': operator.pow
    }[op]
```
G. Подготовитель данных
```python
def get_formatter(sep=' ', end=''):
    def formatter(*args):
        return sep.join(map(str, args)) + end
    return formatter
```
H. Странный рост 
```python
def grow(*args, **kwargs):
    # Создаём список вкладов для каждого позиционного аргумента
    contributions = [0] * len(args)
    
    # Для каждого именованного параметра
    for key, value in kwargs.items():
        key_len = len(key)
        if key_len == 0:
            continue
        # Проверяем каждый позиционный аргумент
        for i in range(len(args)):
            # Если значение кратно длине имени
            if args[i] % key_len == 0:
                contributions[i] += value
    
    # Применяем все вклады к исходным значениям
    result = []
    for i in range(len(args)):
        result.append(args[i] + contributions[i])
    
    return tuple(result)
```
I. Странное произведение
```python
def product(*args, **kwargs):
    result = []
    for s in args:
        product_value = 1
        found = False
        for key, value in kwargs.items():
            if key in s:
                product_value *= value
                found = True
        if found:
            result.append(product_value)
    return tuple(result)
```
J. Наилучший выбор
```python
def choice(*args, **kwargs):
    if 'min' in kwargs:
        func = kwargs['min']
        return min(func(x) for x in args)
    elif 'max' in kwargs:
        func = kwargs['max']
        return max(func(x) for x in args)
```
K. Кофейня
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
L. В эфире рубрика «Эксперименты»
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
M. Длинная сортировка
```python
lambda x: (len(x), x.lower())
```
N. Чётная фильтрация
```python
lambda x: not sum(map(int, str(x))) % 2
```
O. Повторюшка
```python
def get_repeater(func, count):
    def repeater(x):
        result = x
        for _ in range(count):
            result = func(result)
        return result

    return repeater
```
P. Обратная связь
```python
def login(name, password, success, error):
    total = sum(ord(ch) for ch in name)
    val = total * len(name)
    hex_str = f'{val:x}'
    if hex_str[::-1].lower() == password.lower():
        success(name)
    else:
        error(name)
```
Q. Фильтрация словаря
```python
lambda item: isinstance(item[1], list) and any(isinstance(x, int) and x % 2 == 0 for x in item[1])
```
R. Преобразование словаря
```python
lambda item: (
    "".join(ch for ch in item[0].lower() if ch.isalpha()),
    (
        sum(item[1])
        if hasattr(item[1], "__iter__") and not isinstance(item[1], (str, bytes))
        else item[1]
    ),
)
```
S. Ключевой секрет
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
T. База данных пользователей
```python
import re
from datetime import datetime

# Глобальная база данных
database = []


def insert(*users):
    """Добавляет одного или нескольких пользователей в базу данных"""
    for user in users:
        database.append(user)


def select(*conditions):
    """Выбирает пользователей, соответствующих критериям"""
    # Если нет условий, возвращаем всех пользователей
    if not conditions:
        return sorted(database, key=lambda x: x["id"])

    # Начинаем с всех пользователей
    result = database[:]

    # Применяем каждое условие
    for condition in conditions:
        # Парсим условие с помощью регулярного выражения
        match = re.match(r"(\w+)\s*(>=|<=|==|!=|>|<)\s*(.+)", condition.strip())
        if not match:
            continue

        field, operator, value = match.groups()
        value = value.strip()

        # Фильтруем результат по текущему условию
        filtered_result = []
        for user in result:
            if _check_condition(user, field, operator, value):
                filtered_result.append(user)
        result = filtered_result

    # Сортируем по id
    return sorted(result, key=lambda x: x["id"])


def _check_condition(user, field, operator, value):
    """Проверяет, удовлетворяет ли пользователь условию"""
    if field not in user:
        return False

    user_value = user[field]

    # Для дат преобразуем в datetime для сравнения
    if field == "birth":
        try:
            user_date = datetime.strptime(user_value, "%d.%m.%Y")
            condition_date = datetime.strptime(value, "%d.%m.%Y")
            if operator == "==":
                return user_date == condition_date
            elif operator == "!=":
                return user_date != condition_date
            elif operator == ">":
                return user_date > condition_date
            elif operator == "<":
                return user_date < condition_date
            elif operator == ">=":
                return user_date >= condition_date
            elif operator == "<=":
                return user_date <= condition_date
        except ValueError:
            return False
    else:
        # Для других типов данных
        try:
            # Пытаемся преобразовать в число, если возможно
            if isinstance(user_value, (int, float)) or (
                isinstance(user_value, str) and user_value.isdigit()
            ):
                if isinstance(user_value, str) and "." in user_value:
                    user_val = float(user_value)
                    cond_val = float(value)
                elif isinstance(user_value, str) and user_value.isdigit():
                    user_val = int(user_value)
                    cond_val = int(value)
                else:
                    user_val = user_value
                    if "." in value:
                        cond_val = float(value)
                    else:
                        cond_val = int(value)
            else:
                # Строки
                user_val = str(user_value)
                cond_val = value.strip()

            if operator == "==":
                return user_val == cond_val
            elif operator == "!=":
                return user_val != cond_val
            elif operator == ">":
                return user_val > cond_val
            elif operator == "<":
                return user_val < cond_val
            elif operator == ">=":
                return user_val >= cond_val
            elif operator == "<=":
                return user_val <= cond_val
        except (ValueError, TypeError):
            return False

    return False
```