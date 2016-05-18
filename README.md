# uais_bu_data_storage - Хранилище данных

----
### API справочников

* `GET /api/v1/zones` - Получить список всех зон
* `GET /api/v1/zones/:id/nodes` - Получить список всех нод указанной зоны
* `POST /api/v1/zones/:id/nodes` - Добавить ноду в указанную зону
    * _`{"name":"Нода 2"}`_
* `GET /api/v1/nodes` - Получить список всех нод
* `GET /api/v1/nodes/:id` - Получить ноду по id
* `PUT /api/v1/nodes/:id` - Обновить ноду по id
    * _`{"name":"Нода 2"}`_
* `DELETE /api/v1/nodes/:id` - Удалить ноду по id

### API истории изменений архитектуры
* `POST /api/v1/history` - Добавить запись в историю
    * _`{"date":"20160328","zone":"Рабочая зона","node":"Нода 1","server":"is19-p-app-09"}`_
* `GET /api/v1/history/:date` - Получить исторические данные за указанную дату

### API серверов

* `GET /api/v1/servers` - Получить список всех серверов, а также поиск (все параметры опциональные)
    * _`{
                "name": "server_name",
                "alias": "server_alias",
                "zone": "zone_id" | "zone_name" - [необязательный, ищется зона сначала по идентификатору, потом по имени, если не найдена, то создаётся],
                "node": "node_id" | "node_name" - [необязательный, ищется нода сначала по идентификатору, потом по имени (с привязкой к зоне), если не найдена, то создаётся]
            }`_
* `PUT /api/v1/servers` - Добавить сервер
    * _`{"name":"Тест!","alias":"Тест!","zone":14,"node":86}`_
* `GET /api/v1/servers/:id` - Получить сервер по id
* `PUT /api/v1/servers/:id` - Обновить сервер по id
    * _`{"name":"Тест!","alias":"Тест!","zone_id":14,"node_id":86}`_
* `DELETE /api/v1/servers/:id` - Удалить сервер по id

### API серверов СУБД

* `GET /api/v1/dbms-servers` - Получить список всех серверов СУБД
* `POST /api/v1/dbms-servers` - Добавить сервер СУБД
    * _`{"instance_name": "IS19-D-DB-21", "port": 1433, "user": "sa", "password": "Qwe`123", "server_id": 999}`_
* `GET /api/v1/dbms-servers/:id` - Получить сервер СУБД по id
* `PUT /api/v1/dbms-servers/:id` - Обновить сервер СУБД по id
    * _`{"instance_name": "IS19-D-DB-21", "port": 1433, "user": "sa", "password": "Qwe`123", "server_id": 999}`_
* `DELETE /api/v1/dbms-servers/:id` - Удалить сервер СУБД по id

### API баз данных

* `GET /api/v1/databases` - Получить список всех баз данных
* `POST /api/v1/databases` - Добавить базу данных
    * _`{"name": "SM", "recovery_model": "F", "dbms_server_id": 1}`_
* `PUT /api/v1/databases` - Добавить/обновить базу данных (идентификация по имени базы данных и имени существующего сервера СУБД)
    * _`{"name": "SM", "recovery_model": "F", "dbms_server": "IS19-P-DB-11"}`_
* `GET /api/v1/databases/:id` - Получить базу данных по id
* `PUT /api/v1/databases/:id` - Обновить базу данных по id
    * _`{"name": "SM", "recovery_model": "F", "dbms_server_id": 1}`_
* `DELETE /api/v1/databases/:id` - Удалить базу данных по id
* `PUT /api/v1/database-sizes` - Добавить информацию о размере файла базы данных
    * _`{"date": "20160503", "database_name":" SM", "file_name": "SM_log", "file_type": "L", "file_size": "60280602624"}`_
* `GET /api/v1/database-sizes/:date` - Получить данные размеров файлов баз данных за указанную дату
* `GET /api/v1/databases/table/:date` - Отчет по базам данных УАИС БУ за указанную дату (дата указывается в формате yyyy-MM-dd)

### API архивов баз данных
* `PUT /api/v1/backups/last` - Обновить данные по последнему архиву базы данных
    * _`{"database_id":"Идентификатор базы данных", "file_name":"Имя файла архивной копии", "backup_date":"Дата создания архива", "backup_type":"Тип архива - D, I или L", "backup_size": "Размер архива в байтах"}`_
* `GET /api/v1/backups/last` - Получить список всех последних архивов баз данных
