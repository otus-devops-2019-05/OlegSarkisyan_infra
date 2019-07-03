# ДЗ №3 - Знакомство с облачной инфраструктурой. Google Cloud Platform
В ходе дз выполнено:

# 1) Настройка ssh-forwarding для сквозного подключения к ВМ (в одну строку)
а) ssh -J 34.77.88.197 10.132.0.3 - proxy jump 
б) eval $(ssh-agent -s) ssh-add ~/.ssh/osarkisyan && ssh -A -t 34.77.88.197 ssh 10.132.0.3

# 2) Настройка ssh-forwarding для сквозного подключения к ВМ (с помощью alias, с помощью конфига)
а) alias someinternalhost="ssh - J 34.77.88.197 10.132.0.3" вызов someinternalhost 
б) конфиг 

Host bastion 
Hostname 34.77.88.197 
User osarkisyan 
Port 22

Host someinternalhost 
Hostname 10.132.0.3 
User osarkisyan 
Port 22 
ProxyCommand ssh bastion -W %h:%p 
Вызов ssh someinternalhost 

Трудности - не было прав на созданный конфиг:) 
Решено: 
chown $USER ~/.ssh/config 
chmod 644 ~/.ssh/config

# Данные серверов GCP
bastion_IP = 34.77.88.197
someinternalhost_IP = 10.156.0.3
bastion2_IP = 35.228.208.254

Проблема с установкой setupvpn.sh на сервер bastion. 
Решено: разворачиванием идентичного сервера bastion2 (35.228.208.254)

Pritunl установлен и настроен согласно инструкции файл cloud-bastion.ovpn добавлен в репозиторий.

Также в репозиторий добавлен файл setupvpn.sh. Все действия согласно задания внесены в ReadMe.
