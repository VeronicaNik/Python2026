# Задание по ООП: Система уведомлений

## Тема
**Система уведомлений**: email и SMS.

## Цель
Отработать:
- **наследование**
- **абстрактный класс** (`abc.ABC`, `@abstractmethod`)
- вызов родительской логики через **`super()`**

---

## Требования к заданию

### 1) Абстрактный класс
Создай абстрактный класс `NotificationChannel`, который:
- хранит `sender_name` (например, `"MyService"`)
- имеет абстрактный метод `send(recipient: str, message: str) -> None`
- имеет обычный метод `format_message(message: str) -> str`, который возвращает строку в формате:  
  `"[{sender_name}] {message}"`

### 2) Наследники
Создай два класса-наследника:

#### `EmailChannel(NotificationChannel)`
- в `__init__` принимает `sender_name` и `sender_email`
- переопредели `send(...)` так, чтобы:
  - сначала получал отформатированный текст через `super().format_message(message)`
  - затем печатал в консоль "отправку email" (достаточно `print`), например:  
    `EMAIL to <recipient>: <formatted_message> (from <sender_email>)`

#### `SMSChannel(NotificationChannel)`
- в `__init__` принимает `sender_name` и `sender_phone`
- переопредели `send(...)` аналогично:
  - используй `super().format_message(message)`
  - печатай "отправку SMS", например:  
    `SMS to <recipient>: <formatted_message> (from <sender_phone>)`

### 3) Сервис, который использует полиморфизм
Создай класс `NotificationService`, который:
- принимает список каналов `channels: list[NotificationChannel]`
- имеет метод `notify_all(recipient: str, message: str)`, который вызывает `send(...)` у каждого канала

### 4) Демонстрация работы
В конце файла:
- создай `EmailChannel` и `SMSChannel`
- положи их в `NotificationService`
- вызови `notify_all(...)` минимум 2 раза с разными сообщениями

---

## Критерии готовности
- **Нельзя** создавать экземпляр `NotificationChannel` напрямую.
- В `send(...)` у наследников **обязательно** используется **`super()`**.
- `NotificationService` работает с типом **`NotificationChannel`**, а не с конкретными классами.

---

## Формат сдачи
- Создайте один Python файл с решением
- Название файла: `notifications.py`
- Убедитесь, что код запускается без ошибок
- Прикрепите файл к ответу в чате или загрузите в репозиторий
