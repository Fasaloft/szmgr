# Distribuované systémy
> Základní pojmy, principy. Rozdíl mezi centralizovanou a distribuovanou architekturou systému, nevýhody obojího a jejich překonávání. Replikace, sdílení dat. Architektura orientovaná na služby (SOA), webové služby. Příklady existujících technologií a jejich využití. Příklady z praxe pro vše výše uvedené. ([PA053](https://is.muni.cz/auth/el/fi/jaro2023/PA053/um/))

## Základní pojmy, principy

**Distribuovaný systém** se skládá z aktérů (počítačů, serverů) propojených komunikační sítí za cílem sdílet nějaké zdroje, řešit paralelně nějaké problémy a používat služby ostatních aktérů. Řeší se zde problémy jako komunikace, synchronizace, škálovatelnost, transakční zpracování a podobně. 

**Middleware** - Aby aktéři v distribuovaném systému mohli komunikovat a koordinovat svoji činnost tak potřebujeme nějakou společnou a unifikovanou vrstvu, které slepí jednotlivé uzly dohromady za nějakou abstrakci. Zde se dá použít například RPC, OO metody nebo webové služby.

#### Distribuované systémy

Požadavky a vlastnosti distribuovaných systému
- **Škálovatelnost** - musíme umět systém škálovat vertikálně, případně horizontálně pro zvládání větší pracovní zátěže pokud je více požadavků
- **Spolehlivost** - systém by měl být napsaný tak, aby pokud vypadávají ostatní služby tak pořád běžel, tedy měl by být navržený tak, aby selhání nevedlo k selhání celého systému
- **Výkon** - zaměřujeme na výkon a minimalizování latence s maximální propustností. Zaměřujeme se tedy na práci s vyrovnávací pamětí, použití cache a podobně.
- **Flexibilita** - měl by se umět přizpůsobovat měnícím se požadavkům a podporovat dynamické přidělování zdrojů
- **Odolnost vůči chybám** - měli bychom mít mechanismy na detekci, obnovu a také nejlépe nějaký autohealing, abychom zajistili, že chyba shodí celý systém
- **Konzistence a koherence** - měli bychom mít mechanismy pro synchronizaci, replikaci a koordinaci údajů, abychom měli jistotu, že všechny uzly mají konzistentní sdílené údaje
- **Bezpečnost** - spravujeme většinou citlivé údaje subjektů, proto by měly být implementované robustní bezpečnostní opatření, řízení přístupu, autentizace a podobně
- **Interoperabilita** - distribuované systémy obsahují různé technologie, platformy a protokoly. Měli bychom zajistit interoperabilitu, mezi jednotlivými uzly.
- **Spravovatelnost** - systém by měl poskytovat nástroje a rozhraní pro monitorování a řízení zdrojů, které jsou distribuované
- **Rozšiřitelnost** - měl by být navržený pro budoucí přidávání nových funkcí, modulů aby se mohl dále vyvíjet podle požadavků


##### Základní architektury

**Monolitická architektura** 
- obsahuje vše, co systém potřebuje, je možné pouze vertikální škálování
- špatná spolehlivost (pád znamená pád celého systému)
- těžké na testování a znovupoužitelnost
- většinou těžká modularita

**Úrovňová architektura** (nezaměňovat s vrstvenou) 
- jednotlivé úrovně lze distribuovat, paralelizovat, nahradit (komunikace skrz API)
- používá se paradigma klient - server
- klient může být tenký/tlustý dle poskytnuté funkcionality
- Úroveň 1 (tenký klient)
	- všechno řeší server
	- jednoduché na aktualizace, málo vývoje, jednoduché na údržbu
	- většinou drahý server, single point-of-failure
- Úroveň 2 (tlustý klient)
	- přenášíme prezentační vrstvu na klienta
	- prezentační vrstvu můžeme podle klienta přizpůsobovat
	- nevýhoda je tight coupling a musíme vyvíjet k serveru i klienta
- Úroveň 3+ 
	- rozdělujeme vrstvy v rámci serveru
	- zlepšujeme škálovatelnost a rozšiřitelnost

**Component-based architektura**
- software je nějaká komponenta, která poskytuje API a může vyžadovat nějaké API
- je zde interní implementace schovaná před klienty
- jednoduše nahraditelná, znovupoužitelná a robustní na testování

**Service-oriented architecture** 
- založeno na více nezávislých službách, které vystavují svoje rozhraní
- většinou komunikace po síti, může se sdílet databáze, práce s daty je ACID

**Microservice architecture** 
- podtyp SOA 
- vysoká koheze, nízká provázanost služeb, nesdílí spolu databázi
- systém je tvořen velkým množstvím malých služeb
- důležitá je rychlá komunikace mezi službami (gRPC)

**Peer-to-peer architektura**
- klienti jsou jako servery a zároveň jako klienti
- můžeme mít takhle například distribuované uložiště a podobně
- složitější logika nacházení uzlů, spravování výpadků a podobně
- samostatně se organizující

**Shared nothing architektura**
- nezávislé a samostatné *shards*
- nekonečně škálovatelné
- data se rozdělí mezi shards podle nějaké vlastnosti dat
- jeden shard zpracuje s daty a nepotřebuje k tomu nic jiného

**Cloud Computing**
- výhodou je, že můžeme používat platformu/infrastrukturu jako službu
- nemusíme se o ni museli starat/provádět nákladnou iniciální investici
- výpočetní výkon lze upravit/škálovat na základě aktuálního vytížení
- fyzické zdroje mohou být sdílené, čímž je možné dosáhnout nižší ceny
- je možné distribuovat výpočetní požadavky (peaky různých aplikacích v různých dobách)
- datová centra lze volit na základě blízkosti k našim zákazníkům.

#### Middleware
Je zde více definicí, ale dá se to vzít jako jakékoli programování, které propojuje dohromady separátní programy, které dokonce většinou již existují.

Je to tedy nějaký software, který leží většinou mezi aplikací a operačním systémem a poskytuje nějakou společnost funkcionalitu, aby různé aplikace spolu mohli spolupracovat. Tím, že používáme middleware tak zvyšujeme dostupnost aplikace (tedy nějaká odolnost vůči chybám) a také použitelnost, protože díky middleware tak máme zajištěnou určitou míru interoperability.

#### Škálovatelnost

**Vertikální** 
- zvyšujeme výkonnost hardwaru, na kterém daný uzel běží
- škálujeme v rámci jednoho zdroje
- většinou jsou tam vyšší náklady za nějaký upgrade hardwaru, license a podobně
- je zde nějaký limit, kam se můžeme dostat

**Horizontální**
- přidáváme další uzly a rozdělujeme práci mezi ně
- je zde právě distribuovaný charakter, kdy paralelním zpracováním navyšujeme výkon
- je zde flexibilita a redundance, kdy pokud nám umře nějaký uzel tak ho zastoupí jiné uzly
- nicméně pokud škálujeme horizontálně, musíme mít efektivní komunikaci a koordinaci jednotlivých uzlů a nějaké vyvažování zátěže


---

## Rozdíl mezi centralizovanou a distribuovanou architekturou systému, nevýhody obojího a jejich překonávání


##### Centralizovaná architektura
Centralizovaná architektura shromažďuje data a logiku na jednom místě. V jednom místě je tedy rozhodovací pravomoc, data a vše okolo.

**Výhody**
- jednoduchá administrace a správa
- většinou větší bezpečnost a kontrola přístupu
- efektivní přidělování zdrojů a jednodušší procesy
**Nevýhody**
- neumožňuje horizontální škálování => škálujeme vertikálně
- selhání části znamená selhání celku => redundance, záložní servery
- nízká flexibilita, vysoká provázanost => důraz na kvalitu kódu
**Překonání nevýhod**
- plánování škálovatelnosti, mechanismy odolnosti vůči chybám, redundance a zálohy

##### Distribuovaná architektura
Distribuovaná architektura rozptyluje logiku do více samostatných komponentů (běžících třeba i na samostatných strojích), které spolu komunikují.

**Výhody**
- vyšší odolnost vůči chybám a výpadku
- možnost paralelního zpracování, škálování a flexibility
- lepší dostupnost a redundance dat
**Nevýhody**
- komplexita celkového systému, náročnější správa
- vyžadují více/složitější komunikaci
- složitější synchronizace
- jeden pomalý uzel může zpomalit ostatní
- náchylnost na latenci => použití message queues, gRPC, eventual consistency
**Překonávání nevýhod**
- využití autentizačních a autorizačních mechanismů pro vyšší bezpečnost
- implementace konsensuálních algoritmů
- dohody mezi distribuovanými entitami
- rozložení zátěže

**Hlavní kontrasty**
- centralizované systémy dobře mají dobré centralizované řízení a rozhodování, ale jsou citlivé na single point-of-failure
- decentralizované jsou zase odolnější a autonomnější, ale koordinace může být složité
- centralizované chci používat na systémy, které potřebují právě větší kontrolu
- decentralizované, kde je potřeba více škálovat a mít vysokou odolnost vůči chybám
- u decentralizovaných nebývají požadavky/transakce ACID, ale BASE
    - **BAsically available** 
	    - nefunkčnost části nezpůsobí nefunkčnost celku, zbytek funguje i v případě nefunkční části systému
	    - e.g. na netflixu nemusí fungovat služba hledání, ale vše ostatní běží
    - **Soft state** 
	    - změny v systému mohou nastávat i když nepřichází žádné dotazy 
	    - systém takto propaguje data, aby dosáhl konzistence
    - **Eventually consistent** 
	    - data nemusí být konzistentní okamžitě po získání odpovědi na dotaz
	    - většinou ke konzistenci dojde až po nějaké chvíli

##### Hybridní přístupy
Můžeme se pokusit udělat nějaké systémy, které kombinují výhody obou. Tedy chceme větší flexibilitu, škálovatelnost, odolnost vůči chybám ale pořád chceme mít rozhodování centralizované a dodržovat ACID. 

Teoreticky se něco takového dá, ale je tam docela náročný návrh celého systému a řešení právě integrace a koordinace mezi decentralizovanými autonomními komponentami. Můžeme mít jako příklady některé cloudové hybridní architektury, federativní systémy a nebo hybridní databáze s pohledu centralizace a decentralizace.


---

## Replikace, sdílení dat

Celkově jsou replikáce a sdílení dat základními komponentami distribuovaných systémů. Replikace zvyšuje odolnost vůči chybám a dostupnost údajů, zatímco sdílení umožňuje spolupráci a koordinaci mezi distribuovanými komponentami.


#### Replikace dat

V distribuovaných systémech se používá replikace dat z různých důvodů. U distribuovaných databází to může být z důvodu bezpečnosti/dostupnosti/prevence výpadku, obecně se tím ale v systémech snažíme zajistit rychlejší odezvy. Centrální databáze, ve které se sdílí data, se může stát limitujícím bodem. Poté tedy použijeme buď distribuovanou databázi, která replikaci řeší interně, nebo vícero databází, které mohou být jednodušší (MongoDB), protože se distribucí dat vzdáváme ACID a fungujeme s BASE. 

Určitá replikace dat vzniká v cache (Redis). U replikace je potřeba nějakým způsobem řešit invalidaci dat po změně (timeout, nebo CQRS). Replikace je kýžená u content delivery network (CDN), kde se snažíme mít statické zdroje (web, obrázky) co nejblíže uživateli, aby se dosáhlo rychlého načítání.

**Replikační strategie**
- *úplná replikace* - každý uzel obsahuje všechny údaje. Je zajištěná vysoká dostupnost dat, ale je zde problém se šířkou pásma v síti a úložný prostor, abychom to drželi v konzistenci
- *částečná replikace* - replikujeme mezi uzly pouze podmnožinu dat na základě některých kritérií, například podle nějakých vzorů přístupu, hlavně se snažíme snížit množství uložených dat a zatížení sítě
- *selektivní* - určitá množina dat se replikuje na určitou podmnožinu uzlů na základě nějakých pravidel a politik

**Modely konzistence**
- *eventuální konzistence* - mohou nastat stavy systému, kdy nemáme konzistenci, ta se po čase vždy opraví
- *silná konzistence* - po každé operaci jsou všechna data všude konzistentní
- *kauzální konzistence* - nějaký pravidla operací, příklad třeba v sociálních sítích, pokud vidím komentář příspěvku, musím vidět i příspěvek a tedy musím mít nějakou konzistenci v rámci akcí


#### Sdílení dat
Jedná se o nějaké umožnění různým entitám v distribuovaném systému využívat stejné sdílené údaje. Umožňuje to tedy nějakou spolupráci, koordinaci a sdílení mezi aktéry.

**Aspekty sdílení údajů**
- *Kontrola přístupu* - musíme mít nějakou autentizaci a autorizaci, která kontroluje, zda má daná entita právo se k určitým datům dostat
- *Rozdělení dat na oddíly* - můžeme všechny data rozdělit na nějaké oddíly, které poté přidělíme určitým uzlům. Oddíly by měly být přidělené k uzlům, které paralelizují práci s daty a snižují konflikty přístupu
- *Konzistence a soudržnost* - pokud potřebujeme silnou konzistenci, existují principy distribuovaných transakcí, distribuovaných zamykání a nebo nějaké kontroly pro řešení konfliktů, abychom vyřešili souběžný přístup k datům
- *Ukládání údajů do vyrovnávací paměti* - příkladem je například CDN, kdy data uložím na více míst, abych měl lepší výkon z hlediska přístupu a snížil zátěž hlavního úložiště dat
- *Replikace pro sdílení dat* - replikace většinou používám, kdy je potřeba zvýšit dostupnost dat a snížit latence přístupu

Pokud škálujeme horizontálně, jsou zde dva hlavní způsoby jak replikovat a sdílet data. V rámci distribuovaných modelů používáme oba, případně jejich kombinaci.
- **Replikace master-slave**
	- stejná data jsou kopírovaná mezi více uzlů
	- jeden uzel je jako hlavní, který odpovídá za zpracování všech aktualizací dat
	- čtení můžeme provádět z libovolných uzlů
	- pokud škálujeme aplikaci náročnou na čtení, není problém přidat více replik
	- pokud selže master, mohu i tak číst data případně povýšit nějakou repliku
- **Replikace peer-to-peer**
	- nevyužívá žádný master a má všechny uzly stejně rovné
	- každý uzel provádí i zápisy a pak rozšiřuje informaci mezi ostatní
	- problém u peer-to-peer je hlavně v držení konzistence
	- zápisy se řeší za cenu vyšší režie přes síť koordinací
	- většina uzlů shodne na zápisu a pak je možnost provést akci
- **Sdílení (Sharding)**
	- na různých uzlech jsou různé oddíly dat
	- každý uzel si spravuje a odpovídá za určitá svoje data
	- data by měly být spolu tak, aby uživatel získal všechny potřebná data z jednoho uzlu
	- měli bychom se snažit o rovnoměrné zatížení uzlů a fyzických umístění
	- většina NoSQL databází má automatický sharding
	- *sharding jako master-slave*
		- každý shard je replikovaný jedním master uzlem
		- uzel může být master pro jedny shards a replikou pro jiné
	- *sharding jako peer-to-peer*
		- typická strategie pro sloupcově orientované databáze
		- typicky shard replikuji na zhruba 3 uzly


---

## Architektura orientovaná na služby (SOA)

- hybrid mezi microservices a monolitem
- poměrně pragmatická architektura pro škálovatelný systém
- systém je tvořen vzájemně nezávislými, samostatně nasaditelnými službami 
- služby obsahují ucelené jednotky funkcionality 
- příklady služeb: uživatelé, správa produktů, správa objednávek, platební služba
- každá služba může být nezávisle na ostatních škálována
- nad službami může být pro zajištění jednotného API vrstva fasády
- služby obvykle sdílí databázi, ale je možné ji rozbít na vícero nezávislých celků
- náročnější na vývoj, ale celkově je systém díky modularizaci lépe udržitelný a škálovatelný
- SOA je *loosely coupled* a *nezávislý na protokolu*

Každá služba v SOA
- má zveřejněný kontrakt (nějaký interface)
- může být dynamicky nalezena a spuštěna
- udržuje si vlastní stav


---

## Webové služby

Definice asi nejlepší jako: Webové služby jsou specifickým typem distribuovaných služeb, která se řídí protokoly a technologiemi pro interoperabilitu přes síť, většinou přes Internet.

Umožňuje interakci a výměnu dat a vyvolávání funkcí nezávislými od platformy. Jsou jednoduché, škálovatelné, distribuované, ale nejsou tolik efektivní a musí tolerovat chyby.

Obecně zde najdeme několik charakteristik webových služeb:
- *založené na standardech* - většinou se dodržují nějaké standardy, jako je SOAP, XML nebo například WSLD. Díky standardům dosahujeme interoperability.
- *vystavené přes web* - webové služby většinou vystavují a zpřístupňují svoje API přes internet nebo intranet pro široké množství klientů
- *popis služby* - služby bývají dobře popsané pomocí WSDL, kdy se definují rozhraní, metody a typy údajů, se kterými se bude pracovat
- *bezstavová komunikace* - jsou navržené většinou jako bezstavové, což znamená, že se zde neuchovává žádná relace mezi jednotlivými dotazy

Obecnější vysvětlení pro webové služby: Jsou to komponenty umožňující komunikaci a interakci prostřednictvím standardizovaných protokolů a formátů. Jsou založeny na Service Oriented Architecture. Webové služby poskytují abstrakci funkcionalitě služby skrz webové API. Skrz definiční jazyk je formálně popsáno schéma/rozhraní dané služby a je možné generování klientského kódu pro různé programovací jazyky s cílem usnadnit použití webové služby.

#### WSDL (Web Service Description Language)
Je to popisný jazyk založený na XML pro popisování funkcionality poskytovaný webovou službou. Poskytuje formální definici přístupových bodů  služby, požadavky na volání a taky formát odpovědi. Umožňuje automaticky generovat kód  pro přístup ke službě.

Ve WSDL najdeme 4 elementy
- `type` - definice pro vlastní zprávy
- `interface` - definování množiny operací
- `binding` - definice protokolu a datového formátu pro každý `interface`
- `services` - jedno nebo více URL

#### SOAP (Simple Object Access Protocol)
Je to protokol pro výměnu strukturovaných informací v prostředí webových služeb založený na XML. Je navržený, aby uměl pracovat nad různými protokoly, jako je HTTP nebo TCP. Protokol je také nezávislý na platformě a programovacím jazyku. Můžeme buď takto získávat data, nebo provolávat vzdálené procedury.

Struktura SOAP:
- *envelope* 
	- obaluje celou strukturu a umožňuje přidat například namespace
- *header* 
	- žádná nebo jedna, definice rolí atributů, definice kódování
	- použití pro bezpečnost, kvalitu služby případně nějakých session
- *body*
	- obsahuje přenášené zprávy, definuje kódování
	- může opět obsahovat nějaké namespace
- *message payload*
	- přenášená data

Při srovnání s REST:
- je tam větší overhead, nicméně je nezávislý na protokolu
- více operací, méně zdrojů
- hlavní zaměření je na integrování s korporátními systémy
- řízený zprávami


#### REST (REpresentation State Transfer)
Jedná se o architektonický styl orientovaný na zdroje. Nepoužívá se zde žádné posílání zpráv přes SOAP. Není zde žádná specifikace W3C.

Právě zaměření na zdroje funguje na principu, že zdroj je za URL adresou na kterou přistoupí uživatel. Server vrátí reprezentaci a právě tato reprezentace dostane klienta do stavu.

Charakteristiky systémů jsou:
- *bezsstavovost* - žádná relace mezi jednotlivými dotazy
- *jednotné rozhraní* pro interakci se zdroji
- *orientace na zdroje* - velké množství zdrojů, malé množství akcí
- *jednoduchost*, *škálovatelnost*, *snadné cachování*, *flexibilita*

#### RPC (Remote Procedure Control)
Umožňuje spuštění předem vystavené procedury mezi procesy (i na vzdáleném stroji) tak, jako bychom proceduru volali přímo v kódu. Implementace procedury může být v odlišném programovacím jazyce. Časté použití je v distribuovaných službách, abychom snížili zátěž komunikace.

Součástí je definice rozhraní, ze kterého je možné vygenerovat odpovídající volatelné funkce/struktury použité pro argumenty pro náš jazyk. De-facto standardem je dnes gRPC. 

RPC funguje na modelu klient server. Díky tomu máme skrytou komunikaci a vzdálené volání je díky vygenerovaným výplním stejné, jako by to kdybychom pracovali s lokálním kódem.

Pro definici rozhraní se používá *IDL (Interface Definition Language)*, kde popíšeme metody, parametry a návratové hodnoty. Na základě této definice se generuje kód pro komunikaci.


#### CORBA (Common Object Request Broker Architecture)
Docela stará architektura pro komunikaci. Je to vlastně RPC, kdy opět přes IDL definuji všechno rozhraní a pak se vygeneruje kód. Využívá ORB (objektová request broker), což je centrální prvek, který serializuje a deserializuje data.

ORB poté využívá klient pro komunikaci se serverem a server zase vrací skrze ORB zpět.


---




Aktuálně se pro tyto účely spíše používá **REST** (representational state transfer, není to protokol, ale architektonický styl pro definici rozhraní) a **JSON** (byť je možné použít i jiné formáty), definované pomocí **OpenAPI Specification**, případně **GraphQL** (a JSON) se svým **GraphQL Schema** a dotazovacím jazykem. GraphQL používá jeden entrypoint (+1 playground) a umožňuje přesně specifikovat kýžená data (až na úroveň polí) a řešit tak problém s overfetching (1 dotaz obsahuje zbytečná data) a underfetching (v dotazu nemáme dostatek dat, takže děláme vícero různých dotazů).

*SOAP je nezávislý na transportu, REST využívá HTTP. REST je jednodušší, rychlejší a efektivnější. SOAP umožňuje jednu zprávu cílit více příjemcům, přechod zprávy přes prostředníky, kteří mohou zpracovávat hlavičku (tělo je určeno jen příjemci). SOAP umožňuje výměnu strukturovaných a typovaných XML dat SOAP hlavička (nepovinná) může obsahovat metadata, QoS, bezpečnostní informace, SAML data, session identifikátor (a.k.a. cookie)..., SOAP obálka je root XML prvek zprávy, obsahuje namespace (určunící verzi protokolu), styl kódování dat, SOAP tělo obsahuje samotný obsah zprávy. REST umožňuje provázanost (díky hyperlinkům) a je možné se pomocí něj dostat na úplně jinou stránku mimo náš systém.*

*REST se dívá na web jako na zdroje adresovatelné URL, které vrací reprezentaci dat (HTML, XML, PNG, JSON...). Příjem dat uvede klienta do stavu, který může být transformován přístupem na jiný zdroj. Je bezstavový, každá zpráva obsahuje vše, co je nutné pro její interpretaci (správně by zpráva neměla obsahovat cookie, ale třeba JWT), dotazy jsou kešovatelné.*


## Notes

**Middleware** - vrstva softwaru poskytující rozhraní pro interakci s různými službami/systémy, abstrakce k často používané funkcionalitě, případně vrstva propojující existující systémy.
- e.g. CORBA, Web Services, REST, message queue systémy, event brokeři.
