# Cirular dependency problem

Представим, что у нас есть в модуле `container` класс `Container`, который содержит в себе класс `Item` из модуля `item`.

## item.py:
```python
# from container import Container
# предыдущая строчка вызовет ошибку: ImportError: cannot import name 'Item' from partially initialized module 'item'
# чтобы пофиксить это, делаем следующее:

from __future__ import annotations # это надо для того, чтобы использовать Container без кавычек

from typing import TYPE_CHECKING
if TYPE_CHECKING: # подключаем модуль container только на стадии проверки типов
    from container import Container

class Item:
    def __init__(self, container: Container) -> None:
        self.container = container

```

## container.py:
```python
from item import Item

class Container:
    def __init__(self) -> None:
        self.items: list[Item] = []

```