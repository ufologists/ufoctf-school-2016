# UFO CTF School 2016 : qr puzzle

**Category:** Stegano **Points:** 200
**Author:** kit_sbg 

**Description:**
>   RU: Нам кажется что это картинка часть чего-то большего. Разберись с ней  
>  	ENG: We think that this picture is a part of something bigger. Deal with it


## Write_up

В архиве лежит картинка CTF.png. После данных самой картинки записаны данные еще одного архива ufo_ctf.zip. Его нужно извлечь.
В нем будут лежать еще 5 картинок:
*    1.png
*    2.png
*    3.png
*    4.png
*    5.png

В каждой из картинок так же спрятаны по еще одному архиву. Каждый содержит по одной картинке, соответственно:
*    1_часть.png
*    2_часть.png
*    3_часть.png
*    4_часть.png
*    5\_часть.png

В 5\_часть.png содержится еще один архив, содержащий 6\_часть.png  
Каждая их картинок содержит одну из 6 частей qr-кода.  
Прочитать код можно только собрав все 6 частей.  
Собрав все 6 частей в правильном порядке [1 - левый нижний угол, и дальше по порядку по часовой стрелке, 5 - правый нижний угол, 6 правая часть] получается qr-code.  
Содержимое кода является флагом

## Flag

> **flag{dO_yOU_L1Ke_qr_P1zz4}**
