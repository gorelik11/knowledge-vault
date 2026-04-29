# Claude Code & MCP — Структура на этом компьютере

## 1. Claude Code — Файловая структура

### Главная директория: `~/.claude/`

```
~/.claude/
├── .credentials.json          # Учётные данные (авторизация)
├── settings.json              # Глобальные настройки (MCP-серверы, язык, trusted dirs)
├── settings.local.json        # Локальные permissions (разрешения на инструменты)
├── history.jsonl              # История всех сессий
├── stats-cache.json           # Кэш статистики использования
│
├── cache/                     # Кэш (changelog и т.д.)
│   └── changelog.md
│
├── debug/                     # Debug-логи сессий (по UUID)
│
├── file-history/              # История изменений файлов
├── paste-cache/               # Кэш вставок
├── session-env/               # Переменные окружения сессий
├── shell-snapshots/           # Снимки состояния шелла
├── plans/                     # Сохранённые планы (*.md)
├── tasks/                     # Задачи (background agents)
├── todos/                     # Todo-листы сессий
├── downloads/                 # Скачанные файлы
├── telemetry/                 # Телеметрия
│
├── plugins/                   # Плагины (marketplace)
│   ├── known_marketplaces.json
│   └── marketplaces/
│       └── claude-plugins-official/   # Официальный маркетплейс Anthropic
│           └── plugins/               # 31 установленный плагин (см. ниже)
│
└── projects/                  # Проекты (per-directory настройки и сессии)
    ├── -Users-dimagorelik/    # Проект: домашняя директория
    │   ├── memory/            # Персистентная память (MEMORY.md + topic files)
    │   ├── settings.json      # Нет (наследует глобальные)
    │   └── *.jsonl            # Сессии (50+ файлов)
    │
    └── -Volumes-KINGSTON-Code/  # Проект: KINGSTON/Code
        ├── memory/              # (пустая)
        └── settings.json       # Permissions: git add, ls
```

### Персистентная память: `~/.claude/projects/-Users-dimagorelik/memory/`

```
memory/
├── MEMORY.md                 # Главный файл (загружается в system prompt)
├── alignment-workflow.md     # Выравнивание аудио
├── composer-harmony.md       # Гармонический анализ
├── goethe-ikf.md            # Грант Гёте-Института
├── kolot-campaign.md        # Email-кампания Kolot
├── midi-workflow.md         # MIDI/оркестровый workflow
├── project-organization.md  # Организация проектов
├── reaper-technical.md      # Технические заметки Reaper
├── reaper-workflow.md       # Рабочий процесс Reaper
├── render-and-api.md        # Рендер и API
└── tempo-map.md             # Темпо-карта
```

### Конфигурационные файлы

**`~/.claude/settings.json`** — глобальные настройки:
- `trustedDirectories`: `["/Users/dimagorelik"]`
- `mcpServers`: определения MCP-серверов (см. раздел 2)
- `language`: `"Русский"`

**`~/.claude/settings.local.json`** — разрешения (permissions):
- Разрешённые Bash-команды: python3, git, curl, ls, pip3 install, и т.д.
- Разрешённые MCP-инструменты: reaper и total-reaper tools
- Разрешённые домены для WebFetch: github.com, forums.cockos.com, reaper.fm, и др.

### Установленные плагины (из официального маркетплейса)

Источник: `github:anthropics/claude-plugins-official`
Путь: `~/.claude/plugins/marketplaces/claude-plugins-official/plugins/`

Плагины: agent-sdk-dev, clangd-lsp, claude-code-setup, claude-md-management, code-review,
code-simplifier, commit-commands, csharp-lsp, example-plugin, explanatory-output-style,
feature-dev, frontend-design, gopls-lsp, hookify, jdtls-lsp, kotlin-lsp,
learning-output-style, lua-lsp, mcp-server-dev, php-lsp, playground, plugin-dev,
pr-review-toolkit, pyright-lsp, ralph-loop, ruby-lsp, rust-analyzer-lsp,
security-guidance, skill-creator, swift-lsp, typescript-lsp

---

## 2. MCP-серверы — Полная структура

### Обзор

| Сервер | Тип | Кол-во tools | Транспорт | Метод связи |
|--------|-----|-------------|-----------|-------------|
| **reaper** (reapy-based) | stdio | ~15 | stdio → reapy → REAPER OSC | Python-модуль |
| **total-reaper** (Lua file bridge) | stdio | 600+ | stdio → file bridge → Lua в REAPER | Python + Lua |

