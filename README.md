# YDNS

Скрипт добавления/обновления DNS записей сервиса pdd.yandex.ru
==============================================================

![](https://raw.githubusercontent.com/alive-corpse/ydns/master/screen.png)

### Возможности:
* обновление dns записи, в случае её отсутствия - создание записи
* работа на OpenWRT и подобных прошивках, для OpenWRT необходима установка пакетов ca-bundle и curl
* передача параметров в командной строке, либо прописывание в самом скрипте
* обновление сразу нескольких записей для одного домена
* передача в качестве параметра либо IP адреса, либо имени интерфейса

##### Примечание: скрипт изначально рассчитан на работу только с записями A-типа.

### Установка:
```bash
wget https://raw.githubusercontent.com/alive-corpse/ydns/master/ydns
chmod +x ydns
```

### Использование:

Для использования необходим токен. Его можно получить здесь: https://pddimp.yandex.ru/api2/registrar/get_token

##### Передача параметров в командной строке
```
./ydns <subdomain>.<domain.name> <token> <iface|ip> [ttl]
```
Примеры:
```bash
# vailiy.pupkin.ru - доменное имя с сабдоменом
# THIS0IS0MY0TOKEN - токен, полученный на https://pddimp.yandex.ru/api2/registrar/get_token
# wan0 - имя интерфейса, можно указать вместо IP адреса
./ydns vasiliy.pupkin.ru THIS0IS0MY0TOKEN wan0
```
```bash
# в случае обновления нескольких записей, сабдомены можно указать через запятую (без пробелов), в том числе можно указывать символы '*' и '@' для обновления соответствующих записей, в этом случае первый параметр нужно заключить в одиночные кавычки
./ydns 'vasiliy,*,ivan,sergey.pupkin.ru' THIS0IS0MY0TOKEN 123.234.123.234 2600
```

##### Внесение параметров в скрипт
Можно добавить все параметры в скрипт. Найдите и измените в скрипте следующую часть:
```bash
record='' # For example: test.yourdomain.xx
token='' # You can get token at  https://pddimp.yandex.ru/api2/registrar/get_token
cont='' # IP address
ttl='' # Time to live
defttl='1440' # Default ttl for new records
```
После этого скрипт можно запускать без параметров.

### Логирование

Есть три уровня логирования: debug/info/warning, по умолчанию стоит уровень info. Для изменения найдите и замените значение в строке:
```bash
LOGLEVEL='info'
```
По умолчанию текущая дата и время, формат и содержимое в строке:
```bash
LPREF='date +%Y.%m.%d-%H:%M:%S'
```
Ширина разделителя при отсутствии tput:
```bash
DEFAULT_COLS=70
```
Включение/отключение цвета в выводе:
```bash
LCOLOR=1
```
