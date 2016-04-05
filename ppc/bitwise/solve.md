# UFO CTF School 2016 : bitwise

**Category:** ppc **Points:** 100
**Author:** adminlp 

**Description:**

> 	RU: Флагом является ввод, при котором программа печатает 'Success!'
	ENG: The flag is input, in which the program prints 'Success!'

## Write_up

Пишем скрипт и получаем пароль:
```python
verify_arr = [193, 35, 9, 33, 1, 9, 3, 33, 9, 225]
password = ""

for i in range(0,10):
  for j in range(1,256):
    k = (((j << 5) | (j >> 3)) ^ 111) & 255
    if k == verify_arr[i]:
      password = password + chr(j)

print(password)
```
## Flag

> **flag{ub3rs3cr3t}**
