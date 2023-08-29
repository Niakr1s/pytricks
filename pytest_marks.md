# Pytext marks

## Как добавить свою маркировку к тестам

Допустим, мы хотим получить возможность маркировать медленные тесты маркировкой `@pytest.mark.slow`. Для этого добавляем в `pyproject.toml` следующее:
```toml
[tool.pytest.ini_options]
markers = [
    "slow: marks tests as slow (deselect with '-m \"not slow\"')",
    "serial",
]
```

После этого мы можем маркировать наши медленные тесты:
```python
@pytest.mark.slow
    def test_download(self, tmp_path):
        ...
```

Чтобы иэ пропускать, выполняем из командной строки: `pytest -m "not slow"`.

В __vscode__ можно добавить этот флаг, чтобы в тест эксплорере всегда фильтровались тесты. Для этого добавляем в файл `.vscode/settings.json`:
```json
{
    "python.testing.pytestArgs": [
        "tests", "-m not slow"
    ],
    "python.testing.unittestEnabled": false,
    "python.testing.pytestEnabled": true
}
```
Следует обратить внимание, что кавычки вокруг `not slow` не ставятся (с кавычками не работает почему-то), а также первый аргумент - путь к папке с тестами. Обычно этот файл заполняет сам __vscode__, так что нам надо добавить лишь `"-m not slow"` аргумент.