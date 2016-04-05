По `<link src='static/...'>` понять, что исходники раздаются как статика (Или просто попытаться зайти на `site.url/package.json`)
Перейти в `package.json` (Есть почти в любом проекте с node.js)
Перейти в `README.md` (Об этом написанно в `package.json`)
В `README.md` описан процесс установки и запуска. Перейти к файлу `start.sh` и `index.coffee`
`start.sh`: Найти опечатку (`ADMIN_PAS` вместо `ADMIN_PASS`)
`index.coffee`: понять, что в `process.env.ADMIN_PASS` undefined, и, соответственно, `"#{process.env.ADMIN_PASS} === 'undefined'"`
Из этого несложно догадаться, что подстановка 'undefined' вместо пароля откроет доступ к админке
Зайти в админку и получить "секретную информацию"
**flag{N0d3_JS_Und3f1n3d_p4ssw0rd}**
