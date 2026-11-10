# Контракт API — команда 4

GET https://domrf-ai-training-2026.github.io/team-4-dashboard/data.json

Все данные вымышлены. Публичный read-only JSON, без ключа. CORS не требуется между проектами одной организации, поскольку их origin одинаков: https://domrf-ai-training-2026.github.io. Для форков на другом origin проверьте CORS в браузере. Не используйте режим no-cors: он не даёт читать JSON.

## Общий формат

schema_version: строка 1.0; team_id: число 4; synthetic: true; updated_at: ISO UTC; units: единицы; records: массив записей. Ключ строки: period + office_id.

- period — Неделя до
- office_id — Код офиса
- office — Офис
- city — Город
- staff — Менеджеры (чел.)
- commission_mln — Комиссии, млн ₽ (млн RUB)
- marketing_mln — Маркетинг, млн ₽ (млн RUB)
- payroll_mln — ФОТ, млн ₽ (млн RUB)
- rent_mln — Аренда, млн ₽ (млн RUB)

Условный результат = комиссии − маркетинг − ФОТ − аренда. Это не прибыль банка: процентные доходы и прочие расходы не заданы. Штат — снимок на конец недели; по неделям не суммировать.

## Пример чтения

```js
const response = await fetch(API_URL, {cache: 'no-store'});
if (!response.ok) throw new Error('HTTP ' + response.status);
const payload = await response.json();
if (payload.schema_version !== '1.0' || !Array.isArray(payload.records))
  throw new Error('Неверный формат API');
```

Держите видимыми источник, updated_at и время успешного чтения. При ошибке не подменяйте результат нулями и не оставляйте старые цифры без отметки. Публикация коммита и распространение кэша Pages занимают время; проверяйте успешный deploy и updated_at.

## Принимаемый источник

Команда 5: https://domrf-ai-training-2026.github.io/team-5-dashboard/data.json

Покажите число просроченных поручений из API команды 5 рядом с затратами офиса.
