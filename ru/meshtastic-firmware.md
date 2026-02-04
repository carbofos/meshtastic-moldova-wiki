# Прошивка для устройства Meshtastic

Устройство Meshtastic состоит из микроконтроллера и радиопередатчика LoRa. Такое устройство можно собрать самому, а можно приобрести уже готовое. Вот тут подробно об этих устройствах и о том, как собрать самостоятельно:
https://habr.com/ru/articles/568394/

Обратите внимание, что пост довольно давний, а в этом проекте каждый день в репозитории огромное количество изменений. Поэтому за многие годы многое поменялось.

Имея на руках готовое устройство в него нужно записать программу микроконтроллера, которая разрабатывается огромным сообществом энтузиастов вот тут:
https://github.com/meshtastic/firmware/

## Устройства уже прошитые производителем
Такие гаджеты как Heltec идут уже с прошивкой Meshtastic и для работы достаточно включить их и подключиться через BT/BLE с мобильного приложения для Android или iOS.

## Прошивка через web-flasher через USB
Для большинства устройств можно ничего не качать и для прошивки достаточно перейти браузером Chrome на https://flasher.meshtastic.org/, выбрать устройство, версию и прошить.
Прошивки делятся по версиям, которые с каждым релизом увеличиваются. Версии бывают стабильные Beta и нестабильные Alfa, в которые активно добавляются новые функции, которые еще не были тщательно протестированы. На февраль 2026 стабильная версия 2.7.15 и нестабильная 2.7.18.
Однако, для контроллеров на nRF52840 нужно скачать файл .uf2, подключить гаджет Meshtastic к USB компьютера, нажать на мештастике два раза RESET и когда появится диск типа USB флэшки просто залить туда этот файл прошивки. Все прошьется автоматически и перезагрузится.

### Самостоятельная прошивка через USB
Определившись с тем, хочется ли вам иметь самые новые функции или предпочитаете стабильность (примите, что в этом проекте стабильность не найдете ни в какой версии), выбирайте в разделе Releases версию и нажмите "Assets" чтобы увидеть полный список доступных групп прошивок:
https://github.com/meshtastic/firmware/releases

Эти группы разбиты по названию микроконтроллера, на котором строится ваше устройство.

Следующая таблица поможет разобраться какую прошивку выбирать.

