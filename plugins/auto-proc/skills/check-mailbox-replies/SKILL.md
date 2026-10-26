---
name: check-mailbox-replies
description: >-
  IMAP: ответы на запросы КП. Вручную или по расписанию в отдельном чате.
---
# Ответы на КП в почте

**Настройки:** `INBOX` · тема **`[Запрос КП]`** · слова: *коммерческое предложение*, *КП*, *commercial offer* · без журнала — **7** дней.

**Журнал проверок:** `skills/check-mailbox-replies/checkpoint.json` (создай `{ "lastCheckedAt": null, "lastSeenMessageIds": [] }`, если нет).

## Алгоритм

1. MCP mail: `list_accounts` → `mail_query` / `searchMessages` (`since` из checkpoint или −7 дней, пагинация `nextCursor`).
2. Новые Message-ID → `readMessage`, кратко: от кого, суть, цены/вложения.
3. Запиши checkpoint (`lastCheckedAt`, `lastSeenMessageIds` ≤500).
4. Краткий отчёт.

**Регулярно:** запускай этот скилл вручную или настрой напоминание — выполни скилл, обнови checkpoint.
