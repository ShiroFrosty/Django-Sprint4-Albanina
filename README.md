Процесс развертывания проекта (для функционирования базы данных)
Ключевые моменты:

Файл базы blogicum/db.sqlite3 разрешено размещать в системе контроля версий (исключили его из .gitignore) — это дает возможность немедленного запуска.

Каталог blogicum/media/ остался в .gitignore, поэтому графические файлы после копирования репозитория могут быть недоступны (если не добавлены отдельно).

Экспресс-старт (при наличии готовой базы в репозитории)
powershell
python -m venv venv
.\venv\Scripts\python.exe -m pip install -r requirements.txt
.\venv\Scripts\python.exe .\blogicum\manage.py runserver
Способ A — новая база (применение миграций + регистрация администратора)
Из основной директории:

powershell
python -m venv venv
.\venv\Scripts\python.exe -m pip install -r requirements.txt
.\venv\Scripts\python.exe .\blogicum\manage.py migrate
.\venv\Scripts\python.exe .\blogicum\manage.py createsuperuser
.\venv\Scripts\python.exe .\blogicum\manage.py runserver
После выполнения доступ к сайту: http://127.0.0.1:8000/, административный интерфейс: http://127.0.0.1:8000/admin/.

Способ B — демонстрационный контент (миграции + импорт db.json)
Данный подход необходим, если требуется представить проект с заранее подготовленными категориями, публикациями и учетными записями.

powershell
python -m venv venv
.\venv\Scripts\python.exe -m pip install -r requirements.txt
.\venv\Scripts\python.exe .\blogicum\manage.py migrate
.\venv\Scripts\python.exe .\blogicum\manage.py loaddata .\db.json
.\venv\Scripts\python.exe .\blogicum\manage.py runserver
Важно: в db.json содержатся пользователи, однако пароли представлены в хэшированном виде.
Для доступа в административную зону рекомендуется создать собственного администратора:

powershell
.\venv\Scripts\python.exe .\blogicum\manage.py createsuperuser
Объяснение принятых решений
db.sqlite3 допустимо сохранять в репозитории для показа: обеспечивает максимально быструю демонстрацию рабочего проекта.

db.json включен в репозиторий: представляет собой фикстуру данных, позволяющую оперативно восстановить наполнение для презентации.

