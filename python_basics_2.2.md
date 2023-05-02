# Yandex handbook "Python Basics" answers

2.2. Условный оператор

A. Просто здравствуй, просто как дела
```python
name, status = input(), input()
print('Как Вас зовут?', f'Здравствуйте, {name}!', 'Как дела?', sep='\n')
if status == 'хорошо':
    print('Я за вас рада!')
else:
    print('Всё наладится!')    
```
B. Кто быстрее?
```python
petya_speed, vasya_speed = int(input()), int(input())
if petya_speed > vasya_speed:
    print('Петя')
else:
    print('Вася')
```
C. Кто быстрее на этот раз?
```python
petya_speed, vasya_speed, tolya_speed = int(input()), int(input()), int(input())
winner_speed = max(petya_speed, vasya_speed, tolya_speed)
if winner_speed == petya_speed:
    print('Петя')
elif winner_speed == tolya_speed:
    print('Толя')
else:
    print('Вася')
```
D. Список победителей
```python
petya_speed, vasya_speed, tolya_speed = int(input()), int(input()), int(input())
winner_speed = max(petya_speed, vasya_speed, tolya_speed)
loser_speed = min(petya_speed, vasya_speed, tolya_speed)
if winner_speed == petya_speed:
    winner = 'Петя'
    if loser_speed == tolya_speed:
        loser, second = 'Толя', 'Вася'
    else:
        loser, second = 'Вася', 'Толя'       
elif winner_speed == tolya_speed:
    winner = 'Толя'
    if loser_speed == petya_speed:
        loser, second = 'Петя', 'Вася'
    else:
        loser, second = 'Вася', 'Петя'
else:
    winner = 'Вася'
    if loser_speed == tolya_speed:
        loser, second = 'Толя', 'Петя'
    else:
        loser, second = 'Петя', 'Толя'
for place in range(1, 4):
    print(f'{place}. {(winner, second, loser)[place-1]}')
```
E. Яблоки
```python
petya_apples, vasya_apples = int(input()), int(input())
if vasya_apples + 3 > petya_apples:
    print('Вася')
else:
    print('Петя')
```
F. Сила прокрастинации
```python
year = int(input())
if year % 4 or not year % 100 and year % 400:
    print('NO')
else:
    print('YES')
```
G. А роза упала на лапу Азора
```python
number = input()
print('YES') if number == number[::-1] else print('NO')
```
H. Зайка — 1
```python
forest = input()
print('YES') if 'зайка' in forest else print('NO')
```
I. Первому игроку приготовиться
```python
names = input(), input(), input()
print(min(names))
```
J. Лучшая защита — шифрование
```python
number = input()
first = int(number[0]) + int(number[1])
second = int(number[1]) + int(number[2])
print(str(first) + str(second)) if first > second else print(str(second) + str(first))
```
K. Красота спасёт мир
```python
number = list(map(int, input()))
first = max(number) + min(number)
print('YES') if first == 2 * (sum(number) - first) else print('NO')
```
L. Музыкальный инструмент
```python
sides = int(input()), int(input()), int(input())
print('YES') if 2 * max(sides) < sum(sides) else print('NO')
```
M. Властелин Чисел: Братство общей цифры
```python
elf, dwarf, human = input(), input(), input()
if elf[0] == dwarf[0] == human[0]:
    print(elf[0])
elif elf[1] == dwarf[1] == human[1]:
    print(elf[1])
```
N. Властелин Чисел: Две Башни
```python
number = list(map(int, input()))
second = str(max(number)) + str(max(sorted(number)[:-1]))
if number.count(0) == 1:
    first = str(min(sorted(number)[1:])) + str(min(number))
elif number.count(0) == 2:
    first = second
else:
    first = str(min(number)) + str(min(sorted(number)[1:]))
second = str(max(number)) + str(max(sorted(number)[:-1]))
print(first, second)
```
O. Властелин Чисел: Возвращение Цезаря
```python
number = list(map(int, (input() + input())))
print(str(max(number)) + str((sum(number) - max(number) - min(number)) % 10) + str(min(number)))
```
P. Легенды велогонок возвращаются: кто быстрее?
```python
petya_speed, vasya_speed, tolya_speed = int(input()), int(input()), int(input())
winner_speed = max(petya_speed, vasya_speed, tolya_speed)
loser_speed = min(petya_speed, vasya_speed, tolya_speed)
if winner_speed == petya_speed:
    winner = 'Петя'
    if loser_speed == tolya_speed:
        loser, second = 'Толя', 'Вася'
    else:
        loser, second = 'Вася', 'Толя'
elif winner_speed == tolya_speed:
    winner = 'Толя'
    if loser_speed == petya_speed:
        loser, second = 'Петя', 'Вася'
    else:
        loser, second = 'Вася', 'Петя'
else:
    winner = 'Вася'
    if loser_speed == tolya_speed:
        loser, second = 'Толя', 'Петя'
    else:
        loser, second = 'Петя', 'Толя'
print(f'{"": ^8}{winner: ^8}{"": ^8}')
print(f'{second: ^8}{"": ^8}{"": ^8}')
print(f'{"": ^8}{"": ^8}{loser: ^8}')
print(f'{"II": ^8}{"I": ^8}{"III": ^8}')
```
Q. Корень зла
```python
a, b, c = float(input()), float(input()), float(input())
if not a and not b and not c:
    print('Infinite solutions')
elif not a and not b and c or b ** 2 < 4 * a * c:
    print('No solution')
elif b ** 2 == 4 * a * c:
    print(f'{-b / (2 * a):.2f}')
elif not a:
    print(f'{-c / b:.2f}')
else:
    roots = [(-b - (b ** 2 - 4 * a * c) ** 0.5) / (2 * a), (-b + (b ** 2 - 4 * a * c) ** 0.5) / (2 * a)]
    roots.sort()
    print(f'{roots[0]:.2f} {roots[1]:.2f}')
```
R. Территория зла
```python
sides = [int(input()), int(input()), int(input())]
sides.sort()
if sides[2] ** 2 == sides[0] ** 2 + sides[1] ** 2:
    print('100%')
elif sides[2] ** 2 > sides[0] ** 2 + sides[1] ** 2:
    print('велика')
else:
    print('крайне мала')
```
S. Автоматизация безопасности
```python
x, y = float(input()), float(input()) 
if (x ** 2 + y ** 2) ** 0.5 > 10:
    print('Вы вышли в море и рискуете быть съеденным акулой!')
elif x >= 0 and y >= 0 and (x ** 2 + y ** 2) ** 0.5 <= 5:
    print('Опасность! Покиньте зону как можно скорее!')
elif -4 <= x < 0 and 5 >= y >= 0:
    print('Опасность! Покиньте зону как можно скорее!')
elif -7 <= x < -4 and 5 >= y >= 0 and 5 * x - 3 * y > -35:
    print('Опасность! Покиньте зону как можно скорее!')
elif 0.25 * x ** 2 + 0.5 * x - 8.75 <= y <= 0:
    print('Опасность! Покиньте зону как можно скорее!')
else:
    print('Зона безопасна. Продолжайте работу.')
```
T. Зайка — 2
```python
places = [input(), input(), input()]
places.sort()
for place in places:
    if 'зайка' in place:
        print(place, len(place))
        break
```
