# UFO CTF School 2016 : stego_dark_side

**Category:** stegano **Points:** 150
**Author:** adminlp 

**Description:**

> 	RU: Что скрывает темная сторона?  
	ENG: What hides the dark side?

## Write_up

Открываем в 010 Editor. Запускаем PNG шаблон. Видим мусор в конце. Копируем в новый файл. Определяем, что это gif изображение. Вау, QR-код.
Сканируем, получаем hex строку, декодикуем, получаем base64, декодируем, получаем снова hex, Повторяем, пока не получим флаг.


## Flag

> **flag{W0WthisisBASE64}**
