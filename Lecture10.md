# IPv6

## Причины появления IPv6

### Нехватка IPv4 адресов

Одной из главных причин создания IPv6 стала нехватка адресов в протоколе IPv4. Адреса длиной 32 бита перестали удовлетворять запросам стремительно развивающегося интернета. IPv6 предлагает адреса длиной 128 бит, что увеличивает адресное пространство в четыре раза, обеспечивая практически неограниченное количество уникальных адресов.

### Долгосрочное решение

IPv6 задумывался как долгосрочное решение проблемы адресации в интернете. В отличие от краткосрочных методов, таких как NAT (Network Address Translation), PAT (Port Address Translation) и DHCP (Dynamic Host Configuration Protocol).

### Оптимизация маршрутизации

Внедрение IPv6 также связано с необходимостью оптимизации маршрутизации. Изменения в IP заголовке позволили сделать маршрутизацию более эффективной, что способствует снижению задержек и повышению скорости передачи данных.

## Структура IPv6 адреса

IPv6 адреса записываются в шестнадцатеричной форме, что делает их удобными для хранения и обработки в компьютерных системах. Это также существенно отличается от традиционной десятичной записи, используемой для адресов IPv4. Давайте рассмотрим более подробно, как именно структурирован IPv6 адрес:

### Формат записи

- Шестнадцатеричная форма: Адрес состоит из восьми групп, каждая из которых содержит четыре шестнадцатеричных цифры (по два байта). Например:
 
 ```
 2001:0db8:85a3:0000:0000:8a2e:0370:7334
 ```

### Упрощение записи

Для удобности и сокращения записи IPv6 адресов, существуют несколько правил упрощения:

1. Удаление лидирующих нулей: В каждой группе можно опустить ведущие нули. Например, группа 0db8 может быть сокращена до db8.

2. Объединение нулевых групп: Последовательные группы из нулей можно заменить двойным двоеточием ```::```. Однако, такое сокращение возможно лишь один раз в адресе, чтобы избежать путаницы. Например, адрес выше может быть упрощен до:
 
  ```
  2001:db8:85a3::8a2e:370:7334
  ```

### Стандартная маска подмножества

- Маска подмножества: В IPv6, нет традиционных масок, как это было в IPv4 (вроде 255.255.255.0). Вместо этого использование сетевого префикса стало более распространенной практикой. Обычно, стандартный префикс для глобальной унифицированной сети составляет /64, что означает, что первые 64 бита адреса используются для идентификации сети, а оставшиеся 64 бита используются для адресов узлов в этой сети.

- Практическое применение: Стандартным является использование префикса /64, однако могут быть использованы и другие префиксы в зависимости от конкретных нужд сети и конфигураций. Префиксы длиной от /48 до /64 часто зарезервированы для организационных нужд и используются для дальнейшего деления на подсети внутри организации.

<p style="text-align: left"><img src=res/10_1.png width="500px"/></p>

## Типы IPv6 адресов 

**!!! broadcast не существует !!!**

<p style="text-align: left"><img src=res/10_2.png width="500px"/></p>

## Распределение IPv6 адресов

<p style="text-align: left"><img src=res/10_3.png width="500px"/></p>

IPv6 адресация делится на несколько префиксов, которые управляют маршрутизацией и делением пространства адресов:

### 1. Регистровый префикс
- Назначается: IANA (Интернет-корпорация по присвоению имён и номеров) региональному интернет-регистратору (RIR).
- Формат: 2340::/12

### 2. Префикс интернет-провайдера (ISP)
- Назначается: RIR интернет-провайдеру (ISP).
- Формат: 2340:1111/32

### 3. Префикс сайта или глобальный маршрутизируемый префикс
- Назначается: ISP или регистратором клиенту.
- Формат: 2340:1111:AAAA/48

### 4. Префикс подсети
- Назначается: Инженером компании для каждого индивидуального соединения.
- Формат: 2340:1111:AAAA:0001/64

## Детализация глобальных префиксов

### /48 Глобальный маршрутизируемый префикс
- Адрес: 2001:db8:cafe::/64
- Компоненты:
 - L = Location (местоположение): 4 бита
 - B = Building (здание): 4 бита
 - V = VLAN или подсеть: 8 бит

### /32 Глобальный маршрутизируемый префикс
- Адрес: 2001:db8::/64
- Компоненты:
 - L = Location (местоположение): 8 бит
 - B = Building (здание): 12 бит
 - V = VLAN или подсеть: 12 бит

## Зарезервированные адреса

<p style="text-align: left"><img src=res/10_4.png width="600px"/></p>

## Преимущества IPv6

IPv6 — это современный протокол сетевой адресации, который предлагает множество преимуществ по сравнению со своим предшественником, IPv4:

### Большое адресное пространство
IPv6 предоставляет колоссальное количество уникальных IP-адресов, благодаря использованию 128-битного адресного пространства, что делает его практически неисчерпаемым по сравнению с 32-битной структурой IPv4.

### Способ назначения адресов
В IPv6 предусмотрены более гибкие и эффективные механизмы автонастройки, такие как Stateless Address AutoConfiguration (```SLAAC```), которые упрощают управление сетями и уменьшают необходимость ручной конфигурации.

### Интеллектуальная агрегация
IPv6 позволяет провайдерам выделять адреса более крупными блоками, что упрощает маршрутизацию, снижает размер таблиц маршрутизации и повышает общую эффективность сети.

### Иерархичное распределение
Благодаря структуре префиксов, адресация в IPv6 поддерживает более иерархичное распределение, облегчающее управление и организацию сетей крупных организаций и операторов связи.

