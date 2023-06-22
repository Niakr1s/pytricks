# Monkeypatching в тестах

## Патчим функцию или класс в модуле



Предположим, у нас есть функция или класс в модуле a, которую мы хотим запатчить, и она используется в модуле b. В pytest'е это можно сделать так:
```python
pytest.monkeypatch.setattr("b.someClass", NewClass)
pytest.monkeypatch.setattr("b.someFunction", NewFunction)
```
Обрати внимание: патчим функцию именно в модуле b!

Это все из-за следующей особенности, описанной [тут](https://docs.python.org/dev/library/unittest.mock.html#where-to-patch). Предположим, у нас есть класс в модуле a, который мы хотим запатчить. Он инициализируется в модуле b в методе some_function:
```
a.py
    -> Defines SomeClass

b.py
    -> from a import SomeClass
    -> some_function instantiates SomeClass
```
В этом случае корректным будет вызов `@patch('b.SomeClass')`. Если мы тут напишем a вместо b, то не будет никакого эффекта, так как этот класс УЖЕ импортировался из модуля a в модуль b. Корректным вызовом мы патчим эту функцию уже в модуле b.