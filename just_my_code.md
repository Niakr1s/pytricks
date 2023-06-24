# Как отключить justMyCode в тестах в VSCode

В VSCode по умолчанию при дебаге тестов через панель Test Explorer, по умолчанию невозможно зайти внутрь функции из библиотеки.

Решить это можно, добавив в *launch.json* следующую конфигурацию:
```json
{
    "name": "Debug Unit Test",
    "type": "python",
    "request": "test",
    "justMyCode": false,
},
```