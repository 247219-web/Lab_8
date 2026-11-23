# Огляд API FitTrack

## Призначення
Документ описує умовний REST API майбутньої серверної версії FitTrack. Ці endpoint’и наведені для навчального прикладу й не підключені до HTML-прототипу.

Базова адреса: `https://api.example.com/v1`

Формат обміну даними: JSON.

## 1. Отримати список тренувань

`GET /workouts`

Повертає список тренувань користувача.

**Приклад запиту**
```http
GET /v1/workouts
Accept: application/json
```

**Приклад відповіді — 200 OK**
```json
{
  "workouts": [
    {
      "id": 101,
      "name": "Ранкова пробіжка",
      "type": "cardio",
      "duration": 30,
      "date": "2026-11-23"
    },
    {
      "id": 102,
      "name": "Силове тренування",
      "type": "strength",
      "duration": 45,
      "date": "2026-11-22"
    }
  ],
  "total": 2
}
```

## 2. Додати тренування

`POST /workouts`

Створює новий запис про тренування. Поля `name`, `type` і `duration` є обов’язковими.

**Приклад запиту**
```http
POST /v1/workouts
Content-Type: application/json
```

```json
{
  "name": "Вечірня йога",
  "type": "stretching",
  "duration": 25,
  "date": "2026-11-23"
}
```

**Приклад відповіді — 201 Created**
```json
{
  "id": 103,
  "name": "Вечірня йога",
  "type": "stretching",
  "duration": 25,
  "date": "2026-11-23",
  "message": "Тренування успішно додано"
}
```

## 3. Отримати статистику користувача

`GET /stats`

Повертає загальну статистику активності.

**Приклад запиту**
```http
GET /v1/stats
Accept: application/json
```

**Приклад відповіді — 200 OK**
```json
{
  "totalWorkouts": 12,
  "totalMinutes": 480,
  "weeklyGoal": 300,
  "completedThisWeek": 210
}
```

## Коди відповідей

| Код | Назва | Значення |
|---|---|---|
| 200 | OK | Запит виконано успішно |
| 201 | Created | Новий запис створено |
| 400 | Bad Request | Некоректні або відсутні дані |
| 401 | Unauthorized | Потрібна авторизація |
| 404 | Not Found | Запис не знайдено |
| 500 | Internal Server Error | Внутрішня помилка сервера |

## Примітки
- Тривалість тренування задається у хвилинах.
- Тип активності може мати значення `cardio`, `strength`, `stretching` або `other`.
- У реальній системі сервер повинен перевіряти дані та права доступу.
