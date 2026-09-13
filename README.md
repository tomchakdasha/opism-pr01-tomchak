# Практична робота № 1

**Дисципліна:** Основи побудови інформаційних систем та мереж

**Тема:** Спостереження за процесом звернення до вебресурсу. Побудова власної моделі рівнів взаємодії

| | |
|---|---|
| **Прізвище, ім'я** | Томчак Дар'я |
| **Група** | ІПЗ-2.01 |
| **Номер варіанта** | 26|
| **Домен варіанта** | ethz.ch |
| **Середовище виконання** | *Windows* |
| **Версія curl** | *curl 8.21.0 (Windows) libcurl/8.21.0 Schannel zlib/1.3.2 WinIDN WinLDAP* |
| **Дата виконання** | 13.09.2026 |

---

## Частина A. Збір експериментальних даних

### A.1. Запит із діагностичним виводом

**Команда:**

```
curl.exe -v https://ВАШ_ДОМЕН
```

**Вивід:**

```
PS D:\2.01\shcherba\opism-pr01-tomchak> curl.exe -v https://ethz.ch
* Host ethz.ch:443 was resolved.
* IPv6: (none)
* IPv4: 129.132.19.216
*   Trying 129.132.19.216:443...
* schannel: disabled automatic use of client certificate
* ALPN: curl offers http/1.1
* ALPN: server accepted http/1.1
* Established connection to ethz.ch (129.132.19.216 port 443) from 192.168.1.13 port 56966
* using HTTP/1.x
> GET / HTTP/1.1
> Host: ethz.ch
> User-Agent: curl/8.21.0
> Accept: */*
>
* Request completely sent off
* schannel: remote party requests renegotiation
* schannel: renegotiating SSL/TLS connection
* schannel: SSL/TLS connection renegotiated
* schannel: remote party requests renegotiation
* schannel: renegotiating SSL/TLS connection
* schannel: SSL/TLS connection renegotiated
< HTTP/1.1 301
< Date: Sun, 13 Sep 2026 08:32:59 GMT
< Server: Varnish
< X-Varnish: 514784259
< location: https://ethz.ch/de.html
< Content-Length: 0
< Connection: keep-alive
<
* Connection #0 to host ethz.ch:443 left intact
```

---

### A.2. Запит без захисту з'єднання

**Команда:**

```
curl.exe -v http://neverssl.com
```

**Вивід:**

