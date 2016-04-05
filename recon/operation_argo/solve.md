# UFO CTF School 2016 : operation_argo

**Category:** recon **Points:** 200
**Author:** sea-kg, firolunis 

**Description:**

> Хакер спрятал свой код для доступа к муниципальной системе. Найди его и выполни.

## Write_up

**Распаковываем архив**

Внутри архива видим 64 файла картинки

**собрать файлы вместе**

Оригинальный файл разрезан на 8x8 (как шахматная доска)
Всего 64 кусочка размером 80x60 пикселей.
Размер оригинального файла: 640x480 пикселей.

Пример склеивания файла на питоне:
```python
	#!/usr/bin/env python
	# -*- coding: utf-8 -*-

	import Image
	import ImageDraw
	import ImageFont

	input_files = {}
	input_files[0] = "335607f8.png"
	input_files[1] = "52d5195e.png"
	input_files[2] = "35b9bb2d.png"
	input_files[3] = "fd823071.png"
	input_files[4] = "565a1a53.png"
	input_files[5] = "f877d941.png"
	input_files[6] = "1651c5a1.png"
	input_files[7] = "5e2954a2.png"
	input_files[8] = "b81b4b02.png"
	input_files[9] = "24358261.png"
	input_files[10] = "b9173610.png"
	input_files[11] = "1fffccd1.png"
	input_files[12] = "189be293.png"
	input_files[13] = "0422441e.png"
	input_files[14] = "64fe189c.png"
	input_files[15] = "fbf68870.png"
	input_files[16] = "3b19ba3e.png"
	input_files[17] = "088f40dc.png"
	input_files[18] = "f3945d6a.png"
	input_files[19] = "2238ea52.png"
	input_files[20] = "53e7363d.png"
	input_files[21] = "ae2b98d7.png"
	input_files[22] = "343cba7c.png"
	input_files[23] = "361ecd14.png"
	input_files[24] = "d414fbb1.png"
	input_files[25] = "95a4fc49.png"
	input_files[26] = "d9c747c3.png"
	input_files[27] = "5e3dd82a.png"
	input_files[28] = "8114aa5c.png"
	input_files[29] = "b9e184ac.png"
	input_files[30] = "90739bcb.png"
	input_files[31] = "48454fde.png"
	input_files[32] = "eb553376.png"
	input_files[33] = "610dd1a7.png"
	input_files[34] = "73354fad.png"
	input_files[35] = "2bc741d6.png"
	input_files[36] = "32202c9d.png"
	input_files[37] = "5a974ff8.png"
	input_files[38] = "143be729.png"
	input_files[39] = "35d278fc.png"
	input_files[40] = "7fc1c034.png"
	input_files[41] = "06a9a253.png"
	input_files[42] = "0b049bff.png"
	input_files[43] = "c84a2fee.png"
	input_files[44] = "210009a4.png"
	input_files[45] = "eb59be86.png"
	input_files[46] = "10a8a3e1.png"
	input_files[47] = "c5d32992.png"
	input_files[48] = "5e2996c5.png"
	input_files[49] = "85c9c7ac.png"
	input_files[50] = "f2b108a8.png"
	input_files[51] = "0f01a70c.png"
	input_files[52] = "0e11ee38.png"
	input_files[53] = "5967f514.png"
	input_files[54] = "1d16517c.png"
	input_files[55] = "f3d3fc7e.png"
	input_files[56] = "8767997a.png"
	input_files[57] = "4a60068b.png"
	input_files[58] = "cd5b73f8.png"
	input_files[59] = "418cf63a.png"
	input_files[60] = "07d323b6.png"
	input_files[61] = "540f4f90.png"
	input_files[62] = "30992996.png"
	input_files[63] = "ee781a14.png"

	img = Image.new('RGB', (640, 480))

	for i in input_files:
		img2 = Image.open('../public/' + input_files[i])
		box = (0, 0, 80, 60)
		region = img2.crop(box)

		x = 80*(i%8)
		y = 60*(i/8)
		box2 = (x, y, x + 80, y + 60)
		img.paste(region, box2)
	img.save("solveImage.png")
```

**Переписываем код с картинки в файл: operation_argo.py**
```python
	#!/usr/bin/env python3
	# -*- coding: utf-8 -*-
	# author: firolunis
	# version: 0.1
	import re
	FLAG = "".join(
		"d102b331c414b316"+
		"c518b313d114a13c"+
		"462b292c454b310d"+
		"118b199c406b364c"+
		"446b355d104b292a"+
		"15a13c498b310d12"+
		"5"
	)
	def main():
		tmp = re.split("(\D\d+)", FLAG)[1:]
		while tmp.count(""):
			tmp.remove("")
		res = []
		for i in tmp:
			if i[0] == "a":
				res.append(str(int((int(i[1:])-13)/2)))
				continue
			if i[0] == "b":
				res.append(chr(int((int(i[1:])-7)/3)))
				continue
			if i[0] == "c":
				res.append(chr(int((int(i[1:])-26)/4)))
				continue
			if i[0] == "d":
				res.append(chr(int(i[1:])))
				continue
		res = "".join(res)
		print(res)
	if "__main__" == __name__:
		main()
```

**Меняем права и запускаем файл:**
```bash
	$ chmod +X operation_argo.py
	$ ./operation_argo.py
```

**Программа выведет ответ**

>	flag{fr0m_kev@\_with_10ve}

## Flag

> **flag{fr0m_kev@_with_10ve}**
