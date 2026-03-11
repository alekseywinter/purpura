**Протокол ARP**<br>
Протокол компьютерной сети канального уровня, предназначенный для определения MAC-адреса другого компьютера по известному IP-адресу.<br>
<br>
`....`<br>
`IPv4`<br><br>
`ARP- пакет`<br>
├─ `ar$hrd`&nbsp;&nbsp;&nbsp;`Тип канального уровня↓ (16 бит)`<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;см. таблицу ниже<br>
├─ `ar$pro`&nbsp;&nbsp;&nbsp;`Тип протокола сетевого уровня, для которого выполняется ARP- запрос↑`<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`asd`<br>
├─ `ar$hln`&nbsp;&nbsp;&nbsp;`Длина аппаратного адреса канального уровня в байтах`<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`asd`<br>
 ├─ `ar$pln`&nbsp;&nbsp;&nbsp;`Длина адреса протокола сетевого уровня в байтах`<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`asd`<br>
 ├─ `ar$op`&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`Код ARP- операции`<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`asd`<br>
 ├─ `ar$sha`&nbsp;&nbsp;&nbsp;`Аппаратный адрес отправителя пакета`<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`asd`<br>
 ├─ `ar$spa`&nbsp;&nbsp;&nbsp;`Протокольный адрес отправителя пакета`<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`asd`<br>
 ├─ `ar$tha`&nbsp;&nbsp;&nbsp;`Аппаратный адрес получателя пакета`<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`asd`<br>
 └─ `ar$tpa`&nbsp;&nbsp;&nbsp;`Протокольный адрес получателя пакета`<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`asd`<br>↑<br><br>
 `Ethernet-заголовок`<br>
 ├─ `Аппаратный адрес получателя`<br>
 ├─ `Аппаратный адрес отправителя`<br>
 └─ `Тип протокола сетевого уровня`<br><br>