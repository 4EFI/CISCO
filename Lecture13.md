# FHRP (First Hop Redundancy Protocols)

Протоколы Резервирования Следующего Хопа (FHRP) предназначены для обеспечения отказоустойчивости и доступности сетевых маршрутов на уровне шлюзов по умолчанию. Их основная задача — предоставить резервирование для критически важных маршрутных устройств, таких как маршрутизаторы или агрегационные коммутаторы, занимающие важное место между уровнями Core и Access.

## Проблема сетевой недоступности

Если агрегационное устройство выходит из строя, это может сделать недоступными те сети, которые были закреплены за этим устройством. В отсутствии резервирования пользователи, подключённые к данным сетям, не смогут получить доступ к корпоративным ресурсам или интернету, что может быть критически для бизнеса.

## Основные протоколы FHRP

1. HSRP (Hot Standby Router Protocol): 
  Протокол, разработанный Cisco, который позволяет настраивать один активный и один или несколько резервных маршрутизаторов. Резервные маршрутизаторы готовы моментально взять на себя роль активного узла в случае его отказа.

2. VRRP (Virtual Router Redundancy Protocol): 
  Стандартный протокол, схожий с HSRP, обеспечивающий резервирование через конфигурацию нескольких маршрутизаторов в виртуальную маршрутизаторную группу. Активный маршрутизатор отвечает за обработку трафика, а резервные готовы принять на себя нагрузку в случае сбоя.

3. GLBP (Gateway Load Balancing Protocol): 
  Еще один протокол от Cisco, который не только предоставляет резервирование, но и поддерживает балансировку нагрузки между несколькими маршрутизационными устройствами, распределяя трафик более эффективно.


# L3-Switch

Коммутатор третьего уровня сочетает в себе функции коммутатора и маршрутизатора в одном устройстве. Если коммутатор второго уровня работает исключительно с MAC-адресами и занимается коммутацией кадров в пределах одной сети, то коммутатор третьего уровня способен принимать решения на основе IP-адресов, что позволяет ему выполнять маршрутизацию между различными VLAN или сетями.


# LAG (Link Aggregation Group)

<p style="text-align: left"><img src=res/13_1.png width="500px"/></p>

LAG объединяет несколько физических соединений Ethernet в один логический интерфейс. Это позволяет увеличить общую полосу пропускания и обеспечить резервирование. Если один из линков в группе выходит из строя, оставшиеся линки продолжают работу, обеспечивая непрерывность соединения.

## Зачем нужна агрегация каналов?

1. Увеличение пропускной способности: Совокупная пропускная способность логического канала равна сумме пропускных способностей всех агрегированных каналов.
2. Отказоустойчивость: Обеспечивает бесперебойную работу канала при отказе одного или нескольких физических линков.
3. Балансировка нагрузки: Потоки данных можно распределять между агрегированными линками, снижая нагрузки на единичные физические каналы.

## Принципы работы LAG

1. Объединение каналов: Один или несколько физических интерфейсов объединяются в один логический интерфейс. Этот процесс также известен как "link aggregation".
   
2. Протоколы агрегации: IEEE 802.3ad (также известен как LACP — Link Aggregation Control Protocol) — это стандарт, используемый для динамической агрегации линков. Он автоматически определяет какие линейки могут быть объединены и управляет процессом агрегации.
   
3. Балансировка нагрузки: Пакеты распределяются по доступным физическим каналам. Методы могут включать распределение на основе MAC-адресов, IP-адресов, порта TCP/UDP и других характеристик.
   
4. Резервирование и отказоустойчивость: Если один из каналов в агрегате выйдет из строя, LAG автоматически перенаправляет трафик через оставшиеся работающие каналы.

## vPC (virtual Port-Channel) 

vPC использует пару коммутаторов Cisco Nexus, объединённых так называемой vPC peer-link. Оба коммутатора ведут себя как одно логическое устройство по сравнению с подключенными устройствами. Это позволяет подключенному оборудованию «думать», что оно общается с одним коммутатором, хотя на самом деле взаимодействие идёт с двумя коммутаторами одновременно.
