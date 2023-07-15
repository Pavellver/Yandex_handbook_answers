# Yandex handbook "Python Basics" answers

6.3. Модуль requests

A. Проверка системы
```python
from requests import get

print(get('http://127.0.0.1:5000').text)
```
B. Суммирование ответов
```python
from requests import get

address = 'http://' + input()
summ = 0
while data := int(get(address).text):
    summ += data
print(summ)
```
C. Суммирование ответов 2
```python
from requests import get

address = 'http://' + input()
data = get(address).json()
print(sum(i for i in data if type(i) == int))
```
D. Конкретное значение
```python
from requests import get

address = 'http://' + input()
key = input()
data = get(address).json()
print(data.get(key, 'No data'))
```
E. Суммирование ответов 3
```python
from requests import get
from sys import stdin

address = 'http://' + input()
ways = [i.strip() for i in stdin]
summ = 0
for way in ways:
    summ += sum(get(address + way).json())
print(summ)
```
F. Список пользователей
```python
from requests import get

address = 'http://' + input() + '/users'
data = get(address).json()
names = []
for i in data:
    names.append(f"{i['last_name']} {i['first_name']}")
for name in sorted(names):
    print(name)
```
G. Рассылка сообщений
```python
from requests import get
from sys import stdin

address = 'http://' + input() + '/users/' + input()
d = ''.join(i for i in stdin)
data = {}
try:
    data = get(address).json()
except ValueError:
    print('Пользователь не найден')
if data:
    for key in data:
        d = d.replace('{' + key + '}', str(data[key]))
    print(d)  
```
H. Регистрация нового пользователя
```python
from requests import post
from json import dumps

address = 'http://' + input() + '/users'
data = {}
data["username"] = input()
data["last_name"] = input()
data["first_name"] = input()
data["email"] = input()
post(address, data=dumps(data))
```
I. Изменение данных
```python
from requests import put
from json import dumps
from sys import stdin

address = 'http://' + input() + '/users/' + input()
line = [i.strip().split('=') for i in stdin]
data = {}
for j in line:
    data[j[0]] = j[1]
put(address, data=dumps(data))
```
J. Удаление данных
```python
from requests import delete

address = 'http://' + input() + '/users/' + input()
delete(address)
```
