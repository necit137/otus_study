# Лабораторная работа №2. Просмотр таблицы MAC-адресов коммутатора 
### Задача:
1. Создание и настройка сети
2. Изучение таблицы МАС-адресов коммутатора

### Решение:
1. [Создание и настройка сети](https://github.com/necit137/otus_study/edit/main/lab%2002/README.md#часть-1-создание-и-настройка-сети)
    - [Шаг 1. Подключаем сеть в соответствии с топологией](https://github.com/necit137/otus_study/edit/main/lab%2002/README.md#шаг-1-подключаем-сеть-в-соответствии-с-топологией)
    - [Шаг 2. Настраиваем узлы ПК](https://github.com/necit137/otus_study/edit/main/lab%2002/README.md#шаг-2-настраиваем-узлы-пк)
    - [Шаг 3. Выполняем инициализацию и перезагрузку коммутаторов](https://github.com/necit137/otus_study/edit/main/lab%2002/README.md#шаг-3-выполните-инициализацию-и-перезагрузку-коммутаторов)
    - [Шаг 4. Настраиваем базовые параметры каждого коммутатора](https://github.com/necit137/otus_study/edit/main/lab%2002/README.md#шаг-4-настраиваем-базовые-параметры-каждого-коммутатора)
      - [a. Настраиваем имя устройства в соответствии с топологией](https://github.com/necit137/otus_study/edit/main/lab%2002/README.md#a-настраиваем-имя-устройства-в-соответствии-с-топологией)
      - [b.	Настраиваем IP-адреса, как указано в таблице адресации](https://github.com/necit137/otus_study/edit/main/lab%2002/README.md#bнастраиваем-ip-адреса-как-указано-в-таблице-адресации)
      - [c.	Назначаем cisco в качестве паролей консоли и VTY](https://github.com/necit137/otus_study/edit/main/lab%2002/README.md#cназначаем-cisco-в-качестве-паролей-консоли-и-vty)
      - [d.	Назначаем class в качестве пароля доступа к привилегированному режиму EXEC](https://github.com/necit137/otus_study/edit/main/lab%2002/README.md#dназначаем-class-в-качестве-пароля-доступа-к-привилегированному-режиму-exec)

### Часть 1. Создание и настройка сети
### Шаг 1. Подключаем сеть в соответствии с топологией

![](network.png)

### Шаг 2. Настраиваем узлы ПК
Производим настройку PC-A
![](PC-A_configuration.png)

Производим настройку PC-B
![](PC-B_configuration.png)

### Шаг 3. Выполняем инициализацию и перезагрузку коммутаторов
Для первичного подключения к коммутаторам **S1** и **S2**, подключаем к ним компьютер PC-A через COM-порт. 
![](PC-A_comport.png)

Командой ***erase startup-config*** удаляем все конфигурации на коммутаторе: 
```
Switch#erase startup-config 
Erasing the nvram filesystem will remove all configuration files! Continue? [confirm]
[OK]
Erase of nvram: complete
%SYS-7-NV_BLOCK_INIT: Initialized the geometry of nvram
```
после чего перезапускаем коммутатор коммандой ***reload***:
```
Switch#reload 
Proceed with reload? [confirm]
C2960 Boot Loader (C2960-HBOOT-M) Version 12.2(25r)FX, RELEASE SOFTWARE (fc4)
Cisco WS-C2960-24TT (RC32300) processor (revision C0) with 21039K bytes of memory.
2960-24TT starting...
```
Выполняем данные команды на обоих устройствах

### Шаг 4. Настраиваем базовые параметры каждого коммутатора 
Далее будет указана настройка первого коммутатора S1. Настройка коммутатора S2 проводится аналогично, по этому отражена в работе не будет. 
#### a. Настраиваем имя устройства в соответствии с топологией

```
Switch>enable
Switch#configure terminal 
Enter configuration commands, one per line.  End with CNTL/Z.
Switch(config)#no ip domain-lookup 
Switch(config)#hostname S1
S1(config)#
```
#### b.	Настраиваем IP-адреса, как указано в таблице адресации

```
S1#configure terminal 
Enter configuration commands, one per line.  End with CNTL/Z.
S1(config)#interface vlan1
S1(config-if)#ip address 192.168.1.11 255.255.255.0
S1(config-if)#no shutdown

S1(config-if)#
%LINK-5-CHANGED: Interface Vlan1, changed state to up

%LINEPROTO-5-UPDOWN: Line protocol on Interface Vlan1, changed state to up
S1(config-if)#
```
#### c.	Назначаем cisco в качестве паролей консоли и VTY

```
S1#configure terminal 
Enter configuration commands, one per line.  End with CNTL/Z.
S1(config)#line vty 0 15
S1(config-line)#password cisco
S1(config-line)#login
```
#### d.	Назначаем class в качестве пароля доступа к привилегированному режиму EXEC

```
S1(config)#service password-encryption 
S1(config)#enable secret class
S1(config)#
```
### Часть 2. Изучение таблицы МАС-адресов коммутатора
### Шаг 1. Запишем МАС-адреса сетевых устройств
#### а.	Открываем командную строку на PC-A и PC-B и вводим команду ***ipconfig /all***
Пример ввода команды с командной строки PC-A:

Physical Address PC-A................: 0001.C779.43AC
Physical Address PC-B................: 0030.A3B3.36B2
#### b.

