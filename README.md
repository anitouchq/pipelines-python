# pipelines-python

## 📖 О проекте

Простое Python-приложение (`add`, `main`), для которого настроен CI-пайплайн.
При каждом `push` и `pull request` в ветки `main` / `master` автоматически:

- 🧪 запускается линтинг кода через **flake8**
- ✅ прогоняются тесты через **pytest** на Python **3.9, 3.10, 3.11, 3.12**
- 🐳 собирается **Docker-образ** (без публикации, только на `push` в `main`)

---

## 📂 Структура проекта

```
.
├── .github/
│   └── workflows/
│       └── ci.yml          # GitHub Actions workflow
├── myapp/
│   ├── __init__.py         # пакет
│   └── app.py              # приложение (add, main)
├── tests/
│   └── test_app.py         # тесты (pytest)
├── requirements.txt        # pytest, flake8
├── setup.py                # установка пакета
├── Dockerfile              # образ python:3.11-slim
└── README.md
```

---

## ⚙️ Как работает пайплайн

| Шаг | Что делает |
|-----|-----------|
| **Checkout** | Клонирует репозиторий |
| **Setup Python** | Ставит Python нужной версии (matrix 3.9–3.12) |
| **Install deps** | Устанавливает `pytest`, `flake8` и зависимости из `requirements.txt` |
| **Install package** | `pip install -e .` |
| **Lint** | `flake8 .` |
| **Test** | `pytest tests/` |
| **Docker build** | `docker build -t my-python-app:test .` |

---

## 🐳 Проверка локально

Сборка Docker-образа:
<img width="1809" height="869" alt="photo_5413821073230340027_w" src="https://github.com/user-attachments/assets/f396e26e-1e90-4493-9374-b06826800db1" />


```bash
docker build -t my-python-app:test .
```

Запуск контейнера:

```bash
docker run --rm my-python-app:test
```

Ожидаемый вывод:

```
Hello from my Python app!
```

Зайти внутрь контейнера:

```bash
docker run --rm -it my-python-app:test /bin/bash
```

---

## 🧪 Запуск тестов локально

```bash
pip install -r requirements.txt
pip install -e .
pytest tests/
flake8 .
```

---

## 🏗️ Стек

- **Python 3.9 – 3.12**
- **pytest** — тесты
- **flake8** — линтинг
- **Docker** — контейнеризация


---

## 📄 Лицензия

MIT — свободно для учебных целей.
