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
Send Ethernet frame