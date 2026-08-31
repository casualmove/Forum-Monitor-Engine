# Forum Monitor Engine

![Python](https://img.shields.io/badge/Python-3.8+-3776AB?style=for-the-badge&logo=python&logoColor=white)
![Playwright](https://img.shields.io/badge/Playwright-Automation-2EAD33?style=for-the-badge&logo=playwright&logoColor=white)
![Telegram](https://img.shields.io/badge/Telegram_API-Bot_Framework-26A5E4?style=for-the-badge&logo=telegram&logoColor=white)
![BeautifulSoup](https://img.shields.io/badge/BeautifulSoup4-Parsing-00599C?style=for-the-badge)
![License](https://img.shields.io/badge/License-MIT-gray?style=for-the-badge)

> Автоматизированный сервис фонового мониторинга форумов XenForo с поддержкой мультичатовой рассылки, разделения прав администраторов и парсинга отфильтрованных тем.

---

## Архитектура работы

```text
  [ Целевой форум XenForo ]
              |
              v
   ( Playwright / BS4 Engine )
              |
              v
   [ Фильтрация тем за 24ч / 7д ]
              |
              v
   ( Telegram Bot Service )
   ├── [ Модуль рассылки ] ------> Оповещение пользователей (CHAT_IDS)
   └── [ Модуль доступа ]  ------> Управление списками (/add, /del)
Ключевые возможностиФоновый мониторинг разделов: Автоматическое сканирование целевых страниц форума с определением свежих публикаций за 24 часа или 7 дней.Исключение дубликатов: Встроенная система отслеживания отправленных ссылок во избежание повторных уведомлений.Динамическое управление доступом: Команды администратора для добавления (/add) и удаления (/del) получателей рассылки в реальном времени.Мультичатовая рассылка: Одновременное вещание списков найденных тем по нескольким Telegram ID.Автоматическая разбивка сообщений: Безопасная отправка длинных списков с учетом лимитов Telegram API (4096 символов).Стек технологийКомпонентБиблиотека / ТехнологияНазначениеСреда выполненияPython 3.8+Основной runtimeАвтоматизацияplaywrightЭмуляция браузера и сбор HTML страницПарсинг DOMbeautifulsoup4Извлечение структурных элементов и временных метокИнтерфейс Telegrampython-telegram-bot / aiogramУведомления и обработка команд управленияКонфигурацияpython-dotenvЗагрузка конфиденциальных данных и настроекСтруктура проектаPlaintext.
├── main.py             # Основной скрипт мониторинга, парсинга и Telegram-бота
├── .env                # Переменные окружения и ключи доступа
├── bot.log             # Системный журнал работы сервиса
└── README.md           # Документация проекта
Переменные окружения (.env)Создайте файл .env в корневой директории проекта:Фрагмент кодаTELEGRAM_TOKEN=123456789:AAA-BBB1234ghIkl-zyx57
CHAT_IDS=987654321,123456789
TARGET_URL=[https://forum.blackrussia.online/forums/target_board/](https://forum.blackrussia.online/forums/target_board/)
ADMIN_IDS=987654321
Справочник параметровTELEGRAM_TOKEN — HTTP API токен Telegram-бота.CHAT_IDS — Список ID чатов/пользователей через запятую для получения рассылок.TARGET_URL — Прямая ссылка на отслеживаемый раздел форума.ADMIN_IDS — ID администраторов, имеющих доступ к командам /add и /del.Команды ботаУправление доступом (Только для ADMIN_IDS)КомандаФорматОписание/add/add <user_id>Добавить Telegram ID в список получателей рассылки/del/del <user_id>Удалить Telegram ID из списка получателей рассылкиУстановка и запуск1. Подготовка репозиторияBashgit clone [https://github.com/your-username/forum-monitor-engine.git](https://github.com/your-username/forum-monitor-engine.git)
cd forum-monitor-engine
2. Установка зависимостейBashpip install playwright beautifulsoup4 python-telegram-bot python-dotenv aiogram
playwright install chromium
3. Запуск сервисаBashpython main.py
ЛицензияПроект распространяется под лицензией MIT.
