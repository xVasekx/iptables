# iptables
Написал сценарии iptables

1. Реализовал knocking port
   - centralRouter может попасть на ssh inetrRouter через knock скрипт.
2. Добавил inetRouter2, который виден(маршрутизируется (host-only тип сети для виртуалки)) с хоста.
3. Запустил nginx на centralServer.
4. Пробросил 80й порт на inetRouter2 8080.
   - дефолт в инет оставил через inetRouter.
