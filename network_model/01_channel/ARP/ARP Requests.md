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