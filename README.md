<h1>Управление реле через интернет с использованием ESP-01 — это популярная задача для создания умных устройств.</h1>
<p></p>ESP-01 (на базе ESP8266) имеет встроенный Wi-Fi, что позволяет управлять реле через интернет с помощью MQTT, HTTP или WebSocket.<br>
Давай рассмотрим пример с использованием MQTT, так как это один из самых удобных протоколов для IoT.</p>

<p><b>Что понадобится:</b><br>
ESP-01 (модуль на базе ESP8266).<br>
Реле (например, 5V реле).<br>
USB-UART адаптер (для прошивки ESP-01).<br>
MQTT-брокер (например, <a href="https://mosquitto.org/">Mosquitto</a>, <a href="https://www.cloudmqtt.com/">CloudMQTT</a> или <a href="">HiveMQ)</a>.<br>
Arduino IDE для написания и загрузки кода.<br></p>

<p><b>Схема подключения:</b><br>
ESP-01:<br>
VCC -> 3.3V (не подключай к 5V, ESP-01 может сгореть!)<br>
GND -> GND<br>
TX -> RX адаптера<br>
RX -> TX адаптера (через делитель напряжения, так как ESP-01 работает на 3.3V, а адаптер может выдавать 5V)<br>
GPIO2 -> Управление реле (через транзистор, если реле требует больше тока, чем может выдать ESP-01).<br></p>

<p><b>Реле:</b><br>
VCC -> 5V (от внешнего источника питания).<br>
GND -> GND.<br>
IN -> GPIO2 ESP-01 (через транзистор, если необходимо).<br></p>

___________________________________________________________________

<p><b>Как это работает:</b><br>
Wi-Fi подключение: ESP-01 подключается к вашей Wi-Fi сети.<br>
MQTT подключение: ESP-01 подключается к MQTT-брокеру и подписывается на топик relay/control.<br>
Управление реле: Когда в топик relay/control приходит сообщение 1, реле включается. Если приходит 0, реле выключается.<br></p>

<p><b>Как протестировать:</b><br>
Загрузи код на ESP-01 через Arduino IDE.<br>
Используй MQTT-клиент (например, MQTT Explorer или Mosquitto CLI) для отправки сообщений в топик relay/control.<br>
Отправь 1, чтобы включить реле.<br>
Отправь 0, чтобы выключить реле.<br></p>
