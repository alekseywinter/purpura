<b><h2>Протокол ARP (Address Resolution Protocol)</h2></b><h3>Описание</h3>
ARP (Address Resolution Protocol) — это протокол сетевого уровня (в модели TCP/IP) или уровня «2.5» (в модели OSI)*, предназначенный для динамического сопоставления логических IP-адресов с физическими MAC-адресами в широковещательных сетях (Ethernet).<br>
Стандарт был зафиксирован в 1982 году в RFC 826 и с тех пор остается фундаментальным механизмом работы сетей IPv4. Без ARP передача данных по Ethernet была бы невозможна, так как сетевая карта «не понимает» IP-адреса и требует физический адрес целевого устройства для формирования кадра.<br><br>
<i>*Вопрос об уровне ARP — это предмет давних споров среди сетевых инженеров. Ответ зависит от того, какую модель (OSI или TCP/IP) вы берете за основу.</i><br>
Короткий ответ: Это протокол «уровня 2.5».<br>
<li><i>С точки зрения модели OSI:</i><br>
В строгой семиуровневой модели OSI протокол ARP находится между 2-м и 3-м уровнями.<br>
    Почему не 2-й (канальный)? Потому что ARP оперирует IP-адресами (адресами 3-го уровня). Чистый 2-й уровень (Ethernet) «не знает», что такое IP.<br>
    Почему не 3-й (сетевой)? Потому что пакет ARP не имеет IP-заголовка и инкапсулируется напрямую в кадр Ethernet (EtherType 0x0806). Он не может маршрутизироваться — ARP-запрос никогда не покидает пределы своей подсети (L2-сегмента).<br>
    <b>Вердикт для OSI: протокол канального уровня, обслуживающий сетевой уровень. Часто его называют L2+.</b><br><br>
<li><i>С точки зрения модели TCP/IP:</i><br>
В оригинальной модели TCP/IP (RFC 1122) уровни определены менее жестко, чем в OSI и определяются по функциональному назначению. Задача ARP — обеспечить работу IP-протокола, поэтому он является частью межсетевого инструментария.<br>
    <b>Вердикт для TCP/IP: ARP относится к Сетевому уровню (Internet Layer).</b><br><br>
    Итак, ключевые характеристики протокола:<br>
    <li>Сфера действия: ограничена одним широковещательным доменом (L2-сегментом). ARP-запросы не проходят через маршрутизаторы.
    <li>Инкапсуляция: Пакет ARP вкладывается непосредственно в кадр Ethernet. Он не использует заголовки IP или транспортные протоколы (TCP/UDP).
    <li>Тип кадра (EtherType): 0x0806.<br><br>

<h3>Структура пакета</h3>
Согласно спецификации RFC 826, пакет ARP имеет фиксированный набор полей, который позволяет протоколу быть универсальным для различных типов оборудования и сетевых протоколов:<br><br>
<style type="text/css">
.tg  {border-collapse:collapse;border-spacing:0;margin:0px auto;}
.tg td{border-color:black;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;
  overflow:hidden;padding:10px 5px;word-break:normal;}
.tg th{border-color:black;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;
  font-weight:normal;overflow:hidden;padding:10px 5px;word-break:normal;}
.tg .tg-baqh{text-align:center;vertical-align:top}
.tg .tg-vxqb{font-family:"Courier New", Courier, monospace !important;text-align:center;vertical-align:top}
.tg .tg-yfis{font-family:"Courier New", Courier, monospace !important;font-weight:bold;text-align:center;vertical-align:top}
</style>
<table class="tg"><thead>
  <tr>
    <th class="tg-baqh"></th>
    <th class="tg-vxqb"><span style="font-weight:700;font-style:normal">0-7 бит</span></th>
    <th class="tg-vxqb"><span style="font-weight:700;font-style:normal">8-15 бит</span></th>
    <th class="tg-vxqb" colspan="2"><span style="font-weight:700;font-style:normal">16-31 бит</span></th>
  </tr></thead>
