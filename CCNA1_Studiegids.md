CCNA 1 v7 — Compacte Studiegids

Modules 1–17 | ITN v7.0 | Cisco NetAcad

Module 1 — Netwerken in de wereld van vandaag

Netwerktypes

LAN — klein geografisch gebied (gebouw/campus)
WAN — verbindt meerdere LANs over grote afstand
Intranet — privé netwerk binnen organisatie
Extranet — beveiligde toegang voor leveranciers/klanten
Internet — netwerk van netwerken

Betrouwbaar netwerk = 4 eigenschappen

Fault tolerance (redundantie, meerdere paden)
Scalability (groeit zonder kwaliteitsverlies)
QoS — prioriteert realtime verkeer (video/VoIP)
Security — Confidentiality, Integrity, Availability (CIA)

Netwerkbedreigingen

Virussen, wormen, Trojans, spyware, DoS/DDoS, identiteitsdiefstal, zero-day
Thuis minimum: antivirus + firewall
Enterprise extra: IPS, VPN, ACL, dedicated firewall

Trends

BYOD, cloud computing, video, online collaboration
Powerline networking, WISP
Module 2 — Basis IOS-configuratie

CLI Modi

>          User EXEC
#          Privileged EXEC        (enable)
(config)#  Global config          (configure terminal)
(config-if)#  Interface config
(config-line)# Line config
exit = één niveau terug | end of Ctrl-Z = direct naar priv. EXEC
Ctrl-Shift-6 = ping/traceroute onderbreken
Tab = commando aanvullen

Essentiële configuratie

hostname R1
enable secret cisco
line console 0
 password letmein
 login
line vty 0 4
 password telnet123
 login
service password-encryption
banner motd # Authorized access only #
copy running-config startup-config

Geheugen

Type	Inhoud	Vluchtig?
RAM	running-config	Ja
NVRAM	startup-config	Nee
Flash	IOS image	Nee
ROM	Bootstrap/POST	Nee

Switch SVI

interface vlan 1
 ip address 192.168.1.2 255.255.255.0
 no shutdown
ip default-gateway 192.168.1.1

Verificatie

show running-config
show ip interface brief
show interfaces
show version
Module 3 — Protocollen en modellen

OSI model (7 lagen)

Laag	Naam	PDU	Protocollen
7	Application	Data	HTTP, FTP, DNS, DHCP
6	Presentation	Data	SSL, TLS
5	Session	Data	SSH, RPC
4	Transport	Segment	TCP, UDP
3	Network	Packet	IP, ICMP, OSPF
2	Data Link	Frame	Ethernet, 802.11
1	Physical	Bits	UTP, fiber, radio

TCP/IP model (4 lagen)

Laag	TCP/IP	OSI equivalent
4	Application	5+6+7
3	Transport	4
2	Internet	3
1	Network Access	1+2

Encapsulatie (top-down)
Data → Segment → Packet → Frame → Bits

Adressering op laag 2 vs 3

L2 MAC: lokale levering (NIC naar NIC, zelfde netwerk)
L3 IP: end-to-end levering (bron naar eindbestemming)

Standaardorganisaties

IETF (TCP/IP, RFC’s) | IEEE (802.3 Ethernet, 802.11 WiFi) | IANA/ICANN (IP-adressen)
Module 4 — Fysieke laag

Bandbreedte vs. throughput vs. goodput

Bandbreedte = theoretische capaciteit (bps)
Throughput = werkelijk gemeten overdracht (altijd lager)
Goodput = bruikbare data (minus overhead)

Koperkabel

Type	Gebruik	Afscherming
UTP	LAN Ethernet	Nee (twist voor cancellation)
STP	EMI-omgeving	Folieschild per paar
Coax	Kabel-TV, antenne	Centrale geleider + schild
UTP gestandaardiseerd door TIA/EIA, beëindigd met RJ-45
Straight-through: PC naar switch/hub | Crossover: switch naar switch / PC naar PC
Rollover (Cisco-proprietary): console-verbinding

Glasvezel

Immuun voor EMI/RFI, grotere afstand, hogere bandbreedte
Single-mode (geel): WAN/lange afstand | Multi-mode (oranje/aqua): campus
Connectoren: SC, LC, ST, duplex LC

