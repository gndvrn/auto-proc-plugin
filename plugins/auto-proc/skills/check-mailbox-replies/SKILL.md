---
name: check-mailbox-replies
description: >-
  IMAP: ответы поставщиков на запросы КП. Применяй автоматически, если пользователь спрашивает
  про ответы/почту/КП; не блокируй основной цикл auto-proc-cycle.
---
# Проверка почты на ответы поставщиков

## Конфигурация

`config/procurement.yaml` → `mailbox_check`, checkpoint: `config/mailbox-checkpoint.json`.

## Алгоритм

1. MCP **`mail`**: `list_accounts` → первый `accountId`.
2. Окно: `lastCheckedAt` из checkpoint или последние `since_days_if_no_checkpoint` дней.
3. `mail_query` / `searchMessages` (folder, subject/keywords из конфига, `since`, пагинация `nextCursor`).
4. Новые Message-ID → `readMessage`, кратко: от кого, суть, цены/вложения.
5. Обнови checkpoint (`lastCheckedAt`, `lastSeenMessageIds` ≤500).
6. Краткий отчёт.

Критерии поиска совпадают с `email.subject_prefix` и шаблоном КП.

## Ограничения

- Пустая выборка — расширь `keywordsAny` в конфиге.
- Вложения — только по явному запросу.