```
PS D:\2.01\shcherba\opism-pr01-tomchak> curl.exe -v http://neverssl.com
* Host neverssl.com:80 was resolved.
* IPv6: (none)
* IPv4: 34.223.124.45
*   Trying 34.223.124.45:80...
* Established connection to neverssl.com (34.223.124.45 port 80) from 192.168.1.13 port 51837
* using HTTP/1.x
> GET / HTTP/1.1
> Host: neverssl.com
> User-Agent: curl/8.21.0
> Accept: */*
>
* Request completely sent off
< HTTP/1.1 200 OK
< Date: Sun, 13 Sep 2026 08:34:35 GMT
< Server: Apache/2.4.68 ()
< Upgrade: h2,h2c
< Connection: Upgrade
< Last-Modified: Wed, 29 Jun 2022 00:23:33 GMT
< ETag: "f79-5e28b29d38e93"
< Accept-Ranges: bytes
< Content-Length: 3961
< Vary: Accept-Encoding
< Content-Type: text/html; charset=UTF-8
<
<html>
        <head>
                <title>NeverSSL - Connecting ... </title>
                <style>
                body {
                        font-family: Montserrat, helvetica, arial, sans-serif;
                        font-size: 16x;
                        color: #444444;
                        margin: 0;
                }
                h2 {
                        font-weight: 700;
                        font-size: 1.6em;
                        margin-top: 30px;
                }
                p {
                        line-height: 1.6em;
                }
                .container {
                        max-width: 650px;
                        margin: 20px auto 20px auto;
                        padding-left: 15px;
                        padding-right: 15px
                }
                .header {
                        background-color: #42C0FD;
                        color: #FFFFFF;
                        padding: 10px 0 10px 0;
                        font-size: 2.2em;
                }
                .notice {
                        background-color: red;
                        color: white;
                        padding: 10px 0 10px 0;
                        font-size: 1.25em;
                        animation: flash 4s infinite;
                }
                @keyframes flash {
                0% {
                        background-color: red;
                }
                50% {
                        background-color: #AA0000;
                }
                0% {
                        background-color: red;
                }
                }
                <!-- CSS from Mark Webster https://gist.github.com/markcwebster/9bdf30655cdd5279bad13993ac87c85d -->
                </style>

                <script>
                        var adjectives = [ 'cool' , 'calm' , 'relaxed', 'soothing', 'serene', 'slow',
                                                        'beautiful', 'wonderful', 'wonderous', 'fun', 'good',
                                                        'glowing', 'inner', 'grand', 'majestic', 'astounding',
                                                        'fine', 'splendid', 'transcendent', 'sublime', 'whole',
                                                        'unique', 'old', 'young', 'fresh', 'clear', 'shiny',
                                                        'shining', 'lush', 'quiet', 'bright', 'silver' ];

                        var nouns =       [ 'day', 'dawn', 'peace', 'smile', 'love', 'zen', 'laugh',
                                                        'yawn', 'poem', 'song', 'joke', 'verse', 'kiss', 'sunrise',
                                                        'sunset', 'eclipse', 'moon', 'rainbow', 'rain', 'plan',
                                                        'play', 'chart', 'birds', 'stars', 'pathway', 'secret',
                                                        'treasure', 'melody', 'magic', 'spell', 'light', 'morning'];

                        var prefix =
                                        // Choose 3 zen adjectives
                                        adjectives.sort(function(){return 0.5-Math.random()}).slice(-3).join('')
                                        +
                                        // Coupled with a zen noun
                                        nouns.sort(function(){return 0.5-Math.random()}).slice(-1).join('');
                        window.location.href = 'http://' + prefix + '.neverssl.com/online';
                </script>
        </head>
        <body>
        <noscript>
                <div class="notice">
                        <div class="container">
                                ⚠️ JavaScript appears to be disabled. NeverSSL's cache-busting works better if you enable JavaScript for <code>neverssl.com</code>.
                        </div>
                </div>
        </noscript>
        <div class="header">
                <div class="container">
                <h1>NeverSSL</h1>
                </div>
        </div>
        <div class="content">
        <div class="container">

        <h1 id="status"></h1>
        <script>document.querySelector("#status").textContent = "Connecting ...";</script>
        <noscript>

                <h2>What?</h2>
                <p>This website is for when you try to open Facebook, Google, Amazon, etc
                on a wifi network, and nothing happens. Type "http://neverssl.com"
                into your browser's url bar, and you'll be able to log on.</p>

                <h2>How?</h2>
                <p>neverssl.com will never use SSL (also known as TLS). No
                encryption, no strong authentication, no <a
                href="https://en.wikipedia.org/wiki/HTTP_Strict_Transport_Security">HSTS</a>,
                no HTTP/2.0, just plain old unencrypted HTTP and forever stuck in the dark
                ages of internet security.</p>

                <h2>Why?</h2>
                <p>Normally, that's a bad idea. You should always use SSL and secure
                encryption when possible. In fact, it's such a bad idea that most websites
                are now using https by default.</p>

                <p>And that's great, but it also means that if you're relying on
                poorly-behaved wifi networks, it can be hard to get online.  Secure
                browsers and websites using https make it impossible for those wifi
                networks to send you to a login or payment page. Basically, those networks
                can't tap into your connection just like attackers can't. Modern browsers
                are so good that they can remember when a website supports encryption and
                even if you type in the website name, they'll use https.</p>

                <p>And if the network never redirects you to this page, well as you can
                see, you're not missing much.</p>

        <a href="https://twitter.com/neverssl">Follow @neverssl</a>

        </noscript>

        </div>
        </div>

        </body>
</html>
* Connection #0 to host neverssl.com:80 left intact
```

---

### A.3. Запит до служби доменних імен

*Windows: `Resolve-DnsName ВАШ_ДОМЕН`*