---

### 2.1. MCP-сервер `reaper` (reapy-based)

**Описание:** Лёгкий сервер на ~15 инструментов, использующий библиотеку reapy для связи с REAPER через OSC-протокол.

**Конфигурация** (в `~/.claude/settings.json`):
```json
{
  "mcpServers": {
    "reaper": {
      "transport": "stdio",
      "command": "/Library/Frameworks/Python.framework/Versions/3.11/bin/python3",
      "args": ["-m", "reaper_reapy_mcp"]
    }
  }
}
```

**Расположение файлов:**
```
/Library/Frameworks/Python.framework/Versions/3.11/lib/python3.11/site-packages/
├── reaper_reapy_mcp/          # MCP-сервер (pip-пакет)
│   └── (модуль запуска)
├── reaper_reapy_mcp-0.1.3.dist-info/
└── reapy/                     # python-reapy v0.10.0 (зависимость)
```

**Связь:**
```
Claude Code  →  stdio  →  python3 -m reaper_reapy_mcp  →  reapy  →  OSC  →  REAPER
```

**Требования для работы:**
- В REAPER должен быть запущен скрипт `activate_reapy_server.py` (ReaScript action)
- reapy общается с REAPER через OSC на localhost

**Ссылки:**
- Пакет: [github.com/wegitor/reaper-reapy-mcp](https://github.com/wegitor/reaper-reapy-mcp)
- reapy: [github.com/RomeoDespres/reapy](https://github.com/RomeoDespres/reapy)

**Основные инструменты:**
- `test_connection` — проверка связи
- `get_track_list` — список треков
- `get_tempo` / `get_time_signature` — темп и размер
- `get_project_time_signature` — подпись проекта
- `get_items_in_time_range` — айтемы во временном диапазоне
- `get_fx_list` — список FX на треке
- `add_fx`, `get_fx_param`, `set_fx_param` — управление FX
- `create_track`, `rename_track`, `set_track_color`
- `create_midi_item`, `add_midi_note(s)`, `get_midi_notes`
- `get_selected_items`, `get_item_properties`
- `create_marker`, `create_region`, `set_tempo`
- И др.

---

### 2.2. MCP-сервер `total-reaper` (Lua file bridge)

**Описание:** Полнофункциональный сервер с 600+ инструментами, включая DSL-команды. Связывается с REAPER через файловый мост (Lua-скрипт внутри REAPER читает/пишет файлы).

**Расположение проекта:**
```
~/total-reaper-mcp/
├── server/                    # Python MCP-сервер
│   ├── app.py                 # Основной entry point (запуск: python -m server.app)
│   ├── bridge.py              # Файловый мост (чтение/запись через mcp_bridge_data/)
│   ├── websocket_client.py    # WebSocket-клиент
│   ├── tool_registry.py       # Реестр инструментов
│   ├── tool_profiles.py       # Профили инструментов
│   ├── tools/                 # Реализации инструментов
│   └── dsl/                   # DSL-парсер и команды
│
├── lua/
│   └── mcp_bridge.lua         # Lua-мост (исходник — копируется в REAPER)
│
├── .venv/                     # Python venv (зависимости)
├── pyproject.toml             # Конфиг проекта (reaper-mcp-server v0.1.0)
├── launch_mcp_server.sh       # Скрипт запуска
├── launch_mcp_server_dsl.sh   # Запуск с DSL
└── README.md
```

**Lua-мост в REAPER:**
```
~/Library/Application Support/REAPER/Scripts/
├── mcp_bridge_file_v2.lua     # Активный Lua-мост (203 KB)
└── mcp_bridge_data/           # Директория обмена данными (файловый мост)
```

**Связь:**
```
Claude Code  →  stdio  →  python -m server.app  →  записывает файл в mcp_bridge_data/
                                                 ←  читает результат из mcp_bridge_data/
                                                          ↕
                              REAPER  ←  mcp_bridge_file_v2.lua (постоянно работает как Action)
                                         читает команду → выполняет → пишет результат
```

**Конфигурация в Claude:**
Сервер `total-reaper` определён в настройках Claude Code (через `settings.json` или на уровне сессии). Запускается через venv:
```bash
cd ~/total-reaper-mcp && source .venv/bin/activate && python -m server.app
```

**Требования для работы:**
1. В REAPER запущен Action `mcp_bridge_file_v2.lua` (фоновый defer-скрипт)
2. Python-сервер запущен через Claude Code (stdio transport)

**Ссылки:**
- Проект: [github.com/shiehn/total-reaper-mcp](https://github.com/shiehn/total-reaper-mcp)

**Основные категории инструментов (600+):**
- **DSL-команды** (`dsl_*`): высокоуровневые текстовые команды (play, stop, record, create track, и т.д.)
- **Трек-операции** (`get_track_*`, `set_track_*`, `create_track`, `delete_track`, ...)
- **Item-операции** (`get_media_item_*`, `set_media_item_*`, `split_media_item`, ...)
- **MIDI** (`midi_insert_note`, `midi_get_all_events`, `quantize_midi_notes`, ...)
- **FX/эффекты** (`track_fx_*`, `take_fx_*`)
- **Маркеры/регионы** (`add_project_marker`, `create_region`, ...)
- **Темп/размер** (`get_tempo_*`, `set_tempo_*`, `add_tempo_marker`, ...)
- **Рендер** (`render_project`, `render_project_to_file`, ...)
- **Envelope/автоматизация** (`insert_envelope_point`, `get_envelope_*`, ...)
- **Проект** (`save_project`, `open_project`, `get_project_*`, ...)
- **Routing** (`create_track_send`, `create_sidechain_routing`, ...)
- **Анализ** (`analyze_*`: dynamics, MIDI, tempo, structure, ...)
- **Video** (`get_video_*`, `render_video_frame`, ...)

---

## 3. Взаимодействие компонентов

```
┌─────────────────────────────────────────────────────────────┐
│                      Claude Code CLI                         │
│                                                              │
│  Конфиг: ~/.claude/settings.json                            │
│  Память: ~/.claude/projects/-Users-dimagorelik/memory/      │
│  Плагины: ~/.claude/plugins/marketplaces/                   │
│                                                              │
│  ┌──────────────┐     ┌──────────────────────────┐          │
│  │ MCP: reaper  │     │ MCP: total-reaper        │          │
│  │ (stdio)      │     │ (stdio)                  │          │
│  └──────┬───────┘     └──────────┬───────────────┘          │
└─────────┼────────────────────────┼──────────────────────────┘
          │                        │
          │ python3 -m             │ python -m server.app
          │ reaper_reapy_mcp       │ (из ~/total-reaper-mcp/.venv)
          │                        │
          ▼                        ▼
   ┌─────────────┐    ┌─────────────────────────┐
   │ reapy OSC   │    │ Файловый мост            │
   │ (localhost)  │    │ ~/Library/.../REAPER/    │
   │             │    │ Scripts/mcp_bridge_data/  │
   └──────┬──────┘    └────────────┬─────────────┘
          │                        │
          ▼                        ▼
   ┌──────────────────────────────────────────┐
   │              REAPER DAW                   │
   │                                           │
   │  Actions:                                 │
   │  • activate_reapy_server.py (для reapy)   │
   │  • mcp_bridge_file_v2.lua (для total)     │
   │                                           │
   │  Расположение:                            │
   │  ~/Library/Application Support/REAPER/    │
   └──────────────────────────────────────────┘
```

---

## 4. Ключевые пути

| Что | Путь |
|-----|------|
| Claude Code конфиг | `~/.claude/settings.json` |
| Claude Code permissions | `~/.claude/settings.local.json` |
| Claude Code память | `~/.claude/projects/-Users-dimagorelik/memory/` |
| Claude Code плагины | `~/.claude/plugins/marketplaces/claude-plugins-official/` |
| MCP reaper (pip) | `/Library/Frameworks/Python.framework/Versions/3.11/lib/python3.11/site-packages/reaper_reapy_mcp/` |
| reapy (pip) | `/Library/Frameworks/Python.framework/Versions/3.11/lib/python3.11/site-packages/reapy/` |
| MCP total-reaper | `~/total-reaper-mcp/` |
| total-reaper venv | `~/total-reaper-mcp/.venv/` |
| total-reaper server | `~/total-reaper-mcp/server/app.py` |
| Lua мост (исходник) | `~/total-reaper-mcp/lua/mcp_bridge.lua` |
| Lua мост (в REAPER) | `~/Library/Application Support/REAPER/Scripts/mcp_bridge_file_v2.lua` |
| File bridge data | `~/Library/Application Support/REAPER/Scripts/mcp_bridge_data/` |
| REAPER конфиг | `~/Library/Application Support/REAPER/` |
| Python 3.11 | `/Library/Frameworks/Python.framework/Versions/3.11/bin/python3` |

---

*Создано: 2026-03-20*
