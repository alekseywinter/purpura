**Протокол ARP**<br>
Протокол компьютерной сети канального и сетевого уровней, предназначенный для определения MAC-адреса другого компьютера по известному IP-адресу.<br><br>*Формат ARP- пакета*
<style type="text/css">
.tg  {border-collapse:collapse;border-spacing:0;margin:0px auto;}
.tg td{border-color:black;border-style:solid;border-width:1px;
  overflow:hidden;padding:10px 5px;word-break:normal;}
.tg th{border-color:black;border-style:solid;border-width:1px;
  font-weight:normal;overflow:hidden;padding:10px 5px;word-break:normal;}
.tg .tg-baqh{text-align:center;vertical-align:top}
.tg .tg-amwm{font-weight:bold;text-align:center;vertical-align:top}
.tg {
  border-collapse: collapse;
  border-spacing: 0;
  margin: 0px auto;
  width: 90%;
}
</style>
<table class="tg" ><thead>
  <tr>
    <th class="tg-amwm" colspan="2">0-7</th>
    <th class="tg-amwm" colspan="2">8-15</th>
    <th class="tg-amwm" colspan="4">16-31</th>
  </tr></thead>
<tbody>
  <tr>
    <td class="tg-baqh" colspan="4"><span style="font-weight:400;font-style:normal"><code>ar$hrd</code><br>Тип канального уровня↓ </span></td>
    <td class="tg-baqh" colspan="4"><span style="font-weight:400;font-style:normal"><code>ar$pro</code><br>Тип протокола сетевого уровня, для которого выполняется ARP- запрос↑</span></td>
  </tr>
  <tr>
    <td class="tg-baqh" colspan="2"><span style="font-weight:400;font-style:normal"><code>ar$hln</code><br>Длина аппаратного адреса канального уровня в байтах</span></td>
    <td class="tg-baqh" colspan="2"><span style="font-weight:400;font-style:normal"><code>ar$pln</code><br>Длина адреса протокола сетевого уровня в байтах</span></td>
    <td class="tg-baqh" colspan="4"><span style="font-weight:400;font-style:normal"><code>ar$op</code><br>Код ARP- операции</span></td>
  </tr>
  <tr>
    <td class="tg-baqh" colspan="8"><span style="font-weight:400;font-style:normal"><code>ar$sha</code><br>Аппаратный адрес отправителя пакета</span></td>
  </tr>
  <tr>
    <td class="tg-baqh" colspan="8"><span style="font-weight:400;font-style:normal"><code>ar$spa</code><br>Протокольный адрес отправителя пакета</span></td>
  </tr>
  <tr>
    <td class="tg-baqh" colspan="8"><span style="font-weight:400;font-style:normal"><code>ar$tha</code><br>Аппаратный адрес получателя пакета</span></td>
  </tr>
  <tr>
    <td class="tg-baqh" colspan="8"><span style="font-weight:400;font-style:normal"><code>ar$tpa</code><br>Протокольный адрес получателя пакета</span></td>
  </tr>
</tbody></table><br>
Host A                                   Host B

IP packet → needs MAC
   │
   │ ARP Probe (broadcast)
   │ SPA = 0.0.0.0
   │ TPA = 192.168.1.5
   │──────────────────────────────────────►
   │
   │ (если IP занят — Host B отвечает)
   │ ARP Reply
   │◄──────────────────────────────────────
   │
   │ ARP Request (broadcast)
   │ Who has 192.168.1.5?
   │ Tell 192.168.1.10
   │──────────────────────────────────────►
   │
   │ ARP Reply (unicast)
   │◄──────────────────────────────────────
   │ 192.168.1.5 is at MAC_B
   │
Send Ethernet frame<br><br>
<br>
<i>Типы ARP- запросов</i><br><br>
<style type="text/css">
.tg  {border-collapse:collapse;border-spacing:0;margin:0px auto;}
.tg td{border-color:black;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;
  overflow:hidden;padding:10px 5px;word-break:normal;}
.tg th{border-color:black;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;
  font-weight:normal;overflow:hidden;padding:10px 5px;word-break:normal;}
.tg .tg-fymr{border-color:inherit;font-weight:bold;text-align:left;vertical-align:top}
.tg .tg-0pky{border-color:inherit;text-align:left;vertical-align:top}
</style>
<table class="tg"><thead>
  <tr>
    <th class="tg-fymr">Тип</th>
    <th class="tg-fymr">Значение</th>
  </tr></thead>
<tbody>
  <tr>
    <td class="tg-0pky"><code>ARP Request</td>
    <td class="tg-0pky">Запрос MAC-адреса по IP. Особенности: отправляется broadcast с кодом поля <code>ar$op = 1</code><br>Цель — узнать MAC</td>
  </tr>
  <tr>
    <td class="tg-0pky"><code>ARP Reply</td>
    <td class="tg-0pky">Ответ на ARP запрос</td>
  </tr>
  <tr>
    <td class="tg-0pky"><code>Gratuitous ARP</td>
    <td class="tg-0pky">хост объявляет свой IP → MAC</td>
  </tr>
  <tr>
    <td class="tg-0pky"><code>ARP Announcement</td>
    <td class="tg-0pky">частный случай Gratuitous ARP</td>
  </tr>
  <tr>
    <td class="tg-0pky"><code>ARP Probe</td>
    <td class="tg-0pky">проверка свободен ли IP</td>
  </tr>
  <tr>
    <td class="tg-0pky"><code>Proxy ARP</td>
    <td class="tg-0pky">маршрутизатор отвечает за другой хост</td>
  </tr>
  <tr>
    <td class="tg-0pky"><code>Reverse ARP (RARP)</td>
    <td class="tg-0pky">использовался раньше для diskless машин.</td>
  </tr>
</tbody>
</table>