| Бренд | Название устройства | Контроллер (MCU) |
| :--- | :--- | :--- |
| **Seeed Studio** | XIAO nRF52840 Sense / Kit | nRF52840 |
| **Seeed Studio** | XIAO ESP32-S3 | ESP32-S3 |
| **Seeed Studio** | Wio Tracker 1110 | nRF52840 |
| **Seeed Studio** | SenseCAP T1000-E | nRF52840 |
| **Heltec** | WiFi LoRa 32 (v1 / v2) | ESP32 |
| **Heltec** | WiFi LoRa 32 (v3) | ESP32-S3 |
| **Heltec** | Wireless Stick / Lite (v3) | ESP32-S3 |
| **Heltec** | Wireless Tracker | ESP32-S3 |
| **Heltec** | Wireless Paper | ESP32-S3 |
| **Heltec** | Vision Master (E213 / E290 / T190) | ESP32-S3 |
| **Heltec** | Mesh Node T114 | nRF52840 |
| **LilyGO (TTGO)** | T-Beam (v0.7 / v1.1 / v1.2) | ESP32 |
| **LilyGO (TTGO)** | T-Beam Supreme | ESP32-S3 |
| **LilyGO (TTGO)** | LoRa32 (v1.0 / v2.1) | ESP32 |
| **LilyGO (TTGO)** | T-Echo | nRF52840 |
| **LilyGO (TTGO)** | T-Deck / T-Deck Plus | ESP32-S3 |
| **LilyGO (TTGO)** | T-Pager | ESP32-S3 |
| **LilyGO (TTGO)** | T-Watch S3 | ESP32-S3 |
| **LilyGO (TTGO)** | T-LoRa T3-S3 | ESP32-S3 |
| **RAKwireless** | WisBlock Core RAK4631 | nRF52840 |
| **RAKwireless** | WisBlock Core RAK11200 | ESP32 |
| **RAKwireless** | WisBlock Core RAK11310 | RP2040 |
| **RAKwireless** | WisMesh Pocket / Mini / Tag | nRF52840 |
| **B&Q Consulting** | Nano G1 Explorer | ESP32 |
| **B&Q Consulting** | Nano G2 Ultra | nRF52840 |
| **B&Q Consulting** | Station G1 | ESP32 |
| **B&Q Consulting** | Station G2 | ESP32-S3 |
| **Elecrow** | ThinkNode M2 | ESP32-S3 |
| **M5Stack** | Core / Core2 / CoreS3 | ESP32 / ESP32-S3 |
| **M5Stack** | Atom Echo / AtomS3 | ESP32 / ESP32-S3 |
| **M5Stack** | Paper | ESP32 |
| **M5Stack** | StickC / StickC Plus | ESP32 |
| **Raspberry Pi** | Pico / Pico W | RP2040 |
| **Waveshare** | RP2040-LoRa | RP2040 |
| **Waveshare** | ESP32-S3-Pico | ESP32-S3 |
| **Canary Radio** | CanaryOne | nRF52840 |
| **CircuitMess** | Chatter 2 | ESP32-S3 |
| **unPhone** | unPhone | ESP32-S3 |
| **LORA-HF** | Hydra | nRF52840 |
| **DFRobot** | FireBeetle ESP32 | ESP32 |
| **SparkFun** | LoRa Gateway (1-channel) | ESP32 |
| **Custom/DIY** | Portduality | ESP32-S3 |
| **Native** | Linux / macOS / WSL | x86_64 / ARM64 |

Программа прошивки написана на языке C++ и чтобы её прошить нужно этот проект собрать (скомпилировать). Это можно сделать самостоятельно через platformio, а можно взять уже собранные пакеты в разделе Releases:
https://github.com/meshtastic/firmware/releases

Допустим, хотим прошить Heltec V3. Тогда по вышеприведенной таблице находим что прошивка для этого гаджета будет в ZIP архиве для ESP32-S3. Распаковываем архив и видим в директории файл
firmware-heltec-v3-2.7.18.fb3bf78.factory.bin (в конце должно быть .factory.bin)
В зависимости от ОС запускаем

Linux:
```
device-install.sh -f firmware-heltec-v3-2.7.18.fb3bf78.factory.bin
```

Windows:
```
device-install.bat -f firmware-heltec-v3-2.7.18.fb3bf78.factory.bin
```

Убедитесь, что к компьютеру подключен только один гаджет Meshtastic или любое другое устройство на микроконтроллере, чтобы не перепутать и не испорить его.

## Самостоятельная сборка прошивки
В некоторых случаях, например если используется народная плата IKOKA, изготовление которой было заказано нашим сообществом Мештастик в Молдове, может потребоваться самостоятельная сборка прошивки.
К этой плате подходит два контроллера: XIAO ESP32-S3 и XIAO nRF52840. 
Проблема с nRF52840 заключается в том, что изначально в прошивке Meshtastic для этого контроллера используется GPS L76K. На плате IKOKA места для GPS нет, но есть гребёнка для подключения через шину I2C дисплея SSD1306 или поддерживаемых мештастиком метеодатчиков, полный список которых можно найти вот тут:
https://github.com/meshtastic/firmware/tree/develop/src/modules/Telemetry/Sensor

Таким образом, чтобы работала шина I2C нужно в следующем коде отключить GPS и тогда автоматически выходы GPIO будут задействованы для шины I2C:
https://github.com/meshtastic/firmware/blob/538a5f0dfc9f6cd587b076f6c80a801b51a5f064/variants/nrf52840/seeed_xiao_nrf52840_kit/platformio.ini#L20

Проект платы IKOKA, который можно открыть в программе kicad:
https://github.com/ndoo/ikoka-stick-meshtastic-device
