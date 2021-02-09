# Установка и базовая настройка MQTT брокера Eclipse Mosquitto на Ubuntu | Debian | Kali Linux

> **Eclipse Mosquitto** - это брокер сообщений с открытым исходным кодом, который реализует протокол MQTT. Mosquitto легок и подходит для использования на всех устройствах, от одноплатных компьютеров с низким энергопотреблением до полноценных серверов.... Варианты установки на разные операционные системы кратко описаны на официальном сайте: https://mosquitto.org/download/

**_Ниже представлена моя "Шпаргалка" (CheatSheet)_ ;-)**

##### Примечание для "Чайников": 
Для выполнения некоторых команд в терминале могут понадобятся права администратора. Для этого просто наберите перед командой **sudo**:

`sudo <команда>`

##### Для обновления вашей системы (обновление пакетов), выполните:

`apt-get update && apt-get upgrade -y`

##### Устанавливаем  MQTT брокера и клиента Mosquitto:

`apt install mosquitto mosquitto-clients -y`

##### Настроим для Mosquitto подписку по логину и паролю (пример для логина "huny").

`mosquitto_passwd -c /etc/mosquitto/passwd huny`

##### Далее, по запросу, нужно будет ввести два раза ваш пароль для Mosquitto. 

##### Связка логин-пароль будет храниться по следующему пути - /etc/mosquitto/passwd
##### Откроем файл, что бы убедиться, что пароль создан:

`nano /etc/mosquitto/passwd`

##### Закроем файл, нажав CTRL + X

##### Запретим анонимные подключения к Mosquitto. Открываем файл default.conf:

`nano /etc/mosquitto/conf.d/default.conf`

##### Файл должен быть пустой, вставляем туда этот текст:

`allow_anonymous false`

`password_file /etc/mosquitto/passwd`

##### Сохраняем и закрываем файл, нажав CTRL + X, Y, а затем ENTER.

##### Перезагружаем Mosquitto чтобы применить изменения:

`systemctl restart mosquitto`

##### На этом этапе  MQTT брокер Mosquitto  у нас успешно запущен и защищён паролем.

## UPD1: Добавление / удаление пользователей в MQTT брокер (Mosquitto)

##### Для примера добавим пользователя с логином huny2 и паролем parol2:

`mosquitto_passwd -b /etc/mosquitto/passwd huny2 parol2`

##### Проверяем что добавился, открыв файл паролей.

`nano /etc/mosquitto/passwd`

##### Закрываем файл, нажав CTRL + X

##### Перезагружаем Mosquitto чтобы применить изменения:

`systemctl restart mosquitto`

##### Удалить пользователя huny2:

`mosquitto_passwd -D /etc/mosquitto/passwd huny2`

##### Проверяем, что действвительно удалён, открыв файл паролей:

`nano /etc/mosquitto/passwd`

##### Закрываем файл, нажав CTRL + X

##### Перезагружаем Mosquitto чтобы применить изменения:

`systemctl restart mosquitto`

### UPD2: Изменим порт MQTT брокера Mosquitto c 1883 на 8883 (пример), а 1883 привяжем к localhost (недоступен извне).

##### Открываем файл default.conf:

`nano /etc/mosquitto/conf.d/default.conf`

##### Добавляем туда следующее:

`listener 1883 localhost`

`listener 8883`

##### Сохраняем и закрываем файл, нажав CTRL + X, Y, а затем ENTER.

##### Перезагружаем Mosquitto чтобы применить изменения:

`systemctl restart mosquitto`

### UPD3: Управление состоянием Mosquitto:

##### Посмотреть текущий статус:

`systemctl status mosquitto`

`systemctl status mosquitto.service`

##### Изменение статуса текущего сеанса:

`systemctl start mosquitto`

`systemctl stop mosquitto`

`systemctl start mosquitto.service`

`systemctl stop mosquitto.service`

##### Для изменения состояния при запуске (не влияет на текущее состояние):

`systemctl enable mosquitto`

`systemctl disable mosquitto`

`systemctl enable mosquitto.service`

`systemctl disable mosquitto.service`

[Бесплатный и Личный MQTT брокер (Mosquitto) для  IoT-устройств. На базе Ubuntu 20.04 на Always Free VPS сервер от Oracle](https://pikabu.ru/story/besplatnyiy_i_lichnyiy_mqtt_broker_mosquitto_dlya_iotustroystv_na_bazeubuntu_2004_na_always_free_vps_serverot_oracle_7982336)
