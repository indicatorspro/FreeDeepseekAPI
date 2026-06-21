# FreeDeepseekAPI

<p align="center">
<<<<<<< Updated upstream
  <strong>Локальный OpenAI-compatible API proxy для DeepSeek Web Chat</strong>
=======
  <strong>Local OpenAI-compatible API proxy for DeepSeek Web Chat</strong>
>>>>>>> Stashed changes
</p>

<p align="center">
  <a href="https://github.com/ForgetMeAI/FreeDeepseekAPI/blob/main/LICENSE"><img alt="License MIT" src="https://img.shields.io/badge/license-MIT-green.svg" /></a>
  <img alt="Node.js 18 plus" src="https://img.shields.io/badge/node-18%2B-339933.svg" />
  <img alt="No npm dependencies" src="https://img.shields.io/badge/dependencies-0-blue.svg" />
  <img alt="OpenAI compatible" src="https://img.shields.io/badge/OpenAI-compatible-111111.svg" />
</p>

<p align="center">
<<<<<<< Updated upstream
  <a href="#-быстрый-старт">Быстрый старт</a> •
  <a href="#-возможности">Возможности</a> •
  <a href="#-примеры-запросов">Примеры</a> •
  <a href="#-модели">Модели</a> •
=======
  <a href="#-quick-start">Quick Start</a> •
  <a href="#-features">Features</a> •
  <a href="#-examples">Examples</a> •
  <a href="#-models">Models</a> •
>>>>>>> Stashed changes
  <a href="#-endpoints">Endpoints</a> •
  <a href="#-open-webui">Open WebUI</a>
</p>

<<<<<<< Updated upstream
FreeDeepseekAPI поднимает локальный API-сервер для **DeepSeek Web Chat** (`chat.deepseek.com`) и позволяет подключать DeepSeek Web к Open WebUI, LiteLLM, Hermes, Claude Code, OpenAI SDK-style клиентам и другим OpenAI-compatible инструментам.

Проект работает через ваш обычный залогиненный аккаунт DeepSeek в отдельном Chrome-профиле. Локальный сервер принимает API-запросы, а дальше сам ходит в DeepSeek Web через сохранённую browser-сессию.

> ⚠️ Это экспериментальный web-chat proxy. DeepSeek может менять внутренний Web API без предупреждения. Для production-кейсов надёжнее официальный платный API DeepSeek.
=======
FreeDeepseekAPI runs a local API server for **DeepSeek Web Chat** (`chat.deepseek.com`) and lets you connect DeepSeek Web to Open WebUI, LiteLLM, Hermes, Claude Code, OpenAI SDK-style clients, and other OpenAI-compatible tools.

The project works through your regular logged-in DeepSeek account in a separate Chrome profile. The local server accepts API requests and then talks to DeepSeek Web through the saved browser session.

> ⚠️ This is an experimental web-chat proxy. DeepSeek may change the internal Web API without warning. For production use cases, the official paid DeepSeek API is more reliable.
>>>>>>> Stashed changes

ForgetMeAI: https://t.me/forgetmeai

---

<<<<<<< Updated upstream
## Навигация

