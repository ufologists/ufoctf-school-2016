# UFO CTF School 2016 : Find Me

**Category:** forensic **Points:** 100
**Author:** AfftaR 

**Description:**

> *RU*: У нас в конторе админ работает с удаленной машиной как-то странно, попробуй понять как он это делает и найди пароль!  
> *ENG*: In our office, admin work to a remote machine as something strange, try to understand how he does it and find the password!

## Write_up

Открываем скаченный сетевой дамп **dump.pcapng**

Находим протокол **Telnet** с помощью фильстра 'telnet'

Проверяем его данные, видим флаг в строке 'Password'

## Flag

**flag{YoU_knOw_hoW_t()_u$e_w1re$harK}**
