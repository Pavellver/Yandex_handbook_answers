# Yandex handbook "Python Basics" answers

3.4. Встроенные возможности по работе с коллекциями

A. Автоматизация списка
```python
for index, word in enumerate(input().split(), start=1):
    print(f'{index}. {word}')    
```
B. Сборы на прогулку
```python
for kids in zip(a := input().split(', '), b := input().split(', ')):
    print(f'{kids[0]} - {kids[1]}')
```
C. Рациональная считалочка
```python
from itertools import count

a, b, step = list(map(float, input().split()))
for value in count(a, step):
    if value <= b:
        print(f'{value:.2f}')
    else:
        break
```
D. Словарная ёлка
```python
from itertools import accumulate

for value in accumulate(map(lambda x: ' ' + x, input().split())):
    print(value[1:])
```
E. Список покупок
```python
items = set()
for _ in range(3):
    items = items.union({item for item in input().split(', ')})
for i, item in enumerate(sorted(items), start=1):
    print(f'{i}. {item}')
```
F. Колода карт
```python
from itertools import product

nominal = [2, 3, 4, 5, 6, 7, 8, 9, 10, 'валет', 'дама', 'король', 'туз']
suits = ['пик', 'треф', 'бубен', 'червей']
suits.remove(input())
for card in product(nominal, suits):
    print(card[0], card[1])
```
G. Игровая сетка
```python
from itertools import product

players, games = [], []
for _ in range(int(input())):
    players.append(input())
for i in product(players, players):
    if i[0] != i[1] and [i[1], i[0]] not in games:
        games.append([i[0], i[1]])
        print(f'{i[0]} - {i[1]}')
```
H. Меню питания 2.0
```python
cereals = []
for _ in range(int(input())):
    cereals.append(input())
amount = int(input())
cereals *= amount // len(cereals) + 1
for i in range(amount):
    print(cereals[i])
```
I. Таблица умножения 3.0
```python
from itertools import product

for i in (n := range(1, int(input()) + 1)):
    print(' '.join(map(lambda x: str(x[0] * x[1]), product(n, [i]))))
```
J. Мы делили апельсин 2.0
```python
for i in range(1, (n := int(input())) - 1):
    if i == 1:
        print('А Б В')
    for j in range(1, n - i):
        print(f'{i} {j} {n - i - j}')
```
K. Числовой прямоугольник 3.0
```python
from itertools import product

n, m = int(input()), int(input())
for i in range(n):
    line = product(range(1, m + 1), [i * m])
    print(' '.join(map(lambda x: str(sum(x)).rjust(len(str((n - 1 - i) * m + sum(x))), ' '), line)))
```
L. Список покупок 2.0
```python
items = []
for _ in range(int(input())):
    items.extend([item for item in input().split(', ')])
for i, item in enumerate(sorted(items), start=1):
    print(f'{i}. {item}')
```
M. Расстановка спортсменов
```python
from itertools import permutations

items = []
for _ in range(int(input())):
    items.append(input())
for i in sorted(permutations(items)):
    print(', '.join(i))
```
N. Спортивные гадания
```python
from itertools import permutations

items = []
for _ in range(int(input())):
    items.append(input())
for i in sorted(permutations(items, 3)):
    print(', '.join(i))
```
O. Список покупок 3.0
```python
from itertools import permutations

items = []
for _ in range(int(input())):
    items.extend([item for item in input().split(', ')])
for item in sorted(permutations(items, 3)):
    print(' '.join(item))
```
P. Расклад таков...
```python
from itertools import product, permutations

suits_ro = ["бубен", "пик", "треф", "червей"]
suit, exception = input(), input()
best_suit = [s for s in suits_ro if s.startswith(suit[0:3])][0]
nominal = ["2", "3", "4", "5", "6", "7", "8", "9", "10", "валет", "дама", "король", "туз"]
nominal.remove(exception)
comb = permutations(product(sorted(nominal), sorted(suits_ro)), 3)
y = [', '.join(' '.join(j) for j in sorted(i)) for i in comb]
triads = [i for i in y if best_suit in i][:10]
for triad in triads:
    print(triad)
```
Q. А есть ещё варианты?
```python
from itertools import product, permutations

suits_ro = sorted(["бубен", "пик", "треф", "червей"])
suit, exception, situation = input(), input(), input()
best_suit = [s for s in suits_ro if s.startswith(suit[0:3])][0]
nominal = sorted(["2", "3", "4", "5", "6", "7", "8", "9", "10", "валет", "дама", "король", "туз"])
nominal.remove(exception)
comb = permutations(product(nominal, suits_ro), 3)
y = sorted(set([', '.join(' '.join(j) for j in sorted(i)) for i in comb]))
triads = [i for i in y if best_suit in i]
for ind, triad in enumerate(triads):
    if triad == situation:
        print(triads[ind + 1])
        break
```
R. Таблица истинности
```python
x = input()
print('a b c f')
for i in range(8):
    values = list(bin(i)[2:].zfill(3))
    a, b, c = map(int, values)
    print(' '.join(values), int(eval(x)))
```
S. Таблица истинности 2
```python
x = input()
args = sorted({i for i in x if i.isupper()})
print(' '.join(args), 'F')
for i in range(2 ** len(args)):
    values = list(bin(i)[2:].zfill(len(args)))
    exec(', '.join(args) + " = map(int, values)")
    print(' '.join(values), int(eval(x)))
```
T. Таблицы истинности 3
```python
from itertools import product

OPERATORS = {
    'not': 'not',
    'and': 'and',
    'or': 'or',
    '^': '!=',
    '->': '<=',
    '~': '==',
}

PRIORITY = {
    'not': 0,
    'and': 1,
    'or': 2,
    '^': 3,
    '->': 4,
    '~': 5,
    '(': 6,
}


def postfix_expression(expression, variables):
    stack, result, lst = [], [], expression.split()
    for i in lst:
        if i in variables:
            result.append(i)
        elif i == '(':
            stack.append(i)
        elif i == ')':
            while stack[-1] != '(':
                result.append(OPERATORS[stack.pop()])
            stack.pop()
        elif i in OPERATORS.keys():
            while len(stack) and PRIORITY[i] >= PRIORITY[stack[-1]]:
                result.append(OPERATORS[stack.pop()])
            stack.append(i)
    for _ in range(len(stack)):
        result.append(OPERATORS[stack.pop()])
    return result


def result_of_expression(postfix_exp, variables):
    stack = []
    for i in range(len(postfix_exp)):
        if postfix_exp[i] in variables.keys():
            stack.append(variables[postfix_exp[i]])
        else:
            if postfix_exp[i] == 'not':
                stack.append(not stack.pop())
            else:
                var2, var1 = stack.pop(), stack.pop()
                stack.append(eval(f'{var1} {postfix_exp[i]} {var2}'))
    return int(stack.pop())


statement = input()
var_all = sorted(set([i for i in statement if i.isupper()]))
print(' '.join(var_all), 'F')
table = product([0, 1], repeat=len(var_all))
statement = statement.replace('(', '( ').replace(')', ' )')
exp = postfix_expression(statement, var_all)

for row in table:
    res = {}
    for k, v in zip(var_all, row):
        res[k] = v
    print(' '.join(str(x) for x in row), result_of_expression(exp, res))
```
