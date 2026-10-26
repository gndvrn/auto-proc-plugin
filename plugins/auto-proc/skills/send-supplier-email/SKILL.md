---
name: send-supplier-email
description: >-
  Запрос КП поставщику через MCP mail. Автоматически после wholesale-offer-search в auto-proc-cycle;
  также при номенклатуре в чате, если известен email. Не жди «отправь письмо» или «напиши поставщику».
---
# Отправка письма поставщику

## Предварительные условия

MCP **`mail`** из `mcp.json` плагина. Если `list_accounts` пуст: `npx -y @1amsheldon/mail-mcp@latest accounts add`.

Конфиг: `config/procurement.yaml` → `email`; шаблон `config/email-templates/<template_file>`.

Профиль: **`config/sender-profile.yaml`**, иначе **`config/sender-profile.example.yaml`** — **не** спрашивай реквизиты в чате.

## Шаблон

Подстановки `{{variable}}`. Первая строка `Тема: ...` → subject; остальное → body, plain text.

| Переменная | Откуда |
| --- | --- |
| `subject_prefix` | `email.subject_prefix` |
| `supplier_name` | Заказ / лучший оффер / домен |
| `nomenclature`, `quantity`, `unit` | Заказ; дефолты `1`, `шт` |
| `reference_unit_price`, `currency` | Заказ; может быть «—» |
| `delivery_terms`, контакты компании | Профиль отправителя |

Неизвестные ключи — пустая строка или дефолт профиля; **не** блокируй отправку вопросами.

## MCP mail

1. `list_accounts` → **первый** `accountId`.
2. `mail_mutate` / `sendMessage`: `to`, `subject`, `body`, `isHtml: false`.
3. `confirmationRequired` — черновик (to, subject, body) и **сразу** повтор с `confirmationId` **в том же ходе**.
4. `smtp_outcome_unknown` — не повторять; проверка по документации mail MCP.

При необходимости прочитай ресурс `mail://agent-guide` у MCP mail.

## После отправки

Факт, тема, получатель. Мониторинг почты — только по запросу пользователя (`check-mailbox-replies`).