Draadloos

802.11 (WiFi) | 802.15 (Bluetooth) | 802.16 (WiMAX) | 802.15.4 (Zigbee)
Beperkingen: coverage, interferentie, security, gedeeld medium
Module 5 — Binair en hexadecimaal

Binair naar decimaal

8-bits positieswaarden: 128 | 64 | 32 | 16 | 8 | 4 | 2 | 1

Decimaal naar binair (subnet masks)

Decimaal	Binair	Aantallen bits
255	11111111	8
254	11111110	7
252	11111100	6
248	11111000	5
240	11110000	4
224	11100000	3
192	11000000	2
128	10000000	1
0	00000000	0

Hexadecimaal

0-9 + A(10) B(11) C(12) D(13) E(14) F(15)
1 hex-digit = 4 bits (nibble)
Gebruikt voor: MAC-adressen (48-bit = 12 hex) en IPv6 (128-bit = 32 hex)
Module 6 — Datalinklaag

LLC vs. MAC sublayer

LLC (802.2): koppelt naar netwerklaag
MAC: encapsulatie, adressering, foutdetectie (FCS)

Topologieën

WAN: point-to-point, hub-and-spoke, mesh
LAN: ster, uitgebreide ster, bus, ring

Media access control

Half-duplex: één richting tegelijk → CSMA/CD (Ethernet) of CSMA/CA (WiFi)
Full-duplex: gelijktijdig zenden/ontvangen → moderne switched Ethernet

Frame-structuur
Preamble | Dst MAC | Src MAC | EtherType | Data | FCS

Module 7 — Ethernet

MAC-adres

48-bit, 12 hex-cijfers (bijv. 00:1A:2B:3C:4D:5E)
Eerste 6 hex = OUI (fabrikant) | Laatste 6 hex = uniek apparaatnummer
Unicast, broadcast (FF:FF:FF:FF:FF:FF), multicast

Switch forwarding

Methode	Wanneer doorsturen	Latency	Foutcontrole
Store-and-forward	Na volledig frame + FCS	Hoog	Volledig
Cut-through (fast-forward)	Na dst MAC (6 bytes)	Laag	Nee
Fragment-free	Na 64 bytes	Midden	Gedeeltelijk

MAC-adrestabel (CAM table)

Switch leert src MAC van inkomend frame
Stuurt naar enkel poort als dst MAC bekend is
Floods (naar alle poorten behalve inkomend) als onbekend

Auto-MDIX: detecteert automatisch kabeltype (straight/cross)

Runts vs. Giants

Runt: frame < 64 bytes | Giant: frame > 1518 bytes
Oorzaken: half-duplex botsingen, defecte NIC
Module 8 — Netwerklaag (IP)

IP-kenmerken

Connectionless (geen verbinding voor zending)
Best-effort (geen garantie levering)
Media-independent

IPv4 pakket-headers (significant)

Version, TTL, Protocol, Src IP, Dst IP, DS (DSCP/QoS)

IPv6 pakket-headers

Version, Traffic Class, Flow Label, Payload Length, Next Header, Hop Limit

Routeringsproces

show ip route
Codes: C=direct connected, L=local, S=static, O=OSPF, D=EIGRP

Host routing

Zelfde netwerk: stuur direct naar dst MAC (ARP)
Ander netwerk: stuur naar default gateway MAC
Module 9 — ARP en IPv6 ND

ARP (IPv4)

Broadcast request: “Wie heeft IP x.x.x.x? Zeg het aan mij”
Unicast reply: “Ik heb dat IP, mijn MAC is xx:xx:xx”
ARP-tabel (cache) met timer
Gevaar: ARP spoofing / ARP poisoning
arp -a      (Windows/Linux/Mac: toon ARP-cache)

IPv6 Neighbor Discovery (ND)
Vervangt ARP met ICMPv6-berichten:

Bericht	Richting	Functie
RS (Router Solicitation)	Host → Router	Vraag om RA
RA (Router Advertisement)	Router → Alle hosts	Prefix, gateway, DNS
NS (Neighbor Solicitation)	Host → Host	MAC-resolutie (= ARP request)
NA (Neighbor Advertisement)	Host → Host	MAC-antwoord (= ARP reply)
Module 10 — Basisrouterconfiguratie

