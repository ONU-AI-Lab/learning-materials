## Магический Python

![](python-images/magic.gif)

### Что за магические методы?

Магические методы — это специальные методы в python, обрамленные двумя нижними подчеркиваниями. Они также известны как **dunder методы**. Многое из того, что мы делаем в Python, делается с использованием **dunder методов**.

Посмотрите на примеры ниже:

```python
x = 5
x +=  3
print(x) # 8

res = x.__add__(3)
print(res)
``` 

```python
animals = ['cat', 'dog', 'cow', 'horse']
print(animals[2]) # cow

animals.__getitem__(2) # cow 
```

#### \_\_init__
Первый магический метод — это метод init. Он используется в качестве конструктора для классов в Python.
```python
class Student:
    def __init__(self, name, diploma_id):
        self.name = name
        self.diploma_id = diploma_id

a = Student('Alexey', 1)
print(a) # <__main__.Student object at 0x106238d90> 
```
#### \_\_str__
При создании объектов классов очень хотелось бы видеть, что у них внутри, в легко читаемом для человека представлении. И здесь пригождается str:
```python
class Student:
    def __init__(self, name, diploma_id):
        self.name = name
        self.diploma_id = diploma_id
    
    def __str__(self):
        return f"Student name: {self.name} Diploma_id: {self.diploma_id}"

a = Student('Alexey', 1)
print(a) # "Student name: {self.name} Diploma_id: {self.diploma_id}"
```
#### \_\_len__
Теперь, предположим, у нас есть класс School, который хранит детальную информацию о студентах. И вот простой способ посчитать количество студентов в School.
```python
class University:
    def __init__(self, students, grades):
        self.list_of_students = students
        self.grades = grades 
    
    def __len__(self):
        return len(self.grades)
        
students = [Student('Alexey', 1), Student('Dima', 2)]
grades = ['A+', 'F-']

uni = University(students, grades)
len(uni) # 2
```

#### \_\_getitem__ & \_\_setitem__
Нам также нужен простой способ получить доступ к записям о конкретном студенте:
```python
class University:
    def __init__(self, students, grades):
        self.list_of_students = students
        self.grades = grades 
    
    def __getitem__(self, i):
        return self.list_of_students[i].name, self.grades[i]
        
students = [Student('Alexey', 1), Student('Dima', 2)]
grades = ['A+', 'F-']

uni = University(students, grades)
print(uni[0]) # (Alexey, A+)
```
А также мы имеем возможность редактировать их.
```python
class University:
    def __init__(self, students, grades):
        self.list_of_students = students
        self.grades = grades 
    
    def __getitem__(self, i):
        return self.list_of_students[i].name, self.grades[i]
        
    def __setitem__(self, i, g):
        self.grades[i] = g
        
students = [Student('Alexey', 1), Student('Dima', 2)]
grades = ['A+', 'F-']

uni = University(students, grades)
uni[0] = 'A'
uni[0] # (Alexey, A)
```

#### \_\_getattr__ & \_\_setattr__
Эти методы доступны в Python автоматически при создании класса, чтобы получать и задавать его атрибуты, следовательно нам не нужно их определять. Однако мы можем сделать это, если захотим изменить их поведение.
Например, можно изменить поведение \_\_setattr__() для сохранения атрибута в списке, когда бы он ни был задан, чтобы легко получить доступ ко всем атрибутам.

```python
class University:
    def __init__(self, students, grades):
        self._all_attr = {}
        self.list_of_students = students
        self.grades = grades 
    
    def __setattr__(self, k, v):
        if not k.startswith("_"): 
            self._all_attr[k] = v
        super().__setattr__(k, v)
    
    def print_all(self):
        for atr, val in self._all_attr.items(): 
            print(atr, val)
```

#### \_\_iter__
Мы можем создать итератор, используя метод \_\_iter__(). Затем мы можем использовать его для доступа к данным каждого студента.

```python
class University:
    def __init__(self, students, grades):
        self.list_of_students = students
        self.grades = grades 
    
    def __iter__(self):
        for i in range(0, len(self.grades):
            yield self.list_of_students[i].name, self.grades[i]
```



