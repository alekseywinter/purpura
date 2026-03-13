<h3>Исследование механизмов работы и верификация устойчивости протокола ARP к аномальным запросам в среде виртуализации QEMU</h3>
<h4>Используемое ПО:</h4>
Хост: Debian GNU/Linux 12 (bookworm) <br>
Оркестратор: GNS3 v3.0.5<br>
Гипервизор: QEMU v7.2.22 + VMM GUI v4.1.0<br>
Гостевая система: Debian GNU/Linux 12 (bookworm)<br>
Инструмент исследования: Scapy v2.5.0, Wireshark v4.0.17, arp<br>
<h4>Цель работы:</h4> Изучить стандартные и пограничные состояния протокола ARP, используя библиотеку Scapy для генерации произвольных кадров, и проанализировать реакцию сетевого стека гостевых ОС на некорректные параметры.<br>
<h4>Задачи:</h4>
<li>Развернуть в оркестраторе GNS3 топологию сети, включающую несколько независимых узлов на базе QEMU.
<li>Реализовать стандартные сценарии ARP (Request/Reply, Probe, Announcement) и сопоставить их с требованиями RFC 826 и RFC 5227.
<li>Исследовать механизм Proxy ARP (RFC 1027) при межузловой передаче данных.
<li>Провести серию экспериментов по внедрению аномальных ARP-пакетов (нестандартные коды операций, подмена длин адресов).
<li>Проанализировать уязвимость сетевого стека к ARP Poisoning и зафиксировать изменения в кэше гостевой системы.<br>
<h4>Топология тестовой сети</h4>
<p align="center"><img src="../../assets/arp_lab_topology.png"></p>
Руководство по созданию простейшей топологии находится в этом же репозитории в папке <a href="../../manuals/GNS3/Setting up a simple topology in GNS3.md">manuals/GNS3. </a>Для подключения тестовой лаборатории к Интернет (для установки Scapy) нужно добавить NAT и настроить доступ, а так же прописать ACL для хостов.<br><br>
<li>Настройка NAT на роутере:<br>
<code>conf t<br>
interface g0/0<br>
ip address dhcp<br>
no shutdown<br>
exit</code><br>
<li>Настройка ACL на роутере:<br>
<code>access-list 1 permit 192.168.0.0 0.0.0.255<br>
access-list 2 permit 192.168.1.0 0.0.0.255<br>
ip nat inside source list 1 interface g0/0 overload<br>
ip nat inside source list 2 interface g0/0 overload</code><br><br>
Кроме того, <b>необходимо</b> назначить каждому хосту статический IP- адрес для предотвращения конфликтов адресов. Учитывая,что на хостах установлен Linux, делаем следующее:<br>
<li>Исключаем нужные нам адреса из раздачи:<br>
<code>Router(config)# ip dhcp excluded-address 192.168.0.2 192.168.0.4<br>Router(config)# ip dhcp excluded-address 192.168.1.2<br>
</code><br>
<li>Затем редактируем сетевой интерфейс на хосте:<br>
<code>sudo nano /etc/network/interfaces</code><br><br>
<code>auto [интерфейс]<br>
iface [интерфейс] inet static<br>
    address [адрес]<br>
    netmask [маска_подсети]<br>
    gateway [адрес_шлюза]<br>
    dns-nameservers 8.8.8.8 1.1.1.1<br></code><br>
<li>Кроме этого, назначим хостам соответствующие имена для удобства различия кто есть кто:<br>
<code>sudo nano /etc/hostname<br>
sudo nano /etc/hosts</code><br><br>
меняем имя по умолчанию на требуемое.
<h4>Пример формирования Ethernet- кадра с вложенным ARP- пакетом через Scapy</h4>

<code>from scapy.all import *<br>
packet = Ether(src="aa:aa:aa:aa:aa:aa", dst="ff:ff:ff:ff:ff:ff", type=0x0806) / ARP(<br>
    hwtype=1,<br>
    ptype=0x0800,<br>
    hwlen=6,<br>
    plen=4,<br>
    op=1,<br>
    hwsrc="aa:aa:aa:aa:aa:aa",<br>
    psrc="192.168.1.100",<br>
    hwdst="00:00:00:00:00:00",<br>
    pdst="192.168.1.1"<br>
)<br>
sendp(packet, iface="enp3s0")</code><br>