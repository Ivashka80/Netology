# Домашнее задание к занятию "Сеть и сетевые протоколы: VPN"
<details>
Это задание обязательное к выполнению. 
Пожалуйста, присылайте на проверку всю задачу сразу. Любые вопросы по решению задач задавайте в чате учебной группы.

--- 

### Цели задания: 
1. познакомиться с процессом создания VPN (Site-to-Site);
2. научиться создавать VPN-соединение и конфигурировать ее;
3. создать VPN туннель с помощью протокола IPSec.

Данная практика закрепляет знания о создании и настройки виртуальной частной сети. Эти навыки пригодятся для создания собственных сервисов и повышению безопасности сети.

### Чеклист готовности к домашнему заданию
- Прочитайте статью ["Как пользоваться программой Cisco Packet Tracer"](https://pc.ru/articles/osnovy-raboty-s-cisco-packet-tracer)
- Установите программу Cisco Packet Tracer на своем компьютере 
- Выполните домашние задание ["4.6. Сеть и сетевые протоколы: NAT"](https://github.com/netology-code/snet-homeworks/blob/snet-18/4-05.md)

### Инструкция по выполнению: 
- Сделайте скриншоты из Cisco Packet Tracer по итогам выполнения задания 
- Отправьте на проверку в личном кабинете Нетологии скриншоты. Файлы прикрепите в раздел "решение" в практическом задании.
- В комментариях к решению в личном кабинете Нетологии напишите пояснения к полученным результатам. 

---

## Задание. Создание дополнительного офиса и настройка ISAKMP-туннеля для согласования параметров протокола.

### Описание задания
Руководство решило открыть новый филиал в соседней области. Перед вами стоит задача  между главным офисом и филиалом создать VPN-туннель. Новый филиал подключен к тому же интернет-провайдеру. Но имеет другие “белые” ip-адреса для подключения: 87.250.0.0/30

### Требование к результату
- Вы должны отправить файл .pkt с выполненным заданием
- К выполненной задаче добавьте скриншоты с доступностью “внешней сети” и ответы на вопросы.

### Процесс выполнения
1. Запустите программу Cisco Packet Tracer
2. В программе Cisco Packet Tracer загрузите предыдущую практическую работу.
3. На маршрутизаторе интернет-провайдера добавьте в модуль физически порты GLC-TE, предварительно его выключив.
4. Создайте сеть нового филиала, состоящую из 3 ПК, 1 коммутатора и 1 маршрутизатора.
5. Создайте сетевую связность между маршрутизатором филиала и маршрутизатором интернет-провайдера, согласно условиям.
6. На маршрутизаторе филиала создайте NAT-трансляцию с помощью access-листов для внутренней сети. Адресацию внутри сети филиала можно использовать любую.
7. На маршрутизаторе главного офиса настройте политики ISAKMP: 

*R1(config)#  crypto isakmp policy 1*

*R1(config-isakmp)# encr 3des - метод шифрования*

*R1(config-isakmp)# hash md5 - алгоритм хеширования*

*R1(config-isakmp)# authentication pre-share - использование предварительного общего ключа (PSK) в качестве метода проверки подлинности*

*R1(config-isakmp)# group 2 - группа Диффи-Хеллмана, которая будет использоваться*

*R1(config-isakmp)# lifetime 86400 - время жизни ключа сеанса*

8. Укажите Pre-Shared ключ для аутентификации с маршрутизатором филиала. Проверьте доступность с любого конечного устройства доступность роутера интернет-провайдера, командой ping.
9. Создайте набор преобразования (Transform Set), используемого для защиты наших данных.

*crypto ipsec transform-set <название> esp-3des esp-md5-hmac*

10. Создайте крипто-карту с указанием внешнего ip-адреса интерфейса и привяжите его к интерфейсу.

*R1(config)# crypto map <название> 10 ipsec-isakmp*

*R1(config-crypto-map)# set peer <ip-address>*

*R1(config-crypto-map)# set transform-set <название>*

*R1(config-crypto-map)# match address <название access-листа>*

*R1(config- if)# crypto map <название крипто-карты>*

10. Проделайте вышеуказанные операции на маршрутизаторе филиала в соответствии ip-адресов и access-листов и отключите NAT-трансляцию сетевых адресов.
11. Проверьте сетевую доступность между роутерами командой ping.
12. Проверьте установившееся VPN-соединение на каждом роутере командой: “show crypto session”. Статус должен быть UP-ACTIVE. Сделайте скриншот.
13. Ответ внесите в комментарии к решению задания в личном кабинете Нетологии

### Топология после выполнения задания должна выглядеть следующим образом:
[![](https://i.postimg.cc/SRYBKKtR/oYEo8eD2.jpg)](https://postimg.cc/T5G77Txv)

### Критерии оценки
1. Задание выполнено полностью.
2. К заданию прикреплены скриншоты статусов VPN-соединений и доступности сетей двух офисов.
3. Отображены настройки конфигурации VPN.
 
</details>

# Ответ

Ссылка на файлы .pkt - https://drive.google.com/drive/folders/1azS-R6vLMHZfoOToT5VAS4nvz3YLhKuQ?usp=sharing
  
За основу взято последнее задание по CPT – NAT.

Создано новое подразделение NewOffice с «белым» адресом `87.250.0.0/30`. Внутренняя сеть – `192.168.255.0/24`.

Создается access-list для NAT до роутера првайдера. Я решил поэкспериментировать с расширенным access-list’ом. Трафик не «натится» при обращении к сети нового офиса. Но если послать запрос к провайдеру, то трафик уже пойдет через NAT.
Пример такого листа на роутере нового офиса (подобный и на роутере главного офиса):
- `deny ip 192.168.60.0 0.0.0.15 192.168.10.0 0.0.0.15` (не «натить» адреса для сети 192.168.10.0).
- `permit ip 192.168.60.0 0.0.0.15` (для других сетей «натить»).

Проверка доступа до роутеров провайдеров каждой сети (файл `SYS_4-07_VPN_Z1_1F.pkt`).

![Снимок01-02](https://user-images.githubusercontent.com/121082757/225212226-dafc7ed6-07a8-47c0-b239-67ae8dbf34bb.PNG)
  
![Снимок01-02_](https://user-images.githubusercontent.com/121082757/225212242-17bdc4f3-1246-463e-afd5-af42d3eebd42.PNG)

Для связи по VPN между главным и новым офисами на их роутерах нужно совершить следующие настройки: указать политику шифрования ISAKMP; указать метод и алгоритм шифрования; создать крипто-карту и др. Также надо определить какой трафик надо шифровать. В данном случае это будут адреса главного и нового офисов.

Для работы VPN пришлось отключить NAT-трансляцию.

*С расширенным access-list NAT не совсем вышло. Пинг работает через раз: половина пакетов теряется.*

Командой `show crypto ipsec sa` можно увидеть, что пакеты были зашифрованы (файл - `SYS_4-07_VPN_Z1_2F.pkt`).

![Снимок04](https://user-images.githubusercontent.com/121082757/225212926-23b8fe25-f6db-4614-89fa-57d90350f300.PNG)

Команда `show crypto isakmp sa` покажет наличие туннеля, в которм указан адрес интрфейса роутера нового офиса (dst) и адрес ротурера источника (src).

 ![Снимок05](https://user-images.githubusercontent.com/121082757/225212959-06f749d0-5ec6-4a0d-b1e9-01714c9739ce.PNG)

*Вопрос: в ДЗ для просмотра статуса VNP указана команда show crypto session. В моем случае этой команды не было. Она присутствует не у всех роутеров?*

  
  
  