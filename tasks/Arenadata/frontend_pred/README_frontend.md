# Веб-интерфейс для визуализации витрины данных TelecomGuardian

Этот веб-интерфейс предназначен для визуализации витрины данных, создаваемой системой TelecomGuardian. Он позволяет аналитикам безопасности просматривать, анализировать и управлять обнаруженными аномалиями в поведении пользователей телекоммуникационной сети.

## Возможности интерфейса

- **Мониторинг аномалий** — отображение как подтвержденных, так и потенциальных взломанных аккаунтов
- **Интерактивная фильтрация** — фильтрация по типу пользователя, статусу и объему трафика
- **Детальный анализ** — просмотр подробной информации о каждой аномалии с визуализацией поведения
- **Рабочие процессы безопасности** — возможность подтверждения или отклонения потенциальных аномалий
- **Динамика обнаружения** — график изменения количества аномалий во времени

## Структура проекта

```
├── dashboard.html           # Основная HTML-страница
├── styles.css               # Стили для интерфейса
├── script.js                # JavaScript-логика
├── shield-icon.svg          # SVG-иконка для логотипа
└── server.py                # Серверный скрипт для обслуживания интерфейса и данных
```

## Запуск интерфейса

### Предварительные требования

- Python 3.8 или выше
- Flask
- pandas

### Установка зависимостей

```bash
pip install flask pandas
```

### Запуск сервера

```bash
python server.py
```

После запуска сервера интерфейс будет доступен по адресу: http://localhost:5000

## Работа с интерфейсом

### Основные элементы интерфейса

1. **Сводка по аномалиям** — общее количество обнаруженных аномалий, разделенных на подтвержденные и потенциальные
2. **Фильтры** — настройки для отображения только нужных аномалий
3. **График динамики** — отображение изменения количества аномалий во времени
4. **Таблица аномалий** — детальная информация об обнаруженных аномалиях с возможностью сортировки и поиска
5. **Модальное окно деталей** — подробная информация о выбранной аномалии с визуализацией поведения

### Процесс анализа аномалий

1. **Просмотр списка аномалий**
   - В таблице отображаются все обнаруженные аномалии
   - Используйте фильтры и поиск для быстрого нахождения нужных записей
   - Сортируйте по времени обнаружения или объему трафика

2. **Исследование подозрительной активности**
   - Нажмите кнопку "Детали" для просмотра подробной информации
   - Изучите график поведения, показывающий отклонение от нормы
   - Оцените характеристики сессии (объем трафика, тип пользователя и т.д.)

3. **Принятие решения**
   - Для потенциальных аномалий доступны кнопки:
     - "Подтвердить" — подтверждение взлома аккаунта
     - "Отклонить" — отметка аномалии как ложное срабатывание
     - "Дополнительное расследование" — запуск дополнительных проверок

4. **Мониторинг общей ситуации**
   - График показывает динамику обнаружения аномалий
   - Сводка отображает текущее количество подтвержденных и потенциальных аномалий

## Расширение функциональности

### Интеграция с API

Интерфейс использует Flask-бэкенд, который предоставляет следующие API-эндпоинты:

- **GET /api/confirmed-anomalies** — получение списка подтвержденных аномалий
- **GET /api/potential-anomalies** — получение списка потенциальных аномалий
- **GET /api/showcases** — получение всех витрин данных
- **POST /api/confirm/{uid}** — подтверждение аномалии с указанным UID
- **POST /api/reject/{uid}** — отклонение аномалии с указанным UID

### Настройка для работы с живыми данными

Для интеграции с реальной системой TelecomGuardian необходимо:

1. Убедиться, что скрипт `showcase.py` сохраняет результаты в правильных форматах и расположениях:
   - `probably_hacked.csv` — потенциальные аномалии
   - `already_hacked.csv` — подтвержденные аномалии
   - `clients_shocases_per_time/anomaliesN.csv` — витрины данных

2. Модифицировать функцию `enrich_anomaly_data()` в `server.py` для использования фактических путей и структуры данных

3. При необходимости обновить клиентскую часть для корректного отображения всех доступных полей данных

## Рекомендации по использованию

- Регулярно обновляйте данные с помощью кнопки "Обновить данные"
- Используйте фильтры для сосредоточения на определенных типах аномалий
- Анализируйте динамику обнаружения для выявления всплесков активности
- Всегда проверяйте детали аномалии перед принятием решения
- Помните, что система может давать ложноположительные срабатывания, особенно для легитимных изменений в поведении пользователей 