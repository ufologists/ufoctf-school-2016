# UFO CTF School 2016 : colored squares

**Category:** web **Points:** 300
**Author:** chogori 

**Description:**

> *RU*: Мы пролетаем мимо какой-то одинокой планеты. Планета не заселена и вообще никакой жизни не этой планете не может существовать. Но вдруг мы стали получать непонятный сигнал с этой планеты. Мы не знаем, что это за сигнал. Помоги нам понять что это 
> *ENG*: We flew by some lonely planet. The planet is not inhabited , and in general any life this planet can not exist . But then we began to receive strange signal from this planet . We do not know what kind of signal. Help us to understand that this

## Write_up

Открываем таск, замечаем то, что нам якобы пришло сообщение. Смотрим на сообщение - цветные квадраты, не тяжело догадаться по названию таска что в них и состоит основной смысл. Подумав, можно сделать вывод о том, где эти квадраты могут нести какую-то информацию - цвет. Вспомнив каким образом в css можно описать цвет, выбираем самое простое - hex. Производим расшифровку hextosting и если нам повезло, то нам выпадет строка с флагом, потому что там на рандом выбирается одна из 8 строк.

## Flag

> **flag{hExdEciMal_sOnNets_aNd_oThEr_teXtS_or_bRaIn_bOOoooom!!}**
