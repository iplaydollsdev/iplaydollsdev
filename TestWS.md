## Примерное оформление запросов/ответов

### Подключение (Условно)

Client -> Server
```
{
  "type": "connect"
}
```
### Запрос залов

Server -> Client
```
{
  "method": "GetHalls",
  "id": "Guid_1"
}
```
Client -> Server
```
{
  "result": [
    {
      "name": "Бар",
      "guid": "HallGuid_1"
    },
    {
      "name": "Зал",
      "guid": "HallGuid_2"
    }
  ],
  "id": "Guid_1"
}
```

### Запрос столов

Server -> Client
```
{
  "method": "GetTables",
  "id": "Guid_2"
}
```
Client -> Server
```
{
  "result": [
    {
      "guid": "TableGuid_1",
      "name": "1",
      "hallGuid": "HallGuid_1"
    },
    {
      "guid": "TableGuid_2",
      "name": "2",
      "hallGuid": "HallGuid_1"
    },
    {
      "guid": "TableGuid_3",
      "name": "3",
      "hallGuid": "HallGuid_2"
    }
  ],
  "id": "Guid_2"
}
```

### Запрос занятых столов

Server -> Client
```
{
  "method": "GetActiveTables",
  "id": "Guid_3"
}
```
Client -> Server
```
{
  "result": [
    {
      "guid": "TableGuid_1",
      "status": "busy",
      "openTime": "27-11-2023 15:03",
      "orderNumber": "13"
    }
  ],
  "id": "Guid_3"
}
```

### Запрос всех броней после даты входа

Server -> Client
```
{
  "method": "GetAllReservesAfter",
  "id": "Guid_4",
  "data": { "DateFrom": "27-11-2023 16:00" }
}
```
Client -> Server

На каждую имеющуюся бронь отправляется запрос на изменение
```
{
  "type": "update_reservation",
  "data": {
    "guid": "ReserveGuid_1",
    "start_date": "2023-11-27 17:00",
    "end_date": "2023-11-27 18:00",
    "guest": {
      "guid": "GuestGuid",
      "name": " Тестович",
      "phone": "79008000000",
      "email": "",
      "birthday": ""
    },
    "guestCount": "2",
    "status": "cancel",
    "comment": "",
    "tablesGUIDs": [ "TableGuid_1" ]
  },
  "id": "Guid_4"
}
```
### Изменение статуса стола

У нас пока не видел статусов конкретно на стол, только бронирование.

Оно нужно, чтобы без брони можно было изменить статус стола, на случай, если в заведение пришли, заняли столик, не бронируя.

Не знаю планируется ли оно, но пока тоже приложу свой вариант

```
{
  "type": "update_table_status",
  "data": {
    "guid": "TableGuid_1",
    "status": "busy/free",
    "open_time": "2023-11-27 18:00"
  }
}
```


