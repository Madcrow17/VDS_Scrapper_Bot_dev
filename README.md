# Telegram Bot и FastAPI для базы объявлений GunsBroker для калибра .308win

Этот проект реализует Telegram-бота для работы с базой объявлений по охотничьему оружию и веб-сервер на FastAPI.

---

## Что делает бот

- Выводит информацию из CSV базы (позиция, название, цена, дата, ссылка, локация)  
- Поддерживает команды: /start, /help, /top, /row, /col, /search, /today, /count_pos, /price  
- Разбивает длинные сообщения на части для Telegram  
- Сортирует объявления по цене  

---

## Установка и запуск

### Требования

- Python 3.8+  
- Библиотеки из `requirements.txt` (fastapi, uvicorn, python-telegram-bot, pandas и прочее)  

### Запуск в режиме разработки

pip install -r requirements.txt
python main.py


Это запустит:

- Telegram-бот (параллельный процесс)  
- FastAPI сервер на порту 8000  

---

## Запуск в продакшн (удалённый сервер)

Рекомендуется запускать FastAPI через Uvicorn с несколькими воркерами:

uvicorn main:app --host 0.0.0.0 --port 8000 --workers 4



Telegram-бот рекомендуется запускать отдельным процессом через systemd или supervisor.

---

## Пример systemd-сервиса для бота

Создайте файл `/etc/systemd/system/telegram_bot.service` с содержимым:



[Unit]  
Description=Telegram Bot Service
After=network.target

[Service]  
User=youruser  
WorkingDirectory=/opt/VDS_Scrapper_Bot  
Environment="PATH=/opt/VDS_Scrapper_Bot/bot_venv/bin"  
ExecStart=/opt/VDS_Scrapper_Bot/bot_venv/bin/python /opt/VDS_Scrapper_Bot/main.py  

Restart=always  
RestartSec=10  

[Install]  
WantedBy=multi-user.target  




Запустите и добавьте автозапуск:

sudo systemctl daemon-reload  
sudo systemctl enable telegram_bot.service  
sudo systemctl start telegram_bot.service  
sudo journalctl -u telegram_bot.service -f  

text

---

## Пример systemd-сервиса для FastAPI

Создайте файл `/etc/systemd/system/fastapi.service` с содержимым:



[Unit]  
Description=FastAPI Service  
After=network.target  

[Service]  
User=youruser  
WorkingDirectory=/opt/VDS_Scrapper_Bot  
Environment="PATH=/opt/VDS_Scrapper_Bot/bot_venv/bin"  
ExecStart=/opt/VDS_Scrapper_Bot/bot_venv/bin/uvicorn main:app --host 0.0.0.0 --port 8000 --workers 4  

Restart=always  
RestartSec=10  

[Install]  
WantedBy=multi-user.target  




Запустите и добавьте автозапуск:

sudo systemctl daemon-reload  
sudo systemctl enable fastapi.service  
sudo systemctl start fastapi.service  
sudo journalctl -u fastapi.service -f  

![bot1.jpg](screenshots%2Fbot1.jpg)
![bot2.jpg](screenshots%2Fbot2.jpg)
![bot3.jpg](screenshots%2Fbot3.jpg)
![bot4.jpg](screenshots%2Fbot4.jpg)
![bot5.jpg](screenshots%2Fbot5.jpg)
![bot6.jpg](screenshots%2Fbot6.jpg)
![bot7.jpg](screenshots%2Fbot7.jpg)
![bot8.jpg](screenshots%2Fbot8.jpg)
![bot9.jpg](screenshots%2Fbot9.jpg)
![bot10.jpg](screenshots%2Fbot10.jpg)
![bot11.jpg](screenshots%2Fbot11.jpg)
![bot12.jpg](screenshots%2Fbot12.jpg)
![bot13.jpg](screenshots%2Fbot13.jpg)
![pr1.jpg](screenshots%2Fpr1.jpg)
![pr2.jpg](screenshots%2Fpr2.jpg)
![pr3.jpg](screenshots%2Fpr3.jpg)
![pr4.jpg](screenshots%2Fpr4.jpg)
![pr5.jpg](screenshots%2Fpr5.jpg)
![pr6.jpg](screenshots%2Fpr6.jpg)
![pr7.jpg](screenshots%2Fpr7.jpg)
