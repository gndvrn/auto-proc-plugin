---
name: send-supplier-email
description: >-
  Письмо поставщику (запрос КП) через MCP mail. После wholesale-offer-search или по просьбе пользователя.
---
# Письмо поставщику

**Настройки:** префикс темы **`[Запрос КП]`** (тот же — в `check-mailbox-replies`).

Почта: `npx -y @1amsheldon/mail-mcp@latest accounts add` — https://www.npmjs.com/package/@1amsheldon/mail-mcp

## Профиль отправителя (правь здесь)

```yaml
company_name: "ООО Пример"
contact_person: "Иван Иванов"
contact_phone: "+7 ..."
contact_email: "procurement@example.com"
delivery_terms: "склад покупателя, оплата по договору"
```

## Шаблон письма (правь здесь)

Подстановки `{{…}}`. Строка `Тема:` → subject MCP; ниже → body (plain text). `subject_prefix` = `[Запрос КП]`.

```
Тема: {{subject_prefix}} {{nomenclature}}

{{supplier_name}},

Добрый день.

Просим подготовить коммерческое предложение на поставку:

Наименование: {{nomenclature}}
Количество: {{quantity}} {{unit}}
Ориентир по цене закупки (для сравнения): {{reference_unit_price}} {{currency}} за {{unit}}

Условия поставки (желаемые): {{delivery_terms}}

Просим указать:
- цену за {{unit}} при указанном объёме;
- минимальную партию;
- срок поставки;
- условия оплаты и доставки;
- срок действия предложения.

С уважением,
{{contact_person}}
{{company_name}}
{{contact_phone}}
{{contact_email}}
```

## Алгоритм

1. Возьми шаблон и профиль **из этого файла**; добавь данные заказа и `supplier_name` (спроси, если нет).
2. MCP mail: `list_accounts` → `mail_mutate` / `sendMessage`. Подтверждение при `confirmationRequired`; при `smtp_outcome_unknown` — не слать повторно без проверки.
3. Черновик пользователю до отправки. После — тема, получатель; предложи `check-mailbox-replies`.