- [Что это даёт](#-что-это-даёт)
- [Возможности](#-возможности)
- [Быстрый старт](#-быстрый-старт)
- [Windows запуск](#-windows-запуск)
- [Linux / Chromium запуск](#-linux--chromium-запуск)
- [VPS / headless запуск](#-vps--headless-запуск)
- [Diagnostics / doctor](#-diagnostics--doctor)
- [Session reuse и сброс чатов](#-session-reuse-и-сброс-чатов)
- [Multi-account pool](#-multi-account-pool)
- [Идеи для консольной авторизации](#-идеи-для-консольной-авторизации)
- [Проверка работы](#-проверка-работы)
- [Примеры запросов](#-примеры-запросов)
=======
## Navigation

- [What this gives you](#-what-this-gives-you)
- [Features](#-features)
- [Quick Start](#-quick-start)
- [Windows launch](#-windows-launch)
- [Linux / Chromium launch](#-linux--chromium-launch)
- [VPS / headless launch](#-vps--headless-launch)
- [Diagnostics / doctor](#-diagnostics--doctor)
- [Session reuse and chat reset](#-session-reuse-and-chat-reset)
- [Multi-account pool](#-multi-account-pool)
- [Console auth ideas](#-console-auth-ideas)
- [Verify it works](#-verify-it-works)
- [Request examples](#-request-examples)
>>>>>>> Stashed changes
  - [Chat Completions](#chat-completions)
  - [Reasoning](#reasoning)
  - [Web search](#web-search)
  - [Streaming](#streaming)
  - [Anthropic Messages API](#anthropic-messages-api)
  - [OpenAI Responses API](#openai-responses-api)
  - [Tool calling](#tool-calling)
<<<<<<< Updated upstream
- [Модели](#-модели)
=======
- [Models](#-models)
>>>>>>> Stashed changes
- [Endpoints](#-endpoints)
- [Open WebUI](#-open-webui)
- [Update login](#-update-login)
- [Project status](#-project-status)

---

## ✨ What this gives you

<<<<<<< Updated upstream
- Использовать DeepSeek Web как локальный API endpoint.
- Подключать DeepSeek к Open WebUI и другим OpenAI-compatible клиентам.
- Получать обычные JSON-ответы или streaming SSE.
- Использовать reasoning-модели с отдельным `reasoning_content`.
- Работать с Anthropic Messages API shim для Claude Code / Anthropic SDK.
- Использовать OpenAI Responses API shim для новых OpenAI/Codex-style клиентов.
- Держать отдельные web-сессии для разных агентов/users.

## 🚀 Возможности
=======
- Use DeepSeek Web as a local API endpoint.
- Connect DeepSeek to Open WebUI and other OpenAI-compatible clients.
- Get regular JSON responses or streaming SSE.
- Use reasoning models with separate `reasoning_content`.
- Work with Anthropic Messages API shim for Claude Code / Anthropic SDK.
- Use OpenAI Responses API shim for new OpenAI/Codex-style clients.
- Keep separate web sessions for different agents/users.

## 🚀 Features
>>>>>>> Stashed changes

- **OpenAI-compatible API:** `POST /v1/chat/completions`
- **Anthropic-compatible shim:** `POST /v1/messages`
- **OpenAI Responses shim:** `POST /v1/responses`
<<<<<<< Updated upstream
- **Streaming:** SSE chunks и обычные non-stream JSON-ответы
- **Reasoning output:** отдельный `reasoning_content` для thinking-моделей
- **Tool calling:** парсинг OpenAI tools, Anthropic tools и Responses function tools
- **Model capabilities:** `GET /v1/model-capabilities` с alias → real web mode
- **Agent sessions:** отдельная DeepSeek-сессия на `user` / agent id
- **Session recovery:** авто-сброс устаревших chains/sessions
- **Zero dependencies:** Node.js 18+, без npm-зависимостей

---

## ⚡ Быстрый старт
=======
- **Streaming:** SSE chunks and regular non-stream JSON responses
- **Reasoning output:** separate `reasoning_content` for thinking models
- **Tool calling:** parsing OpenAI tools, Anthropic tools, and Responses function tools
- **Model capabilities:** `GET /v1/model-capabilities` with alias → real web mode
- **Agent sessions:** separate DeepSeek session per `user` / agent id
- **Session recovery:** auto-reset of stale chains/sessions
- **Zero dependencies:** Node.js 18+, no npm dependencies
- **Chrome Extension:** Browser extension for session management
- **Dashboard Web:** Administrative web interface with real-time metrics

---

## ⚡ Quick Start
>>>>>>> Stashed changes

```bash
git clone https://github.com/ForgetMeAI/FreeDeepseekAPI.git
cd FreeDeepseekAPI
npm run auth
npm start
```

<<<<<<< Updated upstream
`npm run auth` открывает меню авторизации:

1. выберите пункт `1`;
2. войдите в DeepSeek в отдельном Chrome-профиле;
3. отправьте короткое сообщение вроде `ok`;
4. вернитесь в терминал и нажмите Enter.

`npm start` показывает меню запуска:

- `1` — авторизоваться / обновить DeepSeek login
- `2` — показать модели и статусы
- `3` — запустить proxy
- `4` — выйти

Для headless/CI-запуска без меню:

```bash
NON_INTERACTIVE=1 npm start
# или
SKIP_ACCOUNT_MENU=1 npm start
```

По умолчанию сервер слушает:
=======
`npm run auth` opens the auth menu:

1. select item `1`;
2. log in to DeepSeek in a separate Chrome profile;
3. send a short message like `ok`;
4. return to terminal and press Enter.

`npm start` shows the launch menu:

- `1` — authorize / update DeepSeek login
- `2` — show models and statuses
- `3` — start proxy
- `4` — exit

For headless/CI launch without menu:

```bash
NON_INTERACTIVE=1 npm start
# or
SKIP_ACCOUNT_MENU=1 npm start
```

By default the server listens on:
>>>>>>> Stashed changes

```text
http://localhost:9655
```

---

<<<<<<< Updated upstream
## 🪟 Windows запуск
=======
## 🪟 Windows Launch
>>>>>>> Stashed changes

```powershell
git clone https://github.com/ForgetMeAI/FreeDeepseekAPI.git
cd FreeDeepseekAPI
npm run auth
npm start
```

<<<<<<< Updated upstream
Если Chrome установлен нестандартно, явно укажите путь:
=======
If Chrome is installed in a non-standard location, specify the path explicitly:
>>>>>>> Stashed changes

```powershell
$env:CHROME_PATH="C:\Program Files\Google\Chrome\Application\chrome.exe"
npm run auth
```

<<<<<<< Updated upstream
Если Chrome не найден, `npm run auth` теперь печатает готовые инструкции для Windows/macOS/Linux вместо загадочного stack trace.

---

## 🐧 Linux / Chromium запуск
=======
If Chrome is not found, `npm run auth` now prints ready-to-use instructions for Windows/macOS/Linux instead of a cryptic stack trace.

---

## 🐧 Linux / Chromium Launch
>>>>>>> Stashed changes

```bash
git clone https://github.com/ForgetMeAI/FreeDeepseekAPI.git
cd FreeDeepseekAPI
CHROME_PATH=$(which chromium) npm run auth
npm start
```

<<<<<<< Updated upstream
Если Chromium называется иначе:

```bash
CHROME_PATH=$(which chromium-browser) npm run auth
# или
=======
If Chromium has a different name:

```bash
CHROME_PATH=$(which chromium-browser) npm run auth
# or
>>>>>>> Stashed changes
CHROME_PATH=$(which google-chrome) npm run auth
```

---

<<<<<<< Updated upstream
## 🖥 VPS / headless запуск

Самый надёжный flow без Chrome на сервере:

1. На домашнем ПК, где есть GUI/Chrome:
=======
## 🖥 VPS / Headless Launch

The most reliable flow without Chrome on the server:

1. On your home PC (where you have GUI/Chrome):
>>>>>>> Stashed changes

```bash
npm run auth
```

<<<<<<< Updated upstream
2. Скопируйте `deepseek-auth.json` на VPS:
=======
2. Copy `deepseek-auth.json` to VPS:
>>>>>>> Stashed changes

```bash
scp deepseek-auth.json user@your-vps:/opt/FreeDeepseekAPI/deepseek-auth.json
```

<<<<<<< Updated upstream
3. На VPS импортируйте/проверьте файл и выставьте безопасные права:
=======
3. On VPS import/verify the file and set safe permissions:
>>>>>>> Stashed changes

```bash
cd /opt/FreeDeepseekAPI
npm run auth:import -- --input ./deepseek-auth.json
npm run doctor -- --offline
```

<<<<<<< Updated upstream
4. Запускайте proxy без интерактивного меню:
=======
4. Start proxy without interactive menu:
>>>>>>> Stashed changes

```bash
NON_INTERACTIVE=1 npm start
```

<<<<<<< Updated upstream
Можно импортировать не только готовый `deepseek-auth.json`, но и browser cookie export:
=======
You can import not only a ready-made `deepseek-auth.json`, but also a browser cookie export:
>>>>>>> Stashed changes

```bash
DEEPSEEK_TOKEN="<token>" npm run auth:import -- --input ./cookies.json
```

<<<<<<< Updated upstream
> Важно: `deepseek-auth.json` — это доступ к вашему DeepSeek Web login. Не коммитьте, не публикуйте, храните с правами `0600`.
=======
> Important: `deepseek-auth.json` gives access to your DeepSeek Web login. Do not commit, do not publish, store with `0600` permissions.
>>>>>>> Stashed changes

---

## 🩺 Diagnostics / doctor

```bash
npm run doctor
<<<<<<< Updated upstream
# без сетевых запросов к DeepSeek:
npm run doctor -- --offline
```

`doctor` проверяет:

- найден ли `deepseek-auth.json` / `DEEPSEEK_AUTH_DIR`;
- валидный ли JSON;
- есть ли `token`, `cookie`, `wasmUrl`;
- безопасные ли права файла на macOS/Linux (`0600`);
- при обычном запуске — доступен ли DeepSeek PoW endpoint.

Если видите `data.biz_data is null`, `fetch failed`, `401/403/429` или Hermes/OpenCode не видит модели — первым делом запускайте `npm run doctor`.

---

## ♻️ Session reuse и сброс чатов

FreeDeepseekAPI не создаёт новый DeepSeek чат на каждый HTTP-запрос без причины. Логика такая:

- один `x-agent-session`, `session` или `user` → одна DeepSeek chat session;
- если session id уже есть — proxy переиспользует его и продолжает chain через `parent_message_id`;
- auto-reset происходит при TTL, ошибке DeepSeek session или слишком длинной цепочке сообщений;
- локальная history сохраняется коротким контекстом, чтобы новая DeepSeek session могла продолжить разговор.

Явно задать agent/session:
=======
# without network requests to DeepSeek:
npm run doctor -- --offline
```

`doctor` checks:

- whether `deepseek-auth.json` / `DEEPSEEK_AUTH_DIR` is found;
- whether JSON is valid;
- whether `token`, `cookie`, `wasmUrl` exist;
- whether file permissions are safe on macOS/Linux (`0600`);
- on normal run — whether DeepSeek PoW endpoint is reachable.

If you see `data.biz_data is null`, `fetch failed`, `401/403/429` or Hermes/OpenCode doesn't see models — first run `npm run doctor`.

---

## ♻️ Session reuse and chat reset

FreeDeepseekAPI doesn't create a new DeepSeek chat on every HTTP request without reason. The logic is:

- one `x-agent-session`, `session`, or `user` → one DeepSeek chat session;
- if session id already exists — proxy reuses it and continues chain via `parent_message_id`;
- auto-reset happens on TTL, DeepSeek session error, or too long message chain;
- local history is saved as short context so new DeepSeek session can continue the conversation.

Explicitly set agent/session:
>>>>>>> Stashed changes

```bash
curl -X POST http://localhost:9655/v1/chat/completions \
  -H "Content-Type: application/json" \
  -H "x-agent-session: my-agent" \
<<<<<<< Updated upstream
  -d '{"model":"deepseek-chat","messages":[{"role":"user","content":"Привет"}]}'
```

Посмотреть активные sessions:
=======
  -d '{"model":"deepseek-chat","messages":[{"role":"user","content":"Hi"}]}'
```

View active sessions:
>>>>>>> Stashed changes

```bash
curl http://localhost:9655/v1/sessions
```

<<<<<<< Updated upstream
Сбросить одну session:
=======
Reset a single session:
>>>>>>> Stashed changes

```bash
curl -X POST "http://localhost:9655/reset-session?agent=my-agent"
```

<<<<<<< Updated upstream
Сбросить все sessions:
=======
Reset all sessions:
>>>>>>> Stashed changes

```bash
curl -X POST "http://localhost:9655/reset-session?agent=all"
```

<<<<<<< Updated upstream
Почему чаты всё равно появляются в DeepSeek Web: proxy работает через внутренний Web Chat API, а DeepSeek хранит реальные chat sessions у себя. Это нормально для web-proxy. Задача session reuse — не плодить новые чаты без необходимости и аккуратно сбрасываться только когда chain протух/сломался.
=======
Why chats still appear in DeepSeek Web: proxy works through internal Web Chat API, and DeepSeek stores real chat sessions on their side. This is normal for web-proxy. The task of session reuse is not to spawn new chats unnecessarily and to reset cleanly only when the chain has gone stale/broken.
>>>>>>> Stashed changes

---

## 👥 Multi-account pool

<<<<<<< Updated upstream
Можно подключить несколько auth-файлов. Правильная модель: sticky account per agent/session — proxy не переключает аккаунт внутри живой DeepSeek-сессии. Если аккаунт получил `401/403/429` и ушёл в cooldown, session безопасно сбрасывается и новый запрос может перейти на другой доступный аккаунт.

Вариант 1 — директория с auth-файлами:
=======
You can connect multiple auth files. Correct model: sticky account per agent/session — proxy doesn't switch account inside a live DeepSeek session. If an account gets `401/403/429` and goes into cooldown, the session is safely reset and a new request may switch to another available account.

Option 1 — directory with auth files:
>>>>>>> Stashed changes

```bash
mkdir -p accounts
cp deepseek-auth-main.json accounts/main.json
cp deepseek-auth-backup.json accounts/backup.json
chmod 600 accounts/*.json
DEEPSEEK_AUTH_DIR=./accounts NON_INTERACTIVE=1 npm start
```

<<<<<<< Updated upstream
Вариант 2 — список файлов:
=======
Option 2 — file list:
>>>>>>> Stashed changes

```bash
DEEPSEEK_AUTH_PATH="./accounts/main.json,./accounts/backup.json" NON_INTERACTIVE=1 npm start
```

<<<<<<< Updated upstream
Как работает pool:

- новый agent/session получает доступный аккаунт round-robin;
- выбранный аккаунт закрепляется за session (`sticky`);
- при `401`, `403`, `429` аккаунт уходит в cooldown;
- если sticky-аккаунт session ушёл в cooldown, старая DeepSeek-сессия сбрасывается, чтобы не долбить rate-limited/expired аккаунт;
- статус аккаунтов виден в `/health` без путей к auth-файлам и без имён файлов;
- auth-файлы должны храниться с правами `0600`.

Настроить cooldown:
=======
How the pool works:

- new agent/session gets an available account round-robin;
- selected account is pinned to session (`sticky`);
- on `401`, `403`, `429` account goes into cooldown;
- if sticky-account session went into cooldown, old DeepSeek session is reset to avoid hammering rate-limited/expired account;
- account status visible in `/health` without auth file paths or file names;
- auth files must be stored with `0600` permissions.

Configure cooldown:
>>>>>>> Stashed changes

```bash
DEEPSEEK_ACCOUNT_COOLDOWN_MS=600000 npm start
```

---

<<<<<<< Updated upstream
## 🔑 Идеи для консольной авторизации

Парольный flow из PR #3 можно делать, но безопаснее не хранить пароль и не делать это дефолтом. Нормальная реализация:

1. `npm run auth:console` спрашивает email/телефон и пароль через hidden prompt.
2. Пароль держится только в памяти процесса, не пишется в файлы/logs/history.
3. Скрипт повторяет Web login flow через `fetch`/CDP: получает captcha/verify challenge, отдаёт человеку ссылку/код, ждёт подтверждение.
4. После успешного login сохраняется только `deepseek-auth.json` стандартного формата.
5. Если DeepSeek просит captcha/2FA — скрипт честно говорит “открой ссылку, пройди проверку, нажми Enter”, а не пытается обходить защиту.
6. Для VPS лучше режим `auth:console --no-save-password --output deepseek-auth.json`.

Минимальный безопасный MVP: console auth только интерактивный, без env-пароля. Допустимый automation-вариант: `DEEPSEEK_EMAIL=... npm run auth:console`, но пароль всё равно вводится hidden prompt.

---

## ✅ Проверка работы
=======
## 🔑 Console auth ideas

Password flow from PR #3 can be done, but safer not to store password and not make it default. Normal implementation:

1. `npm run auth:console` asks for email/phone and password via hidden prompt.
2. Password stays only in process memory, not written to files/logs/history.
3. Script replicates Web login flow via `fetch`/CDP: gets captcha/verify challenge, gives human link/code, waits for confirmation.
4. After successful login, only standard-format `deepseek-auth.json` is saved.
5. If DeepSeek asks for captcha/2FA — script honestly says "open link, pass check, press Enter", doesn't try to bypass protection.
6. For VPS better mode `auth:console --no-save-password --output deepseek-auth.json`.

Minimal safe MVP: console auth only interactive, no env password. Acceptable automation variant: `DEEPSEEK_EMAIL=... npm run auth:console`, but password still entered via hidden prompt.

---

## ✅ Verify it works
>>>>>>> Stashed changes

```bash
curl http://localhost:9655/
curl http://localhost:9655/v1/models
curl http://localhost:9655/v1/model-capabilities
```

<<<<<<< Updated upstream
Если всё ок, `/health` вернёт статус сервера, список поддерживаемых aliases и `config_ready: true`.

---

## 🧪 Примеры запросов
=======
If all good, `/health` returns server status, list of supported aliases, and `config_ready: true`.

---

## 🧪 Request examples
>>>>>>> Stashed changes

### Chat Completions

```bash
curl -X POST http://localhost:9655/v1/chat/completions \
  -H "Content-Type: application/json" \
  -d '{
    "model": "deepseek-chat",
<<<<<<< Updated upstream
    "messages": [{"role": "user", "content": "Привет! Ответь одной фразой."}],
=======
    "messages": [{"role": "user", "content": "Hi! Reply with one phrase."}],
>>>>>>> Stashed changes
    "stream": false
  }'
```

### Reasoning

```bash
curl -X POST http://localhost:9655/v1/chat/completions \
  -H "Content-Type: application/json" \
  -d '{
    "model": "deepseek-reasoner",
<<<<<<< Updated upstream
    "messages": [{"role": "user", "content": "Реши коротко: почему небо голубое?"}],
=======
    "messages": [{"role": "user", "content": "Solve briefly: why is the sky blue?"}],
>>>>>>> Stashed changes
    "stream": false
  }'
```

<<<<<<< Updated upstream
Для reasoning-моделей API отдаёт цепочку размышления отдельно от финального ответа:
=======
For reasoning models, API returns the reasoning chain separately from the final answer:
>>>>>>> Stashed changes

- non-stream: `choices[0].message.reasoning_content`
- stream: `choices[0].delta.reasoning_content`
- usage: `usage.completion_tokens_details.reasoning_tokens`

<<<<<<< Updated upstream
`reasoning_tokens` — приблизительная оценка по извлечённому DeepSeek Web `THINK`-тексту, потому что web stream не отдаёт официальный token usage по reasoning отдельно.
=======
`reasoning_tokens` — approximate estimate based on extracted DeepSeek Web `THINK` text, because web stream doesn't return official token usage for reasoning separately.
>>>>>>> Stashed changes

### Web search

```bash
curl -X POST http://localhost:9655/v1/chat/completions \
  -H "Content-Type: application/json" \
  -d '{
    "model": "deepseek-chat-search",
<<<<<<< Updated upstream
    "messages": [{"role": "user", "content": "Найди свежий факт про DeepSeek и ответь кратко."}],
=======
    "messages": [{"role": "user", "content": "Find a fresh fact about DeepSeek and reply briefly."}],
>>>>>>> Stashed changes
    "stream": false
  }'
```

### Streaming

```bash
curl -N -X POST http://localhost:9655/v1/chat/completions \
  -H "Content-Type: application/json" \
  -d '{
    "model": "deepseek-chat",
<<<<<<< Updated upstream
    "messages": [{"role": "user", "content": "Напиши короткую шутку."}],
=======
    "messages": [{"role": "user", "content": "Write a short joke."}],
>>>>>>> Stashed changes
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
<<<<<<< Updated upstream
    "messages": [{"role": "user", "content": "Ответь ровно OK"}],
=======
    "messages": [{"role": "user", "content": "Reply exactly OK"}],
>>>>>>> Stashed changes
    "stream": false
  }'
```

<<<<<<< Updated upstream
Для Claude Code можно указывать backend напрямую:
=======
For Claude Code you can specify backend directly:
>>>>>>> Stashed changes

```bash
export ANTHROPIC_BASE_URL="http://127.0.0.1:9655"
export ANTHROPIC_AUTH_TOKEN="dummy-key"
export CLAUDE_CODE_ENABLE_GATEWAY_MODEL_DISCOVERY=1
claude --model deepseek-chat
```

### OpenAI
```

### OpenAI Responses API

```bash
curl -X POST http://localhost:9655/v1/responses \
  -H "Content-Type: application/json" \
  -d '{
    "model": "deepseek-chat",
<<<<<<< Updated upstream
    "input": "Ответь ровно OK",
=======
    "input": "Reply exactly OK",
>>>>>>> Stashed changes
    "stream": false
  }'
```

### Tool calling

<<<<<<< Updated upstream
FreeDeepseekAPI принимает:
=======
FreeDeepseekAPI accepts:
>>>>>>> Stashed changes

- OpenAI `tools`;
- Anthropic `tools`;
- Responses API function tools.

<<<<<<< Updated upstream
Прокси просит DeepSeek вернуть строгий JSON tool call, но также умеет парсить fallback-форматы:

- `TOOL_CALL:`
- fenced JSON
- `<tool_call>...</tool_call>`

---

## 🧠 Модели

`GET /v1/models` возвращает только aliases, которые сейчас проверены и работают через этот proxy.

### Рабочие aliases

| Alias | Web mode | Reasoning | Web search | Комментарий |
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

```bash
curl http://localhost:9655/v1/model-capabilities
```

По официальной странице DeepSeek V4 Preview `deepseek-chat` и `deepseek-reasoner` сейчас route'ятся в `deepseek-v4-flash` non-thinking/thinking. В самом `chat.deepseek.com` direct stream точное имя чекпойнта не отдаётся (`model: ""`), поэтому proxy фиксирует одновременно web-режим (`default` / `Быстрый`) и актуальную официальную маршрутизацию (`DeepSeek-V4-Flash`).

Текущий вывод DeepSeek Web remote config показывает такие web-режимы:

- `default` / UI `Быстрый` — работает; поддерживает `thinking_enabled` и `search_enabled`.
- `expert` / UI `Эксперт` — работает через актуальный web-контракт (`x-client-version=2.0.0`) и поддерживает `thinking_enabled`. В `/v1/models` выдаются `deepseek-expert` без reasoning и `deepseek-v4-pro` как Expert + reasoning.
- `vision` / UI `Распознавание` — виден в remote config, но сейчас direct Web API возвращает `backend_err_by_model` (`Vision is temporarily unavailable`). Поэтому `deepseek-vision` скрыт из `/v1/models`.

Search для Expert по remote config недоступен, поэтому `deepseek-expert-search` остаётся unsupported.

---

## 🔌 Endpoints

| Method | Path | Назначение |
| --- | --- | --- |
| `GET` | `/` или `/health` | статус proxy |
| `GET` | `/v1/models` | список рабочих OpenAI-compatible aliases |
| `GET` | `/v1/model-capabilities` | полный маппинг aliases, real model, capabilities |
| `POST` | `/v1/chat/completions` | OpenAI-compatible Chat Completions |
| `POST` | `/v1/messages` | Anthropic Messages API shim |
| `POST` | `/v1/responses` | OpenAI Responses API shim |
| `GET` | `/v1/sessions` | активные локальные agent sessions |
| `POST` | `/reset-session?agent=<id>` | сбросить одну session |
| `POST` | `/reset-session?agent=all` | сбросить все sessions |

---

## 🖥 Open WebUI

Base URL для Open WebUI в Docker:

```text
http://host.docker.internal:9655/v1
```

Для локального запуска без Docker:

```text
http://localhost:9655/v1
```

API key можно указать любой: proxy сам ходит в DeepSeek Web через сохранённую browser-сессию.

---

## 🔐 Обновить логин

```bash
npm run auth
npm start
```

Если DeepSeek начал отвечать `401`, `403` или просит новый PoW/session — повторите `npm run auth` и обновите сохранённую browser-сессию.

Локальные файлы авторизации не должны попадать в GitHub:

- `deepseek-auth.json`
- `.chrome-profile-deepseek/`
- `.env`

Они уже добавлены в `.gitignore`.

---

## 🧪 Тесты

Синтаксическая проверка проекта:

```bash
npm test
```

Live smoke-тесты против запущенного локального proxy:

```bash
BASE_URL=http://127.0.0.1:9655 MODEL=deepseek-chat npm run test:live
```

---

## 📌 Статус проекта

FreeDeepseekAPI — экспериментальный web-chat proxy для локального использования и интеграций. Он зависит от текущего контракта DeepSeek Web Chat, поэтому при изменениях на стороне DeepSeek может потребоваться обновление auth/session logic или model mapping.

Если что-то перестало работать:

1. обновите логин через `npm run auth`;
2. проверьте `/v1/model-capabilities`;
3. повторите запрос на свежей сессии;
4. если проблема сохраняется — вероятно, DeepSeek изменил внутренний Web API.

---

<p align="center">
  <strong>ForgetMeAI</strong> · <a href="https://t.me/forgetmeai">Telegram</a>
</p>
=======
Proxy asks DeepSeek to return strict JSON tool call, but also parses fallback formats:

- `TOOL_CALL:`
- fenced JSON
- `<tool_call>...
>>>>>>> Stashed changes
