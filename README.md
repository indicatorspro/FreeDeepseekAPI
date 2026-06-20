# FreeDeepseekAPI

<p align="center">
  <strong>Локальный OpenAI-compatible API proxy для DeepSeek Web Chat</strong>
  <strong>Local OpenAI-compatible API proxy for DeepSeek Web Chat</strong>
</p>

<p align="center">
  <a href="https://github.com/ForgetMeAI/FreeDeepseekAPI/blob/main/LICENSE"><img alt="License MIT" src="https://img.shields.io/badge/license-MIT-green.svg" /></a>
  <img alt="Node.js 18 plus" src="https://img.shields.io/badge/node-18%2B-339933.svg" />
  <img alt="No npm dependencies" src="https://img.shields.io/badge/dependencies-0-blue.svg" />
  <img alt="OpenAI compatible" src="https://img.shields.io/badge/OpenAI-compatible-111111.svg" />
</p>

<p align="center">
  <a href="#-быстрый-старт">Быстрый старт</a> •
  <a href="#-возможности">Возможности</a> •
  <a href="#-примеры-запросов">Примеры</a> •
  <a href="#-модели">Модели</a> •
  <a href="#-quick-start">Quick Start</a> •
  <a href="#-features">Features</a> •
  <a href="#-request-examples">Examples</a> •
  <a href="#-models">Models</a> •
  <a href="#-endpoints">Endpoints</a> •
  <a href="#-open-webui">Open WebUI</a>
</p>

FreeDeepseekAPI поднимает локальный API-сервер для **DeepSeek Web Chat** (`chat.deepseek.com`) и позволяет подключать DeepSeek Web к Open WebUI, LiteLLM, Hermes, Claude Code, OpenAI SDK-style клиентам и другим OpenAI-compatible инструментам.
FreeDeepseekAPI runs a local API server for **DeepSeek Web Chat** (`chat.deepseek.com`) and allows connecting DeepSeek Web to Open WebUI, LiteLLM, Hermes, Claude Code, OpenAI SDK-style clients, and other OpenAI-compatible tools.

Проект работает через ваш обычный залогиненный аккаунт DeepSeek в отдельном Chrome-профиле. Локальный сервер принимает API-запросы, а дальше сам ходит в DeepSeek Web через сохранённую browser-сессию.
The project works through your regular logged-in DeepSeek account in a separate Chrome profile. The local server accepts API requests and then communicates with DeepSeek Web via the saved browser session.

> ⚠️ Это экспериментальный web-chat proxy. DeepSeek может менять внутренний Web API без предупреждения. Для production-кейсов надёжнее официальный платный API DeepSeek.
> ⚠️ This is an experimental web-chat proxy. DeepSeek may change the internal Web API without notice. For production use cases, the official paid DeepSeek API is more reliable.

ForgetMeAI: https://t.me/forgetmeai

---

## Навигация
## Navigation

