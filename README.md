# pipelines-python

<img width="1553" height="554" alt="image" src="https://github.com/user-attachments/assets/936ec86b-06c5-44a5-a0f8-5eeb90e2d32f" />
# 🐍 pipelines-python

Учебный проект: **CI-пайплайн на GitHub Actions** для Python-приложения.

---

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
<img width="611" height="294" alt="image" src="https://github.com/user-attachments/assets/f0dfe17b-2f0f-44ab-a248-45bbdef4a586" />

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
- **GitHub Actions** — CI

---

## 📄 Лицензия

MIT — свободно для учебных целей.
