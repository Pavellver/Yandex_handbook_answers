# Yandex handbook "Python Basics" answers

5.3. Модель исключений Python. Try, except, else, finally. Модули

A. Обработка ошибок
```python
try:
    func()
except Exception as error:
    print(type(error).__name__)
else:
    print('No Exceptions')   
```
B. Ломать — не строить
```python
try:
    func('2', None)
except ValueError:
    print('Ура! Ошибка!')
```
C. Ломать — не строить 2
```python
class Broken:
    def __repr__(self):
        raise Exception


try:
    a = Broken()
    func(a)
except Exception:
    print('Ура! Ошибка!')
```
D. Контроль параметров
```python
def only_positive_even_sum(a, b):
    if type(a) != int or type(b) != int:
        raise TypeError
    if not (a > 0 and not a % 2) or not (b > 0 and not b % 2):
        raise ValueError
    return a + b
```
E. Слияние с проверкой
```python
def merge(a, b):
    try:
        iterator_1 = iter(a)
        iterator_2 = iter(b)
    except TypeError:
        raise StopIteration
    if not (all(isinstance(i, type(a[0])) for i in a) and all(isinstance(i, type(a[0])) for i in b)):
        raise TypeError
    if list(a) != sorted(a) or list(b) != sorted(b):
        raise ValueError
    c = list(a) + list(b)
    c.sort()
    return tuple(c)
```
F. Корень зла 2
```python
class InfiniteSolutionsError(Exception):
    pass


class NoSolutionsError(Exception):
    pass


def find_roots(a, b, c):
    if sum(1 for i in (a, b, c) if type(i) not in (int, float)):
        raise TypeError
    elif not a and not b and not c:
        raise InfiniteSolutionsError
    elif not a and not b and c or b ** 2 < 4 * a * c:
        raise NoSolutionsError
    elif b ** 2 == 4 * a * c:
        return -b / (2 * a), -b / (2 * a)
    elif not a:
        return -c / b
    else:
        roots = [(-b - (b ** 2 - 4 * a * c) ** 0.5) / (2 * a), (-b + (b ** 2 - 4 * a * c) ** 0.5) / (2 * a)]
        roots.sort()
        return roots[0], roots[1]
```
G. Валидация имени
```python
class CyrillicError(Exception):
    pass


class CapitalError(Exception):
    pass


def name_validation(name):
    if not isinstance(name, str):
        raise TypeError
    if sum(i.lower() not in 'абвгдеёжзийклмнопрстуфхцчшщьыъэюя' for i in name):
        raise CyrillicError
    if name != name.lower().capitalize():
        raise CapitalError
    return name
```
H. Валидация имени пользователя
```python
class BadCharacterError(Exception):
    pass


class StartsWithDigitError(Exception):
    pass


def username_validation(name):
    if not isinstance(name, str):
        raise TypeError
    if sum(not (i.isalnum() or i == '_') for i in name):
        raise BadCharacterError
    if name[0].isdigit():
        raise StartsWithDigitError
    return name
```
I. Валидация пользователя
```python
class BadCharacterError(Exception):
    pass


class StartsWithDigitError(Exception):
    pass


class CyrillicError(Exception):
    pass


class CapitalError(Exception):
    pass


def name_validation(name):
    if not isinstance(name, str):
        raise TypeError
    if sum(i.lower() not in 'абвгдеёжзийклмнопрстуфхцчшщьыъэюя' for i in name):
        raise CyrillicError
    if name != name.lower().capitalize():
        raise CapitalError
    return name


def username_validation(username):
    if not isinstance(username, str):
        raise TypeError
    if sum(not (i.isalnum() or i == '_') for i in username):
        raise BadCharacterError
    if username[0].isdigit():
        raise StartsWithDigitError
    return username


def user_validation(**kwargs):
    if [i for i in kwargs] != ['last_name', 'first_name', 'username'] or len(kwargs) != 3:
        raise KeyError
    if any(not isinstance(k, str) for k in kwargs.values()):
        raise TypeError
    kwargs['last_name'] = name_validation(kwargs['last_name'])
    kwargs['first_name'] = name_validation(kwargs['first_name'])
    kwargs['username'] = username_validation(kwargs['username'])
    return kwargs
```
J. Валидация пароля
```python
import hashlib


class MinLengthError(Exception):
    pass


class PossibleCharError(Exception):
    pass


class NeedCharError(Exception):
    pass


def password_validation(password, min_length=8,
                        possible_chars='ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789',
                        at_least_one=str.isdigit):
    if not isinstance(password, str):
        raise TypeError
    if len(password) < min_length:
        raise MinLengthError
    if any(i not in possible_chars for i in password):
        raise PossibleCharError
    if not any(map(at_least_one, password)):
        raise NeedCharError
    return hashlib.sha256(password.encode()).hexdigest()
```
