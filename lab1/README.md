# Лабораторная работа 1

**Название:** "Разработка драйверов символьных устройств"

**Цель работы:** "Получить знания и навыки разработки драйверов символьных устройств для операционной системы Linux."

## Описание функциональности драйвера

При записи в файл символьного устройства текста типа “5+6” должен запоминаться результат операции, то есть 11 для
данного примера. Должны поддерживаться операции сложения, вычитания, умножения и деления. Последовательность полученных
результатов с момента загрузки модуля ядра должна выводиться при чтении созданного файла /dev/var2 в консоль
пользователя. При чтении из файла символьного устройства в кольцевой буфер ядра должен осуществляться вывод тех же
данных, которые выводятся при чтении файла /dev/var2.

## Инструкция по сборке

Сборка:

`make build`

Сборка и установка:

`make`

Выгрузка модуля:

`make uninstall`

## Инструкция пользователя

Передача строки в драйвер:

`echo "2 + 2" > /dev/var2`

Чтение результата:

`cat /dev/var2`

## Примеры использования

```user@user-VirtualBox:~$ echo "2 + 2" > /dev/var2
user@user-VirtualBox:~$ echo "3 - 4" > /dev/var2
user@user-VirtualBox:~$ echo "5 * 7" > /dev/var2
user@user-VirtualBox:~$ echo "2 / 2" > /dev/var2
user@user-VirtualBox:~$ echo "5 / 0" > /dev/var2
user@user-VirtualBox:~$ cat /dev/var2
ERR: ZeroDivision
Result 4: 1
Result 3: 35
Result 2: -1
Result 1: 4
user@user-VirtualBox:~$ dmesg | tail -n 19
[  594.303149] drv_module: Sum of all correct expressions: 8
[  622.385863] Unloading module
[  622.395960] drv_module: Device /dev/var2 destroyed
[  647.600039] Loading module
[  647.600044] drv_module: Registered with major 240
[  647.600065] drv_module: Registered device class: drv_modules
[  647.602078] drv_module: Registered device: /dev/var2
[  758.778789] drv_module: Result 5: ERR: ZeroDivision
[  758.778793] drv_module: Result 4: 1
[  758.778794] drv_module: Result 3: 35
[  758.778795] drv_module: Result 2: -1
[  758.778795] drv_module: Result 1: 4
[  758.778796] drv_module: Sum of all correct expressions: 39
[  758.778806] drv_module: Result 5: ERR: ZeroDivision
[  758.778807] drv_module: Result 4: 1
[  758.778808] drv_module: Result 3: 35
[  758.778809] drv_module: Result 2: -1
[  758.778809] drv_module: Result 1: 4
[  758.778810] drv_module: Sum of all correct expressions: 39```

