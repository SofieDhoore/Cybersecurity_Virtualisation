# Netwerk afluisteren

## Voorbeeld: 0-FTP.pcap

Capture van FTP activiteit

**Hoeveel TCP-verbindingen?**

Statistics menu -> Conversations -> TCP Tab geeft aantal TCP verbindingen weer. In deze file: 45

**Hoe start elke TCP-verbinding?**

Elke TCP-verbinging start met een 3-way-handshake. Dit proces zorgt ervoor dat beide partijen klaar zijn voor communicatie en dat de verbinding betrouwbaar tot stand komt.

SYN (Synchronize): De initiërende host (client) stuurt een pakket met de SYN-vlag aan naar de server om een verbinding aan te vragen.
SYN-ACK (Synchronize-Acknowledge): De server antwoordt met een pakket waarin zowel de SYN- als de ACK-vlaggen aanstaan.
ACK (Acknowledge): De client bevestigt de ontvangst met een ACK-pakket. De verbinding is nu tot stand gebracht.

**Kan je de reden voor de drie dataverbindingen afleiden uit de controleverbinding?**

Als je drie aparte SYN, SYN-ACK, ACK-handshakes ziet op verschillende poorten, weet je dat drie dataverbindingen zijn gebruikt.

Request: PORT 157, 193, 214, 191, 19, 137. Dit betekent 157.193.214.191 als IP-adres. (19\*256) + 137 = 5001. 5001 is de poort. Als je dan `tcp.port == 5001` intikt, krijg je alle pakketten die via deze poort verstuurd worden.

SYN → Client vraagt om een verbinding op poort 5001.
SYN-ACK → Server bevestigt.
ACK → Client voltooit de handshake.

Je zult meerdere PORT-commando's zien, elk met een andere poort. Als je dit invoert in Wireshark `tcp.flags.syn == 1`, je ziet drie aparte SYN-handshakes met verschillende poorten, dit betekent dat drie dataverbindingen zijn opgezet.

### Ter info

FTP = File Transfer Protocol om bestanden over te dragen tussen client en server.

TCP = Transmission Control Protocol om data uit te wisselen tussen netwerken.
