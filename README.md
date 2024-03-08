<h1>TreeStore</h1>

<h2>Задание</h2>

Дан массив объектов, имеющих поля id и parent, которые позволяют связать объекты массива в древовидную структуру данных.

Необходимо написать класс, принимающий в конструктор массив данных объектов и включающий 4 метода:
<ol>
    <li><b>getAll()</b> - возвращает изначальный массив элементов;</li>
    <li><b>getItem(id)</b> - принимает id элемента и возвращает сам объект элемента;</li>
    <li><b>getChildren(id)</b> - принимает id элемента и возвращает массив элементов, являющихся дочерними для заданного элемента;</li>
    <li><b>getAllParents(id)</b> - принимает id элемента и возвращает массив из цепочки родительских элементов, начиная с заданного элемента, заканчивая корневым элементом дерева.</li>
</ol>

<h2>Требования</h2>
Максимальное быстродействие, минимальное количество обходов массива при операциях. В идеале прямой доступ к элементам без поиска их в массиве.

<h2>Реализация</h2>


```python
class TreeStore():
    def __init__(self, items):
        self.items = items

    def getAll(self):
        return items

    def getItem(self, id):
        #for i in items:
        #    if i['id'] == id:
        #        return i  
        return list(filter(lambda items: items['id'] == id, items))[0]

    def getChildren(self, id):
        #children = list()
        #
        #    if i['parent'] == id:
        #        children.append(i)
        #        
        #return children
        return list(filter(lambda items: items['parent'] == id, items))

    def getAllParents(self, id):
        parents = list()
        item = self.getItem(id)
        
        while item['parent'] != 'root':
            item = self.getItem(item['parent'])
            parents.append(item)
            
        return parents
        
```

<h2>Примеры использования</h2>

<h3>Исходные данные</h3>


```python
items = [
    {'id': 1, 'parent': 'root'},
    {'id': 2, 'parent': 1, 'type': 'test'},
    {'id': 3, 'parent': 1, 'type': 'test'},
    {'id': 4, 'parent': 2, 'type': 'test'},
    {'id': 5, 'parent': 2, 'type': 'test'},
    {'id': 6, 'parent': 2, 'type': 'test'},
    {'id': 7, 'parent': 4, 'type': 'None'},
    {'id': 8, 'parent': 4, 'type': 'None'}
]
```


```python
ts = TreeStore(items)
```

<h3>1. Вывод всех элементов массива</h3>


```python
ts.getAll()
```




    [{'id': 1, 'parent': 'root'},
     {'id': 2, 'parent': 1, 'type': 'test'},
     {'id': 3, 'parent': 1, 'type': 'test'},
     {'id': 4, 'parent': 2, 'type': 'test'},
     {'id': 5, 'parent': 2, 'type': 'test'},
     {'id': 6, 'parent': 2, 'type': 'test'},
     {'id': 7, 'parent': 4, 'type': 'None'},
     {'id': 8, 'parent': 4, 'type': 'None'}]



<h3>2. Вывод элемента массива под номером 7</h3>


```python
ts.getItem(7)
```




    {'id': 7, 'parent': 4, 'type': 'None'}



<h3>3. Вывод дочерних элементов для элемента под номером 4</h3>


```python
ts.getChildren(4)
```




    [{'id': 7, 'parent': 4, 'type': 'None'},
     {'id': 8, 'parent': 4, 'type': 'None'}]



<h3>4. Вывод дочерних элементов для элемента под номером 5</h3>


```python
ts.getChildren(5)
```




    []



<h3>5. Вывод родительских элементов для элемента под номером 7</h3>


```python
ts.getAllParents(7)
```




    [{'id': 4, 'parent': 2, 'type': 'test'},
     {'id': 2, 'parent': 1, 'type': 'test'},
     {'id': 1, 'parent': 'root'}]