Router initial setup

hostname R1
enable secret class
line console 0
 password cisco
 login
line vty 0 4
 password cisco
 login
 transport input ssh telnet
service password-encryption
banner motd # Authorized only #

interface GigabitEthernet0/0/0
 ip address 192.168.1.1 255.255.255.0
 description Link to LAN
 no shutdown

interface GigabitEthernet0/0/1
 ip address 10.0.0.1 255.255.255.252
 no shutdown

copy running-config startup-config

Default gateway op switch

ip default-gateway 192.168.1.1

Verificatie

show ip interface brief
show ipv6 interface brief
show ip route
show interfaces GigabitEthernet0/0/0
Module 11 — IPv4-adressering en subnetting

Adresstructuur

32-bit, 4 octetten, dotted decimal
Subnet mask (AND met IP) geeft netwerk-/hostdeel

Adrestypen per subnet

Netwerkadres: host-bits allemaal 0 (bijv. 192.168.1.0)
Broadcastadres: host-bits allemaal 1 (bijv. 192.168.1.255)
Hostbereik: alles daartussenin

Unicast / Broadcast / Multicast

Multicast IPv4: 224.0.0.0 – 239.255.255.255

Privéadressen (RFC 1918)

Klasse	Bereik	CIDR
A	10.0.0.0 – 10.255.255.255	/8
B	172.16.0.0 – 172.31.255.255	/12
C	192.168.0.0 – 192.168.255.255	/16

Subnetting — formules

Subnets = 2^n (n = geleende bits)
Hosts/subnet = 2^h - 2 (h = resterende hostbits)

Subnetting voorbeeld: 192.168.1.0/24, 4 subnets nodig

2^2 = 4 subnets → 2 bits lenen → /26
Hosts per subnet: 2^6 - 2 = 62
Subnets: .0/26 | .64/26 | .128/26 | .192/26

VLSM — subnettan van subnets voor efficiënt gebruik

Begin altijd met het grootste subnet
Vul daarna kleinere in op de volgende beschikbare grens
Module 12 — IPv6-adressering

IPv6 basics

128-bit, 32 hex-cijfers, 8 hextetten van 4 hex (: gescheiden)
Compressieregels:
Leidende nullen per hextet weglaten
Één aaneengesloten reeks all-zero hextetten → :: (slechts één keer)

Adrestypes

Type	Prefix	Functie
GUA (Global Unicast)	2000::/3	Publiek, wereldwijd routeerbaar
LLA (Link-Local)	FE80::/10	Alleen lokaal segment, verplicht
Loopback	::1/128	Zelf testen
Unspecified	::/128	Bron bij boot
Unique Local	FC00::/7	Privé, niet routeerbaar internet
Multicast	FF00::/8	Groepsberichten

Bekende multicast-adressen

FF02::1 = alle IPv6-nodes (= broadcast equivalent)
FF02::2 = alle routers

GUA-structuur
[Global Routing Prefix (48)][Subnet ID (16)][Interface ID (64)]

Interface ID methoden

EUI-64: MAC (48-bit) + FFFE in het midden, 7e bit geflipped
Willekeurig gegenereerd (privacy)

Dynamische GUA-toewijzing via RA

Methode	GUA	Default GW	DNS
SLAAC	Zelf (prefix uit RA)	RA (router LLA)	Nee
SLAAC + Stateless DHCPv6	Zelf	RA	DHCPv6 server
Stateful DHCPv6	DHCPv6	RA	DHCPv6

Belangrijk: Default gateway komt ALTIJD uit de RA, nooit uit DHCPv6.

IPv6 configuratie

ipv6 unicast-routing
interface GigabitEthernet0/0/0
 ipv6 address 2001:db8:1::1/64
 ipv6 address FE80::1 link-local
 no shutdown

Verificatie

show ipv6 interface brief
show ipv6 route
ping ipv6 2001:db8:1::2
Module 13 — ICMP en troubleshooting

ICMPv4 vs. ICMPv6

Type	ICMPv4	ICMPv6
Echo Request/Reply	Type 8/0	Type 128/129
Destination Unreachable	Type 3	Type 1
Time Exceeded	Type 11	Type 3
Port Unreachable code	Code 3	Code 4