### Отсутствие необходимости в переводе адресов (NAT/PAT)
IPv6 устраняет необходимость в использовании Network Address Translation (NAT) или Port Address Translation (PAT), что облегчает прямую связь между устройствами и улучшает производительность сетей.

### Отсутствие broadcast
IPv6 отказывается от использования широковещательной передачи (broadcast), вместо этого применяя многоадресные (multicast) и любые (anycast) адресации, что снижает нагрузку на сеть и увеличивает её быстродействие.

### Улучшения заголовка
Заголовок IP-пакета в IPv6 был упрощён и оптимизирован, что улучшает эффективность маршрутизации. Некоторые ненужные поля были удалены, а важные расширения вынесены за пределы основного заголовка.

## Формат заголовка пакета

<p style="text-align: left"><img src=res/10_5.png width="700px"/></p>

У него фиксированная длина. Исключена контрольная сумма, значит теперь не нужно роутерам ее пересчитывать. IPv6 не поддерживает фрагментацию на маршрутизаторах. Фрагментация выделена в отдельные заголовки и доступна только отправителю, что оптимизирует обработку пакетов.

## Известные групповые адреса 

<p style="text-align: left"><img src=res/10_6.png width="600px"/></p>

## Методы назначения адресов IPv6

<p style="text-align: left"><img src=res/10_7.png width="600px"/></p>

### Stateful DHCP

Stateful DHCPv6 (Dynamic Host Configuration Protocol) используется для централизованного управления и назначения IP-адресов и других сетевых параметров. В этом режиме DHCP-сервер отслеживает, какие устройства используют какие адреса, и обеспечивает дополнительную информацию, такую как DNS-серверы и доменные имена. Это особенно полезно в крупных или сложных сетях, где требуется управление сетевыми параметрами из единой точки.

### Stateless Autoconfiguration

Stateless Address Autoconfiguration (SLAAC) позволяет устройствам самостоятельно конфигурировать свои IPv6-адреса без участия сервера DHCP. Используя префиксы, которые объявляются маршрутизаторами через сообщения Router Advertisement (RA), устройство автоматически формирует свой адрес на основе идентификатора интерфейса. Этот метод упрощает распределение адресов и снижает необходимость в дополнительной инфраструктуре, такой как DHCP-серверы.

### Static Config with EUI-64 (Extended Unique Identifier)

Статическая конфигурация с использованием EUI-64 позволяет устройствам формировать уникальный адрес на основе их MAC-адреса. Метод подразумевает автоматическое преобразование MAC-адреса в 64-битный идентификатор интерфейса, который используется для создания уникального IPv6-адреса. Это облегчает процесс статической настройки, обеспечивая уникальность и унификацию адресов без ручного ввода полного адреса.

<p style="text-align: left"><img src=res/10_8.png width="600px"/></p>

1. Деление MAC-адреса: 
  - MAC-адрес (48 бит) делится на две половины. Например, если MAC-адрес устройства XX:XX:XX:YY:YY:YY, то первая половина — это XX:XX:XX, а вторая — YY:YY:YY.

2. Вставка FFFE:
  - Между этими двумя половинками вставляется фиксированная последовательность байтов FFFE. Это расширяет адрес до 64 бит. Таким образом, преобразованный адрес будет выглядеть как XX:XX:XX:FF:FE:YY:YY:YY.

3. Инверсия 7-го бита:
  - Необходимо инвертировать 7-й бит в первом байте. Этот бит указывает, кем назначен MAC-адрес — производителем или пользователем.

## Время жизни SLAAC адреса IPv6

<p style="text-align: left"><img src=res/10_9.png width="600px"/></p>

При автоматической генерации IPv6-адреса с помощью Stateless Address Autoconfiguration (SLAAC) существуют несколько периодов его жизни, каждый из которых имеет свои характеристики и функции:

### 1. Preferred Lifetime

На этом этапе адрес является "предпочитаемым", и устройства могут активно использовать его для установления соединений с другими узлами. Он доступен для входящих и исходящих соединений, и другие узлы также могут использовать его в качестве обратного адреса.

### 2. Valid Lifetime

В течение "действительного" времени жизни адрес остаётся функциональным, но новые соединения уже не устанавливаются с его использованием. В этот период создается новый адрес, который станет "предпочитаемым". Старый адрес продолжает функционировать для поддержания текущих соединений.

### 3. Invalid

После завершения срока "действительного" времени адрес становится "недействительным". Он больше не может использоваться для каких-либо соединений, и устройства должны переключиться на новый "предпочитаемый" адрес для продолжения сетевых операций. Недействительные адреса больше не могут использоваться даже для продолжения существующих соединений. 

## NDP (Neighbor Discovery Protocol)

Neighbor Discovery Protocol (NDP) — это протокол, используемый в IPv6 для различных сетевых функций, заменяющих и расширяющих возможности ARP в IPv4. NDP работает на основе ICMPv6, предоставляя механизмы для обнаружения соседних узлов и управления сетью.

### Поиск маршрутизаторов IPv6

<p style="text-align: left"><img src=res/10_10.png width="600px"/></p>

В контексте NDP поиск маршрутизаторов — это ключевая функция, которая позволяет узлам находить маршрутизаторы в локальной сети. Это осуществляется посредством сообщений типа ```Router Solicitation``` и ```Router Advertisement```:

- Router Solicitation (RS): Узлы отправляют эти сообщения, чтобы запрашивать присутствие маршрутизаторов в сети, стараясь ускорить процесс обнаружения.

- Router Advertisement (RA): Маршрутизаторы периодически (или в ответ на RS) отправляют эти сообщения, содержащие информацию о доступных префиксах, настройках автоконфигурации и других параметрах, необходимых для узлов.