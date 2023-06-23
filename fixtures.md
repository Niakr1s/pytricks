# Pytext fixtures

## Как вынести fixture в отдельный файл

Все очень просто: оспределяем функцию в новом файле, затем в папке tests создаем файл по адресу `{PROJECT_DIR}/tests/conftest.py`, в который просто импортируем нашу fixture.

### Пример файла `conftest.py`:
```python
from tests.project.fixtures import custom_fixture  # noqa: F401
```