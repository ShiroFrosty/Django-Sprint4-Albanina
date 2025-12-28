# django_sprint4 (Blogicum)

## Как запустить проект после клонирования (чтобы работала БД)

Важно:
- Файл БД **`blogicum/db.sqlite3` можно хранить в репозитории** (мы убрали его из `.gitignore`) — тогда проект запускается сразу “как есть”.
- Папка **`blogicum/media/`** по‑прежнему в `.gitignore`, поэтому изображения после `git clone` могут отсутствовать (если их отдельно не передать).

### Быстрый запуск (если БД уже есть в репозитории)

```powershell
python -m venv venv
.\venv\Scripts\python.exe -m pip install -r requirements.txt
.\venv\Scripts\python.exe .\blogicum\manage.py runserver
```

### Вариант A — “чистая” база (миграции + свой админ)

Из корня проекта:

```powershell
python -m venv venv
.\venv\Scripts\python.exe -m pip install -r requirements.txt
.\venv\Scripts\python.exe .\blogicum\manage.py migrate
.\venv\Scripts\python.exe .\blogicum\manage.py createsuperuser
.\venv\Scripts\python.exe .\blogicum\manage.py runserver
```

После запуска сайт доступен по `http://127.0.0.1:8000/`, админка — `http://127.0.0.1:8000/admin/`.

### Вариант B — демо‑данные (миграции + загрузка `db.json`)

Этот вариант нужен, если вы хотите показать проект сразу с категориями/постами/пользователями из фикстуры.

```powershell
python -m venv venv
.\venv\Scripts\python.exe -m pip install -r requirements.txt
.\venv\Scripts\python.exe .\blogicum\manage.py migrate
.\venv\Scripts\python.exe .\blogicum\manage.py loaddata .\db.json
.\venv\Scripts\python.exe .\blogicum\manage.py runserver
```

Примечание: в `db.json` есть пользователи, но пароли в фикстуре — **хэши**.  
Чтобы войти в админку, проще всего создать своего админа:

```powershell
.\venv\Scripts\python.exe .\blogicum\manage.py createsuperuser
```

## Почему так (коротко)
- **`db.sqlite3` можно коммитить для демонстрации**: это самый быстрый вариант “показать проект преподавателю”.
- **`db.json` коммитится**: это “снимок данных” (fixture), чтобы быстро восстановить контент для демонстрации.