**Команда (перше виконання):**

```
Resolve-DnsName ВАШ_ДОМЕН
```

**Вивід:**

```
PS D:\2.01\shcherba\opism-pr01-tomchak> Resolve-DnsName ethz.ch

Name                                           Type   TTL   Section    IPAddress
----                                           ----   ---   -------    ---------
ethz.ch                                        AAAA   41    Answer     2001:67c:10ec:254::216
ethz.ch                                        A      84    Answer     129.132.19.216

PS D:\2.01\shcherba\opism-pr01-tomchak> nslookup -debug ethz.ch
------------
Got answer:
    HEADER:
        opcode = QUERY, id = 1, rcode = NOERROR
        header flags:  response, want recursion, recursion avail.
        questions = 1,  answers = 1,  authority records = 0,  additional = 0

    QUESTIONS:
        8.8.8.8.in-addr.arpa, type = PTR, class = IN
    ANSWERS:
    ->  8.8.8.8.in-addr.arpa
        name = dns.google
        ttl = 9048 (2 hours 30 mins 48 secs)

------------
Server:  dns.google
Address:  8.8.8.8

------------
Got answer:
    HEADER:
        opcode = QUERY, id = 2, rcode = NXDOMAIN
        header flags:  response, want recursion, recursion avail.
        questions = 1,  answers = 0,  authority records = 1,  additional = 0

    QUESTIONS:
        ethz.ch.NetisRouter_e4beed5d4000, type = A, class = IN
    AUTHORITY RECORDS:
    ->  (root)
        ttl = 86399 (23 hours 59 mins 59 secs)
        primary name server = a.root-servers.net
        responsible mail addr = nstld.verisign-grs.com
        serial  = 2026091300
        refresh = 1800 (30 mins)
        retry   = 900 (15 mins)
        expire  = 604800 (7 days)
        default TTL = 86400 (1 day)

------------
------------
Got answer:
    HEADER:
        opcode = QUERY, id = 3, rcode = NXDOMAIN
        header flags:  response, want recursion, recursion avail.
        questions = 1,  answers = 0,  authority records = 1,  additional = 0

    QUESTIONS:
        ethz.ch.NetisRouter_e4beed5d4000, type = AAAA, class = IN
    AUTHORITY RECORDS:
    ->  (root)
        ttl = 86340 (23 hours 59 mins)
        primary name server = a.root-servers.net
        responsible mail addr = nstld.verisign-grs.com
        serial  = 2026091300
        refresh = 1800 (30 mins)
        retry   = 900 (15 mins)
        expire  = 604800 (7 days)
        default TTL = 86400 (1 day)

------------
------------
Got answer:
    HEADER:
        opcode = QUERY, id = 4, rcode = NOERROR
        header flags:  response, want recursion, recursion avail.
        questions = 1,  answers = 1,  authority records = 0,  additional = 0

    QUESTIONS:
        ethz.ch, type = A, class = IN
    ANSWERS:
    ->  ethz.ch
        internet address = 129.132.19.216
        ttl = 209 (3 mins 29 secs)

------------
Non-authoritative answer:
------------
Got answer:
    HEADER:
        opcode = QUERY, id = 5, rcode = NOERROR
        header flags:  response, want recursion, recursion avail.
        questions = 1,  answers = 1,  authority records = 0,  additional = 0

    QUESTIONS:
        ethz.ch, type = AAAA, class = IN
    ANSWERS:
    ->  ethz.ch
        AAAA IPv6 address = 2001:67c:10ec:254::216
        ttl = 2560 (42 mins 40 secs)

------------
Name:    ethz.ch
Addresses:  2001:67c:10ec:254::216
          129.132.19.216
```

**Команда (повторне виконання через 5–7 хвилин):**

```
Resolve-DnsName ВАШ_ДОМЕН
```

**Вивід:**