Ping-procedure (troubleshoot stappen)

ping 127.0.0.1 — loopback (test TCP/IP stack lokaal)
ping <eigen IP> — test NIC configuratie
ping <default gateway> — test lokale connectiviteit
ping <remote host> — test end-to-end

Traceroute

Gebruik TTL (IPv4) of Hop Limit (IPv6) om routers te detecteren
Elke router die een TTL=0 packet ontvangt stuurt “Time Exceeded” terug
traceroute (IOS/Linux/Mac) | tracert (Windows)
Module 14 — Transport Layer (TCP & UDP)

TCP vs. UDP vergelijking

Eigenschap	TCP	UDP
Verbinding	Ja (3-way handshake)	Nee
Betrouwbaar	Ja (ACK, retransmit)	Nee
Volgorde	Ja (sequence numbers)	Nee
Flow control	Ja (window size)	Nee
Overhead	20 bytes	8 bytes
Gebruik	HTTP, FTP, SMTP, Telnet, SSH	DNS, DHCP, TFTP, VoIP, video

TCP 3-way handshake

Client → SYN →       Server
Client ← SYN-ACK ←  Server
Client → ACK →       Server

TCP verbinding sluiten = 4-way (FIN, ACK, FIN, ACK)

TCP control bits: URG, ACK, PSH, RST, SYN, FIN

Poortnummers

Bereik	Type	Voorbeeld
0–1023	Well-known	80=HTTP, 443=HTTPS, 22=SSH, 21=FTP ctrl, 20=FTP data, 25=SMTP, 53=DNS
1024–49151	Registered	3306=MySQL, 8080=HTTP alt
49152–65535	Dynamic/Private	Ephemeral (client)

Socket = IP-adres + poortnummer (bijv. 192.168.1.1:80)

Flow control / sliding window

Window size in TCP header (16-bit)
SACK (Selective ACK): retransmit alleen missing segments
MSS = Maximum Segment Size (typisch 1460 bytes bij Ethernet)

netstat — toont actieve TCP-verbindingen

Module 15 — Applicatielaag

DNS

Resolveert domeinnaam → IP-adres
UDP poort 53 (kleine queries), TCP 53 (grote responses/zone transfers)
Hiërarchie: root → TLD (.com) → domein → host
nslookup — handmatig DNS opvragen

DHCP (IPv4)

DORA: Discover → Offer → Request → ACK
Broadcast-gebaseerd
Lease bevat: IP, subnet mask, default gateway, DNS

DHCPv6

Berichten: SOLICIT, ADVERTISE, REQUEST/INFORMATION-REQUEST, REPLY
Geeft GEEN default gateway (komt uit RA)

HTTP vs. HTTPS

HTTP: TCP 80, plaintext
HTTPS: TCP 443, SSL/TLS encryptie

HTTP methoden: GET, POST, PUT

E-mail protocollen

Protocol	Poort	Richting	Opmerking
SMTP	25	Verzenden	Client → server & server → server
POP3	110	Ontvangen	Download + verwijder van server
IMAP	143	Ontvangen	Sync, mail blijft op server

FTP

Poort 21: controle (commando’s)
Poort 20: data-overdracht
Client kan uploaden (push) en downloaden (pull)

SMB — bestandsdeling (Windows netwerken), langdurige verbinding

Module 16 — Netwerkbeveiliging

Bedreigingscategorieën

Malware: virus (host nodig), worm (verspreidt zelf), Trojan horse (vermommd)
Reconnaissance: ping sweep, port scan, internet queries
Access attacks: brute force, man-in-the-middle, trust exploitation
DoS / DDoS

Beveiligingscomponenten enterprise

VPN, ASA firewall, IPS/IDS, ESA/WSA, AAA-server
DMZ — zone voor publiek toegankelijke servers

AAA

Authentication (wie ben je?)
Authorization (wat mag je?)
Accounting (wat heb je gedaan?)

Firewall-technieken

Packet filtering (op IP/poort)
Application filtering (inhoud)
URL filtering
SPI (Stateful Packet Inspection)

Device hardening (IOS)

service password-encryption
security passwords min-length 8
login block-for 120 attempts 3 within 60
exec-timeout 10 0

