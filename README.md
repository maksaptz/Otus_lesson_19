# Настройка PXE сервера для автоматической установки

## Цель: Отрабатываем навыки установки и настройки DHCP, TFTP, PXE загрузчика и автоматической загрузки

## Описание домашнего задания:

Бывают ситуации, когда ИТ-специалисту потребуется переустановить ОС на большом количестве хостов. Переустановка вручную потребует от специалиста большого количества времени. В этот момент стоит обратить внимание на PXE.
PXE (Preboot eXecution Environment) — это набор протоколов, которые позволяют загрузить хост из сети. Для загрузки будет использоваться сетевая карта хоста.

## Задачи домашнего задания:
1) установить и настроить загрузку по сети для дистрибутива CentOS7;
2) поменять установку из репозитория NFS на установку из репозитория HTTP;
3) настроить автоматическую установку для созданного kickstart файла (*) Файл загружается по HTTP.


### Описание домашнего задания

1) Для выполнения домашнего задания создадим 2 машины: pxeserver и pxeclient;
2) На pxeserver настроим веб сервер, загрузим на него утсновщик centos7;
3) Затем настроим tftp через http для работы pxe;
4) Подправим конфиг dhcp чтобы он начал выдывать адрес pxe сервера;
5) pxeclient настроим в Vagrantfile чтобы bios загружался через pxe.

#### Действия описаны в названии задач ansible

#### Проверка дз
1) Для проверки домашнего задания запускаем Vagrantfile, процесс настройки автоматизирован при помощи ansible;
2) После успешной установки заходим в pxexclienta через оснастку Virtualbox выбираем 4 пункт;
3) Когда операциооная система завершит установку необходимо перезагрузиться и в настройках Virtualbox выставить загрузку с жесткого диска;
4) Пользователь для тестирования root, pass 123.
