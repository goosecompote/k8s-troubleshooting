### Задание. 
При деплое приложение web-consumer не может подключиться к auth-db. Необходимо это исправить
1.Установить приложение по команде:

kubectl apply -f https://raw.githubusercontent.com/netology-code/kuber-homeworks/main/3.5/files/task.yaml

2.Выявить проблему и описать.

3.Исправить проблему, описать, что сделано.

4.Продемонстрировать, что проблема решена.

### Ответ.
Проблема:

Приложение web-consumer не может подключиться к сервису auth-db

Причина:

Сервис auth-db развернут в namespace data, а приложение web-consumer находится в namespace web
Обращение к сервису выполняется по имени auth-db без указания namespace
В Kubernetes поиск сервисов по короткому имени происходит только внутри текущего namespace
В результате web-consumer не находит сервис auth-db

Решение:

Необходимо указать namespace сервиса в DNS имени

Было.
while true; do curl auth-db; sleep 5; done

Стало.
while true; do curl auth-db.data; sleep 5; done

Либо можно использовать полное DNS имя
auth-db.data.svc.cluster.local

Результат.
После исправления web-consumer успешно подключается к auth-db
В логах приложения появляется ответ от nginx, что подтверждает работоспособность соединения

Вывод.
Проблема вызвана обращением к сервису без учета namespace
Исправление DNS имени решает проблему подключения