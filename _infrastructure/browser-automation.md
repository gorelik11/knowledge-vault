# Browser Automation на macOS High Sierra

Инструкция по автоматизации через браузер (Selenium + Firefox).
Проверено на YouTube Studio bulk update (52 видео, март 2026).

---

## Почему не Playwright

Playwright **не работает** на High Sierra (macOS 10.13):
- Bundled Node.js: `dyld: cannot load 'node'` — бинарник несовместим с ядром
- Bundled Chromium: тоже не запускается
- Системный Chrome через Playwright: Google блокирует CAPTCHA

**Рабочее решение:** Selenium + geckodriver 0.30.0 + Firefox с копией реального профиля.

---

## Установка

```bash
# 1. Selenium
pip3 install selenium

# 2. geckodriver 0.30.0 (ТОЛЬКО эта версия для High Sierra)
curl -L -o /tmp/geckodriver.tar.gz \
  "https://github.com/nicoswan/geckodriver_arm64/releases/download/v0.30.0/geckodriver-v0.30.0-macos-aarch64.tar.gz"
tar -xzf /tmp/geckodriver.tar.gz -C /tmp/
chmod +x /tmp/geckodriver

# Проверка
/tmp/geckodriver --version
# geckodriver 0.30.0
```

Новые версии geckodriver (0.31+) **НЕ работают** на High Sierra.

---

## Ключевая проблема: авторизация

Google/Gmail/YouTube блокируют логин из автоматизированного браузера:
> "Nie udało się zalogować — Ta przeglądarka lub aplikacja może nie być bezpieczna"

### Решение: копия реального Firefox профиля

Вместо логина копируем куки и сессию из вашего обычного Firefox.

```python
import shutil, os

REAL_PROFILE = os.path.expanduser(
    "~/Library/Application Support/Firefox/Profiles/i5hvs9sf.default-release"
)
PROFILE_COPY = "./firefox_profile_copy"

# Копируем ТОЛЬКО нужные файлы (не весь профиль — он может быть 1+ ГБ)
essential_files = [
    "cookies.sqlite",       # Залогиненные сессии
    "permissions.sqlite",   # Разрешения сайтов
    "cert9.db",             # Сертификаты
    "key4.db",              # Ключи
    "logins.json",          # Сохранённые пароли
    "pkcs11.txt",           # Модули безопасности
    "storage.sqlite",       # LocalStorage/SessionStorage
]
essential_dirs = ["storage"]  # Директория хранилища

if os.path.exists(PROFILE_COPY):
    shutil.rmtree(PROFILE_COPY)
os.makedirs(PROFILE_COPY)

for fname in essential_files:
    src = os.path.join(REAL_PROFILE, fname)
    if os.path.exists(src):
        shutil.copy2(src, PROFILE_COPY)

for dname in essential_dirs:
    src = os.path.join(REAL_PROFILE, dname)
    if os.path.exists(src):
        shutil.copytree(src, os.path.join(PROFILE_COPY, dname))
```

**ВАЖНО:** Firefox должен быть ЗАКРЫТ во время копирования профиля.

---

## Создание WebDriver

```python
from selenium import webdriver
from selenium.webdriver.firefox.service import Service
from selenium.webdriver.firefox.options import Options

options = Options()
options.binary_location = "/Applications/Firefox.app/Contents/MacOS/firefox"

# Подключаем копию профиля
options.add_argument("-profile")
options.add_argument(PROFILE_COPY)

# Маскируемся под обычный браузер
options.set_preference("dom.webnotifications.enabled", False)
options.set_preference("media.autoplay.default", 5)
options.set_preference("dom.webdriver.enabled", False)
options.set_preference("useAutomationExtension", False)

service = Service(executable_path="/tmp/geckodriver")
driver = webdriver.Firefox(service=service, options=options)
driver.set_window_size(1280, 900)
```

---

## Применение к Email Campaign

Для Gmail/email кампании тот же подход:
1. Копируем Firefox профиль (вы уже залогинены в Gmail)
2. Открываем Gmail через Selenium
3. Автоматизируем создание черновиков / отправку

```python
# Пример: открыть Gmail
driver.get("https://mail.google.com")
time.sleep(5)
# Вы уже залогинены через скопированный профиль!
```

---

## Rate Limits и Anti-Spam

- **Пауза между действиями:** минимум 10 секунд (лучше больше для email)
- **Bulk операции (50+):** YouTube/Google блокирует запросы (429) на часы
- **Email:** Gmail лимит 500 писем/день, 90 сек между отправками (уже в email_campaign.py)
- После bulk операций yt-dlp и curl к YouTube тоже блокируются

---

## Уборка после работы

Копия профиля Firefox занимает **~700 МБ**. После завершения задачи **обязательно удалить:**

```bash
rm -rf ./firefox_profile_copy
rm -rf ./screenshots  # если были
```

Каждый запуск скрипта создаёт новую копию. 3 запуска = 2+ ГБ мусора.

---

## Чеклист перед запуском

1. [ ] Firefox закрыт
2. [ ] geckodriver 0.30.0 в `/tmp/geckodriver`
3. [ ] `pip3 install selenium`
4. [ ] Профиль Firefox: `~/Library/Application Support/Firefox/Profiles/i5hvs9sf.default-release`
5. [ ] Залогинены в нужном сервисе (Gmail/YouTube) в обычном Firefox
6. [ ] Достаточно места на диске (~1 ГБ на копию профиля + скриншоты)

---

## Рабочий пример

Полный рабочий скрипт: `/Users/dimagorelik/Social-Media/youtube-bulk-update/yt_studio_updater.py`
- 52 видео обновлены через YouTube Studio
- Поддерживает dry run, скриншоты, автоматический и ручной режим
