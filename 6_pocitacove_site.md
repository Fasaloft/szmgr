# Počítačové sítě

> Koncepty, principy, architektury. ISO/OSI a TCP/IP model, IP protokol, transportní protokoly (TCP, UDP). Protokoly na síťových vrstvách, funkce IPv4, pokročilé funkce IPv6. Peer-to-peer (P2P) sítě, ad-hoc/senzorové sítě, vysokorychlostní sítě, počítačové sítě a multimédia. Příklady z praxe pro vše výše uvedené. ([PA159](https://is.muni.cz/auth/el/fi/podzim2022/PA159/um/), PA191)

## Koncepty, principy, architektury.

> Počítačová síť je skupina počítačů a zařízení, propojená komunikačními kanály, která umožňuje komunikaci uživatelů sítě a sdílení prostředků (informací, souborů, dat, SW, HW).

Základní vlastnosti a parametry
- **propustnost** (bandwidth) - šířka pásma
- **ztrátovost** (packet loss) - ztráta paketů
- **zpoždění přenosu** (delay) - 
- **rozptyl** (jitter) - kolísání zpoždění

**Ideální** síť je (tam máme cíl, kam se chceme dostat)
- transparentní (uživatel si ani nevšimne, že komunikuje skrz síť)
- neomezenou propustností
- bezztrátová
- bez latence
- zachovávající pořadí paketů

Základní typy sítí
- **Connection-oriented (propojované)** - pro komunikaci se stanoví/vyhradí kapacita, která není využívaná nikým jiným (e.g. dřívější drátový telefon), snadno se zajišťuje kvalita služeb, v QoS tomu odpovídají integrované služby, můžeme mít fyzické okruhy, případně virtuální, tedy tak jak funguje TCP na transportní vrstvě
- **Connection-less (paketové)** - kapacita využívána všemi komunikujícími, komunikátoři své zprávy dělí a balí na pakety, těžko se řeší kvalita služeb (e.g. Internet), v QoS tomu odpovídají diferencované služby, můžeme nicméně používat docela dobře multicast. Opět na transportní vrstvě takto funguje UDP.

Typy přenosů dat
- **proudové přenosy**
	- převedeme na bity a posíláme jako jeden proud
	- předpokládáme spojovaný přenos
- **blokový**
	- rozdělujeme na větší kusy dat (packety) a ty poté přenášíme

Typy signálů
- **analogový** 
	- spojitý v čase, většinou se dobře přenáší analogově zvuk apod.
	- podléhá rušení elektromagnetických vln
	- umožňuje například multiplexing přes frekvenci nebo vlnovou délku
- **digitální**
	- musíme analogový převést do digitálního, tedy na diskrétní nuly a jedničky
	- multiplexing většinou jako časový

Klasifikace sítí podle rozlohy
- **WAN** - rozsáhlé území, třeba pro celé země nebo kontinenty
- **MAN** - metropolitní pro města
- **LAN** - lokální sítě (firmy, domácnosti)
- **PAN** - personal area networks - tedy jen nějaké osobní, bluetooth apod.
- **VLAN** - virtuální pro logické vytvoření sítě nezávislé na fyzickém uspořádání
- **WLAN** - bezdrátové sítě, využívající většinou radiové vlny

Koncepty sítí:
- **Architektury peer-to-peer** - propojení na stejné úrovni
- **Klient-server** - klienti komunikují pouze se serverem

Topologie:
- **sběrnicová topologie**
- **kruhová topologie**
- **hvězdicová topologie** - klasické, většinou za použití kroucené dvoulinky
- **stromová topologie** - propojení více hvězdic dohromady (LAN)

Síťové prvky
- **Aktivní**: vysílače, přijímače, opakovače, switch, hub, router, router
- **Pasivní**: kroucená dvoulinka, optické vlákno, koaxiální kabel

Směrování probíhá pomocí směrovacích tabulek routerů - na základě adresy (a případně typu) paketu se podle tabulky určí další směr, hop-by-hop princip. Další destinace se určuje na základě nejdelšího CIDR prefixu adresy. Směrovací jsou obvykle aktualizovány distribuovanými algoritmy. Na routerech je možné pakety filtrovat (zatoulané, k zajištění QoS) a případně klasifikovat (při modelech pay-as-you-go). Směrovat je možné nejen pomocí nejkratší cesty, ale i s ohledem na aktuální stav/vytíženost sítě.

**Protokoly**
- řeší komunikaci dvou a více entit
- je to množina nějakých pravidel, které nám definují formát a pořadí zpráv při komunikaci dvou a více entit, stejně tak jako akce během odesílání a přijímání
- SSL, UDP, HTTPS, TSP

## ISO/OSI,  TCP/IP model

### ISO/OSI 

- skládá se ze 7 vrstev
- každá zodpovědná za určitou funkcionalitu, vrstva komunikuje pouze se svými sousedy
- každá vrstva slouží jako abstrakce, díky tomu máme *interoperabilitu* a *kompatibilitu*
- je to spíš nějaký návod a abstrakce

##### 01 Fyzická vrstva
Přímo sedí na vodiči a přenáší jednotlivé bity co přijdou. Může zde být nějaké přepínání obvodů, kontrola a oprava odeslaných dat. Je zde například multiplexing, synchronizace, kontrola poslaných bitů za sekundu.

**Služby této vrstvy**
- transformace bitů na signál
- kontrola přenesených bitů za vteřinu
- synchronizace bitů při komunikaci
- multiplexing
- přepínání okruhů

**Kódování**
- Manchester, NRZ, 4B/5B

**Signál**
- jsou to fyzikální změny ve vodiči v nějakém časovém úseku
- *analogový*
	- spojitý v čase, vážeme na frekvenci, amplitudu nebo fázi
- *digitální* 
	- posíláme diskrétní hodnoty

**Protokoly**
- FDMA, TDMA - frekvenční a časový multiplexing

##### 02 Linková
Propojujeme mezi sebou dva body na lokální síti. Používají se zde **rámce**, které obsahují fyzickou adresu (MAC). Vrstva má za úkol data, který dostala z vyšší vrstvy převést na rámce a naopak přijatá data z vrstvy níže je třeba opravit, zkontrolovat a předat výše. Také zde najdeme komponenty jako **bridge**, případně **switch**.

Používáme v rámci **MAC adresu**.

**Služby**
- překlad paketů na rámce a naopak
- adresování na lokální síti
- kontrola errorů a kontrola zahlcení příjemce
- kontrola přístupu k médiu (Medium Access Control)

**Lokální sítě**
- používáme *Backward learning algorithm*, tedy učíme se svoji lokaci tím, že posloucháme
- druhá možnost je *Distributed Spanning Tree* algoritmus, kdy vypočítáváme minimální kostru podle charakteristik sítě. Není dobré pro velké sítě, které se často mění.

MAC (Medium Access control)
- snažíme se přistupovat k médiu a eliminovat kolice
- Aloha - vysílám kdykoli a pokud je kolize čekám
- CSMA-CD - posílá jen když je detekován klid (při drátovém spojení)
- CSMA-CA - ohlásím, že chci vysílat a pak začnu vysílat

**Protokoly**: Aloha, CSMA/CD, CMSA/CD

##### 03 Síťová vrstva
Řešíme směrování v celém internetu. Jdeme tedy za hranice lokální sítě. Používáme **pakety**, které nesou označení cílové stanice přes IP adresu. Má za úkol segmenty, které dostane z vrstvy výše rozdělit na jednotlivé pakety.

Používáme **IP adresu** v rámci paketu.

**Služby**
- změna segmentů na pakety a naopak
- rozdělování na menší fragmenty, pokud je segment moc velká pro odeslání
- adresuje podle IP adresy
- logicky se propojují sítě, aby vznikl dojem jednoho uceleného internetu
- vybírá cesty pro doručení paketu
- rozlišování adres pomocí ARP, případně RARP

**Protokoly**: IPv4, IPv6, ARP, RARP, RIP

##### 04 Transportní vrstva
Zde se určuje kvalita služby a propojení na úrovni portu. Vyšší vrstvy si tedy řeknou jakou kvalitu potřebují a tato vrstva ji zařídí. Používáme zde segmenty, které nesou cílový port.

Porty jsou na 16 bitů a prvních 1024 jsou **wellknown**, další potom **registrované** a poslední **dynamické**.

Pro posílání se používá virtuální spojovaná (TCP) nebo nespojovaná služba (UDP).

Používáme **port** v rámci segmentu.

**Protokoly**: TCP, UDP

##### 05 Relační vrstva
Vytváří relaci mezi jednotlivými uzly a snaží se o bezpečnou výměnu dat a koordinovat komunikaci. Zde už pojmenováváme přenosové entity jako zprávy. Může si vytvářet body, kdy se pak řeší, od jakého bodu se pokračuje v komunikaci, pokud dojde k chybě.

Řízení relace může být *simplexní* (TV, rozhlas), *poloduplexní* (vysílačka) nebo *duplexní*.

**Protokoly**: RPC, TLS/SSL

##### 06 Prezenční vrstva
Transformace dat do tvaru, kterému rozumí aplikace. Můžeme tedy zde komprimovat data, případně převádět na ASCII znaky.

**Protokoly**: ASCII

##### 07 Aplikační vrstva
Poskytuje aplikacím přístup ke komunikačnímu systému. Přímo sedí pod aplikací.

**Protokoly**: HTTP, FTP, DNS, IMAP


### TCP/IP
V praxi se ujal model TCP/IP, který jednotlivé vrstvy ISO/OSI slučuje. 

##### Aplikační
- poskytuje služby uživatelům (web, mail...)
- používají se aplikační protokoly (HTTP, SMTP, DNS, FTP...), které jsou součástí aplikací, 
- každý protokol definuje syntaxi, sémantiku, typy a pravidla výměny zpráv
- rozlišujeme zde
	- *peer-to-peer* vs *klient-server*
	- pull (datový přenos iniciuje klient) vs push (datový přenos iniciuje server) model

##### Transportní - TCP, UDP
- bere **data**, transformuje je na **segmenty**
- zajištění transportu segmentů do cílové aplikace, komunikace mezi procesy
- adresování pomocí portu (16 bitové číslo 0-65535)
- může poskytovat end-to-end spolehlivost, spojení (segmenty jsou číslovány, záleží na pořadí, dodání je potvrzeno)
- může poskytovat kontrolu spojení, quality of service
- logický komunikační kanál, iluze přímé komunikace

##### Síťová (internet layer)
- IP (internet protocol)
- bere **segmenty**, transformuje je na **pakety** (= datagramy)
- zajišťuje přenos paketů mezi komunikujícími uzly 
- tím, že přenášíme napříč různými LAN se de facto vytváří WAN
- umožňuje adresování každého zařízení na internetu pomocí IP adresy
- zajišťuje směrování paketů - závisí na vytíženosti sítě a její topologii
	- topologie celého internetu se těžko určuje, dynamicky se mění
	- používá se na to **Distance Vector**, **Link state** nebo **Path Vector**
	- je možné použít interní (RIP, OSPF) pro naši doménu (autonomní systém)
	- externí routing (EGP, BGP-4) pro směrování mezi doménami (autonomními systémy)
	
##### Vrstva síťového rozhraní (network access layer)
- **linková vrstva** 
	- bere **pakety**, transformuje je na rámce
	- rámce obsahující mimo jiné adresu odesílatele i příjemce
	- poskytuje adresování pomocí fyzických/MAC adres
	- zajišťuje spolehlivost fyzické vrstvy 
		- detekce chyb & případná korekce, možné díky redundanci, 
		- e.g. paritní bit, Hammingův kód
	- flow control - snažím se nezahltit příjemce
	- řeší koordinaci přístupu více zařízení ke sdílenému médiu (dělením na kanály, na základě rezervací, náhodnosti...) - MAC protokol
	- na této úrovni lze zapojovat sítě do topologií (běžné topologie bus, hvězda, kruh) 
- **fyzická**
	- poskytuje rozhraní ve formě přebrání rámce a převod na bity
	- poskytuje přístup k přenosovému médiu,
	- interně vrstva transformuje bitu na signály přenosového média
	- zajišťuje synchronizaci
	- multiplexing 
		- skloubení více signálů/datových toků do jednoho pro přenos na sdíleném médiu,
		- časový/frekvenční/vlnovědélkový multiplexing), demultiplexing...
	- médiem může být 
		- metalický/optický kabel
		- vzduch (pro bezdrátový přenos, rádiové/infračervené signály...)

### Routing
Na síťové vrstvě se snažím přenést data do cílového uzlu. Každý router řeší doručení paketu na své nejbližší sousedy ve snaze doručit paket blíže (domnělému) cíli na základě své **směrovací tabulky**.

Aby routing byl trochu efektivnější, vytváříme Autonomní systémy, kde potom řešíme vnitřní a vnější směrování. U vnějších, tedy *exterior gateway protocols* se zaměřujeme na škálovatelnost a obrovské sítě. U *interior gateway protocols* potom na výkonnost.

**Distance Vector** (pro IGP)
- *vše co vím řeknu svým sousedům*
- protokol **RIP**
- sousedící routery si periodicky/při změně vyměňují směrovací tabulky ve kterých jsou informace o vzdálenostech (hop distance) k různým cílům (distance vector)
- princip [Bellman-Ford](https://www.youtube.com/watch?v=obWXjtg0L64) algoritmu
- používaný pro malé sítě, kde není redundance
- má horší konvergenci pokud dojde ke změně, protože trvá než se změna zpropaguje
- dále se používají IGRP, EIGRP

**Link State** (pro IGP)
- *všem řeknu informaci o svých sousedech*
- routery si vyměňují informace o stavu svých sousedů
- je uchovávána topologie celkové sítě
- každý si dopočítá svou routovací tabulku, pro cesty se používá [Dijkstra](https://www.youtube.com/watch?v=_lHSawdgXpI).
- protokol **OSPF**, open shortest path first
- metrikou (výhodou hrany) je cena odvozená od šířky pásma, nižší je lepší
- robustnější, protože si každý počítá routing tabulky sám
- používaný pro velké sítě
- dále se používá IS-IS

**Path Vector** (pro EGP)
- distance vector, ale vyměňují se nejen ceny cest, ale celé jejich trasy
- lepší routing, protože detekujeme dobře cykly
- protokol **BGP (Border Gateway Protocol)**, umožňuje routing pravidla (policies)
- používá CIDR na zefektivnění routování
- používá se pro směrování mezi autonomními systémy


### Protokoly

**DNS (Domain name system)**
Hierarchická struktura doménových jmen a serverů. Překládá mi doménové jméno na IP adresu. Pro vyhledání se postupně navštěvují DNS servery a snaží se získat překlad.
- Local DNS - většinou poskytovatel internetu, má nějakou cache
- Root DNS - 13 po světě, pokud neví lokální, jde sem
- Top level domain DNS - pro domény jako .com, .cz apod.
- Name server DNS - konkrétní pro domény nižšího řádu

**DHCP (Dynamic Host Configuration)**
- pro dynamické přidělování adres v síti
- automaticky novému PC přidělíme IP adresu z nějakého poolu hodnot

**HTTP (Hypertext Transfer Protocol)**
- je to bezestavový internetový protokol pro komunikaci s www serveru
- nejvíce používaný protokol společně s SMTP
- specifikuje metody jako je GET, POST, PUT, DELETE

**SMTP (Simple Mail Transfer Protocol)**
Standartní protokolo pro posílání elektronické pošty. Pracuje na portu 25 pod TCP a definuje, jak klienti a servery komunikují skrze síť.


**ARQ (Automatic Repeat reQuest)**
Pro automatické zopakování zprávy pokud dojde k výpadku nějakého paketu během přenosu.
- **Stop and Wait ARQ**
	- nejjednodušší,
	- pakety mají střídavě 0 a 1
	- ACK se posílá s číslem dalšího očekávaného paketu
	- dá se používat **Piggybacking** pro obousměrný přenost
- **Go back N ARQ**
	- vylepšení předchozího, posílá více paketů bez čekání
	- pakety se číslují postupně a udržuje se plovoucí okno
- **Selective Repeat ARQ**
	- vzestupné číslování
	- pakety mimo pořadí se držím v paměti a nezahazuji jako u předchozího
	- pro zopakování konkrétního paketu pošlu NAK a číslo paketu

**TCP (Transmission Control Protocol)**
- chceme zaručit pořadí paketů a doručené všech paketů
- pracuje na transportní vrstvě a používá se *Go back N ARG*
- je zde řízení toku, abychom nepřehltili příjemce a síť
- hlavička obsahuje
	- zdrojový a cílový port
	- sekvenční číslo
	- číslo potvrzovacího paketu
	- délka hlavičky a rezervované bity
	- řídící data (bity, které říkají zda jde o ACK, URG, PSH)
	- velikost okna velikost okna
	- kontrolní součet a urgentní data
- pro navázání spojení se používá 3 cestný handshake
- jedna strana zahajuje, ale obě ukončují
- neumí pracovat multicast a směrovače nevidí toto spojení
- u TCP musíme řešit agresivitu, responsivitu a férovost při chování se v síti
- *Flow Control* znamená, že příjemce v rámci ACK zprávy pošle, kolik mu zbývá místa v jeho bufferu (např. 500 bytů), takže sender ví, že víc poslat nemůže. Když má příjemce plný buffer, tak pošle, že jeho window size je 0 a odesílatel čeká, dokud nepřijde nová ACK zpráva od příjemce o tom, že už má volné místo v bufferu.
- *Congestion Control* funguje tak, že při startu se exponenciálně zvyšuje velikost okna, dokud nedosáhneme učité hranice. Od této hranice lineárně zvyšujeme velikost, dokud nedojde ke ztrátě paketu. V ten moment snížíme velikost na hraniční hodnotu a pokračujeme v lineárním zvyšování rychlosti. Jednotlivé varianty si tuto metodu přizpůsobují
- Výsledný strop pro velikost odeslaných dat je dán minimální hodnotou těchto dvou parametrů.
- pro řešení zahlcení sítě nebo klienta se používají přístupy
	- TCP Tahoe 
		- pomalu zvyšuji cwnd, pokud dojde ke ztrátě, jdu od jedničky
		- nevýhoda je slow start
	- TCP Reno
		- rychlejší obnova po ztrátě paketu
		- slow start jen na začátku
	- TCP Vegas
		- monitoruje a pokud je detekování problém tak snižuje cwnd

**UDP** (User datagram protocol)
- jednoduché, ale nespolehlivé
- používá ho třeba DNS, radio, streamování apod.
- negarantuje pořadí ani doručení
- prakticky jen rozšíříme IP vrstvu o port
- Hlavička obsahuje
	- Zdrojový port
	- Cílový port
	- Celkovou délku
	- Checksum
- máme ještě možnost RUDP (Reliable UDP)
	- garantuje pořadí a doručení
	- použití, kde je pro TCP moc velký overhead problém

**SSL/TLS**
Vyskytuje se na vrstvě transportní a zajišťuje symetricky šifrovanou komunikaci po ustanovení TCP spojení. Typicky HTTPS, FTPS.


---

## IP protokol, Protokoly na síťových vrstvách

Zajišťuje doručení IP datagramů (data rozřezané na kousky s obálkou) v rámci internetu host-to-host (i přes prostředníky, a.k.a. routery), síť je connection-less, paketová, best-effort služba, není garance o doručení.

Více v sekcích [IPv4](./6_pocitacove_site.md#funkce-ipv4) a [IPv6](./6_pocitacove_site.md#pokročilé-funkce-ipv6).

**Protokoly**
- Aplikační - HTTP, SMTP, DNS, FTP...
- Transportní - TCP UDP
- Síťová IP - IPv4 (spolu s ARP, RARP, ICMP, IGMP), IPv6 (ICMPv6)
    - pro směrování Distance vector: RIP, IGRP, EIGRP, Link state: OSPF, IS-IS
- Vrstva síťového rozhraní - ethernet, 802.11 (Wi-Fi)


---

##  IPv4

Protokol umožňující komunikaci host-to-host.

- 32 bitů, 0.0.0.0 - 255.255.255.255
- typy adres
    - **unicast** - komunikace 1 na 1
    - **broadcast** - zpráva všem na LAN
    - **multicast** - zpráva těm, kteří se přihlásili k odběru dat na dané multicast adrese

Hlavička obsahuje
- *verzi*, *délku hlavičky*, *type of service* (pro zajištění quality of service), *délku datagramu*
- *identifikaci*, *flags*, *offset (používá se při fragmentaci)*
- *time to live* (dekrementován na každém hopu/routeru
- *protokol* - specifikace protokolu vyšší úrovně, ICMP, IGMP, TCP, UDP, OSPF...
- *checksum* hlavičky (ne těla, přepočítávání by trvalo, na každém hopu kvůli změně TTL)
- *adresa* odesilatele i příjemce
- *options* - slouží pro testování, debugging, volitelná část díky poli "délka hlavičky"

IPv4 je docela hloupý a potřebuje další protokoly, aby mu zajistily věci okolo
- *ICMP* 
	- poskytuje informace o stavu sítě (e.g. echo request/reply)
	- poskytuje odesilateli informace o chybě doručení (e.g. TTL šlo na nulu)
- *IGMP* - správa skupin pro multicast, (od)registrace do skupin
- *ARP*, *RARP* - překlad IP na MAC a obRáceně


Původně se IP adresy dělily pouze do tříd. Třídu A vlastní nadnárodní společnosti, B a C se používá nejčastěji. D je pro multicast a E je speciální pro nějaké experimentování apod.

![](img/20230530162603.png)

Kvůli nedostatku se začala používat i maska sítě (CIDR) pro jemnější dělení
- 0.0.0.0 - je to default sítě
- 192.168.1.255 - používaný jako multicast pro LAN
- 127.0.0.1 je loopback

ICMP (Internet Control Message Protocol)
- doplnění pro IP protokolu
- poskytuje dodatečné informace o síti
- e. g. *TTL expired*, *destination unreachable*, *time exceeded*

**IP Security**
Rozlišujeme dva přístupy
- *Authentication Header (AH)* - autentizace odesílatele a integrita, ne důvěrnost
- *Encapsulation Security Payload (ESP)* - pro autentizaci, integritu a důvěrnost
Dva módy
- *Transportní mód* - vkládáme IPSec hlavičku mezi IP hlavičku a data
- *Tunelovací mód* - obalíme celou IP a pak vygenerujeme novou hlavičku

**Směrování**
- přeposlání paketu na další bod (podle prefixu), aby se dostal do cíle
- vždy při směrování se provede
	- validace IP hlavičky a kontrolního součtu
	- kontrola TTL a případného zahození paketu
	- přepočítání hodnoty kontrolního součtu, protože snižujeme TTL
	- vyhledání nejkratší cesty
	- fragmentace
	- klasifikace paketu pro QoS a případně překlad paketu pomocí NAT
- směrovač má komponenty jako
	- rozhraní sítě
	- enginy pro přeposílání
	- queue manažery - řeší zahlcení
	- traffic manažery - prioritizuje pakety
	- route control processor - vykonává směrovací protokoly

**Multicast**
- máme multicastové adresy a skládá se strom linek
	- Source based tree 
		- každý odesílatel má vlastní strom
		- má tendenci zahlcovat síť
	- Shared tree 
		- vytvoří se jádro pro multicast skupinu
		- když chce odesílatel něco odeslat tak to pošle na 
- do multicastových skupin se přihlašují uživatelé přes IGMP

**TE - Traffic engeneering**
- interní routing je většinou založený na hledání nekratší trasy, nicméně problém nastává při vyšším provozu, kdy jsou nejkratší cesty zahlcené, ale ostatní zůstávají nevyužité
- traffic engineering je ty hlavně o hledání dalším cest dostupných v síti, abychom nasměrovali jen po nejkratší trase a optimálně využívali zdroje
- většinou administrátor sítě jednou denně provede úpravu na základě monitorování provozu
- používají se pro to algoritmy pro nalezení maximálních toků

**MPLS** (multiprotocol label switching)
- je to mechanismus směrování na základě labelů
- při vstupu do této sítě se přiřadí třeba jako další IP hlavička **Forward Equivalence Class**
- pak se uvnitř routuje spojovaně, tedy směrování je překonfigurovatelné
- rozdělujeme na
	- Okrajové směrovače - analyzují vstupující paket a přiřazují FEC
	- Vnitřní směrovače - přeposílají jen podle přiřazeného labelu


---

## IPv6
- řeší problém nedostatku IPv4 adres 128 bitovou délkou
- `0000:0000:0000:0000:0000:0000:0000:0000` - `FFFF:FFFF:FFFF:FFFF:FFFF:FFFF:FFFF:FFFF`
- možnost zkráceného zápisu:
    - vynecháním prefixových nul
        - `1050:0000:0000:0000:0005:0600:300c:326b` lze přepsat na
        - `1050:0:0:0:5:600:300c:326b`
    - dále vynecháním nejvýše jedné sekvence nul:
        - `1050::5:600:300c:326b`
- oproti IPv4
	- je chytřejší a má v sobě integrované protokoly, díky nimž není potřeba třeba ARP apod.
    - IPSec je povinnou součástí
    - delší adresa => možnost více zařízení v síti
    - jednodušší hlavička (chybí checksum (úplně odstraněn), options, fragmentation)
    - možností extension headers
    - podpora označování toků a jejich priorit
    - podpora bezpečnosti, šifrování, autentizace, integrity dat
    - podpora mobility - každé zařízení je někde doma, kde má svého *Home Agenta*
	    - pokud je zařízení mimo domov, posílá informace o své cizí adrese Home Agentovi
	    - HA se stará o případné přeposílání zpráv
	    - HA spolupracuje pro ustanovení přímého tunelu
    - podpora autokonfigurace zařízení
    - má i **anycast** - jako multicast, ale stačí, aby se data doručily jen jednomu členu skupiny
    - odebrána fragmentace při doručování, toto si musí ohlídat odesílatel
	    - pokud je datagram moc velký, je zahozen
	    - vygeneruje se ICMP zpráva obsahující zprávu o maximální velikosti na daném linku 
	    - procesu určení správné velikosti se říká **Path MTU Discovery**
	    - když se nevejde, fragmentuj na hodnotu dle ICMP zprávy
	    - opakuj proces. (MTU = maximum transmission unit)
    - odebrání checksumu (řeší se na nižší, nebo vyšší vrstvě)
    - broadcast nahrazen specifickými multicastovými skupinami (e.g. skupina routerů na LAN)

Hlavička (40B) obsahuje
- *verzi protokolu*
- *prioritu* (obsahuje i pole, které může indikovat, zda byla po cestě zaznamenáno zpoždění)
- *label toku* (pakety toku musí být zpracovány stejným způsobem, volbu směrování lze kešovat)
- *délka dat*
- *další hlavička* - může být rozšiřující hlavička (auth, options...), nebo třeba TCP hlavička dat
- *hop limit* 
- *adresy*

Podpůrný ICMPv6 rozšiřuje funkcionalitu i o to co dělal IGMP a ARP.

**Neighbour Discovery Protocol**
- nahrazuje ARP
- funguje díky komunikaci přes multicast skupiny
- obsahuje zprávy:
	- Router Solicitation (RS)
	- Router Advertisement (RA)
	- Neighbour Solicitation (NS) 135
	- Neighbour Advertisement (NA) 136
	- ICMP Redirect
- pro **získání adresy L2** nějakého uzlu
	- na multicast (FF02::::) se pošle posledních 24 bitů IP adresy hledaného uzlu jako (NS)
	- dostane zpět zprávu (NA) a to buď, že *je to router*, *je nalezen*, *má si něco přepsat*
- detekce duplikace (DAD)
	- pošle se zpráva NS, pokud někdo odpoví tak vím, že je v systému duplikace
- detekce nedosažitelnost (NUD)
	- periodicky si kontroluji dosažitelnost sousedů
	- mám několik stavů a udržuji si stavy svých sousedů

**Autokonfigurace**
- buď statefull jako u DHCP
- nově ale máme i stateless, kdy se síť konfiguruje sama
- RA zprávu posílá čas od času router aby informoval o parametrech sítě
- nový uzel buď čeká na RA, nebo pošle RS a vyžádá si ji
	- *Link Local Address Generation*: vygeneruje se link local adresa s prefixem, nulami a nakonec 64 bitů buď MAC nebo náhodné číslo
	- *Link Local Address Uniqueness Test*: pošle se NS zpráva a poslouchá se na NA odpovědi
	- *Link Local Address Assignment*: pokud projde unikátnost tak si nastaví zařízení IP na svůj interface
	- *Router Contact*: kontaktuje se router pro získání informace o konfiguraci buď posloucháním na RA nebo vysláním RS zprávy
	- *Router Direction*: směrovač předá instrukce, například, že je stateful autokonfigurace a předá adresu DHCP serveru

**Mobility support**
- bere se v potaz, že máme hodně zařízení, které přechází mezi sítěmi
- rozdělíme tedy sítě na jednu domovskou a pak nějaké další podsítě
	- *Home Agent (HA)* - router v domácí sítě, vždy dostupný
	- *Correspondent node (CN)* - s ním chceme komunikovat
- máme pak dvě adresy
	- *Home address* - vždy dostupná v naší domácí síti
	- *Care-of address* - síť mobilního zařízení když je v jiné síti
- probíhá ve dvou módech
	- *bidirectional tunnelling* - všechna komunikace jde přes HA
	- *route optimization* - vytvoříme si s CN přímou cestu na komunikování
- pokud jsem v cizí síti, musím svému domovskému routeru sdělit svoji care-of adresu

**Bezpečnost**
- máme dvě možnost
	- Authentication Header - zajišťuje autentizaci a integritu celého datagramu
	- Encapsulation Security Payload - poskytuje navíc důvěrnost, ale jen dat
- opět zde jsou možné dva režimy - tunelovací a transportní
- AH není kryptograficky tak silné jako ESP

**Quality of service**
- rozlišujeme buď
	- **Integrated Services**
		- dopředu si vyžádáme dostupnost a podmínky
		- dojde k rezervaci cesty a je zaručena požadovaná kvalita
		- náročné si udržovat tyhle věci v uzlech
	- **Differentiated Services**
		- používá se traffic class a flow label
		- uzly si dělají cache, kam se co posílá podle flow label a pak dodržují směrování
		- dá se označovat priorita paketu

**MTU Path Discovery**
- může fragmentovat jen uzel co posílá, ostatní ne
- pokud neprojde paket, pošle se zpět Packet Too Big a dojde k fragmentaci u zdroje


**Přechod z IPv4 na IPv6**
- nutnost úpravy legacy systémů
- složitější zpracovávání IPv6 adresy
- možnost
	- *Dual stack* - podpora zároveň IPv4 a IPv6 na jednom zařízení
	- *Tunneling* - zabalíme IPv6 datagramy do IPv4 datagramů
	- *Translators* - přeložíme IPv6 na IPv4, ale ztratíme výhody IPv6


---

## Peer-to-peer (P2P) sítě

Systém je tvořen vícero identickými (a na stejné úrovni) moduly, peery, které vzájemně komunikují. Každý peer funguje jako klient (posílá požadavky) i server (odpovídá na požadavky) současně. U P2P není potřeba znát topologii celé sítě.

Peer to peer sítě dobře škálují a mají tendenci být nestabilní a nespolehlivý.

**Oproti Server-Client:**
- lepší škálovatelnost (ale u C-S lze poměrně solidně obstát s load balancingem)- s počtem klientů roste i výpočetní kapacita
- decentralizace 
	- fajn z pohledu dostupnosti (pád 1 peera neznamená pád celého systému)
    - může být problém z pohledu konzistence dat
- větší proměnlivost topologie
- sdílení výpočetní kapacity
- sebeorganizace
- klient server je jednodušší a zavedenější na vývoj, snadněji se spravuje
- v klient-server je server jasnou autoritou, která zajišťuje bezpečnost a autenticitu dat
- u P2P je to složitější zajistit nějakou autoritu

**Využití P2P sítí**
- herní aplikace, sdílení obsahu, sdílení výpočetního výkonu
- distribuované výpočty Folding@Home
- filesharing BitTorrent
- Apache Cassandra (db)
- blockchain (veřejný - kryptoměny, privátní - e.g. Hyperledger) 

**Základní rozdělení na vrstvy:**
- *Aplikační vrstva*
	- celkové aplikace nad middleware pro sdílení souborů, distribuované systémy apod.
	- příklady: Gnutella, Napster
- *Middleware*
    - abstrakce nad overlay
    - poskytuje přístup ke službám/zdrojům peerů
    - kontroluje přístup ke službám/zdrojům
    - hledání a udržování zdrojů (skupin peerů) distribuovaných služeb
    - příklady: JXTA - Java P2P platform
- *Base overlay*
    - vrstva nad fyzickou sítí (obvykle TCP/UDP)
    - peery se berou jako hopy (fyzicky vzdálení mohou být v p2p síti sousedi a naopak)
    - peer discovery, přeposílání zpráv, udržování (části) sítě

**Peer discovery**
P2P sítě jsou většinou virtuální v rámci internetu. Musíme vědět jak se připojit k nějakému jinému peeru (tedy musíme zjistit IP adresu a port). Velmi důležité pro vůbec sestavení P2P sítí. Pokud připojíme nový uzel pak buď pasivně čeká, nebo aktivně vyhledává další uzly.
- **Static/Manuální** 
	- peer má předkonfigurovaný seznam informací o ostatních možných peerech (IP, port)
	- na ty peery se zkouší připojovat
	- nevhodné pro dynamické systémy
	- u větších systémů lze omezit seznam na pár dlouhodobě běžících stabilnějších peerů.
- **Centralizovaný registr peerů** 
	- udržuje seznam aktivních peerů
	- používá se pro discovery
	- následně probíhá komunikace napřímo
	- registr je de fakto server, a tedy single point of failure
	- registr provádí healthcheck (peer může znenadání spadnout)
- **Member propagation techniques with Initial Member Discovery**
	- není potřeba vždy odhalit všechny peery v síti, ale jen několik
	- peer může mít seznam buď kompletní o peerech v síti
	- peer může mít částečný seznam
##### Topologie P2P sítí
Overlay (jak jsou mezi sebou peerové vzájemně provázání) určuje celkovou výkonnost P2P sítě, ovšem samozřejmě všechno má své výhody a nevýhody.

1. **Podle struktury** hlavně mezi plochými a hierarchickými.
2. **Podle topologie** hlavně mezi uspořádanými a neuspořádanými.


**Random mesh** 
- po discovery peerů se k několika z nich připojím 
- vybírám podle latence, díky tomu je větší šance výběru fyzicky blízkých peerů
- vše je v jedné ploše

**Vrstvy** 
- peeři se organizují do vrstev dle poskytovaných služeb/připojení
- na nejvyšší úrovni jsou ti nejspolehlivější s kapacitou přeposílání zpráv
- na každé vrstvě je peer spojen s několika peery nižších vrstev 
- každý peer přeposílá zprávy na vyšší/nižší vrstvy
- struktura je tree-like, ale je třeba zajistit, aby výpadek jednoho nezpůsobil rozdělení sítě
- fajn třeba pro video streaming - peer může zprávu jdoucí dolů zduplikovat a šetřit tak 
- bandwidth na vyšších vrstvách.

**Mřížka/Grid** 
- peeři jsou propojeni do mřížky
- může být vícedimenzionální, i okrajoví mohou být vzájemně propojení
- problém může být přidávání/odebírání peerů, řádky/sloupce nemusí mít konzistentní počet
- koordináty peerů mohou být použity k adresování poskytovaných služeb

##### Směrování v P2P
Není úplně jednoduché v dynamických P2P sítí dobře směrovat. Musí se hlavně řešit:
- *ukládání metadat* - nemůže si každý uzel pamatovat vše
- *efektivita* - nechci aby se mi doručovaly věci moc dlouho
- *použitelnost* - podporuje to všechny typy dotazů
- *pokrytí* - zda když se na něco dotážu do prostoru tak na to dostanu odpověď
- *škálovatelnost* - dává to smysl i u obrovských sítích

**Routing in Unstructured P2P Networks**
- každá node si udržuje informace o sobě a o linkách na další peery
- pokud se připojí nový peer tak si kopíruje spojení aby formoval svoje linky
- pokud chci hledat tak musím zaplatit prostor dotazem
- používám TTL aby zaplavení nebylo obrovské a snažím se optimalizovat vyhledávání
- můžeme použít prohledání do hloubky, do šířky nebo heuristické routovací strategie

**Routing in Structured P2P Networks**
- nestrukturované sítě trpí na neefektivní prohledávání
- strukturované sítě se snaží vytvořit nějakou topologii (Ring, Mesh, Multiple List)
- díky tomu je garance, že pokud záznam existuje tak bude nalezen
- nevýhoda - udržování topologie vyžaduje velkou údržbu
- můžeme rozdělit do kategorií
	- *Distributed Hash Table*
	- *Skip List based systems*
	- *Tree based systems*

**Routing in Hybrid P2P Networks**
- organizace peerů do hierarchické sítě
- *powerful* peers ve vyšších vrstvách
- *common* peers v nižších vrstvách
- vyhledávání funguje tak, že pošlu dotaz na supernode
- SN prohledá svoji složku a rozhodne se zda poslat dotaz na jiný super node nebo client node


---

## Ad-hoc a senzorové sítě

Ideálně začít popisem [ad-hoc](./6_pocitacove_site.md#ad-hoc) a [senzorových](./6_pocitacove_site.md#senzorové-sítě) sítí.

Rádiové sítě obecně
- distribuované řízení ke sdílenému médiu
- možná nutnost řešení problému odposlechů
- možná velká chybovost, kolize... => používají se spojované protokoly, které mohou mít rezervační, nebo plánovací mechanismy pro zajištění QoS.
- pro signalizaci přenosu (aby byla zajištěna prevence kolizí) je nutné použít separátní kanál, nebo tato signalizace musí proběhnout před samotným přenosem
- absence interference u odesílatele neznamená nutně absenci interference u přijímajícího

### Ad-hoc
- sítě fungující bez předešlé existující infrastruktury
- využívající síťových schopností jednotlivců => distribuované
- každý účastník funguje zároveň jako server i klient
- na rozdíl od P2P sítí 
    - je mnohem větší dynamicita topologie, mobilita účastníků 
    - účastníci jsou sami zodpovědni za přístup k přenosovému médiu 
    - přenosové médium je většinou vzduch
    - možná vysoká chybovost, interference
- *výhody*
	- rychle vybudované a není zde single point of failure
	- efektivnější než mobilní sítě
- *problémy*
	- není zde centrální autorita a je zde limitovaný rozsah

**Příklady**
- komunikace mezi autonomními automobily
- vytvoření komunikační infrastruktury při nouzových/záchranných situacích
- MANET - mobile ad-hoc networks
- VANET - vehicular ad-hoc networks

**Směrování může být**
- *adresové* 
	- každý účastník musí mít přiřazenou unikátní adresu
	- problém je najít ho v síti
	- výhodou je podpora uni/multi/broadcastu
- *data-centrické* 
	- zprávy na sobě nemají cílovou adresu, ale identifikátor dat
	- příjemci v síti avizují, o jaká data mají zájem -> ta jsou jim přeposílána
	- není nutnost řešit unikátní adresy

**Další dělení směrování**
- *proaktivní*
	- pravidelná výměna informací o stavu sítě
	- udržuje se info o topologii
	- záleží na kýžené rychlosti a vytíženosti sítě, energetických nárocích..
- *reaktivní*
	- objevuje cesty až když jsou potřeba
	- velký overhead a malé tabulky pro směrování
- směrování *hop-by-hop* vs. *znalost celé topologie*
- *ploché* vs. *hierarchické* (nadřízení mohou mít přidané zodpovědnosti)

### Senzorové sítě
Koncová zařízení jsou obvykle zařízení obsahující
- procesor a paměť
- komunikační modul (rádio)
- baterii (může být i s HW pro sběr energie, e.g. solární panel)
- samotný senzor (světlo, pohyb...)

Specifikem senzorových sítí je
- důraz na energickou efektivitu, protože baterka může být malá
- přísun energie omezený, toto mohou mít společné s ad-hoc sítěmi
- omezenou výpočetní/paměťovou kapacitu
- omezenou šířku pásma  
- možnou nespolehlivost
- nutnost řešit unikátní adresování obvykle to v sobě tato zařízení nemají pořešené
- možný důraz na sebeorganizaci, multi-hop v rámci sítě
- pro šetření energie se může používat dočasné uspávání zařízení v případě neaktivity v síti

Příklady
- sledování přírodních jevů, chování/přesunů (ohrožených) zvířat
- detekce požárů, zemětřesení, vln
- automatizace zemědělství, detekce sucha, škůdců...
- řízení dopravy
- automatizace řízení teploty v budovách
- měření kvality vzduchu
- zabezpečení objektů

**Směrování**
Můžeme zde mít specializované protokoly pro směrování
- *geografický routing* - ukládáme si přesné fyzické polohy uzlů
- *energy-aware routing* - bereme v potaz, že máme hodně málo energie a musíme šetřit

---

## Počítačové sítě a multimédia

**Multimédia** data složená z různých typů médií (text, zvuk, video, obrázky...) integrovaných dohromady. E.g. videokonference (video + zvuk), televize/stream (video + zvuk + (text, titulky)). Některé média mohou být analogové, pro přenos je nutná konverze. Je kýžená komprese pro snížení objemu přenášených dat, ale komprese může znamenat overhead navíc, což nemusí být přijatelné u realtime přenosů. Dle aplikace nám může (ne)vadit chybovost.

**Jitter** - rozdílná doba přenosu mezi jednotlivými pakety

**Delay** - doba přenosu ze zdroje k cíli (člověk si všimne latence > 100-200 ms)
- *Processing delay* - časový overhead u odesílatele/příjemce, záleží na rychlosti/vytíženosti komunikujícího systému
- *Transmission delay* - doba, jakou trvá nacpat všechny bity do přenosového média (záleží na velikosti)
- *Propagation delay* - doba přenosu přes samotné přenosové médium, záleží na technologii a vzdálenosti
- *Routing/queuing delay* - záleží na vytíženosti sítě, rychlosti směrování

Pro minimalizaci overheadu a zajištění maximální rychlosti (i za cenu chyb, výpadků...) se pro realtime aplikace používá UDP, příjemce může používat techniky jako odhadování chybějících dat, případně odesílatel může použít techniky pro detekci/korekci chyb pomocí redundance (nebo opětovaného zaslání). 

Je možné použít interleaving - e.g. u videa přeskládáme sousedící snímky tak, aby nesousedily. Pokud vypadne paket, tak bude ovlivněno sice více částí, ale každá jen trochu, namísto znatelného výpadku jedné části. Toto ale zvyšuje latenci.

Pro realtime přenosy se používá multicast, namísto spousty unicastů (síť není zahlcená tolik). Pokud multicast síť nepodporuje, můžeme na ní nasadit reflektor - odesílatel posílá jeden datový tok, reflektor přijímá a replikuje příjemcům, každému unicastem.

Na přenos multimédií je potřeba většinou velká šířka pásma. Tu úplně internet sám osobě neumí zajistit a rezervovat, protože funguje na principu best effort. Při TCP se zahlcení kontroluje automaticky, u UDP hrozí zahlcení sítě, protože tam kontrolní mechanismy chybí.

Média se mohou přenášet diskrétně (soubor, zpráva), nebo kontinuálně (stream).

**Text** 
- e.g. HTTP, SMTP, FTP
- vyžaduje relativně málo bandwidth, delay a nároky na chybovost závisí na aplikaci
- komprese pomocí Huffman, nebo Shannon-fano kódování (více v [otázka 5 - databáze](./5_databaze.md#kódování-a-komprese-dat))
- na webu se používá gzip (obsahuje Huffmana), drobné chyby dělají problémy
**Audio** 
- v základu analog
- digitalizace pomocí vzorkování (hodnota v čase) signálu a kvantitatizace
- požadavky na šířku pásma záleží na požadované kvalitě a případné komprimaci,
- jsme ochotni tolerovat drobné chyby
**Grafika** 
- obvykle nejsou požadavky na rychlost (pokud není tragická)
**Video** 
- obvykle náročné na šířku pásma, jinak se specifiky podobá audiu


---

## Vysokorychlostní sítě

Vysokorychlostní sítě v porovnání s tradičními sítěmi přenáší výrazně větší objem dat a tedy mohou sloužit jako páteřní sítě, které přenáší data mezi MAN případně WAN.

Mezi moderní protokoly patří například 400 Gigabit ethernet.

Hlavní parametry takových sítí jsou hlavně šířka pásma a nízká latence. Většinou ještě v kombinaci s nějakou redundancí, pokud by došlo k výpadku. Další aspekt je škálovatelnost, kdy tyto sítě jsou navrhnuté aby zvládali vyšších zatížení.


---

## Notes

**Protokol** je sada syntaktických (jak mají jednotlivé zprávy vypadat) a sémantických (jaký je význam jednotlivých zpráv) pravidel pro komunikaci nebo výměnu dat mezi systémy/zařízeními/komunikačními partnery

**CIDR** - kromě IP adresy uchováváme i masku sítě (e.g. 147.209.5.0/24 říká, že relevantních je jen prvních 24 bitů). Umožňuje subneting a efektivnější směrování - pokud máme v tabulkce adresy se stejným prefixem a stejnou cestou, můžeme říct, že naší cestou mají chodit pakety pro celý prefix 

**Piggybacking** - Pokud chceme odesilateli poslat nějaká data a zároveň potvrdit příjem dat, můžeme tyto informace spojit do jednoho paketu 

**NAT** Překlad adres na rozhraní sítě. E.g. pro naši síť máme 1 veřejnou IP adresu. Aby se zajistilo správné směrování všem v síti, musí se na rozhraní překládat veřejná adresa na interní adresu.

**SSL, TLS** - Kryptografické protokoly (SSL nahrazen TLS) používané mezi transportní a aplikační vrstvou, zajišťují autenticitu a šifrování dat komunikujících stran. Nejprve se účastníci dohodnou na podporovaných algoritmech, pak proběhne výměna klíčů (pro symetrické šifrování) založená na asymetrickém šifrování (certifikát serveru, může požadovat i certifikát klienta). Pak probíhá komunikace pomocí symetrického šifrování.

Pro zefetkivnění směrování je možné použít **Multiprotocol Label Switching** - pro předpokládané/známé toky definujeme cesty, každému toku dáme label a směrujeme jen podle labelů (rychlejší, je možné nastavit i více cest, třeba jako backup, nebo pro distribuci pro load balancing).

**Flow control** se řeší pro příjemce, **congestion control** se řeší pro síť

**Autenticita** - data jsou od správného odesilatele

**Integrita** - data nebyla cestou změněna

**Šifrování** - data nejsou čitelná/srozumitelná třetím stranám
