# UFO CTF School 2016 : press any key

**Category:** web **Points:** 100
**Author:** chogori 

**Description:**

> *RU*: Наш глупый админ решил добавить в наш бортовой компьютер немного функционала, но у него ничего не получается хорошо и теперь мы не можем найти важную для нас информацию. Помоги нам найти ее
> *ENG*: Our stupid admin decided to add to our onboard computer a bit functional , but he did not do well and now we can not find important information for us. Help us find her

## Write_up

Смотрим на таск и замечаем некоторые изменения в уже привычной нам картине - добавились несколько "волшебных" кнопок. Каждая из них при нажатии выводит цитату. Раз добавились только они, первым делом надо посмотреть все, что связанно с ними. Открыв js скрипты, видим, что они обфусцированы. Деобфусцировав все скрипты, можно увидеть, что флаг находится в скрипте 4 кнопки.

## Flag

> **flag{oNe_sHot_onE_FlaG}**
