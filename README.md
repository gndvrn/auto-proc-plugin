# Контроль цен поставщиков

Плагин для **ChatGPT Desktop** (Windows): поиск оптовых предложений, запрос КП по почте, проверка ответов.

> Только десктоп: локальный MCP (`requires_local_executor`).

## Требования

- [ChatGPT Desktop](https://chatgpt.com/download) (Windows)
- **Node.js 20.19+** (для MCP `mail-mcp`; в комплекте идут `node` и `npx`) — [nodejs.org](https://nodejs.org/)

### Установка Node.js (Windows)

**PowerShell** (рекомендуется — актуальный LTS):

```powershell
winget install -e --id OpenJS.NodeJS.LTS
```

Или ветка Node 20 (если нужна именно она):

```powershell
winget install -e --id OpenJS.NodeJS.20
```

**Chocolatey** (если установлен):

```powershell
choco install nodejs-lts -y
```

После установки **закройте и откройте** терминал (и при необходимости ChatGPT Desktop), затем проверка:

```powershell
node -v
npm -v
npx -v
```

Нужно `node` **v20.19.0** или новее (в т.ч. 22.x / 24.x LTS). Если команды не находятся — перезайдите в Windows или добавьте Node в PATH через установщик с [nodejs.org](https://nodejs.org/en/download).

## 1. Установка плагина

### Из каталога OpenAI

1. ChatGPT Desktop → **Plugins** → найти «Контроль цен поставщиков» → **Install**.
2. Пройти шаги авторизации при установке, если запросит.

### Из GitHub

Каталог в репо: `.agents/plugins/marketplace.json` (корень репозитория, без `Path`).

1. **ChatGPT Desktop** → **Plugins** → **Add** → **Add plugin marketplace**.
2. В **Source** — URL репозитория (не ссылка на `marketplace.json`):

   ```
   https://github.com/gndvrn/auto-proc-plugin
   ```

3. **Git ref** и **Sparse paths** — пусто → **Add marketplace**.
4. Выбрать marketplace «Контроль цен поставщиков» → **Install** у `supplier-price-control`.

Обновления подтягивает приложение при sync marketplace; вручную: **Plugins** → обновить marketplace или `codex plugin marketplace upgrade`.

**CLI (без ручного clone):**

```powershell
codex plugin marketplace add gndvrn/auto-proc-plugin
```

Дальше установка плагина — в **Plugins** в Desktop. См. [Build plugins — Add a marketplace](https://developers.openai.com/plugins/build/plugins).

## 2. Настройка почты (обязательно для отправки и проверки inbox)

В **PowerShell** или **cmd**:

```powershell
npx -y @1amsheldon/mail-mcp@latest accounts add
npx -y @1amsheldon/mail-mcp@latest accounts list
```

Мастер `accounts add`: IMAP/SMTP или Microsoft Graph — под вашего провайдера. Учётные данные хранятся в системном хранилище Windows.

Проверка версии Node / npx:

```powershell
node -v
npx -y @1amsheldon/mail-mcp@latest --version
```

## 3. Настройки плагина

Перед работой задайте реквизиты компании и параметры писем в настройках скиллов плагина (или в `plugins/supplier-price-control/customization/skills/*/settings.md` при локальной сборке).

## 4. Использование

Новый **локальный** чат с установленным плагином:

- пришлите номенклатурную позицию — поиск опта;
- попросите отправить запрос КП — отправка через почту;
- «проверь почту» — ответы поставщиков.

При первой отправке письма подтвердите черновик, если запросит `mail-mcp`.

## Ссылки

- [Плагины в ChatGPT](https://help.openai.com/en/articles/20001256-plugins-in-chatgpt)
- [Desktop-only плагины](https://developers.openai.com/plugins/deploy/desktop-only)
- [@1amsheldon/mail-mcp](https://www.npmjs.com/package/@1amsheldon/mail-mcp)