<tbody>
  <tr>
    <td class="tg-yfis">0-3 байт</td>
    <td class="tg-vxqb" colspan="2"><span style="font-weight:400;font-style:normal">ar$hrd</span></td>
    <td class="tg-vxqb" colspan="2"><span style="font-weight:400;font-style:normal">ar$pro</span></td>
  </tr>
  <tr>
    <td class="tg-yfis">4-7</td>
    <td class="tg-vxqb"><span style="font-weight:400;font-style:normal">ar$hln</span></td>
    <td class="tg-vxqb"><span style="font-weight:400;font-style:normal">ar$pln</span></td>
    <td class="tg-vxqb" colspan="2"><span style="font-weight:400;font-style:normal">ar$op</span></td>
  </tr>
  <tr>
    <td class="tg-yfis">8-13</td>
    <td class="tg-vxqb" colspan="4"><span style="font-weight:400;font-style:normal">ar$sha</span></td>
  </tr>
  <tr>
    <td class="tg-yfis">14-17</td>
    <td class="tg-vxqb" colspan="4"><span style="font-weight:400;font-style:normal">ar$spa</span></td>
  </tr>
  <tr>
    <td class="tg-yfis">18-23</td>
    <td class="tg-vxqb" colspan="4"><span style="font-weight:400;font-style:normal">ar$tha</span></td>
  </tr>
  <tr>
    <td class="tg-yfis">24-27</td>
    <td class="tg-vxqb" colspan="4"><span style="font-weight:400;font-style:normal">ar$tpa</span></td>
  </tr>
</tbody></table><br>
<i>*Тонкий момент: «Абстракция адресов»</i><br>
В RFC 826 автор (Дэвид Пламмер) подчеркивает, что длина адресов (ar$hln и ar$pln) берется из самого пакета. Это позволяет протоколу работать, например, с IPv6 (теоретически) или старыми сетями типа Token Ring без изменения логики работы, просто меняя цифры длин.<br><br>
<i>Проблема выравнивания (Padding):</i><br> Минимальный размер кадра Ethernet — 64 байта. Пакет ARP для IPv4 занимает всего 28 байт. Это значит, что при передаче сетевая карта добавит к нему «мусорные» байты (padding), чтобы дотянуть до минимума.<br>
<h3>Алгоритм работы</h3>
Логика работы ARP строится на простом цикле, который инициируется каждый раз, когда узлу нужно отправить IP-пакет, но в его локальной таблице (ARP-кэше) отсутствует MAC-адрес получателя.<br>
Согласно RFC 826, процесс разделен на пять ключевых этапов:<br>
<table class="tg"><thead>
  <tr>
    <th class="tg-baqh">Проверка кэша и инициация<br>
Перед отправкой данных узел проверяет свою внутреннюю таблицу. Если запись для целевого IP уже существует, процесс завершается мгновенно. Если записи нет, узел формирует ARP-пакет с кодом операции 1 (Request).</th>
  </tr></thead>
<tbody>
  <tr>
    <td class="tg-baqh">Широковещательный запрос (Broadcast)
Так как отправитель не знает, где находится цель, он упаковывает ARP-запрос в Ethernet-кадр с адресом назначения FF:FF:FF:FF:FF:FF.
Результат: Этот кадр получают и обрабатывают абсолютно все устройства в данном сегменте сети (VLAN).</td>
  </tr>
  <tr>
    <td class="tg-baqh">Фильтрация и обновление у получателей Каждое устройство, получившее запрос, выполняет следующую проверку:
«Является ли мой IP-адрес тем, который ищет отправитель (Target Protocol Address)?»

    Нюанс из RFC: Даже если узел не является целью, он проверяет, есть ли у него в кэше запись об отправителе. Если есть — он обновляет её актуальным MAC-адресом отправителя, чтобы избежать устаревания данных.

    Если узел не является целью и записи об отправителе нет — пакет просто отбрасывается.</td>
  </tr>
  <tr>
    <td class="tg-baqh">Формирование ответа (Unicast Reply)
Узел, чей IP совпал с запросом, выполняет два действия:

Вносит (или обновляет) данные отправителя в свой ARP-кэш.

Формирует ARP-пакет с кодом операции 2 (Reply).

Важный момент: Ответ отправляется адресно (Unicast), так как MAC-адрес инициатора уже известен из поля Sender Hardware Address пришедшего запроса.</td>
  </tr>
  <tr>
    <td class="tg-baqh">Завершение обмена Инициатор получает ответ, сохраняет пару IP-MAC в свою таблицу и приступает к отправке накопленных IP-пакетов, которые ожидали разрешения адреса.</td>
  </tr>
</tbody>
</table><br>
ARP-кэш: Как система это помнит

Чтобы не засорять сеть постоянными запросами, используется таблица соответствия (кэш). Посмотреть её в Windows/Linux можно командой:
arp -a

Нюансы реализации (из RFC 1122):

    Тайм-аут: Записи в кэше не вечны. Обычно они живут от 2 до 20 минут (в зависимости от ОС).

    Очередь: Пока идет ARP-запрос, система должна держать в памяти хотя бы один последний IP-пакет, который спровоцировал этот запрос.

