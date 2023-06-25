#  Коммандный проект meetup_bot
Telegram bot для реализации функционала организатора

# Задачи бота
Организатор:
* Организую выступления докладчиков → хочу внести в бота докладчиков, которые будут выступать → внёс список людей, которые будут выступать. они видят, что они теперь помечены как докладчики
* Организую мероприятие → хочу поменять программу дня → поменял
* Поменял программу выступления → хочу оповестить других пользователей, что она поменялась → оповестил
* Что-либо случилось → хочу всем массово сообщить о чём-то → могу организовать рассылку
* Прошло мероприятие → хочу провести ещё одно → могу воспользоваться ботом ещё раз
* Идёт мероприятие → хочу узнать, кто донатил → получил список поддержавших и суммы, которые они пожертвовали


## Требования к использованию

Требуется [Python](https://www.python.org/downloads/) версии 3.7 или выше и установленный [pip](https://pip.pypa.io/en/stable/getting-started/). Для установки необходимых зависимостей используйте команду:  
1. Для PIP:
```commandline
python -m pip install -r requirements.txt
```

2. Для Poetry:
```commandline
    poetry init
```

## Установка

1. Выполнить миграцию: `python3 manage.py migrate`
2. Создать файл `.env`, заполнить его по образцу:
```comandline
TG_ORGANIZER_BOT_TOKEN=ваш токен
ID_CHAT_CHANEL=id телеграмм канала #-тут13цифр
SECRET_KEY=ThisIsSoMuchSecretKey
DEBUG=True
ALLOWED_HOSTS=localhost,127.0.0.1
DATABASE=sqlite:///db.sqlite3
```

3. Переместить скрипт со своим ботом в главную директорию.
4. Добавить в него следующее (в начало, до импорта моделей):
```python
os.environ['DJANGO_SETTINGS_MODULE'] = 'storage.settings'
django.setup()

from db.models import User, Donation, Event

env = Env()
env.read_env(override=True)
bot = Bot(env('TG_ORGANIZER_BOT_TOKEN'))
dp = Dispatcher(bot, storage=MemoryStorage())
```

5. Вызывать его простой командой `python3 bot_organizer.py`.