# 🛡 Обход блокировки телеграм в России с помощью MTProto прокси

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Docker](https://img.shields.io/badge/Docker-nineseconds%2Fmtg%3A2-2496ED?logo=docker&logoColor=white)](https://hub.docker.com/r/nineseconds/mtg)
[![Telegram](https://img.shields.io/badge/Канал-@telegaLIFEpls-26A5E4?logo=telegram&logoColor=white)](https://t.me/telegaLIFEpls)

Установка личного MTProto прокси-сервера **одной командой**. Автоматически ставит Docker, генерирует секрет, запускает контейнер и выдаёт готовую ссылку для Telegram.

---

## Быстрый старт

```bash
ssh root@YOUR_IP_ADDRESS
```

```bash
bash <(curl -sL https://raw.githubusercontent.com/nrfx/MTProto-telegram-server/main/install.sh)
```

Готово. Скрипт выдаст ссылку — отправьте её в Telegram и подключитесь.

---

## Содержание

- [Что такое MTProto](#что-такое-mtproto)
- [Требования](#требования)
- [Установка](#установка)
- [Как это работает](#как-это-работает)
- [FAQ](#faq)

---

## Что такое MTProto

MTProto — протокол, разработанный Telegram для быстрой и безопасной работы мессенджера. Прокси на этом протоколе работает как посредник между вами и серверами Telegram.

Для интернет-провайдера ваш трафик выглядит как обычное HTTPS-соединение, а не как Telegram — это позволяет обходить блокировки и замедления.

**Почему свой прокси лучше?**

MTProto — крайне лёгкий протокол. Даже самый дешёвый VPS (1 CPU, 512 MB) без проблем обслуживает **тысячи одновременных подключений** — можно смело делиться ссылкой с друзьями, семьёй и подписчиками.

| | Публичный | Свой |
|---|---|---|
| Контроль | Неизвестно кто владеет | Полный контроль над сервером |
| Стабильность | Часто падает или исчезает | 99.9% uptime, автоперезапуск |
| Блокировки | IP быстро попадает в чёрные списки | IP неизвестен провайдерам |
| Масштаб | Нельзя повлиять на качество | Можно раздать тысячам людей без потери скорости |

---

## Требования

Вам нужен **VPS** (виртуальный сервер) с Linux. Минимальные параметры:

| Параметр | Значение |
|---|---|
| OS | Ubuntu 20.04+ / Debian 11+ |
| CPU | 1 ядро |
| RAM | 512 MB |
| Сеть | Без ограничений на порт 443 |

**Рекомендуемый хостер:** [Fornex](https://fornex.com)

**Рекомендуемая локация:** Нидерланды или Финляндия — ближе всего к дата-центрам Telegram.

---

## Установка

### 1. Подключитесь к серверу

```bash
ssh root@YOUR_IP_ADDRESS
```

### 2. Запустите скрипт

```bash
bash <(curl -sL https://raw.githubusercontent.com/nrfx/MTProto-telegram-server/main/install.sh)
```

### 3. Готово

Скрипт выведет ссылку вида:

```
https://t.me/proxy?server=185.21.9.61&port=777&secret=ee9fe4b27de45ee5f794432d4c01004d
```

Отправьте её себе в Telegram → нажмите → «Подключить прокси».

<details>
<summary>Пример вывода скрипта</summary>

```
🛡  Установка MTProto Proxy для Telegram
=========================================

📦 Устанавливаю Docker...
   ✅ Docker установлен
🔑 Сгенерирован секрет: ee9fe4b27de45ee5f794432d4c01004d
🌐 IP сервера: 185.21.9.61
🚀 Запускаю прокси...
   ✅ Прокси запущен

=========================================
✅ Готово! Ваш прокси работает.

📎 Ссылка для подключения:

   https://t.me/proxy?server=185.21.9.61&port=777&secret=ee9fe4b27de45ee5f794432d4c01004d

Отправьте эту ссылку в Telegram и нажмите
«Подключить прокси».
=========================================
```

</details>

---

## Как это работает

```
Вы (Telegram) ──► Ваш VPS (прокси) ──► Серверы Telegram
                      ↑
              Провайдер видит только
              HTTPS-соединение с VPS
```

Скрипт автоматически:
- Устанавливает Docker (если не установлен)
- Генерирует уникальный секретный ключ
- Создаёт оптимизированный конфиг (BBR, concurrency 8192)
- Запускает контейнер [`nineseconds/mtg:2`](https://github.com/9seconds/mtg) с автоперезапуском
- Устанавливает ulimit 65536 (поддержка 1000+ подключений)

---

## FAQ

**Сколько человек могут подключиться?**
> MTProto настолько лёгкий, что даже самый дешёвый VPS (1 CPU, 512 MB RAM) выдерживает тысячи одновременных подключений. Делитесь — скорость не пострадает.

**Это легально?**
> Да. MTProto-прокси — это не VPN. Он работает только с Telegram и не нарушает законодательство.

**Нужно ли что-то обновлять?**
> Нет. Контейнер автоматически перезапускается при сбоях и после перезагрузки сервера.

**Как удалить?**
> ```bash
> docker rm -f mtg && rm -rf /opt/mtg
> ```

---

## Наш проект

Мы используем эту же технологию в нашем боте — **[@ProxyRUSbot](https://t.me/ProxyRUSbot)** — который бесплатно раздаёт MTProto прокси сотням пользователей из России.


---

## Поддержать проект

Проект бесплатный и живёт на энтузиазме. Если хотите помочь — любой донат пойдёт на оплату серверов и расширение покрытия по всей России.

<a href="https://dalink.to/gdetim"><img src="https://img.shields.io/badge/DonationAlerts-F57B20?style=for-the-badge&logo=data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAA4AAAAOCAYAAAAfSC3RAAAAAXNSR0IArs4c6QAAAARnQU1BAACxjwv8YQUAAAAJcEhZcwAADsMAAA7DAcdvqGQAAACKSURBVDhPY/wPBAxUBExQmjqAiYGKgOo2MlIlqBgYGf8DFTMwMjIyNDU1/W9ubv4/efLk/01NTf+BCv8TYSMjMygYgIr/g2xsamr6D7KZGDYRZTMI0N5GUDCQBqgSjGAbMbOACCCIRlRTSDSguI14PUnMIUIqINpGWpka2/N4ePj/zs7O/wHrn0ISFSmmYAAAAABJRU5ErkJggg==&logoColor=white" alt="DonationAlerts" height="36"></a>

**Крипто (USDT):**

| Сеть | Адрес |
|---|---|
| TON | `UQBJnm86z1fPPycbWPB1EJmYvM3kSxqGP5Xsj7MGqjhFb_og` |
| TRC-20 | `TQZ16G4jz44TxTnKkqwbc9GXYx8CR4yTVj` |
| ERC-20 | `0x64FF8A5eEf5f0F9E3E010FC368FAA278475cF795` |
| BEP-20 | `0x8763F035C6C57E7Ac2046352e21a71F002f65fe9` |

---

<p align="center">
  <sub>Сделано для тех, кто верит что Telegram должен жить.</sub>
</p>