```
PS D:\2.01\shcherba\opism-pr01-tomchak> Resolve-DnsName ethz.ch

Name                                           Type   TTL   Section    IPAddress
----                                           ----   ---   -------    ---------
ethz.ch                                        AAAA   3171  Answer     2001:67c:10ec:254::216
ethz.ch                                        A      219   Answer     129.132.19.216


PS D:\2.01\shcherba\opism-pr01-tomchak> nslookup -debug ethz.ch
------------
Got answer:
    HEADER:
        opcode = QUERY, id = 1, rcode = NOERROR
        header flags:  response, want recursion, recursion avail.
        questions = 1,  answers = 1,  authority records = 0,  additional = 0

    QUESTIONS:
        8.8.8.8.in-addr.arpa, type = PTR, class = IN
    ANSWERS:
    ->  8.8.8.8.in-addr.arpa
        name = dns.google
        ttl = 8543 (2 hours 22 mins 23 secs)

------------
Server:  dns.google
Address:  8.8.8.8

------------
Got answer:
    HEADER:
        opcode = QUERY, id = 2, rcode = NXDOMAIN
        header flags:  response, want recursion, recursion avail.
        questions = 1,  answers = 0,  authority records = 1,  additional = 0

    QUESTIONS:
        ethz.ch.NetisRouter_e4beed5d4000, type = A, class = IN
    AUTHORITY RECORDS:
    ->  (root)
        ttl = 86399 (23 hours 59 mins 59 secs)
        primary name server = a.root-servers.net
        responsible mail addr = nstld.verisign-grs.com
        serial  = 2026091300
        refresh = 1800 (30 mins)
        retry   = 900 (15 mins)
        expire  = 604800 (7 days)
        default TTL = 86400 (1 day)

------------
------------
Got answer:
    HEADER:
        opcode = QUERY, id = 3, rcode = NXDOMAIN
        header flags:  response, want recursion, recursion avail.
        questions = 1,  answers = 0,  authority records = 1,  additional = 0

    QUESTIONS:
        ethz.ch.NetisRouter_e4beed5d4000, type = AAAA, class = IN
    AUTHORITY RECORDS:
    ->  (root)
        ttl = 86399 (23 hours 59 mins 59 secs)
        primary name server = a.root-servers.net
        responsible mail addr = nstld.verisign-grs.com
        serial  = 2026091300
        refresh = 1800 (30 mins)
        retry   = 900 (15 mins)
        expire  = 604800 (7 days)
        default TTL = 86400 (1 day)

------------
------------
Got answer:
    HEADER:
        opcode = QUERY, id = 4, rcode = NOERROR
        header flags:  response, want recursion, recursion avail.
        questions = 1,  answers = 1,  authority records = 0,  additional = 0

    QUESTIONS:
        ethz.ch, type = A, class = IN
    ANSWERS:
    ->  ethz.ch
        internet address = 129.132.19.216
        ttl = 200 (3 mins 20 secs)

------------
Non-authoritative answer:
------------
Got answer:
    HEADER:
        opcode = QUERY, id = 5, rcode = NOERROR
        header flags:  response, want recursion, recursion avail.
        questions = 1,  answers = 1,  authority records = 0,  additional = 0

    QUESTIONS:
        ethz.ch, type = AAAA, class = IN
    ANSWERS:
    ->  ethz.ch
        AAAA IPv6 address = 2001:67c:10ec:254::216
        ttl = 3152 (52 mins 32 secs)

------------
Name:    ethz.ch
Addresses:  2001:67c:10ec:254::216
          129.132.19.216
```

**Зафіксовані значення:**

| Параметр | Перше виконання | Повторне виконання |
|---|---|---|
| Час виконання (год:хв) | 11:32 | 11:45 |
| IP-адреса | IPv6: 2001:67c:10ec:254::216 <br> IPv4: 129.132.19.216 | IPv6: 2001:67c:10ec:254::216 <br> IPv4: 129.132.19.216 |
| Значення TTL | IPv6: 41 <br> IPv4: 84  | IPv6: 3171 <br> IPv4: 219 |

> Якщо друге значення TTL виявилося більшим за перше — це нормально: кеш резолвера встиг оновитися. Зафіксуйте як є.

---

### A.4. Контрольний ресурс

**Команда:**

```
curl.exe -v https://google.com
```

**Вивід:**

