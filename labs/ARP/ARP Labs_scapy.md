<h4>asdasd</h4>

from scapy.all import *

packet = Ether(src="aa:aa:aa:aa:aa:aa", dst="ff:ff:ff:ff:ff:ff") / ARP(
    hwtype=1,
    ptype=0x0800,
    hwlen=6,
    plen=4,
    op=1,
    hwsrc="aa:aa:aa:aa:aa:aa",
    psrc="192.168.1.100",
    hwdst="00:00:00:00:00:00",
    pdst="192.168.1.1"
)

sendp(packet, iface="eth0")