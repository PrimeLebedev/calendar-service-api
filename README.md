# calendar-service-api
## Запуск приложения

```
./venv/bin/flask --app ./calendar-service/server.py run
или
python server.py
```


## cURL тестирование

### Добавление нового события
```
curl http://127.0.0.1:5000/api/v1/calendar/ -X POST -d "2024-06-12|title|text"
```

### Получение всего списка событий
```
curl http://127.0.0.1:5000/api/v1/calendar/
```

### Получение события по идентификатору / ID == 1
```
curl http://127.0.0.1:5000/api/v1/calendar/1/
```

### Обновление текста события по идентификатору / ID == 1 /  новый текст == "new text"
```
curl http://127.0.0.1:5000/api/v1/calendar/1/ -X PUT -d "2024-6-24|title|new text"
```

### Удаление события по идентификатору / ID == 1
```
curl http://127.0.0.1:5000/api/v1/calendar/1/ -X DELETE
```


## Пример исполнения команд с выводом

```
$ curl http://127.0.0.1:5000/api/v1/calendar/ -X POST -d "2024-6-24|title|text"
new id: 1

$ curl http://127.0.0.1:5000/api/v1/calendar/ -X POST -d "2024-6-24|title|text"
failed CREATE operation with: The event has already been added on
the 2024-06-24 date in storage

$ curl http://127.0.0.1:5000/api/v1/calendar/
1|2024-6-24|title|text

$ curl http://127.0.0.1:5000/api/v1/calendar/1/
1|2024-6-24|title|text

$ curl http://127.0.0.1:5000/api/v1/calendar/1/ -X PUT -d "2024-6-24|title|new text"
updated

$ curl http://127.0.0.1:5000/api/v1/calendar/1/
1|2024-6-24|title|new text

$ curl http://127.0.0.1:5000/api/v1/calendar/1/ -X PUT -d "2024-6-24|title|loooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooong text"
failed to UPDATE with: text lenght > MAX: 200

$ curl http://127.0.0.1:5000/api/v1/calendar/1/ -X PUT -d "2024-6-24|loooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooong title|text"
failed to UPDATE with: title lenght > MAX: 30

$ curl http://127.0.0.1:5000/api/v1/calendar/1/ -X DELETE
deleted

$ curl http://127.0.0.1:5000/api/v1/calendar/
-- пусто --
```