```
PS D:\2.01\shcherba\opism-pr01-tomchak> curl.exe -v https://google.com
*   Trying 142.250.120.139:443...
* Host google.com:443 was resolved.
* IPv6: (none)
* IPv4: 142.250.120.139, 142.250.120.102, 142.250.120.138, 142.250.120.101, 142.250.120.113, 142.250.120.100
* schannel: disabled automatic use of client certificate
* ALPN: curl offers http/1.1
* ALPN: server accepted http/1.1
* Established connection to google.com (142.250.120.139 port 443) from 192.168.1.13 port 60828
* using HTTP/1.x
> GET / HTTP/1.1
> Host: google.com
> User-Agent: curl/8.21.0
> Accept: */*
>
* Request completely sent off
* schannel: remote party requests renegotiation
* schannel: renegotiating SSL/TLS connection
* schannel: SSL/TLS connection renegotiated
< HTTP/1.1 301 Moved Permanently
< Location: https://www.google.com/
< Content-Type: text/html; charset=UTF-8
< Content-Security-Policy-Report-Only: object-src 'none';base-uri 'self';script-src 'nonce-_QjG2yLhMnOJg2AXTj8CWw' 'strict-dynamic' 'report-sample' 'unsafe-eval' 'unsafe-inline' https: http:;report-uri https://csp.withgoogle.com/csp/gws/other-hp
< Date: Sun, 13 Sep 2026 09:05:18 GMT
< Expires: Tue, 13 Oct 2026 09:05:18 GMT
< Cache-Control: public, max-age=2592000
< Server: gws
< Content-Length: 220
< X-XSS-Protection: 0
< X-Frame-Options: SAMEORIGIN
< Alt-Svc: h3=":443"; ma=2592000,h3-29=":443"; ma=2592000
<
<HTML><HEAD><meta http-equiv="content-type" content="text/html;charset=utf-8">
<TITLE>301 Moved</TITLE></HEAD><BODY>
<H1>301 Moved</H1>
The document has moved
<A HREF="https://www.google.com/">here</A>.
</BODY></HTML>
* Connection #0 to host google.com:443 left intact
```

---

### A.5. Ресурси з некоректною конфігурацією сертифіката

**Випадок 1**

```
curl.exe -v https://expired.badssl.com
```

```
PS D:\2.01\shcherba\opism-pr01-tomchak> curl.exe -v https://expired.badssl.com
*   Trying 104.154.89.105:443...
* Host expired.badssl.com:443 was resolved.
* IPv6: (none)
* IPv4: 104.154.89.105
* schannel: disabled automatic use of client certificate
* ALPN: curl offers http/1.1
* schannel: next InitializeSecurityContext failed: SEC_E_CERT_EXPIRED (0x80090328) - The received certificate has expired.
* closing connection #0
curl: (35) schannel: next InitializeSecurityContext failed: SEC_E_CERT_EXPIRED (0x80090328) - The received certificate has expired.
```

**Випадок 2**

```
curl.exe -v https://wrong.host.badssl.com
```

```
PS D:\2.01\shcherba\opism-pr01-tomchak> curl.exe -v https://wrong.host.badssl.com
*   Trying 104.154.89.105:443...
* Host wrong.host.badssl.com:443 was resolved.
* IPv6: (none)
* IPv4: 104.154.89.105
* schannel: disabled automatic use of client certificate
* ALPN: curl offers http/1.1
* schannel: SNI or certificate check failed: SEC_E_WRONG_PRINCIPAL (0x80090322) - The target principal name is incorrect.
* closing connection #0
curl: (60) schannel: SNI or certificate check failed: SEC_E_WRONG_PRINCIPAL (0x80090322) - The target principal name is incorrect.
More details here: https://curl.se/docs/sslcerts.html

curl failed to verify the legitimacy of the server and therefore could not
establish a secure connection to it. To learn more about this situation and
how to fix it, please visit the webpage mentioned above.
```

**Випадок 3**

```
curl.exe -v https://self-signed.badssl.com
```

