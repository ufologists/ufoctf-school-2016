# UFO CTF School 2016 : abcdefgh

**Category:** Crypto **Points:** 100
**Author:** kit_sbg 

**Description:**
>   RU: Мы перехватили зашифрованное сообщение. Расшифруй его  
>  	ENG: We intercepted an encrypted message. Decipher it


## Write_up

Имеется зашифрованное сообщение:  
> bac bai jh bad bcd gf bbf jj ej ej jf hh jh bbf bbg fb ic bcf

Каждое *слово* являеется отдельной частью:  
> ['bac', 'bai', 'jh', 'bad', 'bcd', 'gf', 'bbf', 'jj', 'ej', 'ej', 'jf', 'hh', 'jh', 'bbf', 'bbg', 'fb', 'ic', 'bcf']

Заменяем каждую букву ее порядковым номером в алфавите(начиная с 0)
> [abcde/01234]:  
[102, 108, 97, 103, 123, 65, 115, 99, 49, 49, 95, 77, 97, 115, 116, 51, 82, 125]

Полученные цифры являются ASCII-кодом, заменяем на их значения
> [102 = f, 97 = a]:  
['f', 'l', 'a', 'g', '{', 'A', 's', 'c', '1', '1', ' _ ' , 'M', 'a', 's', 't', '3', 'R', '}']

Соединяем в одно слово и получаем флаг:

**flag{Asc11_Mast3R}**

## Flag

> **flag{Asc11_Mast3R}**
