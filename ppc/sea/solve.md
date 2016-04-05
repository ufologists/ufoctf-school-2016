# UFO CTF School 2016 : Black sea

**Category:** PPC **Points:** 200
**Author:** kit_sbg 

**Description:**
> RU: We're trying to decipher this file for many years. Unfortunately part of the program has not survived to our days.No we know for sure that the key 'chtsrazstb'. As usual, all hope only on you  
> ENG: Мы пытаемся расшифровать этот файл уже много лет. К сожалению часть программы не сохранилась до наших дней. Но мы знаем точно что ключ 'chtsrazstb'. Как обычно, вся надежда только на тебя


## Write_up

Есть функция с помощью которой зашифровали файл. Нужно написать функцию дешифровки.  
Если посмотреть внимательно код можно понять, что это шифр AES-128 (Rijendael).  
Можно дописать функцию самому, можно было поискать готовый код.
Недостающая функция:
```python
def decrypt(cipher, key):
    state = [[] for i in range(nb)]
    for r in range(4):
        for c in range(nb):
            state[r].append(cipher[r + 4 * c])

    key_schedule = key_expansion(key)

    state = add_round_key(state, key_schedule, nr)

    rnd = nr - 1
    while rnd >= 1:
        state = shift_rows(state, inv=True)
        state = sub_bytes(state, inv=True)
        state = add_round_key(state, key_schedule, rnd)
        state = mix_columns(state, inv=True)

        rnd -= 1
    state = shift_rows(state, inv=True)
    state = sub_bytes(state, inv=True)
    state = add_round_key(state, key_schedule, rnd)

    output = [None for i in range(4 * nb)]
    for r in range(4):
        for c in range(nb):
            output[r + 4 * c] = state[r][c]

    return output
```
Воспользоваться ключем, данным в описании и расшифровать файл.  
Флаг в картинке, написан на вместо марки телефона

## Flag

> **flag{UFO_PHon3}**
