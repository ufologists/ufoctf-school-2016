# UFO CTF School 2016 : UFOdump

**Category:** forensic **Points:** 300
**Author:** innhunter 

**Description:**

> RU: Пришельцы похитили одну из наших рабочих машин с флагом, но нам удалось сделать ее дамп памяти. Попробуй его найти.  
> ENG: The aliens stolen one of your machines working with the flag, but we have done a memory dump. Try to find it.


## Write_up

Скачиваем архив. Открываем его с помощью *volatility*
```
volatility imageinfo -f mem.raw
Volatility Foundation Volatility Framework 2.4
Determining profile based on KDBG search...

          Suggested Profile(s) : Win2008R2SP0x64, Win7SP1x64, Win7SP0x64, Win2008R2SP1x64
                     AS Layer1 : AMD64PagedMemory (Kernel AS)
                     AS Layer2 : FileAddressSpace (/root/Desktop/meme.raw)
                      PAE type : No PAE
                           DTB : 0x187000L
                          KDBG : 0xf800028080a0
          Number of Processors : 1
     Image Type (Service Pack) : 1
                KPCR for CPU 0 : 0xfffff80002809d00L
             KUSER_SHARED_DATA : 0xfffff78000000000L
           Image date and time : 2016-02-26 07:35:28 UTC+0000
     Image local date and time : 2016-02-26 11:35:28 +0400
```

Используем профиль из предложенных и получаем список процессов.
```
volatility pslist --profile Win7SP1x64 -f mem.raw
Volatility Foundation Volatility Framework 2.4
Offset(V)          Name                    PID   PPID   Thds     Hnds   Sess  Wow64 Start                          Exit                          
------------------ -------------------- ------ ------ ------ -------- ------ ------ ------------------------------ ------------------------------
0xfffffa8000396040 System                    4      0     70      480 ------      0 2016-02-26 06:31:06 UTC+0000                                 
0xfffffa8000b0a040 smss.exe                212      4      2       29 ------      0 2016-02-26 06:31:06 UTC+0000                                 
0xfffffa8000bfb890 csrss.exe               284    276      9      368      0      0 2016-02-26 06:31:14 UTC+0000                                 
0xfffffa8000be46b0 wininit.exe             320    276      3       77      0      0 2016-02-26 06:31:14 UTC+0000                                 
0xfffffa8000bdbb30 csrss.exe               328    312      7      206      1      0 2016-02-26 06:31:14 UTC+0000                                 
0xfffffa8000bd33d0 winlogon.exe            356    312      6      118      1      0 2016-02-26 06:31:14 UTC+0000                                 
0xfffffa80012f8360 services.exe            416    320      8      187      0      0 2016-02-26 06:31:14 UTC+0000                                 
0xfffffa800130cb30 lsass.exe               424    320      6      531      0      0 2016-02-26 06:31:14 UTC+0000                                 
0xfffffa800130db30 lsm.exe                 432    320     10      140      0      0 2016-02-26 06:31:14 UTC+0000                                 
0xfffffa80013615a0 svchost.exe             540    416     10      350      0      0 2016-02-26 06:31:15 UTC+0000                                 
0xfffffa8001388b30 VBoxService.ex          600    416     12      110      0      0 2016-02-26 06:31:15 UTC+0000                                 
0xfffffa800139db30 svchost.exe             664    416      7      257      0      0 2016-02-26 07:31:16 UTC+0000                                 
0xfffffa80013d0520 svchost.exe             748    416     20      447      0      0 2016-02-26 07:31:17 UTC+0000                                 
0xfffffa80013f25c0 svchost.exe             796    416     21      434      0      0 2016-02-26 07:31:17 UTC+0000                                 
0xfffffa8001406b30 svchost.exe             824    416     35      945      0      0 2016-02-26 07:31:17 UTC+0000                                 
0xfffffa80014383b0 audiodg.exe             908    748      6      125      0      0 2016-02-26 07:31:17 UTC+0000                                 
0xfffffa8001469800 svchost.exe             984    416     11      260      0      0 2016-02-26 07:31:17 UTC+0000                                 
0xfffffa8001497b30 svchost.exe             332    416     16      351      0      0 2016-02-26 07:31:17 UTC+0000                                 
0xfffffa80014f9b30 spoolsv.exe            1120    416     13      285      0      0 2016-02-26 07:31:18 UTC+0000                                 
0xfffffa8001542b30 svchost.exe            1148    416     19      306      0      0 2016-02-26 07:31:18 UTC+0000                                 
0xfffffa80015b1b30 svchost.exe            1240    416     12      179      0      0 2016-02-26 07:31:18 UTC+0000                                 
0xfffffa8000c45b30 taskhost.exe           1784    416     10      169      1      0 2016-02-26 07:31:47 UTC+0000                                 
0xfffffa80014cd810 dwm.exe                1844    796      4       71      1      0 2016-02-26 07:31:47 UTC+0000                                 
0xfffffa80015df6a0 explorer.exe           1864   1828     36      942      1      0 2016-02-26 07:31:48 UTC+0000                                 
0xfffffa8001757b30 VBoxTray.exe           1048   1864     12      169      1      0 2016-02-26 07:31:50 UTC+0000                                 
0xfffffa80015f6320 SearchIndexer.         1656    416     15      589      0      0 2016-02-26 07:31:55 UTC+0000                                 
0xfffffa800120fb30 SearchProtocol         1984   1656      6      220      1      0 2016-02-26 07:31:56 UTC+0000                                 
0xfffffa800147d3f0 sppsvc.exe             1956    416      4      142      0      0 2016-02-26 07:33:20 UTC+0000                                 
0xfffffa8000b9d630 svchost.exe            1420    416     16      328      0      0 2016-02-26 07:33:20 UTC+0000                                 
0xfffffa8000676060 mspaint.exe            2036   1864      6      159      1      0 2016-02-26 07:34:08 UTC+0000                                 
0xfffffa8000624060 svchost.exe            1020    416      7      107      0      0 2016-02-26 07:34:08 UTC+0000                                 
0xfffffa8000627a90 WmiPrvSE.exe           2060    540      6      161      0      0 2016-02-26 07:34:09 UTC+0000                                 
0xfffffa8000694630 notepad.exe            2128   1864      1       64      1      0 2016-02-26 07:34:14 UTC+0000                                 
0xfffffa8000658820 svhst.exe              2352   1864      2       45      1      1 2016-02-26 07:34:34 UTC+0000                                 
0xfffffa80006d5060 conhost.exe            2364    328      2       55      1      0 2016-02-26 07:34:34 UTC+0000                                 
0xfffffa800060d060 WMIADAP.exe            2432    824      6       86      0      0 2016-02-26 07:35:19 UTC+0000                                 
0xfffffa80017c4410 WmiPrvSE.exe           2468    540      8      117      0      0 2016-02-26 07:35:19 UTC+0000    
```
Видим процесс `mspaint PID 2036`. Дампим...
```
volatility memdump -p 2036 --profile Win7SP1x64 -f meme.raw --dump-dir /root/Desktop
Volatility Foundation Volatility Framework 2.4
************************************************************************
Writing mspaint.exe [  2036] to 2036.dmp
```
Переименовыеваем в `2036.data`

Запускаем GIMP -> Открыть как Raw Image Data. Далле играемся с ползунками (или если вы получили скриншот с машины, то на ней был запущен notepad.exe c указанием на размер картинки) и получаем четкое изображение с флагом.

![](./img/1.png)


## Flag

> **flag{we've come with peace(no)}**