- [Что это даёт](#-что-это-даёт)
- [Возможности](#-возможности)
- [Быстрый старт](#-быстрый-старт)
- [Windows запуск](#-windows-запуск)
- [Linux / Chromium запуск](#-linux--chromium-запуск)
- [VPS / headless запуск](#-vps--headless-запуск)
- [What this gives you](#-what-this-gives-you)
- [Features](#-features)
- [Quick Start](#-quick-start)
- [Windows Launch](#-windows-launch)
- [Linux / Chromium Launch](#-linux--chromium-launch)
- [VPS / Headless Launch](#-vps--headless-launch)
- [Diagnostics / doctor](#-diagnostics--doctor)
- [Session reuse и сброс чатов](#-session-reuse-и-сброс-чатов)
- [Session reuse and chat reset](#-session-reuse-and-chat-reset)
- [Multi-account pool](#-multi-account-pool)
- [Идеи для консольной авторизации](#-идеи-для-консольной-авторизации)
- [Проверка работы](#-проверка-работы)
- [Примеры запросов](#-примеры-запросов)
- [Ideas for console authentication](#-ideas-for-console-authentication)
- [Verification](#-verification)
- [Request Examples](#-request-examples)
  - [Chat Completions](#chat-completions)
  - [Reasoning](#reasoning)
  - [Web search](#web-search)
  - [Streaming](#streaming)
  - [Anthropic Messages API](#anthropic-messages-api)
  - [OpenAI Responses API](#openai-responses-api)
  - [Tool calling](#tool-calling)
- [Модели](#-модели)
- [Models](#-models)
- [Endpoints](#-endpoints)
- [Open WebUI](#-open-webui)
- [Обновить логин](#-обновить-логин)
- [Статус проекта](#-статус-проекта)

---

## ✨ Что это даёт

- Использовать DeepSeek Web как локальный API endpoint.
- Подключать DeepSeek к Open WebUI и другим OpenAI-compatible клиентам.
- Получать обычные JSON-ответы или streaming SSE.
- Использовать reasoning-модели с отдельным `reasoning_content`.
- Работать с Anthropic Messages API shim для Claude Code / Anthropic SDK.
- Использовать OpenAI Responses API shim для новых OpenAI/Codex-style клиентов.
- Держать отдельные web-сессии для разных агентов/users.
- Use DeepSeek Web as a local API endpoint.
- Connect DeepSeek to Open WebUI and other OpenAI-compatible clients.
- Get regular JSON responses or streaming SSE.
- Use reasoning models with separate `reasoning_content`.
- Work with Anthropic Messages API shim for Claude Code / Anthropic SDK.
- Use OpenAI Responses API shim for new OpenAI/Codex-style clients.
- Maintain separate web sessions for different agents/users.

## 🚀 Возможности
## 🚀 Features

- **OpenAI-compatible API:** `POST /v1/chat/completions`
- **Anthropic-compatible shim:** `POST /v1/messages`
- **OpenAI Responses shim:** `POST /v1/responses`
- **Streaming:** SSE chunks и обычные non-stream JSON-ответы
- **Reasoning output:** отдельный `reasoning_content` для thinking-моделей
- **Tool calling:** парсинг OpenAI tools, Anthropic tools и Responses function tools
- **Model capabilities:** `GET /v1/model-capabilities` с alias → real web mode
- **Agent sessions:** отдельная DeepSeek-сессия на `user` / agent id
- **Session recovery:** авто-сброс устаревших chains/sessions
- **Zero dependencies:** Node.js 18+, без npm-зависимостей
- **Streaming:** SSE chunks and regular non-stream JSON responses
- **Reasoning output:** separate `reasoning_content` for thinking models
- **Tool calling:** parsing OpenAI tools, Anthropic tools, and Responses function tools
- **Model capabilities:** `GET /v1/model-capabilities` with alias → real web mode
- **Agent sessions:** separate DeepSeek session per `user` / agent id
- **Session recovery:** auto-reset of stale chains/sessions
- **Zero dependencies:** Node.js 18+, no npm dependencies

---

## ⚡ Быстрый старт
## ⚡ Quick Start

```bash
git clone https://github.com/ForgetMeAI/FreeDeepseekAPI.git
cd FreeDeepseekAPI
npm run auth
npm start
```

`npm run auth` открывает меню авторизации:
`npm run auth` opens the authentication menu:

1. выберите пункт `1`;
2. войдите в DeepSeek в отдельном Chrome-профиле;
3. отправьте короткое сообщение вроде `ok`;
4. вернитесь в терминал и нажмите Enter.
1. select item `1`;
2. log into DeepSeek in a separate Chrome profile;
3. send a short message like `ok`;
4. return to terminal and press Enter.

`npm start` показывает меню запуска:
`npm start` shows the launch menu:

- `1` — авторизоваться / обновить DeepSeek login
- `2` — показать модели и статусы
- `3` — запустить proxy
- `4` — выйти
- `1` — authorize / update DeepSeek login
- `2` — show models and statuses
- `3` — run proxy
- `4` — exit

Для headless/CI-запуска без меню:
For headless/CI launch without menu:

```bash
NON_INTERACTIVE=1 npm start
# или
# or
SKIP_ACCOUNT_MENU=1 npm start
```

По умолчанию сервер слушает:
By default the server listens on:

```text
http://localhost:9655
```

---

## 🪟 Windows запуск
## 🪟 Windows Launch

```powershell
git clone https://github.com/ForgetMeAI/FreeDeepseekAPI.git
cd FreeDeepseekAPI
npm run auth
npm start
```

Если Chrome установлен нестандартно, явно укажите путь:
If Chrome is installed in a non-standard location, specify the path explicitly:

```powershell
$env:CHROME_PATH="C:\Program Files\Google\Chrome\Application\chrome.exe"
npm run auth
```

Если Chrome не найден, `npm run auth` теперь печатает готовые инструкции для Windows/macOS/Linux вместо загадочного stack trace.
If Chrome is not found, `npm run auth` now prints ready-to-use instructions for Windows/macOS/Linux instead of a mysterious stack trace.

---

## 🐧 Linux / Chromium запуск
## 🐧 Linux / Chromium Launch

```bash
git clone https://github.com/ForgetMeAI/FreeDeepseekAPI.git
cd FreeDeepseekAPI
CHROME_PATH=$(which chromium) npm run auth
npm start
```

Если Chromium называется иначе:
If Chromium has a different name:

```bash
CHROME_PATH=$(which chromium-browser) npm run auth
# или
# or
CHROME_PATH=$(which google-chrome) npm run auth
```

---

## 🖥 VPS / headless запуск
## 🖥 VPS / Headless Launch

Самый надёжный flow без Chrome на сервере:
The most reliable flow without Chrome on the server:

1. На домашнем ПК, где есть GUI/Chrome:
1. On your home PC where you have GUI/Chrome:

```bash
npm run auth
```

2. Скопируйте `deepseek-auth.json` на VPS:
2. Copy `deepseek-auth.json` to your VPS:

```bash
scp deepseek-auth.json user@your-vps:/opt/FreeDeepseekAPI/deepseek-auth.json
```

3. На VPS импортируйте/проверьте файл и выставьте безопасные права:
3. On VPS import/verify the file and set secure permissions:

```bash
cd /opt/FreeDeepseekAPI
npm run auth:import -- --input ./deepseek-auth.json
npm run doctor -- --offline
```

4. Запускайте proxy без интерактивного меню:
4. Run proxy without interactive menu:

```bash
NON_INTERACTIVE=1 npm start
```

Можно импортировать не только готовый `deepseek-auth.json`, но и browser cookie export:
You can import not only a ready `deepseek-auth.json`, but also a browser cookie export:

```bash
DEEPSEEK_TOKEN="<token>" npm run auth:import -- --input ./cookies.json
```

> Важно: `deepseek-auth.json` — это доступ к вашему DeepSeek Web login. Не коммитьте, не публикуйте, храните с правами `0600`.
> Important: `deepseek-auth.json` is access to your DeepSeek Web login. Do not commit, do not publish, store with `0600` permissions.

---

## 🩺 Diagnostics / doctor

```bash
npm run doctor
# без сетевых запросов к DeepSeek:
# without network requests to DeepSeek:
npm run doctor -- --offline
```

`doctor` проверяет:
`doctor` checks:

- найден ли `deepseek-auth.json` / `DEEPSEEK_AUTH_DIR`;
- валидный ли JSON;
- есть ли `token`, `cookie`, `wasmUrl`;
- безопасные ли права файла на macOS/Linux (`0600`);
- при обычном запуске — доступен ли DeepSeek PoW endpoint.
- whether `deepseek-auth.json` / `DEEPSEEK_AUTH_DIR` is found;
- whether JSON is valid;
- whether `token`, `cookie`, `wasmUrl` are present;
- whether file permissions are secure on macOS/Linux (`0600`);
- on regular run — whether DeepSeek PoW endpoint is accessible.

Если видите `data.biz_data is null`, `fetch failed`, `401/403/429` или Hermes/OpenCode не видит модели — первым делом запускайте `npm run doctor`.
If you see `data.biz_data is null`, `fetch failed`, `401/403/429` or Hermes/OpenCode doesn't see models — first run `npm run doctor`.

---

## ♻️ Session reuse и сброс чатов
## ♻️ Session reuse and chat reset

FreeDeepseekAPI не создаёт новый DeepSeek чат на каждый HTTP-запрос без причины. Логика такая:
FreeDeepseekAPI does not create a new DeepSeek chat on every HTTP request without reason. The logic is:

- один `x-agent-session`, `session` или `user` → одна DeepSeek chat session;
- если session id уже есть — proxy переиспользует его и продолжает chain через `parent_message_id`;
- auto-reset происходит при TTL, ошибке DeepSeek session или слишком длинной цепочке сообщений;
- локальная history сохраняется коротким контекстом, чтобы новая DeepSeek session могла продолжить разговор.
- one `x-agent-session`, `session` or `user` → one DeepSeek chat session;
- if session id already exists — proxy reuses it and continues chain via `parent_message_id`;
- auto-reset happens on TTL, DeepSeek session error, or too long message chain;
- local history is saved as short context so a new DeepSeek session can continue the conversation.

Явно задать agent/session:
Explicitly set agent/session:

```bash
curl -X POST http://localhost:9655/v1/chat/completions \
  -H "Content-Type: application/json" \
  -H "x-agent-session: my-agent" \
  -d '{"model":"deepseek-chat","messages":[{"role":"user","content":"Привет"}]}'
  -d '{"model":"deepseek-chat","messages":[{"role":"user","content":"Hello"}]}'
```

Посмотреть активные sessions:
View active sessions:

```bash
curl http://localhost:9655/v1/sessions
```

Сбросить одну session:
Reset one session:

```bash
curl -X POST "http://localhost:9655/reset-session?agent=my-agent"
```

Сбросить все sessions:
Reset all sessions:

```bash
curl -X POST "http://localhost:9655/reset-session?agent=all"
```

Почему чаты всё равно появляются в DeepSeek Web: proxy работает через внутренний Web Chat API, а DeepSeek хранит реальные chat sessions у себя. Это нормально для web-proxy. Задача session reuse — не плодить новые чаты без необходимости и аккуратно сбрасываться только когда chain протух/сломался.
Why chats still appear in DeepSeek Web: proxy works through internal Web Chat API, and DeepSeek stores real chat sessions on their side. This is normal for web-proxy. The task of session reuse is not to spawn new chats unnecessarily and to reset cleanly only when chain is stale/broken.

---

## 👥 Multi-account pool

Можно подключить несколько auth-файлов. Правильная модель: sticky account per agent/session — proxy не переключает аккаунт внутри живой DeepSeek-сессии. Если аккаунт получил `401/403/429` и ушёл в cooldown, session безопасно сбрасывается и новый запрос может перейти на другой доступный аккаунт.
You can connect multiple auth files. The correct model: sticky account per agent/session — proxy does not switch account inside a live DeepSeek session. If an account gets `401/403/429` and goes into cooldown, session is safely reset and a new request can switch to another available account.

Вариант 1 — директория с auth-файлами:
Option 1 — directory with auth files:

```bash
mkdir -p accounts
cp deepseek-auth-main.json accounts/main.json
cp deepseek-auth-backup.json accounts/backup.json
chmod 600 accounts/*.json
DEEPSEEK_AUTH_DIR=./accounts NON_INTERACTIVE=1 npm start
```

Вариант 2 — список файлов:
Option 2 — list of files:

```bash
DEEPSEEK_AUTH_PATH="./accounts/main.json,./accounts/backup.json" NON_INTERACTIVE=1 npm start
```

Как работает pool:
How pool works:

- новый agent/session получает доступный аккаунт round-robin;
- выбранный аккаунт закрепляется за session (`sticky`);
- при `401`, `403`, `429` аккаунт уходит в cooldown;
- если sticky-аккаунт session ушёл в cooldown, старая DeepSeek-сессия сбрасывается, чтобы не долбить rate-limited/expired аккаунт;
- статус аккаунтов виден в `/health` без путей к auth-файлам и без имён файлов;
- auth-файлы должны храниться с правами `0600`.
- new agent/session gets an available account round-robin;
- selected account is pinned to session (`sticky`);
- on `401`, `403`, `429` account goes into cooldown;
- if sticky-account session went into cooldown, old DeepSeek session is reset to avoid hammering rate-limited/expired account;
- account status visible in `/health` without paths to auth files and without file names;
- auth files must be stored with `0600` permissions.

Настроить cooldown:
Configure cooldown:

```bash
DEEPSEEK_ACCOUNT_COOLDOWN_MS=600000 npm start
```

---

## 🔑 Идеи для консольной авторизации
## 🔑 Ideas for console authentication

Парольный flow из PR #3 можно делать, но безопаснее не хранить пароль и не делать это дефолтом. Нормальная реализация:
Password flow from PR #3 can be done, but safer not to store password and not make it default. Normal implementation:

1. `npm run auth:console` спрашивает email/телефон и пароль через hidden prompt.
2. Пароль держится только в памяти процесса, не пишется в файлы/logs/history.
3. Скрипт повторяет Web login flow через `fetch`/CDP: получает captcha/verify challenge, отдаёт человеку ссылку/код, ждёт подтверждение.
4. После успешного login сохраняется только `deepseek-auth.json` стандартного формата.
5. Если DeepSeek просит captcha/2FA — скрипт честно говорит “открой ссылку, пройди проверку, нажми Enter”, а не пытается обходить защиту.
6. Для VPS лучше режим `auth:console --no-save-password --output deepseek-auth.json`.
1. `npm run auth:console` asks for email/phone and password via hidden prompt.
2. Password stays only in process memory, not written to files/logs/history.
3. Script repeats Web login flow via `fetch`/CDP: gets captcha/verify challenge, gives human link/code, waits for confirmation.
4. After successful login only standard-format `deepseek-auth.json` is saved.
5. If DeepSeek asks for captcha/2FA — script honestly says "open link, pass check, press Enter", doesn't try to bypass protection.
6. For VPS better mode `auth:console --no-save-password --output deepseek-auth.json`.

Минимальный безопасный MVP: console auth только интерактивный, без env-пароля. Допустимый automation-вариант: `DEEPSEEK_EMAIL=... npm run auth:console`, но пароль всё равно вводится hidden prompt.
Minimal safe MVP: console auth only interactive, no env password. Acceptable automation variant: `DEEPSEEK_EMAIL=... npm run auth:console`, but password still entered via hidden prompt.

---

## ✅ Проверка работы
## ✅ Verification

```bash
curl http://localhost:9655/
curl http://localhost:9655/v1/models
curl http://localhost:9655/v1/model-capabilities
```

Если всё ок, `/health` вернёт статус сервера, список поддерживаемых aliases и `config_ready: true`.
If all is ok, `/health` returns server status, list of supported aliases and `config_ready: true`.

---

## 🧪 Примеры запросов
## 🧪 Request Examples

### Chat Completions

```bash
curl -X POST http://localhost:9655/v1/chat/completions \
  -H "Content-Type: application/json" \
  -d '{
    "model": "deepseek-chat",
    "messages": [{"role": "user", "content": "Привет! Ответь одной фразой."}],
    "messages": [{"role": "user", "content": "Hello! Reply with one phrase."}],
    "stream": false
  }'
```

### Reasoning

```bash
curl -X POST http://localhost:9655/v1/chat/completions \
  -H "Content-Type: application/json" \
  -d '{
    "model": "deepseek-reasoner",
    "messages": [{"role": "user", "content": "Реши коротко: почему небо голубое?"}],
    "messages": [{"role": "user", "content": "Solve briefly: why is the sky blue?"}],
    "stream": false
  }'
```

Для reasoning-моделей API отдаёт цепочку размышления отдельно от финального ответа:
For reasoning models API returns reasoning chain separately from final answer:

- non-stream: `choices[0].message.reasoning_content`
- stream: `choices[0].delta.reasoning_content`
- usage: `usage.completion_tokens_details.reasoning_tokens`

`reasoning_tokens` — приблизительная оценка по извлечённому DeepSeek Web `THINK`-тексту, потому что web stream не отдаёт официальный token usage по reasoning отдельно.
`reasoning_tokens` — approximate estimate from extracted DeepSeek Web `THINK` text, because web stream doesn't return official token usage for reasoning separately.

### Web search

```bash
curl -X POST http://localhost:9655/v1/chat/completions \
  -H "Content-Type: application/json" \
  -d '{
    "model": "deepseek-chat-search",
    "messages": [{"role": "user", "content": "Найди свежий факт про DeepSeek и ответь кратко."}],
    "messages": [{"role": "user", "content": "Find a fresh fact about DeepSeek and answer briefly."}],
    "stream": false
  }'
```

### Streaming

```bash
curl -N -X POST http://localhost:9655/v1/chat/completions \
  -H "Content-Type: application/json" \
  -d '{
    "model": "deepseek-chat",
    "messages": [{"role": "user", "content": "Напиши короткую шутку."}],
    "messages": [{"role": "user", "content": "Write a short joke."}],
    "stream": true
  }'
```

### Anthropic Messages API

```bash
curl -X POST http://localhost:9655/v1/messages \
  -H "Content-Type: application/json" \
  -d '{
    "model": "deepseek-chat",
    "max_tokens": 512,
    "messages": [{"role": "user", "content": "Ответь ровно OK"}],
    "messages": [{"role": "user", "content": "Reply exactly OK"}],
    "stream": false
  }'
```

Для Claude Code можно указывать backend напрямую:
For Claude Code you can specify backend directly:

```bash
export ANTHROPIC_BASE_URL="http://127.0.0.1:9655"
export ANTHROPIC_AUTH_TOKEN="dummy-key"
export CLAUDE_CODE_ENABLE_GATEWAY_MODEL_DISCOVERY=1
claude --model deepseek-chat
```

### OpenAI Responses API

```bash
curl -X POST http://localhost:9655/v1/responses \
  -H "Content-Type: application/json" \
  -d '{
    "model": "deepseek-chat",
    "input": "Ответь ровно OK",
    "input": "Reply exactly OK",
    "stream": false
  }'
```

### Tool calling

FreeDeepseekAPI принимает:
FreeDeepseekAPI accepts:

- OpenAI `tools`;
- Anthropic `tools`;
- Responses API function tools.

Прокси просит DeepSeek вернуть строгий JSON tool call, но также умеет парсить fallback-форматы:
Proxy asks DeepSeek to return strict JSON tool call, but also knows how to parse fallback formats:

- `TOOL_CALL:`
- fenced JSON
- `<tool_call>...</tool_call>`

---

## 🧠 Модели
## 🧠 Models

`GET /v1/models` возвращает только aliases, которые сейчас проверены и работают через этот proxy.
`GET /v1/models` returns only aliases that are currently verified and working through this proxy.

### Рабочие aliases
### Working aliases

| Alias | Web mode | Reasoning | Web search | Комментарий |
| Alias | Web mode | Reasoning | Web search | Comment |
| --- | --- | --- | --- | --- |
| `deepseek-chat` | `Быстрый` / `default` | нет | нет | базовый chat |
| `deepseek-v3` | `Быстрый` / `default` | нет | нет | совместимый alias |
| `deepseek-default` | `Быстрый` / `default` | нет | нет | совместимый alias |
| `deepseek-reasoner` | `Быстрый` / `default` | да | нет | `thinking_enabled=true` |
| `deepseek-r1` | `Быстрый` / `default` | да | нет | R1-compatible alias |
| `deepseek-chat-search` | `Быстрый` / `default` | нет | да | web search |
| `deepseek-default-search` | `Быстрый` / `default` | нет | да | web search alias |
| `deepseek-reasoner-search` | `Быстрый` / `default` | да | да | reasoning + search |
| `deepseek-r1-search` | `Быстрый` / `default` | да | да | R1-compatible + search |
| `deepseek-expert` | `Эксперт` / `expert` | нет | нет | Expert mode |
| `deepseek-v4-pro` | `Эксперт` / `expert` | да | нет | Expert + reasoning |

Полный маппинг:
| `deepseek-chat` | `Default` / `default` | no | no | basic chat |
| `deepseek-v3` | `Default` / `default` | no | no | compatible alias |
| `deepseek-default` | `Default` / `default` | no | no | compatible alias |
| `deepseek-reasoner` | `Default` / `default` | yes | no | `thinking_enabled=true` |
| `deepseek-r1` | `Default` / `default` | yes | no | R1-compatible alias |
| `deepseek-chat-search` | `Default` / `default` | no | yes | web search |
| `deepseek-default-search` | `Default` / `default` | no | yes | web search alias |
| `deepseek-reasoner-search` | `Default` / `default` | yes | yes | reasoning + search |
| `deepseek-r1-search` | `Default` / `default` | yes | yes | R1-compatible + search |
| `deepseek-expert` | `Expert` / `expert` | no | no | Expert mode |
| `deepseek-v4-pro` | `Expert` / `expert` | yes | no | Expert + reasoning |

Full mapping:

```bash
curl http://localhost:9655/v1/model-capabilities
```

По официальной странице DeepSeek V4 Preview `deepseek-chat` и `deepseek-reasoner` сейчас route'ятся в `deepseek-v4-flash` non-thinking/thinking. В самом `chat.deepseek.com` direct stream точное имя чекпойнта не отдаётся (`model: ""`), поэтому proxy фиксирует одновременно web-режим (`default` / `Быстрый`) и актуальную официальную маршрутизацию (`DeepSeek-V4-Flash`).
According to the official DeepSeek V4 Preview page, `deepseek-chat` and `deepseek-reasoner` currently route to `deepseek-v4-flash` non-thinking/thinking. In `chat.deepseek.com` direct stream the exact checkpoint name is not returned (`model: ""`), so proxy captures both web mode (`default` / `Default`) and actual official routing (`DeepSeek-V4-Flash`).

Текущий вывод DeepSeek Web remote config показывает такие web-режимы:
Current DeepSeek Web remote config output shows these web modes:

- `default` / UI `Быстрый` — работает; поддерживает `thinking_enabled` и `search_enabled`.
- `expert` / UI `Эксперт` — работает через актуальный web-контракт (`x-client-version=2.0.0`) и поддерживает `thinking_enabled`. В `/v1/models` выдаются `deepseek-expert` без reasoning и `deepseek-v4-pro` как Expert + reasoning.
- `vision` / UI `Распознавание` — виден в remote config, но сейчас direct Web API возвращает `backend_err_by_model` (`Vision is temporarily unavailable`). Поэтому `deepseek-vision` скрыт из `/v1/models`.
- `default` / UI `Default` — works; supports `thinking_enabled` and `search_enabled`.
- `expert` / UI `Expert` — works via current web contract (`x-client-version=2.0.0`) and supports `thinking_enabled`. In `/v1/models` `deepseek-expert` without reasoning and `deepseek-v4-pro` as Expert + reasoning are exposed.
- `vision` / UI `Vision` — visible in remote config, but currently direct Web API returns `backend_err_by_model` (`Vision is temporarily unavailable`). Therefore `deepseek-vision` is hidden from `/v1/models`.

Search для Expert по remote config недоступен, поэтому `deepseek-expert-search` остаётся unsupported.
Search for Expert is unavailable per remote config, so `deepseek-expert-search` remains unsupported.

---

## 🔌 Endpoints

| Method | Path | Назначение |
| Method | Path | Purpose |
| --- | --- | --- |
| `GET` | `/` или `/health` | статус proxy |
| `GET` | `/v1/models` | список рабочих OpenAI-compatible aliases |
| `GET` | `/v1/model-capabilities` | полный маппинг aliases, real model, capabilities |
| `GET` | `/` or `/health` | proxy status |
| `GET` | `/v1/models` | list of working OpenAI-compatible aliases |
| `GET` | `/v1/model-capabilities` | full mapping of aliases, real model, capabilities |
| `POST` | `/v1/chat/completions` | OpenAI-compatible Chat Completions |
| `POST` | `/v1/messages` | Anthropic Messages API shim |
| `POST` | `/v1/responses` | OpenAI Responses API shim |
| `GET` | `/v1/sessions` | активные локальные agent sessions |
| `POST` | `/reset-session?agent=<id>` | сбросить одну session |
| `POST` | `/reset-session?agent=all` | сбросить все sessions |
| `GET` | `/v1/sessions` | active local agent sessions |
| `POST` | `/reset-session?agent=<id>` | reset one session |
| `POST` | `/reset-session?agent=all` | reset all sessions |

---

## 🖥 Open WebUI

Base URL для Open WebUI в Docker:
Base URL for Open WebUI in Docker:

```text
http://host.docker.internal:9655/v1
```

Для локального запуска без Docker:
For local launch without Docker:

```text
http://localhost:9655/v1
```

API key можно указать любой: proxy сам ходит в DeepSeek Web через сохранённую browser-сессию.
API key can be anything: proxy goes to DeepSeek Web via the saved browser session.

---

## 🔐 Обновить логин
## 🔐 Update login

```bash
npm run auth
npm start
```

Если DeepSeek начал отвечать `401`, `403` или просит новый PoW/session — повторите `npm run auth` и обновите сохранённую browser-сессию.
If DeepSeek starts responding with `401`, `403` or asks for new PoW/session — repeat `npm run auth` and update the saved browser session.

Локальные файлы авторизации не должны попадать в GitHub:
Local auth files must not end up on GitHub:

- `deepseek-auth.json`
- `.chrome-profile-deepseek/`
- `.env`

Они уже добавлены в `.gitignore`.
They are already added to `.gitignore`.

---

## 🧪 Тесты
## 🧪 Tests

Syntax check of the project:

```bash
npm test
```

Live smoke-тесты против запущенного локального proxy:
Live smoke tests against running local proxy:

```bash
BASE_URL=http://127.0.0.1:9655 MODEL=deepseek-chat npm run test:live
```

---

## 📌 Статус проекта
## 📌 Project status

FreeDeepseekAPI — экспериментальный web-chat proxy для локального использования и интеграций. Он зависит от текущего контракта DeepSeek Web Chat, поэтому при изменениях на стороне DeepSeek может потребоваться обновление auth/session logic или model mapping.
FreeDeepseekAPI — experimental web-chat proxy for local use and integrations. It depends on the current DeepSeek Web Chat contract, so when DeepSeek makes changes, auth/session logic or model mapping may need updates.

Если что-то перестало работать:
If something stops working:

1. обновите логин через `npm run auth`;
2. проверьте `/v1/model-capabilities`;
3. повторите запрос на свежей сессии;
4. если проблема сохраняется — вероятно, DeepSeek изменил внутренний Web API.
1. update login via `npm run auth`;
2. check `/v1/model-capabilities`;
3. repeat request on a fresh session;
4. if problem persists — DeepSeek likely changed the internal Web API.

---

<p align="center">
  <strong>ForgetMeAI</strong> · <a href="https://t.me/forgetmeai">Telegram</a>
</p>
