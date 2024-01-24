
```python
from collections import deque

dq = deque() # обьявление без ограничения
dq = deque(['1', 'test', 'hello'])
dq = deque([], maxlen=10) # обьявление с максмальным количеством элементов 10
```
***

#### Методы

Метод `Deque.append()` добавляет `x` к правой стороне (в конец) контейнера `deque()`.

```python
dq.append('new')
>>> ['1', 'test', 'hello', 'new']
```
***

Метод `Deque.appendleft()` добавляет `x` к левой стороне (в начало) контейнера `deque()`.

```python
dq.appendleft('new')
>>> ['new' ,'1', 'test', 'hello']
```
***

Метод `Deque.copy()` создает мелкую копию контейнера `deque()`.

```python
new = dq.copy()
>>> ['1', 'test', 'hello']

dq = deque(['1', [1,[1,2]]])  
new = dq.copy()  
>>> deque(['1', [1, [1, 2]]])
```
***

Метод `Deque.clear()` удаляет все элементы из контейнера `deque()`, оставляя его длиной 0.

```python
new = dq.clear()
>>> deque([])
```
***

Метод `Deque.count()` подсчитывает количество элементов контейнера `deque()`, равное значению `x`.

```python
new = dq.count('hello')
>>> 1
```
***

Метод `Deque.extend()` расширяет правую сторону (с конца) контейнера `deque()`, добавляя элементы из итерируемого аргумента `iterable`.

```python
new = dq.extend(['new', '2'])
>>> ['1', 'test', 'hello', 'new', '2']
```
***

Метод `Deque.extendleft()` расширяет левую сторону (с начала) контейнера `deque()`, добавляя элементы из итерируемого"Итератор Iterator, протокол итератора в Python. аргумента `iterable`.

**Обратите внимание**, что ряд последовательных добавлений в начало контейнера приводит к изменению порядка элементов в аргументе `iterable`.

```python
new = dq.extendleft(['new', '2'])
>>> ['2','new','1', 'test', 'hello']
```
***

Метод `Deque.index()` вернет позицию ([индекс](https://docs-python.ru/tutorial/obschie-operatsii-posledovatelnostjami-list-tuple-str-python/izvlechenie-elementa-sequence-indeksu/ "Получение значения элемента по индексу sequence[i] в Python.")) первого совпадения значения аргумента `x` в контейнере `deque()`, расположенного после необязательного аргумента `start` и до необязательного аргумента `stop`.

Вызывает [исключение `ValueError`](https://docs-python.ru/tutorial/vstroennye-iskljuchenija-interpretator-python/vstroennye-iskljuchenija/ "Исключения наследуемые от Exception в Python."), если значения аргумента `x` не найдено.

```python
index = dq.index('test')
>>> 1
```
***

Метод `Deque.insert()` вставляет значение аргумента `x` в позицию `i` контейнера `deque()`.

Если вставка значение аргумента `x` приведет к тому, что ограниченный контейнер `deque()` выйдет за пределы `maxlen`, будет вызвано [исключение `IndexError`](https://docs-python.ru/tutorial/vstroennye-iskljuchenija-interpretator-python/vstroennye-iskljuchenija/ "Исключения наследуемые от Exception в Python.").

```python
dq.insert(2, 'new')
>>> ['1', 'test', 'new', 'hello']
```
***

Метод `Deque.pop()` удаляет и возвращает элемент с правой стороны (с конца) контейнера `deque()`. Если элементы отсутствуют, возникает [ошибка `IndexError`](https://docs-python.ru/tutorial/vstroennye-iskljuchenija-interpretator-python/vstroennye-iskljuchenija/ "Исключения наследуемые от Exception в Python.").

```python
deleted = dq.pop()
>>> 'hello' # deleted
>>> ['1', 'test'] # deque
```
***

Метод `Deque.popleft()` удаляет и возвращает элемент с левой стороны (с начала) контейнера `deque()`. Если элементы отсутствуют, возникает [ошибка `IndexError`](https://docs-python.ru/tutorial/vstroennye-iskljuchenija-interpretator-python/vstroennye-iskljuchenija/ "Исключения наследуемые от Exception в Python.").

```python
deleted = dq.popleft()
>>> '1' # deleted
>>> ['1', 'test', 'hello'] # deque
```
***


Метод `Deque.remove()` удаляет первое вхождение значения `value` в контейнер `deque()`. Если значение `value` не найдено, возникает [ошибка `IndexError`](https://docs-python.ru/tutorial/vstroennye-iskljuchenija-interpretator-python/vstroennye-iskljuchenija/ "Исключения наследуемые от Exception в Python.").

```python
dq.remove('hello')
>>> ['1', 'test'] # deque
```
***

Метод `Deque.reverse()` разворачивает элементы контейнера `deque()` на месте и возвращает `None`.

```python
dq.reverse()
>>> ['hello', 'test', '1'] # deque
```
***

Метод `Deque.rotate()` разворачивает контейнер `deque()` на `n` шагов вправо. Если аргумент `n` имеет отрицательное значение, то разворачивает контейнер налево.

Когда контейнер не пуст, вращение на один шаг вправо эквивалентно `dq.appendleft(d.pop())`, а вращение на один шаг влево эквивалентно `dq.append(d.popleft())`.

```python
dq.rotate(2)
>>> ['hello', '1', 'test'] # deque
```
***

Метод `Deque.rotate()` разворачивает контейнер `deque()` на `n` шагов вправо. Если аргумент `n` имеет отрицательное значение, то разворачивает контейнер налево.

Когда контейнер не пуст, вращение на один шаг вправо эквивалентно `dq.appendleft(d.pop())`, а вращение на один шаг влево эквивалентно `dq.append(d.popleft())`.

```python
dq.maxlen()
>>> 10
```
***







