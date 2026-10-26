---
id: cp-request
name: Запрос коммерческого предложения (RU)
description: Письмо поставщику с просьбой сформировать КП по номенклатурной позиции
variables:
  - supplier_name
  - nomenclature
  - quantity
  - unit
  - reference_unit_price
  - currency
  - delivery_terms
  - company_name
  - contact_person
  - contact_phone
  - contact_email
---
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
