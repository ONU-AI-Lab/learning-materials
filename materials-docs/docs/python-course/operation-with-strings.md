---
id: operation-with-strings
title: Операции со строками
sidebar_label: Операции со строками
---

## Методы split и join

Элементы списка могут вводиться по одному в строке, в этом случае строку целиком можно считать функцией `input()`. После этого можно использовать метод строки `split()`, возвращающий список строк, которые получатся, если исходную строку разрезать на части по пробелам. Пример:
```python
s = input()  # s == '1 2 3'
a = s.split()  # a == ['1', '2', '3']
```
Если при запуске этой программы ввести строку `1 2 3`, то список a будет равен `['1', '2', '3']`. Обратите внимание, что список будет состоять из строк, а не из чисел.
У метода `split()` есть необязательный параметр, который определяет, какая строка будет использоваться в качестве разделителя между элементами списка. Например, вызов метода `split('.')` вернет список, полученный разрезанием исходной строки по символам `'.'`:
```python
a = '192.168.0.1'.split('.')
```
В Python можно вывести список строк при помощи однострочной команды. Для этого используется метод строки `join`. У этого метода один параметр: список строк. В результате возвращается строка, полученная соединением элементов переданного списка в одну строку, при этом между элементами списка вставляется разделитель, равный той строке, к которой применяется метод. Мы знаем, что вы не поняли предыдущее предложение с первого раза. Поэтому смотрите примеры:
```python
a = ['red', 'green', 'blue']
print(' '.join(a)) # вернёт red green blue
print(''.join(a)) # вернёт redgreenblue
print('***'.join(a)) # вернёт red***green***blue
```

## len 
Строка состоит из последовательности символов. Узнать количество символов (длину строки) можно при помощи функции `len`.
Любой другой объект в Питоне можно перевести к строке, которая ему соответствует. Для этого нужно вызвать функцию `str()`, передав ей в качестве параметра объект, переводимый в строку.
```python
s = input()
print(len(s))

t = input()
number = int(t)
u = str(number)
print(s * 3)
print(s + ' ' + u)
```

## Срезы (slices)
Срез (slice) — извлечение из данной строки одного символа или некоторого фрагмента подстроки или подпоследовательности.

Есть три формы срезов. Самая простая форма среза: взятие одного символа строки, а именно, `S[i]` — это срез, состоящий из одного символа, который имеет номер `i`. При этом считается, что нумерация начинается с числа `0`. То есть если `S = 'Hello'`, то `S[0] == 'H', S[1] == 'e', S[2] == 'l', S[3] == 'l', S[4] == 'o'`.
Номера символов в строке (а также в других структурах данных: списках, кортежах) называются *индексом*.
Если указать отрицательное значение индекса, то номер будет отсчитываться с конца, начиная с номера `-1`. То есть `S[-1] == 'o', S[-2] == 'l', S[-3] == 'l', S[-4] == 'e',S[-5] == 'H'`.
Срез с двумя параметрами: `S[a:b]` возвращает подстроку из `b - a` символов, начиная с символа c индексом a, то есть до символа с индексом b, не включая его. Например, `S[1:4] == 'ell'`, то же самое получится если написать `S[-4:-1]`. Можно использовать как положительные, так и отрицательные индексы в одном срезе, например, `S[1:-1]` — это строка без первого и последнего символа (срез начинается с символа с индексом 1 и заканчиватеся индексом `-1`, не включая его).
Если опустить второй параметр (но поставить двоеточие), то срез берется до конца строки. Например, чтобы удалить из строки первый символ (его индекс равен 0), можно взять срез `S[1:]`. Аналогично если опустить первый параметр, то можно взять срез от начала строки. То есть удалить из строки последний символ можно при помощи среза `S[:-1]`. `Срез S[:]` совпадает с самой строкой `S`.
Если задать срез с тремя параметрами `S[a:b:d]`, то третий параметр задает шаг, как в случае с функцией range, то есть будут взяты символы с индексами `a`, `a + d`, `a + 2 * d` и т. д. При задании значения третьего параметра, равному `2`, в срез попадет кажый второй символ, а если взять значение среза, равное `-1`, то символы будут идти в обратном порядке. Например, можно перевернуть строку срезом `S[::-1]`.

Проверь этот код:
```python
s = 'abcdefg'
print(s[1])
print(s[-1])
print(s[1:3])
print(s[1:-1])
print(s[:3])
print(s[2:])
print(s[:-1])
print(s[::2])
print(s[1::2])
print(s[::-1])
```

## Методы строки
**Метод** — это функция, применяемая к объекту, в данном случае — к строке. Метод вызывается в виде `Имя_объекта.Имя_метода(параметры)`. Например, `S.find("e")` — это применение к строке `S` метода `find` с одним параметром `"e"`.

### Методы find и rfind
Метод `find` находит в данной строке (к которой применяется метод) данную подстроку (которая передается в качестве параметра). Функция возвращает индекс первого вхождения искомой подстроки. Если же подстрока не найдена, то метод возвращает значение `-1`.
```python
S = 'Hello'
print(S.find('e')) # вернёт 1
print(S.find('ll')) # вернёт 2
print(S.find('L')) # вернёт -1
```
Аналогично, метод `rfind` возвращает индекс последнего вхождения данной строки (“поиск справа”).
Если вызвать метод `find` с тремя параметрами `S.find(T, a, b)`, то поиск будет осуществляться в срезе `S[a:b]`. Если указать только два параметра `S.find(T, a)`, то поиск будет осуществляться в срезе `S[a:]`, то есть начиная с символа с индексом a и до конца строки. Метод `S.find(T, a, b)` возращает индекс в строке `S`, а не индекс относительно среза.

### Метод replace
Метод `replace` заменяет все вхождения одной строки на другую. Формат: `S.replace(old, new)` — заменить в строке `S` все вхождения подстроки `old` на подстроку `new`.
```python
print('Hello'.replace('l', 'L'))
```  
Если методу `replace` задать еще один параметр: `S.replace(old, new, count)`, то заменены будут не все вхождения, а только не больше, чем первые count из них.
```python
print('Abrakadabra'.replace('a', 'A', 2)) # вернёт 'AbrAkAdabra'
```
### Метод count
Подсчитывает количество вхождений одной строки в другую строку. Простейшая форма вызова `S.count(T)`  возвращает число вхождений строки `T` внутри строки `S`. При этом подсчитываются только непересекающиеся вхождения, например:
```python
print('Abracadabra'.count('a')) # вернёт 4
print(('a' * 10).count('aa')) # вернёт 5
```
При указании трех параметров `S.count(T, a, b)`, будет выполнен подсчет числа вхождений строки `T` в срезе `S[a:b]`.