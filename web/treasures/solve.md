# UFO CTF School 2016 : treasures

**Category:** web **Points:** 150
**Author:** chogori 

**Description:**

> *RU*:Заговорщики снова в деле! они сделали что-то непонятное с одним из корабельных терминалов - на экране огромная надпись, в которой сказано, что они хотят сокровищ и анимация падающих монеток. Помогите нам разобраться с этим  
> *ENG*:The conspirators back in business ! they did that - something strange with one of the ship terminals - on a huge screen legend , which says that they want to treasure and animation of falling coins . Help us to deal with this

## Write_up

Открываем таск, видим:

![Screen_1.png](./img/Screen_1.png)

Пробуем вводить различные данные, но это приводит только к "Access denied". Долго мучаясь пробуя в url получить бэкапы, можно случайно найти магическую штуку php sources, для этого нужно в url написать "auth.phps" и данный файл успешно скачается с сервера

![Screen_2.png](./img/Screen_2.png)

Открываем:

![Screen_3.png](./img/Screen_3.png)

Вводим логин и пароль:

![Screen_4.png](./img/Screen_4.png)

## Flag

> **flag{wHAt_IS_PhpS?}**
