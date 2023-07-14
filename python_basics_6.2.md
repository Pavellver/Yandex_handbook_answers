# Yandex handbook "Python Basics" answers

6.2. Модуль pandas

A. Длины всех слов - 2
```python
import pandas as pd


def length_stats(text):
    text = ''.join(i for i in text if i.isalpha() or i == ' ')
    arr = sorted(set(text.lower().split()))
    s = pd.Series([len(i) for i in arr], index=arr)
    return s 
```
B. Длины всех слов по чётности
```python
import pandas as pd


def length_stats(text):
    text = ''.join(i for i in text if i.isalpha() or i == ' ')
    arr = sorted(set(text.lower().split()))
    arr_odd = [i for i in arr if len(i) % 2]
    arr_even = [i for i in arr if not len(i) % 2]
    odd = pd.Series([len(i) for i in arr_odd], index=arr_odd, dtype='int64')
    even = pd.Series([len(i) for i in arr_even], index=arr_even, dtype='int64')
    return odd, even
```
C. Чек - 2
```python
import pandas as pd


def cheque(price_list, **kwargs):
    my_products = sorted(kwargs)
    product_dict = {
        'product': my_products,
        'price': [price_list[i] for i in my_products],
        'number': [kwargs[i] for i in my_products]
    }
    product_dict['cost'] = [price_list[i] * product_dict['number'][ind] for ind, i in enumerate(my_products)]
    s = pd.DataFrame(product_dict)
    return s
```
D. Акция
```python
import pandas as pd


def cheque(price_list, **kwargs):
    my_products = sorted(kwargs)
    product_dict = {
        'product': my_products,
        'price': [price_list[i] for i in my_products],
        'number': [kwargs[i] for i in my_products]
    }
    product_dict['cost'] = [price_list[i] * product_dict['number'][ind] for ind, i in enumerate(my_products)]
    s = pd.DataFrame(product_dict)
    return s


def discount(s):
    new_s = s.copy()
    for i in range(len(new_s.loc[:, 'cost'])):
        new_s.loc[i, 'cost'] /= 1 + (s.loc[:, 'number'][i] > 2)
    return new_s
```
E. Длинные слова
```python
def get_long(data, min_length=5):
    return data[data >= min_length]
```
F. Отчёт успеваемости
```python
def best(j):
    new_j = j.copy()
    return new_j[(new_j['maths'] > 3) & (new_j['physics'] > 3) & (new_j['computer science'] > 3)]
```
G. Отчёт неуспеваемости
```python
def need_to_work_better(j):
    new_j = j.copy()
    return new_j[(new_j['maths'] < 3) | (new_j['physics'] < 3) | (new_j['computer science'] < 3)]
```
H. Обновление журнала
```python
def update(journal):
    j = journal.copy()
    for i in range(len(j.loc[:, 'name'])):
        j.loc[:, 'average'] = (j['maths'] + j['physics'] + j['computer science']) / 3
    return j.sort_values(by=['average', 'name'], ascending=(False, True))
```
I. Бесконечный морской бой
```python
import pandas as pd

a, b = map(int, input().split())
c, d = map(int, input().split())
data = pd.read_csv('data.csv')
print(data[(a <= data['x']) & (data['x'] <= c) & (d <= data['y']) & (data['y'] <= b)])
```
J. Экстремум функции
```python
import numpy as np
import pandas as pd


def values(func, start, end, step):
    index = np.arange(start, end + step, step)
    return pd.Series(map(func, index), index=index, dtype='float64')


def min_extremum(data):
    return min(data[data == min(data)].index)


def max_extremum(data):
    return max(data[data == max(data)].index)
```
