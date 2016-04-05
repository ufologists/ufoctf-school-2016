# UFO CTF School 2016 : find_the_way

**Category:** web **Points:** 100
**Author:** chogori 

**Description:**

> *RU*: Где-то в должна быть очень важная информация, но после нашего глупого администратора мы ничего не может найти. Помоги нам, пожалуйста  
> *ENG*: Somewhere it must be very important information, but after our stupid Administrator 's nothing we can not find . Help us, please

## Write_up

Открываем таск, видим:

![Screen_1.png](./img/Screen_1.png)

Поковырявшись в сорсах находим интересную строчку:

![Screen_2.png](./img/Screen_2.png)

Думаю это какая-то директория на сервере, пробуем:

![Screen_3.png](./img/Screen_3.png)

Да, это действительно директория, переходим в директорию backup/

![Screen_4.png](./img/Screen_4.png)

Открываем и смотрим что внутри:

![Screen_5.png](./img/Screen_5.png)

## Flag

> **flag{hTtP_iNDExiNgGGg}**
