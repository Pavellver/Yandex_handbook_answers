# Yandex handbook "Python Basics" answers

5.1. Объектная модель Python. Классы, поля и методы

A. Классная точка
```python
class Point:
    def __init__(self, x, y):
        self.x = x
        self.y = y   
```
B. Классная точка 2.0
```python
class Point:
    def __init__(self, x, y):
        self.x = x
        self.y = y

    def move(self, shift_x, shift_y):
        self.x += shift_x
        self.y += shift_y

    def length(self, p):
        return round(((self.x - p.x)**2 + (self.y - p.y)**2)**0.5, 2)
```
C. Не нажимай красную кнопку!
```python
class RedButton:
    def __init__(self):
        self.counter = 0

    def click(self):
        print('Тревога!')
        self.counter += 1

    def count(self):
        return self.counter
```
D. Работа не волк
```python
class Programmer:

    def __init__(self, name, position="Junior"):
        self.name = name
        self.position = position
        self.worked = 0
        self.money = 0
        self.overrises = 0

    def work(self, time):
        P = {
            "Junior": 10,
            "Middle": 15,
            "Senior": 20,
        }
        self.worked += time
        self.money += time * (P[self.position] + self.overrises)

    def rise(self):
        if self.position == "Junior":
            self.position = "Middle"
        elif self.position == "Middle":
            self.position = "Senior"
        elif self.position == "Senior":
            self.overrises += 1

    def info(self):
        return f'{self.name} {self.worked}ч. {self.money}тгр.'
```
E. Классный прямоугольник
```python
class Rectangle:
    def __init__(self, *coords):
        self.coords = coords
        self.first_line = abs(self.coords[0][0] - self.coords[1][0])
        self.second_line = abs(self.coords[0][1] - self.coords[1][1])

    def perimeter(self):
        return round(2 * (self.first_line + self.second_line), 2)

    def area(self):
        return round(self.first_line * self.second_line, 2)
```
F. Классный прямоугольник 2.0
```python
class Rectangle:
    def __init__(self, *coords):
        self.coords = coords
        self.upper_left_x = round(min(self.coords[0][0], self.coords[1][0]), 2)
        self.upper_left_y = round(max(self.coords[0][1], self.coords[1][1]), 2)
        self.lower_right_x = round(max(self.coords[0][0], self.coords[1][0]), 2)
        self.lower_right_y = round(min(self.coords[0][1], self.coords[1][1]), 2)
        self.width = abs(self.coords[0][0] - self.coords[1][0])
        self.height = abs(self.coords[0][1] - self.coords[1][1])

    def perimeter(self):
        return round(2 * (self.width + self.height), 2)

    def area(self):
        return round(self.width * self.height, 2)

    def get_pos(self):
        return self.upper_left_x, self.upper_left_y

    def get_size(self):
        return round(self.width, 2), round(self.height, 2)

    def move(self, dx, dy):
        self.coords = (self.coords[0][0] + dx, self.coords[0][1] + dy), (self.coords[1][0] + dx, self.coords[1][1] + dy)
        self.__init__(*self.coords)

    def resize(self, width, height):
        self.coords = self.get_pos(), (self.upper_left_x + width, self.upper_left_y - height)
        self.__init__(*self.coords)
```
G. Классный прямоугольник 3.0
```python
class Rectangle:
    def __init__(self, coord1, coord2):
        self.left = min(coord1[0], coord2[0])
        self.top = max(coord1[1], coord2[1])
        self.right = max(coord1[0], coord2[0])
        self.bottom = min(coord1[1], coord2[1])
        self.w = round(abs(coord1[0] - coord2[0]), 2)
        self.h = round(abs(coord1[1] - coord2[1]), 2)
        self.x = min(coord1[0], coord2[0])
        self.y = max(coord1[1], coord2[1])
        self.flag = False

    def perimeter(self):
        return round(abs(self.left - self.right) * 2 + abs(self.top - self.bottom) * 2, 2)

    def area(self):
        return round(abs(self.left - self.right) * abs(self.top - self.bottom), 2)

    def get_pos(self):
        return self.left, self.top

    def get_size(self):
        if self.flag:
            return self.w, self.h
        return ((round(abs(self.left - self.right), 2), round(abs(self.top - self.bottom), 2)))

    def resize(self, width, height):
        self.flag = False
        self.right = round(self.left + width, 2)
        self.bottom = round(self.top + height, 2)
        self.w, self.h = width, height

    def turn(self):
        self.flag = False
        width, height = self.get_size()
        d = (width - height) / 2
        self.left = round(self.left + d, 2)
        self.right = round(self.right - d, 2)
        self.top = round(self.top + d, 2)
        self.bottom = round(self.bottom - d, 2)
        d = (self.w - self.h) / 2
        self.x = round(self.x + d, 2)
        self.y = round(self.y + d, 2)
        self.w, self.h = self.h, self.w

    def scale(self, factor):
        self.flag = False
        width, height = self.get_size()
        self.flag = False
        if abs(width - self.w) <= 0.01:
            width = self.w
        if abs(height - self.h) <= 0.02:
            height = self.h
        self.left = round(self.left - (factor * width - width) / 2, 2)
        self.top = round(self.top + (factor * height - height) / 2, 2)
        width = round(width * factor, 2)
        height = round(height * factor, 2)
        self.right = round(self.left + width, 2)
        self.bottom = round(self.top - height, 2)
        self.x = round(self.x - (factor * self.w - self.w) / 2, 2)
        self.y = round(self.y + (factor * self.h - self.h) / 2, 2)
        self.w = round(self.w * factor, 2)
        self.h = round(self.h * factor, 2)
```
H. Шашки
```python
class Checkers:

    def __init__(self):
        self.desk = {
            'A': {
                '8': 'X',
                '7': 'B',
                '6': 'X',
                '5': 'X',
                '4': 'X',
                '3': 'W',
                '2': 'X',
                '1': 'W',
            },
            'B': {
                '8': 'B',
                '7': 'X',
                '6': 'B',
                '5': 'X',
                '4': 'X',
                '3': 'X',
                '2': 'W',
                '1': 'X',
            },
            'C': {
                '8': 'X',
                '7': 'B',
                '6': 'X',
                '5': 'X',
                '4': 'X',
                '3': 'W',
                '2': 'X',
                '1': 'W',
            },
            'D': {
                '8': 'B',
                '7': 'X',
                '6': 'B',
                '5': 'X',
                '4': 'X',
                '3': 'X',
                '2': 'W',
                '1': 'X',
            },
            'E': {
                '8': 'X',
                '7': 'B',
                '6': 'X',
                '5': 'X',
                '4': 'X',
                '3': 'W',
                '2': 'X',
                '1': 'W',
            },
            'F': {
                '8': 'B',
                '7': 'X',
                '6': 'B',
                '5': 'X',
                '4': 'X',
                '3': 'X',
                '2': 'W',
                '1': 'X',
            },
            'G': {
                '8': 'X',
                '7': 'B',
                '6': 'X',
                '5': 'X',
                '4': 'X',
                '3': 'W',
                '2': 'X',
                '1': 'W',
            },
            'H': {
                '8': 'B',
                '7': 'X',
                '6': 'B',
                '5': 'X',
                '4': 'X',
                '3': 'X',
                '2': 'W',
                '1': 'X',
            },
        }

    def move(self, f, t):
        self.desk[f[0]][f[1]], self.desk[t[0]][t[1]] = self.desk[t[0]][t[1]], self.desk[f[0]][f[1]]

    def get_cell(self, p):
        return Cell(self.desk[p[0]][p[1]])


class Cell:

    def __init__(self, coords):
        self.coords = coords

    def status(self):
        return self.coords
```
I. Очередь
```python
class Queue(list):
    def __init__(self):
        a = []

    def push(self, item):
        self.a.append(item)

    def pop(self):
        return self.a.pop(0)

    def is_empty(self):
        return self.a == []
```
J. Стек
```python
class Stack(list):
    def __init__(self):
        a = []

    def push(self, item):
        self.a.append(item)

    def pop(self):
        return self.a.pop()

    def is_empty(self):
        return self.a == []
```
