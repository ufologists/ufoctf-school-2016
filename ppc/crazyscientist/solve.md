# UFO CTF School 2016 : Calculate

**Category:** ppc **Points:** 100
**Author:** AfftaR 

**Description:**

> RU: Безумному ученому дали задание перехватить и расшифровать координаты маршрута следования кортежа Папы Римского для организации похищения инопланетными существами, помоги ему сделать это! Но помни Папа Римский не должен узнать об этом!  
ENG: Mad scientist were asked to intercept and decrypt Pope's path coordinates for the kidnapping by aliens, help him to do it! But remember the Pope shouldn't know about it!

## Write_up

Подключаемся к серверу, получаем строку

```
==gZjZWYzgHM * ==QYwYTN5gHM
```
Взглянув на строку, понимаем что это реверстнутый base64.  
Переворачиваем
```
MHg5NTYwYQ== * MHgzYWZjZg==
```
Расшифровываем
```
0x9560a * 0x3afcf
```
Переводим числа из HEX
```
611850 * 241615
```
Получаем ответ
```
147832137750
```
Теперь нам нужно его опять зашифровать (ведь Папа Римский не должен узнать что мы перехватили его координаты следования!)  
Переводим в HEX
```
226B7B6816
```
Шифруем и переворачиваем
```
==gNxgjNCdjQ2IjM
```
Теперь осталось отправить его на сервер и получить ответ **The answer is correct, but too long!**  
Ответ верный, но мы слишком медленные!  
Значит пришло время писать скрипт.  

```python
import socket
from base64 import b64encode, b64decode

sock = socket.socket()

sock.connect(('localhost', 14489))
data = sock.recv(1024)
print(data)
while True:
    data = sock.recv(1024)[:-1]
    data = data[::-1]
    print(data)
    data = str(data, encoding='utf8')
    test1 = data.split('*')
    res = b64encode(bytes(hex(int((b64decode(test1[0])), 16) *
          int((b64decode(test1[1])), 16)), encoding='utf8'))[::-1]
    print(res)
    sock.send(res)
```

После 64 попыток решения - получаем флаг **flag{eAsY_brEEzzzY}**

## Flag

> **flag{eAsY_brEEzzzY}**
