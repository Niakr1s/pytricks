# Логгирование ([документация](https://docs.python.org/3/library/logging.html#logger-objects))

Имя логгера - разделенное через точку (`foo.bar.baz`). Создавать логгер напрямую через объект `logging.Logger` нельзя. Чтобы получить логгер, надо вызывать команду `logging.getLogger(name)`. Чтобы получить базовый логгер, надо вызвать команду без аргументво, т.е `logging.getLogger()`. Таким образом, при вызове функции `logging.getLogger` выстраивается иерархия логгеров с главным родительским логгером, полученным при вызове этой функции без параметров.

Как написано в доках, наилучший способ логирования - в каждом модуле обращаться к `logging.getLogger(__name__)`. Тут есть одна особенность: при вызове питоновского кода, у главного файла скрипта `__name__ == "__main__"`, соответственно родительский логгер не будет являться родительским для всех других модулей. Решение: в главном модуле необходимо вызвать `logging.getLogger()` без аргументов и настроить его.

## Пример настройки логгера:

```python
if __name__ == "__main__":
    logging.basicConfig(
        format="%(asctime)s [%(levelname)s] %(name)s: %(message)s",
        level=logging.WARNING,
    )
```

## Уровни логгирования:

| Level  | Numeric value |
| :---   | :---: |
CRITICAL | 50
ERROR    | 40
WARNING  | 30
INFO     | 20
DEBUG    | 10
NOTSET   | 0