SSH configuratie

ip domain-name cisco.com
crypto key generate rsa modulus 1024
ip ssh version 2
username admin secret Admin123
line vty 0 4
 login local
 transport input ssh

Let op: modulus 1024 is vereist voor SSH 2.0 in Packet Tracer (512-bit geeft SSH 1.5)

Module 17 — Klein netwerk en troubleshooting

Troubleshoot-methodiek (6 stappen)

Probleem identificeren
Theorie van waarschijnlijke oorzaken opstellen
Theorie testen
Plan opstellen en oplossing implementeren
Oplossing verifiëren + preventieve maatregelen
Bevindingen documenteren

Veelvoorkomende problemen

Symptoom	Mogelijke oorzaak
Geen verbinding local	Verkeerd IP/mask, verkeerde kabel
Verbinding local, niet remote	Geen/verkeerde default gateway
Naam niet resolveert	DNS fout/onbereikbaar
Slechte performance	Duplex mismatch, CRC-fouten
IP conflict	Twee devices zelfde IP, DHCP-probleem

Duplex mismatch

Eén kant full-duplex, andere kant half-duplex
Verbinding werkt maar met hoge latency/fouten

Host verificatie commando’s

ipconfig /all             (Windows)
ipconfig /release         (DHCP vrijgeven)
ipconfig /renew           (nieuw DHCP-lease)
ipconfig /displaydns
ifconfig / ip address     (Linux/Mac)
arp -a                    (ARP cache tonen)
netstat -r / route print  (routeringstabel host)

IOS verificatie commando’s

show running-config
show interfaces
show ip interface brief
show ipv6 interface brief
show ip route
show arp
show mac address-table
show cdp neighbors
show cdp neighbors detail
show version
debug ip routing          (real-time debug)
terminal monitor          (debug op VTY-sessie)

CDP / LLDP

CDP: Cisco proprietary, laag 2, ontdekt Cisco-buren
LLDP: open standaard (IEEE 802.1AB), vendor-neutraal
show cdp neighbors
show cdp neighbors detail
show lldp neighbors

Extended ping / traceroute

R1# ping              ← geen IP → extended mode
R1# traceroute        ← geen IP → extended mode
Belangrijke examen-valkuilen
Onderwerp	Valkuil / Onthoud dit
copy run start	Correct syntax voor CCNA examen (niet write mem)
SSH modulus	1024-bit voor SSH 2.0; 512 = SSH 1.5
Default gateway IPv6	Komt ALTIJD uit RA, nooit uit DHCPv6
ICMP type 3	IPv4 = Destination Unreachable; IPv6 type 3 = Time Exceeded
Port Unreachable	ICMPv4 code 3; ICMPv6 code 4
SVI	Software-interface zonder fysieke hardware, voor remote beheer switch
no shutdown	Verplicht bij router-interfaces, SVI vereist het ook
Subnet borrowing	Meer subnets = minder hosts, nooit meer dan 30 bits voor hosts
VLSM volgorde	Altijd beginnen met het grootste subnet
ARP broadcast	Verstuurd als broadcast, reply is unicast
MAC table leren	Op basis van SRC MAC van inkomend frame
Store-and-forward	Enige methode die foutcontrole (FCS) doet
FTP poorten	21 = control, 20 = data
POP3 vs. IMAP	POP3 verwijdert van server, IMAP sync/bewaart
transport input all	Workaround als transport input ssh telnet faalt op router VTY
ip default-gateway	Commando voor switch (niet voor router)
PT Skills Assessment — checklist

Wat je in het lab moet kunnen

Router en switch hostname + wachtwoorden instellen
Console, VTY, enable secret configureren
service password-encryption + banner
Router-interface IP + no shutdown
Switch SVI IP + ip default-gateway
SSH volledig configureren (domain, RSA 1024, ssh v2, login local)
IPv6 GUA + LLA op router-interface
ipv6 unicast-routing inschakelen
Connectiviteit verifiëren met ping/traceroute
show-commando’s correct interpreteren
copy running-config startup-config afsluiten

Studiegids gegenereerd op basis van Cisco NetAcad ITN v7 Modules 1–17, checkpoint-examens en practice final.
