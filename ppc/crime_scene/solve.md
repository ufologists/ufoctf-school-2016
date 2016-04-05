# UFO CTF School 2016 : Сrime scene

**Category:** PPC **Points:** 200
**Author:** kit_sbg 

**Description:**
>  RU: Наши агенты уже прибыли на место. Но ничего кроме запароленной системы они не смогли найти. Может быть ты сможешь взломать систему как настоящий hackerman?Говорят у тебя лучший балл по тестам был. Так вот. Мы ждем от тебя пароль
>  ENG: Our agents have already arrived at the scene. But nothing except the password-protected system, they could not find. Maybe you'll be able to crack the system as a real hackerman?They say you got a better score on the test was. So. We expect from you the password.


## Write_up

На картинке в блокноте записан кусочки sha-256 от пароля, которые нужно сконкатенировать.  
Буквы используемые в пароле можно увидеть на клавиатуре через **stegsolve**.  
На одном из слоев появляются отпечатки пальцев. Таким образом можно определить длину пароля и его "алфавит".  
Далее брут пароля. Пароль-флаг **nevshtql***

## Flag

> **flag{nevshtql}**
