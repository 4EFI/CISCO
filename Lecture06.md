# ARP: Связующее Звено Между Канальным и Сетевым Протоколами

ARP (Address Resolution Protocol) играет ключевую роль в связке технологии Ethernet и протокола IPv4. Основная задача ARP заключается в определении MAC-адреса, необходимого для правильной маршрутизации трафика **внутри одной локальной сети**.

## Как Работает ARP?

1. Обнаружение MAC-адреса:
  Перед тем как отправить IP-пакет другому устройству в том же сетевом сегменте, необходимо узнать его MAC-адрес. Ведь именно на уровне канального слоя данные передаются с использованием MAC-адресов.

2. Отправка ARP-запроса:
  Когда устройство хочет узнать MAC-адрес другого устройства, оно рассылает ARP-запрос (```ARP Request```) для всех устройств в сетевом сегменте.

3. Получение ARP-ответа:
  Устройство, обладающее запрашиваемым IP-адресом, отвечает с помощью ARP-ответа (```ARP Reply```), в котором указывает свой MAC-адрес.

## Структура ARP Сообщения (в 32-битных Словах)

ARP-сообщение состоит из нескольких полей, каждое из которых выполняет определённую функцию. Давайте подробно разберём их:

<p style="text-align: left"><img src=res/6_1.png width="500px"/></p>

### Основные Поля

1. HTYPE (Hardware Type):
  - Определяет тип аппаратного оборудования. Например, для Ethernet значение будет равно 1.
  
2. PTYPE (Protocol Type):
  - Определяет тип протокола, который будет использоваться. Для IPv4, значение равно 0x0800.

3. HLEN (Hardware Length):
  - Задаёт длину аппаратного адреса в байтах. Для Ethernet значение будет равно 6.
  
4. PLEN (Protocol Length):
  - Определяет длину адреса протокола в байтах. Например, для IPv4 это значение составляет 4.
  
5. OPER (Operation):
  - Определяет тип операции ARP: запрос (1) или ответ (2).

#### Адресные Поля

После основных полей следуют четыре поля, представляющие собой комбинации MAC- и IP-адресов:

1. SHA (Sender Hardware Address):
  - MAC-адрес отправителя. Это адрес устройства, отправляющего ARP-запрос или ответ.

2. SPA (Sender Protocol Address):
  - IP-адрес отправителя. Используется для идентификации устройства в сети.

3. THA (Target Hardware Address):
  - MAC-адрес получателя. Используется только в ответе и оставляется пустым в запросе.

4. TPA (Target Protocol Address):
  - IP-адрес получателя. Этот адрес идентифицирует целевое устройство в сети.

**!!! ARP сообщает только в рамках локального Ethernet сегмента. Не передаются через маршрутизаторы !!!**

## Рассмотрим пример работы ARP 

<p style="text-align: left"><img src=res/6_2.png width="600px"/></p>

<p style="text-align: left"><img src=res/6_3.png width="400px"/></p>

1. A → B: Взаимодействие внутри одной подсети

  - Узел A и узел B находятся в одной и той же подсети. Это подтверждается путём наложения маски подсети на их IP-адреса.
  - Взаимодействие происходит непосредственно между устройствами, без необходимости обращения к маршрутизатору.

2. A → C: Взаимодействие между разными подсетями

  - Узел A обнаруживает, что узел C находится в другой подсети, рассчёт сделан путём наложения маски подсети.
  - Чтобы передать пакет узлу C, узел A формирует сетевой кадр (frame), который отправляется к маршрутизатору R1.
  - Для этого кадра необходимо определить MAC-адрес шлюза по умолчанию (маршрутизатора R1), чтобы успешно передать данные за пределы локальной подсети.


# Proxy ARP

## Ситуация Сети

- У нас есть сеть, где C и D — это серверы. 
- Слева находятся клиенты, а справа — серверный сегмент.

## Проблема Настройки

- При смене IP-адреса была допущена ошибка: вместо верной маски /24 ошибочно указали /16.
- В результате, сервер C считает, что клиент A находится в той же подсети.

## Поведение Пакетов

- Путь от A к C: Данные успешно достигают сервера C, так как клиент A использует правильную маску и находит путь к серверу.
- Путь Обратно от C к A: Возврат пакетов невозможен. Сервер C считает A частью своей подсети и пытается отправить данные напрямую, без нужды в маршрутизации и зная некорректное локальное назначение.

## Решение: Proxy ARP

- На маршрутизаторе R2 включена функция Proxy ARP. Эта технология помогает исправить возникшую проблему.
- Функция Proxy ARP:
 - Маршрутизатор R2 перехватывает некорректный кадр и обнаруживает несоответствие в маске.
 - Используя Proxy ARP, он отвечает на запросы ARP за клиента A, притворяясь узлом в его подсети.
 - Это позволяет доставить пакеты обратно к A, создавая иллюзию, что все узлы находятся в одной и той же сети.
