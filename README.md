# Выполнено ДЗ №8 - Практика Infrastructure as a Code (IaC).

##  Основное ДЗ
Создали ветку ansible-1
установили pip и ansible
Создали и несколько раз модифицировали файлы inventory, ansible.cfg, inventory.yml
Поупражнялись в подключении и выполнении на хостах app и db
Использовали разные модули для выполнения схожих запросов
Клонировали репозиторий git
Написали простой playbook


# Выполнено ДЗ №7 - Практика Infrastructure as a Code (IaC).

##  Основное ДЗ
Созддали новую ветку terraform2
Определили правила Firewall
Импортировали существующую структуру в Terraform
Создали план с двумя ВМ
Разбили конфигурацию по файлам
Внедрили Модули
Переиспользовали внедрённые модули
Выполнили требуемые самостоятельные задания

# Выполнено ДЗ №6 - Практика Infrastructure as a Code (IaC).

##  Основное ДЗ
Установили terraform
Создали шаблон main.tf c секциями reosurse и provisioners
Добавили скрипты для провижининга
Определили input переменную для приватного ключа,
использующегося в определении подключения для
провижинеров (connection)
Определили input переменную для задания зоны в ресурсе
"google_compute_instance" "app". 
Отформатировали все конфигурационные файлы используя
команду terraform fmt
Запушили ветку terraform1

# Выполнено ДЗ №5 - Модели управления инфраструктурой.

##  Основное ДЗ
Установили packer
Установили ADC
Создали шаблон Ubuntu16.json c секциями builders и provisioners
Добавили скрипты для провижининга
Задеплоили и запусили приложение, проверили результаты работы
Добавили параметры variables.json 
Запушили ветку packer-base


# Выполнено ДЗ №4 - Основные сервисы Google Cloud Platform (GCP).

##  Основное ДЗ - реализован набор из трёх скриптов

## Задание со * - реализован запуск с помощью одного startup скрипта, настройка правила брендмауэра через gcloud

В процессе сделано:
Установили gcloud
Создали VM
Установили ruby, mongodb, запустили сервер, проверили работу
Написали три скрипт:
install_ruby.sh
install_mongodb.sh
deploy.sh
написали один скрипт:
startup_install.sh
строка для создания правила firewall:
gcloud compute firewall-rules create default-puma-server --source-ranges="0.0.0.0/0" --allow=tcp:9292 --target-tags=puma-server

## Как запустить проект:
testapp_IP = 35.187.165.179
testapp_port = 9292

## Как проверить работоспособность:
Перейти по ссылке http://35.187.165.179:9292/


# ДЗ №3 - Знакомство с облачной инфраструктурой. Google Cloud Platform
В ходе дз выполнено:

## 1) Настройка ssh-forwarding для сквозного подключения к ВМ (в одну строку)
а) ssh -J 34.77.88.197 10.132.0.3 - proxy jump 
б) eval $(ssh-agent -s) ssh-add ~/.ssh/osarkisyan && ssh -A -t 34.77.88.197 ssh 10.132.0.3

## 2) Настройка ssh-forwarding для сквозного подключения к ВМ (с помощью alias, с помощью конфига)
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

## Данные серверов GCP
bastion_IP = 35.228.208.254
someinternalhost_IP = 10.132.0.3
bastion2_IP = 34.77.88.197

Проблема с установкой setupvpn.sh на сервер bastion. 
Решено: разворачиванием идентичного сервера bastion2 (35.228.208.254)

Pritunl установлен и настроен согласно инструкции файл cloud-bastion.ovpn добавлен в репозиторий.

Также в репозиторий добавлен файл setupvpn.sh. Все действия согласно задания внесены в ReadMe.
