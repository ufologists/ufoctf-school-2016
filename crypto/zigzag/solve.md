# UFO CTF School 2016 : zigzag

**Category:** crypto **Points:** 50
**Author:** innhunter 

**Description:**

> RU: Давай выясним, насколько ты крут! Найди флаг!!  
> ENG: Let's find out how tough you are! Find the Flag!!

## Write_up

> cRWnek}oesc.wf,F,--r-fhhyoeTo-rmured'e-AryibeosY-r-latyr-so{reugedraa--llf

С помощью google понимаем, что был использован Rail Fence Cipher.

Находим декодер, например, http://www.geocachingtoolbox.com/index.php?page=railFenceCipher и пытаемся подобрать сдвиг.  
В данном случае сдвиг равен 19. Но еще нужно подобрать оффсет равный 1.  
В итоге получаем текст с флагом:

**Wow,-you're-a-real-destroyer-of-fences,-here-is-your-flag{rlYbAdmThrFckR}.**

## Flag

> **flag{rlYbAdmThrFckR}**
