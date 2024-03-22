# Дано два csv-файла с данными о клиентах и их транзакциях
## Загрузить csv-файлы на HDFS 
## Приложить к отчету скрин команды hdfs dfs -ls
![hdfs_ls_transaction](https://github.com/easykvasha/de_sber/assets/61687166/db427933-e477-40b9-b310-7768dee1bbad)
![hdfs_ls_customer](https://github.com/easykvasha/de_sber/assets/61687166/8393eac6-bc29-4104-a732-4c28a7124f48)


## Создать над csv-файлами по 2 таблицы (managed и external). 
## Приложить к отчету скрин вывода команды describe formatted
![customer_managed](https://github.com/easykvasha/de_sber/assets/61687166/4c9512ee-a22f-487f-8d58-25396cf298a3)
![customer_external](https://github.com/easykvasha/de_sber/assets/61687166/7861d03b-cfa2-4fed-bf5c-70ab1bf9cf52)

![transaction_managed](https://github.com/easykvasha/de_sber/assets/61687166/d3d3928f-941c-4f3a-96a6-f36f7e27d8cc)
![transaction_external](https://github.com/easykvasha/de_sber/assets/61687166/ea0a3a6b-0102-49b1-bc8a-12d0e6f25fc6)

## Создать еще две таблицы с форматом хранения данных parquet и загрузить данные из пункта 2. 
## Приложить к отчету скрин вывода команды describe formatted
![customer_parquet](https://github.com/easykvasha/de_sber/assets/61687166/7207260c-3c03-43ec-bc64-4a2957c7b79a)
![transaction_parquet](https://github.com/easykvasha/de_sber/assets/61687166/827d7a61-dbff-4a52-b2b0-0eb4de5f6111)

## Создать еще одну таблицу с транзакциями, партицированную по полю transaction_date (предварительно привести дату к виду YYYY-MM-DD)
## Приложить к отчету скрин вывода команды describe formatted
![transaction_partition](https://github.com/easykvasha/de_sber/assets/61687166/403fd169-cc21-42f9-920c-27312cc5051f)

## Выполнить запросы с таблицами из пункта 2-4 и посмотреть на время выполнение
## Приложить к отчету скрин вывода запросов со временем выполнения

### 1) Вывести количество подтвержденных транзакций по каждому клиенту.
![transaction_managed_1](https://github.com/easykvasha/de_sber/assets/61687166/b18cc264-18ca-4fec-9a0d-c708683a9704)
![transaction__external_1](https://github.com/easykvasha/de_sber/assets/61687166/3eaa155b-d133-46e5-9e56-3f2a6eac43cc)
![transaction_parquet_1](https://github.com/easykvasha/de_sber/assets/61687166/16da1e14-16b7-4c4f-b4cc-6ac42725df31)

### 2) Вывести распределение транзакций по месяцам и сферам деятельности.
![transaction__external_2](https://github.com/easykvasha/de_sber/assets/61687166/e3382ebc-5bb1-494e-a694-7f94bf681efc)
![transaction_managed_2](https://github.com/easykvasha/de_sber/assets/61687166/e2ebaa04-ce20-48f4-b703-b106e5a4265a)
![transaction_parquet_2](https://github.com/easykvasha/de_sber/assets/61687166/929327ca-c4bb-4f3e-ba16-275bbdb06e87)

### 3) Вывести ФИО клиентов, у которых нет транзакций.
![transaction__external_3](https://github.com/easykvasha/de_sber/assets/61687166/1cae7363-a9bc-4d31-9881-30c6b293570f)
![transaction_managed_3](https://github.com/easykvasha/de_sber/assets/61687166/0876a3ce-bc0a-45eb-ae24-6a52de46c781)
![transaction_parquet_3](https://github.com/easykvasha/de_sber/assets/61687166/990be0b0-32be-49fe-bb27-508a4fc8f821)

### 4) Найти ФИО  клиентов с минимальной/максимальной суммой транзакций (sum(list_price)) за весь период (сумма транзакций не может быть null).
![transaction_parquet_4](https://github.com/easykvasha/de_sber/assets/61687166/8d9fc0b6-0354-4e15-894d-b3a98df9fd06)
![transaction__external_4](https://github.com/easykvasha/de_sber/assets/61687166/592cd15f-df1e-4bd6-b307-b0219b8f7060)
![transaction_managed_4](https://github.com/easykvasha/de_sber/assets/61687166/ec6c58b8-d978-409d-af22-81537d4165ce)

### 5) Вывести ФИО клиентов, между соседними транзакциями которых был максимальный интервал (интервал вычисляется в днях)
![transaction_managed_5](https://github.com/easykvasha/de_sber/assets/61687166/7e26364e-9b2e-46f7-81f1-c5fe9ef25940)
![transaction_parquet_5](https://github.com/easykvasha/de_sber/assets/61687166/c926de93-94b4-40e2-9dae-e36bc2aeedcc)
![transaction__external_5](https://github.com/easykvasha/de_sber/assets/61687166/1549ab1f-e6fc-49b9-aaae-342b943a9b69)

## Написать отчет, где описать с какими форматами хранения данных быстрее работает hive, и как влияют на производительность партиции и тип таблицы (managed и external).
### В ходе выполнения запросов было выяснено, что Hive работает быстрее с форматом хранения данных Parquet, чем с CSV. Это связано с тем, что Parquet является колоночным форматом хранения, в то время как CSV - строчным. Колоночный формат хранения позволяет эффективнее читать и обрабатывать только те данные, которые необходимы для выполнения запроса, в то время как строчный формат хранения требует чтения всей строки, даже если необходимо обработать только одну колонку.

### Партицирование таблиц также улучшает производительность запросов, так как позволяет разбить таблицу на более мелкие части, которые могут быть обработаны параллельно. В нашем случае, партицирование таблицы транзакций по полю transaction_date позволило значительно ускорить выполнение запроса по распределению транзакций по месяцам и сферам деятельности.

### Также стоит отметить, что внешние таблицы (external) имеют преимущество перед управляемыми таблицами (managed) в том, что при удалении внешней таблицы данные не удаляются из HDFS, а только ссылка на них. Это позволяет избежать потери данных при необходимости удаления таблицы.

### В целом, для оптимизации производительности Hive рекомендуется использовать формат хранения данных Parquet, партицировать таблицы по наиболее часто используемым полям и использовать внешние таблицы для хранения данных.