```
PS D:\2.01\shcherba\opism-pr01-tomchak> curl.exe -v https://self-signed.badssl.com
* Host self-signed.badssl.com:443 was resolved.
* IPv6: (none)
* IPv4: 104.154.89.105
*   Trying 104.154.89.105:443...
* schannel: disabled automatic use of client certificate
* ALPN: curl offers http/1.1
* schannel: SEC_E_UNTRUSTED_ROOT (0x80090325) - The certificate chain was issued by an authority that is not trusted.
* closing connection #0
curl: (60) schannel: SEC_E_UNTRUSTED_ROOT (0x80090325) - The certificate chain was issued by an authority that is not trusted.
More details here: https://curl.se/docs/sslcerts.html

curl failed to verify the legitimacy of the server and therefore could not
establish a secure connection to it. To learn more about this situation and
how to fix it, please visit the webpage mentioned above.
```

> Якщо використано альтернативний спосіб із параметром `--resolve` — зазначити це та навести фактичну команду.

---

## Частина B. Власна модель рівнів

**Кількість виділених груп:** ___

| № | Назва групи (власне формулювання) | Рядки виводу, віднесені до групи | Обґрунтування |
|---|---|---|---|
| 1 | Запит і відповідь | > GET / HTTP/1.1 <br> > Host: ethz.ch <br> > User-Agent: curl/8.21.0 <br> > Accept: */* <br> < HTTP/1.1 301 <br> < Server: Varnish <br> < location: [https://ethz.ch/de.html](https://ethz.ch/de.html) <br> < Content-Length: 0 <br> < Connection: keep-alive| У цих рядках відбувається комунікація між сервером та комп'ютером, де комп'ютер просить надати інформацію про сайт, а сервер йому відповідає, що цей сайт тепер має іншу адресу |
| 2 | Перевірка справжності та шифрування | * ALPN: curl offers http/1.1 <br> * ALPN: server accepted http/1.1 <br> * schannel: renegotiating SSL/TLS connection | Комп'ютер і сервер домовляються використовувати версію протоколу http/1.1 та оновлюється безпечне шифроване з'єднання |
| 3 | З'єднання, порти та доставка  | * Trying 129.132.19.216:443... <br> * Established connection to ethz.ch ... port 443 <br> * using HTTP/1.x | Встановлюється з'єднання з портом сервера |
| 4 | Адреса в мережі та маршрут| * Host ethz.ch:443 was resolved. <br> * IPv6: (none) <br> * IPv4: 129.132.19.216 | Знаходять хост в мережі, його адресу та маршрут для передання пакетів |

*Групи впорядковано від найближчої до користувача (№ 1) до найближчої до апаратного забезпечення. Зайві рядки вилучити, за потреби — додати.*

**Рядки, які не вдалося віднести до жодної групи:**

| Рядок виводу | Причина утруднення |
|---|---|
| * Request completely sent off | Повідомлення про завершення відправки запиту |
| * Connection #0 to host ethz.ch:443 left intact | Повідомлення про те, що зв'язок з сервером не розірвано|

---

## Контрольні питання

**1. Скільки рядків діагностичного виводу передує отриманню даних сторінки (завдання A.1)?**

> 21

**2. Які рядки наявні у виводі A.1 і відсутні у виводі A.2? Чим це зумовлено?**

> У завданні А.2 відсутні рядки, що стосуються безпеки та шифровки з'єднання, бо там в завданні А.1 сайт має протокол https, що має захищене з'єднання, а тут http. У завданні А.1 присутні такі рядки, що стосуються захищенного з'єднання: <br> * schannel: disabled automatic use of client certificate <br> * ALPN: curl offers http/1.1 <br> * ALPN: server accepted http/1.1 

**3. Звідки у виводі з'явилося значення `443`, якщо його не було вказано в адресі?**

> 443 це порт за замовчуванням для https

**4. Як змінилося значення TTL між двома запитами (A.3)? Що означає це число?**

> Значення TTL зросло як для IPv6 з 41 до 3171, так і для IPv4 з 84 до 219, це означає, що кеш встиг оновитися, а саме число це залишок часу життя в кеші резолвера

**5. Чим відрізняються між собою три причини помилок із завдання A.5? Сформулювати кожну однією фразою.**

| Випадок | Причина недовіри |
|---|---|
| `expired` | Час дії сертифікату закінчився |
| `wrong.host` | Невідповідність адреси тій, що є в сертифікаті |
| `self-signed` | Відсутність третьої сторони, що підтвердила б сертифікат |

**6. Три рядки з власних виводів, про які не йшлося на лекції 1:**

| № | Рядок виводу | Джерело (номер завдання) |
|---|---|---|
| 1 | * schannel: disabled automatic use of client certificate | А.1 |
| 2 | * ALPN: curl offers http/1.1 | А.1 |
| 3 | < X-Varnish: 514784259 | А.1 |

*Пояснення до цих рядків не потрібне.*

---

## Висновки

*150–300 слів. Спиратися на власні спостереження, а не на матеріал лекції.*

**D.1. Що виявилося неочевидним або несподіваним**

*Назвати конкретно, з посиланням на рядок виводу.*

> Несподіванкою для мене стала наявність великої кількості комунікацій між сервером та комп'ютером, яку ми зазвичай не бачимо, а саме те, як комп'ютер запрошує інформацію у сервера
```
> GET / HTTP/1.1
```
 перевіряє захищеність з'єднання та сертифікати
 ```
 * schannel: renegotiating SSL/TLS connection
 ```
 домовляється з сервером щодо версії використовуваного протоколу
 ```
 * ALPN: curl offers http/1.1
 ```
 наявність двох IP адрес, IPv6 та IPv4, або ж однієї
 ```
 * IPv4: 129.132.19.216
 ```
 зміна адреси сайту, як це відбулося в завданні А.1
 ```
 < HTTP/1.1 301
 ```
 а також можливі помилки та їх причини, що стосуються сертифікатів

**D.2. Чому саме така кількість груп у частині B**

*На якій підставі ухвалено рішення. Що змусило б його змінити.*

> В частині В у мене вийшло всього 4 групи, тому що, переглядаючи рядки, я сортувала їх за схожими ознаками та сферами, за які відповідають ці рядки. До прикладу, запитам або прийняттю інформації, визначенню захищеності, з'єднанню чи доставці, або ж адресам. В інших рядках виявити збіги за якимись ознаками не вдалося, тому я не створила більшу кількість груп. Якби було виявлено рядки, які стосувалися б іншої сфери, яка не схожа на попередні 4 групи, це б змусило змінити моє рішення та додати п'яту групу

**D.3. Питання, яке залишилося без відповіді**

> Особисто мені став не зрозумілим рядок 
 ```
< X-Varnish: 514784259 
 ```
і яку саме функцію він виконує

---

## Використання штучного інтелекту

*Розділ обов'язковий. Заповнюється незалежно від того, чи використовувався ШІ. Детальні вимоги — у документі «Політика використання технологій штучного інтелекту».*

**Факт використання:** використано / не використано *(потрібне залишити)*

**Установлений рівень для цієї роботи:** Р3 — ШІ як співвиконавець

**Фактичний рівень використання:** Р1

### Використані системи

| Система | Версія або модель | Період використання |
|---|---|---|
| | | |

### Промпти

*Наводити дослівно, у тому вигляді, у якому запит було надано системі. Переказ не приймається.*

| № | Розділ роботи | Текст промпта |
|---|---|---|
| 1 | | |
| 2 | | |
| 3 | | |

### Дії з отриманим результатом

| № промпта | Що перевірено | Що змінено | Що відхилено і чому |
|---|---|---|---|
| 1 | | | |
| 2 | | | |
| 3 | | | |

### Підтвердження

Підтверджую, що всі наведені в цьому звіті виводи команд отримано мною особисто внаслідок фактичного виконання відповідних дій, а відомості цього розділу є повними та достовірними.

> Виводи `curl`, `dig` та інші артефакти не можуть бути згенеровані. Це стосується будь-якого рівня використання ШІ.

---

## Примітки виконавця

*(необов'язковий розділ: що не спрацювало, які команди довелося змінити, які виникли труднощі)*

> 
