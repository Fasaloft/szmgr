# 1. Programování a softwarový vývoj.

> Vývoj softwarových řešení, specifika implementace webových informačních systémů. Nástroje a prostředí pro softwarový vývoj rozsáhlých systémů. Základní koncepty softwarových architektur z pohledu implementace. Vícevrstvá architektura moderních informačních systémů, architektura model-view-controller. Persistence, ORM. Příklady z praxe pro vše výše uvedené. (PA165 || PV179)

## Vývoj softwarových řešení

Vývoj je více rozebraný v otázce na softwarové inženýrství, ale dá se to ve zkratce popsat:

> Je to proces, kdy jsou **uživatelovy potřeby** transformovány na **požadavky na software**, které jsou dále transformovány na **návrh systému**, která je implementovaný na **zdrojový kód** a ten je poté testován, dokumentován a certifikovaná pro **operační použití**.

Vývoj softwaru je tedy složeno z kroků *Analýza*, *Návrh*, *Implementace*, *Testování*, *Nasazení*.

Běžné aktivity při vývoji softwaru jsou *Specifikace*, *Vývoj*, *Validace* a *Evoluce*.

Když se vyvíjí software, většinou máme nějaké viditelné znaky toho, že se něco děje:
- **Artefakty** - výpisy programů, dokumentace, data, zdrojové soubory
- **Procesy** - pracovní postupy, uznávaná pravidla, interakce mezi členy týmu

Také potřebujeme nějak charakterizovat jednotlivé výrobní procesy:
- **Srozumitelnost** - explicitně definovaný a snadno pochopitelný
- **Viditelnost** - máme nějaké aktivity a výsledky, které jsou zvenku vidět
- **Spolehlivost** - máme navržený proces aby odolal nečekaným nástrahám
- **Přijatelnost** - je oblíbený mezi členy týmu
- **Udržovatelnost** - umí se přizpůsobit rozvíjející se firmě
- **Rychlost** - není zde spousta redundantních procesů, které zpozdí projekt
- **Podporovatelnost** - existují nástroje, které mohu používat v rámci procesu

#### Prediktivní životní cykly
##### Životní cyklus vodopád
- je zde sekvence fází - *Definování*, *Návrh*, *Implementace*, *Testování*, *Provoz*
- oblíbený manažery
- **výhody** - snadný na řízení, pokud jde vše hladce je nejlevnější
- **nevýhody** - špatná reakce na změny, potřeba mít velmi jasné požadavky

##### Inkrementální životní cyklus
- modifikace vodopádu, kdy rozdělíme projekt na menší vodopády 
- přidáváme po každé iteraci nový inkrement
- vytváří se verze jednotlivých aplikací

##### Spirálový životní cyklus
- pořád mám fáze návrh, implementace, vyzkoušet
- kombinace inkrementu a vodopádu, ale více dbám na analýzu rizik
- na konci cyklu je zpětná vazba a návrh dalšího vývoje

##### Model životního cyklu výzkumník
- většinou je to neuchopitelné manažersky
- je to jen pokus omyl, kdy něco implementuji a pokud to nefunguje tak zahodím

##### Model životního cyklu prototypování
- tvorba prototypů, abychom pochopili problém
- je to předloha pro vývoj i pro zákazníka
- na konci se zahodí a jde se implementovat úplně od začátku finální aplikace

#### Agilní životní cykly
Obecně se agilní přístup zaměřuje na více adaptivní způsob vývoje. Máme fixní čas a cenu a nemáme fixní rozsah.

Obecně agilní vývoj klade důraz na:
- *Individuality* a *interakce* mají přednost před procesy a nástroji.
- *Fungující software* má přednost před obsáhlou dokumentací.
- *Spolupráce se zákazníkem* má přednost před sjednáváním smluv.
- *Reakce na změnu* má přednost před plněním plánu.

##### Extreme programing
Na hodně malé projekty pro zkušené vývojáře a pro zadání, které se často mění nebo je nejasné. Viditelným znakem a jednotným zdrojem pravdy je jen kód. Dbá se na extrémní důraz na věci, které fungují. Pokud nám vyhovuje a osvědčilo se testování tak pořád testuj. Pokud kontrolování kódu tak dělej párové programování.

Je zde přírůstková změna, předpoklad jednoduchosti a okamžitá zpětná vazba.

##### Fetature-driven development
Vývoj po malých obrysech, které mají přínos pro uživatele. Je zde pět fází, kdy první 3 jsou sekvenční a poslední 2 se cyklí. Začíná se vytvořením návrhu a modelu systému. Poté se z toho vytvoří jednotlivé features a ty se pak implementují. Hlavně se v tomto přístupu měří pokrok v procesu a nový inkrement je cca každé 2 týdny.

#### Obecně k vývoji
 Klíčové je zajistit pravidelnou a dobře definovanou komunikaci mezi stakeholdery (nejen na začátku, ale i v průběhu vývoje), definovat *univerzální jazyk domény* a vynucovat jeho používání, aby v rámci úzce spolupracujících skupin nedocházelo k vytváření vlastních výrazů a následnému neporozumění mezi skupinami.

Při vývoji se často používá kontinuální integrace a nasazení *(CI/CD)*, čímž se mohou vynucovat standardy (dobré pro udržitelnost kódu) a spouštět se *automatizované testy*. Bývá součástí verzování kódu.

Klíčovou součástí analýzy a návrhu bývá *dekompozice* (a abstrakce) na komponenty, při které dělíme komplexní systém na jednodušší *nezávislé části*, abychom nemuseli neustále držet v hlavě kontext celého systému. Cílem je minimalizovat závislost mezi komponenty a dodržovat SOLID principy. Komponenty systému mají dobře *definovaný kontrakt*, nezávisí na konkrétních implementacích, ale na abstrakcích.

---

## Specifika implementace webových informačních systémů

Jde většinou o systémy s následujícími charakteristikami:
- jsou *složité*, *velké* a většinou *stavěné na míru*
- *přizpůsobují se zákazníkům* a jejich potřebám
- většinou pro *velké množství uživatelů* a *integrované se systémy* společnosti
- silné požadavky na *kvalitu*, *bezpečnost* a *spolehlivost*
- dodávané většinou jako *SaaS* (Software as a service)
- můžeme nasazovat většinou jako PaaS (OpenShift), IaaS (Azure) případně lokálně
- snadnost aktualizací klienta, na rozdíl od desktop aplikací
- nutnost *responzivity*, ke kterému uživatelé mohou přistupovat i z mobilních zařízení
- většinou *tenký klient*, aplikační logika se provádí z pravidla na serveru.
- webové systémy bývají většinou přístupné z celého internetu
- řeší se *autentizaci a autorizaci*, a jejich *zabezpečení proti útokům*
- mohou být používané větším množstvím uživatelů, proto je vhodně třeba řešit škálování 
- obvykle se používá model klient-server

Hlavní rozdělení je na 
- **Fat-client** - většina věcí se vykonává na klientovi, jsou více reaktivní, více náchylné na nasazování, levnější na provoz
- **Thin-client** - většina věcí se vykonává na serveru, dražší z pohledu provozu

Většinou součástí specifik webových informačních systémů bývá DevOps
- pravidelně se integrují nové věci do hlavní branch
- jsou zde automatizované testy
- automaticky se provádí operations - tedy nasazuje se na servery a aktualizuje se
##### Technologie pro Client-side
Zpřístupnění aplikace přes webový prohlížeš. Můžeme rozdělovat na SPA a SSR aplikace, případně na staticky generované SSG. Je zde velké množství knihoven, frameworků a metaframeworků.

- *HTML, CSS*, Javascript - základní stavební kameny pro práci v prohlížeči
- *AJAX, jQuery* - spíše historie, umožňovaly asynchronní dotazy a lepší práci s elementy
- *React*, *Vue.js*, *Angular*, *Svelte* - frameworky a knihovny pro lepší práci s frontend
- *SvelteKit*, *NextJS* - meta fullstack frameworky

##### Technologie pro Server-side
V základu rozdělujeme na stavové a bezstavové. Ty bezstavové se lépe škálují. Backend zajišťuje autentizaci, autorizaci a interaguje s databází pro persistování dat.

- *PHP* - skriptovací jazyk na straně serveru, hodně používaný
- *Java* - robustní a škálovatelný objektově orientovaný jazyk
	- *Spring* - široce používaný pro enterprise aplikace
	- *Quarkus* - modernější a Kubernetes-nativní framework
- *Python* - vysokoúrovňový skriptovací jazyk
	- *Django* - rychlý a bezpečný vývoj větších aplikací
	- *Flask* - jednoduchý a flexibilní webový framework
- *Ruby* - dynamický, objektový jazyk, většinou ve frameworky Ruby on Rails
- *Node.js* - hodně používaný, většinou má dobrý cold start a můžeme mít jednotný jazyk pro vývoj jak na serveru tak na klientovi
- *ASP.NET* - framework od společnosti Microsoft pro C# se silnými knihovnami pro robustní webové systémy

##### Technologie pro databáze
Uchovává stav systému a persistenci dat. Tradičně se používá relační databáze (Postgres, MySQL, Oracle), ale může být vhodnější použít dokumentovou (MongoDB) či grafovou (Neo4j).


##### Útoky na webové informační systémy
Vzhledem k tomu, že informační systémy uchovávají velké množství dat a v hodně případech i citlivých dat, je zde velký problém s četnými útoky. Mezi ty základní patří například:
- **SQL injection**
	- do vstupního pole vložíme specifický string, který dokáže způsobit akci v databázi
	- příklad: `ahoj; DROP TABLE Users; --`
    - obrana pomocí prepared statements
- **Session hijacking**
	- útočník se zmocní cookie/tokenu, který se používá pro prokázání identity
	- tokeny ukládáme jako cookie případně do local storage pro mobilní aplikace
    - obrana pomocí nastavení cookie jako "Secure" (lze poslat jen skrz https) 
    - další obrana je nastavení "HttpOnly" (nelze číst/upravit pomocí JS)
- **Cross site scripting (XSS)** 
	- útočník vloží na web obsah, který je validní html/js
	- oběti se zobrazí/spustí při načtení stránky. 
    - obrana pomocí sanitizace vstupů
- **Cross site request forgery (CSRF)** 
	- útočník připraví a pošle klientovi URL odkaz vyvolávající akci na našem serveru.
    - obrana pomocí CSFR náhodných tokenů (jednorázově vydaný s požadavkem dávající)
    - token vložíme do formuláře a zároveň si ho buď uložíme, nebo ho nastavíme jako cookie. Při zpracování požadavku zkontrolujeme, zda se tokeny shodují.
    - obrana pomocí cookie atributu "SameSite", který brání odeslání z jiné domény
	    - `Strict` neposílá cookie nikdy při cross site požadavcích
	    - `Lax` jen při GET požadavcích - ty by stejně neměly vyvolávat akci
	- problém však přetrvává u starých prohlížečů, nebo pokud se útočníkovi podaří umístit vlastní formulář na naši doménu či subdoménu.
    - obrana pomocí explicitního potvrzení (nebo MFA) u důležitých akcí
- **Phishing** útočník vytvoří vizuálně identický web, na kterém chce po uživatelích přihlášení
    - obrana pomocí kontroly domény uživatelem, nutný trénink uživatelů
    - pomoct může přizpůsobení webu - pokud je uživatel zvyklý vídat u kritických akcí svou fotku a všimne si, že na útočníkově webu chybí, může pojmout podezření

##### Autentizace a autorizace informačních systémů
Ověření identity a vydání nějakých rolí případně povolení na akce. Pokud nám nevadí používat autorizaci poskytnutou třetí stranou, bývá nejbezpečnější a nejjednodušší řešení použít federalizovanou identitu. 
- **Session based** 
	- uživatel poskytne údaje, server vydá cookie, kterou si udržuje (db/paměť)
	- uživatel následně s každým požadavkem zasílá cookie
- **Token based** 
	- server zapouzdří údaje o uživateli do tokenu, který podepíše
	- podepsání zajistí detekování modifikace tokenu
	- uživatel následně zasílá token, kterým prokazuje svou totožnost
	- v tokenu mohou zde být i informace o právech
	- nevýhoda je, že nemůžeme rychle zrušit platnost, musíme počkat až vyprší

Technologie pro autentizace a autorizaci jsou například:
- **HTTP basic** 
	- http header `Authorization: Basic <data>`
	- `<data>` obsahují hodnoty `<jmeno>:<heslo>` v base64
    - hlavička je viditelná (použij aspoň https), údaje se zasílají s každým požadavkem
- **OAuth2** 
	- protokol pro poskytnutí autorizace třetím stranám
	- funguje na principu vydávání tokenů (Refresh token, Access token)
- **OpenID Connect** 
	- nadstavba nad OAuth2, přidává autentizaci a informace o identitě uživatele
	- používá se pro federalizovanou správu identity (single sign-on)
	- *Klient* je aplikace, která potřebuje autentizovat uživatele
	- *Autorizační server* autentizuje uživatele, vydává token
	- token autorizuje držitele k přístupu ke *scopes* obsahující *claims* 
	- scope profil pro claimy id, email, name, picture umístěných na *resource serveru*
	- *resource server* slouží jako endpoint pro poskytování claimů na základě scopes
- **SAML** 
	- starší xml protokol pro výměnu autentizačních a autorizačních dat
- **Kerberos** 
	- na rozdíl od OAuth2 a OpenID connect používá v základu symetrickou kryptografii
	- uživatelovo heslo je na autorizačním serveru, uživatel posílá pouze svou identitu
	- server vrací přístupová data šifrovaná heslem uživatele


---

## Nástroje a prostředí pro vývoj rozsáhlých systémů

Pro vývoj rozsáhlých systémů se používají následující zejména typy nástrojů:
- **Editory a vývojová prostředí** 
	- v ideálním případě (pokud jazyk podporuje LSP0), závisí na preferencích vývojáře. 
	- od jednoduchých editorů až po plně integrovaná vývojová prostředí
- **Verzovací systémy** 
	- umožňují správu verzí zdrojového kódu a spolupráci vývojářů (git, SVN)
	- obvykle běží na platformě, která může být hostovaná (GitHub, Gitlab)
	- případně si hostujeme sami na vlastních serverech (Gitlab)
	- platformy obvykle nabízí víc, než jen správu zdrojového kódu (CI/CD, issue tracking)
- **Nástroje pro správu projektů**
	- slouží pro správu úkolů, sledování chyb a komunikaci v týmu
	- příklady: Clickup, Jira, ale i třeba Github
- **Nástroje pro testování**
	- umožňují vytvářet, spouštět a automatizovat testy
	- simulování uživatelské interakce, ověřování funkčnost systému
	- příklady: Jest, cargo test, Selenium, JUnit, pytest
- **Nástroje pro kontinuální integraci a nasazení** 
	- automatizují spouštění testů a sestavení výsledného produktu
	- příklady: GitHub workflows, Gitlab CI/CD, Travis CI, Jenkins
- **Monitoring a logování** 
	- slouží pro sledování výkonu systému a analýzu chyb a problémů
	- příklad: Grafana
- **Dokumentační nástroje** 
	- popisující fungování systému a jeho částí
	- dokumentace je důležitá zvlášť pro vystavované API
	- je nejlepší generovaná z kódu, aby se minimalizoval problém neaktuálnosti
	- OpenAPI 
		- JSON/YAML formát
		- generování z anotací
		- generování příkladů a dokumentace
	- příklady: cargo doc, OpenAPI 
- **Kontejnerová prostředí**
	- slouží pro minimalizaci rozdílů mezi prostředími, usnadňují reprodukovatelnost
	- příklady: Docker, Podman
- **Nástroje pro statickou analýzu kódu**
	- kontrolují dodržování standardů, zajišťují určitou kvalitu kódu
	- hledají potenciální chyby/slabá místa
	- příklady: cargo clippy, ESLint, SonarQube


---

## Základní koncepty SW architektur z pohledu implementace

##### Enterprise patterns
Některé specifika a patterny použité do velký systémů

- **DTO (Data Transfer Object)**
	- používá se pro přenášení mezi jednotlivými vrstvami
	- obsahuje většinou podmnožinu atributů celé entity
	- může nějak agregovat informace z více entit
	- můžeme ho vytvářet na jakékoli vrstvě a je serializovatelný
	- nemá žádnou komplexní funkcionality, jen gettery a settery
	- pro klienta je read-only, takže při editaci si dělá nový DTO a pošle na server
- **DAO (Data Access Object)**
	- oddělení persistentní vrstvy a business logiky
	- můžeme měnit persistentní vrstvu bez ovlivnění business vrstev
- **Façade**
	- interface, který obaluje složitou business logiku
	- zveřejňuje jasné a jednoduché API pro komunikaci s aplikací nebo její částí
	- provádí nějaké orchestrace nižších business vrstev, tedy pořadí operací apod.
- **Dependency injection**
	- implementace principu *Inversion of Control*
		- spoléhám se na poskytnuté implementace 
	- vychází z principu *Dependency inversion*
		- snažíme se aby komponenta spoléhala na interface a ne na implementaci
	- za běhu poté dodáváme zvenku nějaké konkrétní implementace
	- většinou se o to stará Framework
	- umožňuje to jednoduché testování
	- typy: *Field Injection*, *Property Injection*, *Constructor Injection*


##### Základní typy architektur
Dá se definovat jako nějaká struktura celého systému, která je obtížně měnitelné po implementaci.

- **Monolitická architektura**
	- tradiční přístup v architekturách
	- všechny komponenty a funkce systému jsou integrovány jako do jednoho kódu
	- relativně jednoduchý, nicméně málo flexibilní a špatně škálovatelný
	- pokud je dobře napsaný, má velmi dobrou performance
- **SOA (Service Oriented Architecture)**
	- je založený na navzájem spolupracujících službách
	- cílem je vytvořit robustní a odolný systém, který je *loosely coupled*
	- služba (service) je entita, která má popis a je dostupná přes rozhraní
	- hybrid mezi monolitem a microservices
	- pokud chceme jednotné API, používají se fasády, která přeposílá komunikaci službám
	- většinou sdílíme nějaké databáze mezi službami
	- použití přístupu ACID (Atomicity, Consistency, Isolation, Durability)
- **Microservices**
	- je to speciální případ SOA
	- máme menší a plně samostatné služby, které komunikují přes rozhraní
	- služba odpovídá za určitou oblast funkcionality systému
	- služby jsou škálovány, nasazovány a vyvíjeny nezávisle
	- většinou kvůli škálování se snažíme je dělat stateless
	- hlavní cíl je nezávislost a to i za cenu duplikace kódu
	- nesdílí se databáze
	- občas se může stát, že data v jednotlivých databázích nejsou úplně konzistentní
	- použití přístupu BASE (Basically Available, Soft state, Eventual consistency)
- **Architektura client-server**
	- běžně používaná ve webových aplikacích
	- máme dvě část - klient a server
	- klient komunikuje a posílá požadavky na server
	- klient poskytuje uživatelské rozhraní a interaguje s uživatelem
	- server poskytuje logiku a zpracování dat
- **Peer-to-Peer** 
	- každý klient je současně i serverem
	- klienti spolu komunikují napřímo
	- klienti takto sdílí výpočetní výkon, distribuují data
- **Vrstvená architektura**
	- systém rozdělujeme do vrstev, kdy každá vrstva má svoji odpovědnost
	- typicky jde o prezentační vrstvu, business a datovou
	- odpovědnost umožňuje přepoužití kódu a modularitu
	- další vrstvy jsou například Domain layer, Cross Cutting Layer
- **Event-driven architektura**
	- propojujeme systémy díky událostem
	- komponenty generují na událost a reagují na události jiných komponent
	- máme zde Publish-Subscribe pattern
	- je to loosely coupled a díky komunikaci můžeme skvěle škálovat systémy
- **Microkernel/Hexagonal/Component-based architektura** 
	- monolitická, dělí systém na jádro (core) a (ideálně) plug-in komponenty
	- aplikační logika je v komponentách 
	- jednoduchost, rozšiřitelnost, adaptabilita, přizpůsobení
    - jádro obsahuje minimální nutnou funkcionalitu, která se rozšiřuje skrz pluginy
    - pluginy by měly být nezávislé, připojitelné za běhu, mohou mít vlastní db
    - pluginy mohou být vzdálené a komunikovat s jádrem přes e.g. REST.
    - důležité je dobře definovat standardizované kontrakty, které musí pluginy splňovat
    - například VS Code - jádro je textový editor, pluginy jsou extensions
- **Pipeline architektura**
	- monolitická, funguje na principu MapReduce
    - komponenty jsou pipe, point-to-point komunikace
    - jsou typy komponent
        - *producer/source -* zdroj, iniciátor akce
        - *transformer (map) -* transformuje vstup na výstup
        - *tester (reduce) -* testuje kritérium, pošle dál nebo vyvolá akci (zápis do DB)
        - *consumer/sink -* ukončuje akci
    - filtry je možné snadno používat znovu
    - vede k batch processingu, což není fajn pro rychlou odezvu systému
    - příklad je unix terminal, compiler

---

## Vícevrstvá architektura moderních informačních systémů

Je to nějaký standard pro většinu enterprise aplikací, hlavně asi využívaný v Java, ale můžeme aplikovat na jakýkoli programování jazyk. Hlavní rysy této architektury jsou:
- aplikace rozdělené do *horizontálních vrstev* (jako u ISO/OSI modelu)
- každá vrstva *komunikuje* hlavně se *svým sousedem* a má svoji *zodpovědnost*
- vrstvy mohou být *otevřené* nebo *zavřené*
	- otevřené vrstvy můžeme při průchodu požadavku přeskočit
	- použití otevřených vrstev může zhoršit kvalitu aplikace
- počet vrstev není pevně daný, záleží na implementaci, většinou jsou alespoň 3 vrstvy
##### Příklady hlavních vrstev
- **Presentation**
	- čistě jen jako rozhraní pro komunikaci se systémem
- **Business (Application Layer)**
	- logika celé aplikace
	- je specifická a odráží požadavky zákazníka a domény, kde se aplikace nachází
- **Persistence (Data Access Layer)**
	- abstrakce pro ukládání a práci s daty
	- může tam být databáze, případně i nějaká jiná service

##### Příklady dalších vrstev
- **Facade**
	- je to nějaký interface, který shlukuje a orchestruje několik komponent systému
	- většinou používáme pro vytvoření nějaký čistějších rozhraní pro komunikaci
	- hlavní role je abstrakce a zjednodušení obalovaného systému
- **Domain vrstva**
	- je to nějaký core business logiky
	- orientuje se podle toho, k čemu je aplikace používaná a podle požadavků zákazníka
- **Infrastructure**
	- technická infrastruktura pro vyšší vrstvy
	- abstrahuje komunikaci s externími systémy, případně se souborovým systémem
- **Cross-Cutting vrstva**
	- je položena přes ostatní vrstvy vertikálně
	- většinou nějaká společná funkcionalita
	- logování, správa chyb

##### Výhody
- *oddělaná zodpovědnost* a dekompozice - každá vrstva řeší jen svoje věci
- *modifikace* a *rozšiřitelnost* změny mají minimální vliv a můžeme je zaměňovat
- *znovupoužitelnost* vrstev a nebo kódu
- *zapouzdření* - schování implementačních detailů a závislostí na konkrétní implementace
- *testovatelnost* - klíčové, kdy mohu ostatní vrstvy použít jako test doubles

##### Nevýhody
- někdy se zbytečně požadavky jen *přesouvají mezi vrstvami beze změny*
- monolitická aplikace se *těžko nasazuje a je méně robustní*
- špatně navržené mají tendence být spíše tightly coupled
- můžeme mít nějaký overhead, protože je zde mnoho vnitřní logiky
- *slabá škálovatelnost* a udržovatelnost, musíme *většinou celou aplikaci škálovat*
- dlouhý startup time a pád jednoho prvku může shodit celou appku


---

## Architektura model-view-controller

**MVC pattern - model, view, controller** - Model obsahuje data a business logiku. View  je zobrazením těchto dat a controller slouží k manipulaci nad modelem

`USER uses > CONTROLLER manipulates > MODEL updates > VIEW shown to >  USER`

Většinou používáme ve webových službách, kdy tato dekompozice umožňuje lepší testovatelnost a znovupoužitelnost kódu. Každá část má svoji zodpovědnost a soustředí se pouze na jednu věc. Celek se soustředí na interakci s uživatelem a prezentování dat.

- *Controller* - mapování URL na sadu akcí, které se provedou
- *Model* - seskupení dat, které se bude prezentovat uživateli například DTO
- *View* - způsob, jakým chceme data zobrazovat


Modifikace tohoto patternu jsou například
- **MVP pattern - model, view, presenter** 
	- presenter je prostředník mezi modelem a view, jde přes něj veškerá komunikace
	- uživatel používá pouze view, akce uživatele view předává presenteru
	- presenter aktualizuje model a zasílá view nová data
	- příkladem je třeba SPA
- **MVVM pattern - model, view, view model**
	- uživatel interaguje pouze přes view, veškerá komunikace jde přes view model
	- view model převádí data a propisuje je do modelu
	- rozdíl oproti MVP je, že view model může být použit pro vícero views
	- změny se sledují pomocí observeru
	- příklad je android aplikace.


---

## Persistence

Hlavní cílem je schopnost programu získat data i na hranicemi svého působení v rámci určité výpočetní session. Tedy chci se dostat k nějakým datům případně stavu i po restartování aplikace nebo jejími různými spuštěními a to za pomoci databází, cloudových služeb případně souborového systému.

Způsob ukládání dat musíme volit podle struktury dat, kterou chceme ukládat, případně nějakých dalších faktorů, jako je výkon, škálovatelnost a nějaké speciální potřeby aplikací.

- **Relační databáze** 
	- nejběžnější způsob uchovávání data v softwarových systémech
	- data jsou strukturována do tabulek obsahující sloupce
	- pro manipulaci nad daty se využívá SQL
	- příklady jsou Postgres, MySQL, Sqlite
	- jsou široce podporovány v programovacích jazycích
	- při použití SQL v aplikacích se doporučuje použít repository/DAO pattern
- **Souborový systém** 
	- data je možné ukládat přímo do souborového systému
	- toto je vhodné třeba pro obrázky nebo dokumenty
	- je potřeba ošetřit, abychom neposkytli přístup k jiným částem systému
	- odkazy na tyto data si můžeme poté ukládat do relačních databází
- **NoSQL** 
	- alternativa k relačním DB
	- umožňují ukládání a manipulaci s nestrukturovanými daty
	- proti relačním databázím poskytují lepší škálovatelnost a flexibilitu
	- problém může být konzistence (často se používá duplikaci pro vyšší rychlost)
	- příklady - MongoDB, Cassandra
- **Cachování** 
	- dočasné ukládání často používaných dat/výsledků operací
	- lze provádět na úrovni RAM, před databází, před serverem
	- příklady - Redis


---

## ORM

*Objektově relační mapování* - technika dat, která umožňuje mapování objektového modelu programovacího jazyka do na relační databázi.

Pokud chceme používat ORM, měli bychom se přesvědčit, že umožňuje i tak použití čistého SQL na nějaké složité dotazy, případně alespoň QueryBuilder. Také je potřeba si zajistit, že vytvoření tabulek je na základě námi napsaného schématu. Pokud si odvozuje ORM tabulky implicitně z nějaké třídy, databáze může být potom docela dost chaotická.

Výhody
- nemusíme psát čisté SQL a kód je agnostický vůči databázi
- většinou příjemné a rychlé na jednoduchou práci

Nevýhody
- složitější příkazy mohou být hodně komplikované
- většinou je těžší optimalizovat více manuálně dotazy
- může být omezena funkcionalita SQL
- můžeme mít horší výkon než u čistého SQL

Některé příklady ORM pro programovací jazyky:
- Java Hibernate
	- velmi rozšířený pro mapování objektů na databázové tabulky
	- podporuje MySQL, PostgreSQL, Oracle
- C# Entity Framework
	- velmi silný ORM framework pro práci s databází
	- podporuje dokonce několik databází zároveň
- Node.js Drizzle, Prisma
- Python SQLAlchemy
	- opět podpora pro více databází a vysoko i nízko úrovňové i vysoko úrovňové API

Některé problémy mezi objekty a relacemi
- *Dědičnost* - velmi podporované v OOP, ale v databázích tenhle koncept není
- *Identita* - v databázích podle primárního klíče, ale v OOP třeba pomocí equals
- *Granularita* - jeden objekt se může rozpadnout na více tabulek
- *Přístup k objektům* - v OOP přes odkazy, v SQL přes cizí klíče, tedy chceme joiny


## Notes

**Validace** - systém dělá to, co se od něj čeká (v rámci požadavků)

**Verifikace** - systém dělá věci správně interně

**Continuous deployment** - pravidelně dodáváme, automaticky testujeme výsledek

**Regresní testy** - provádí se po změnách, abychom detekovali nechtěné efekty

**Software as a service** - dostaneme hotovu aplikaci nebo službu v cloudu

**Platform as a service** - staráme se jen o vývoj, vše ostatní zajišťuje služba (e.g. Heroku)

**Infrastructure as a service** - pronajímáme si infra, tedy klasický cloud, AWS, Azure

**Aspect Oriented Programming** - technika, kde se definuje aspekt, který je volán pokaždé definované akci. Například pro logování - aspekt je definován jednou a je řečeno, že se má provádět pro všechny metody. Není nutné upravit každou metodu, aby explicitně logovala.

**Message queue** - namísto synchronního zpracování je možné použít message queue (používá se často interně v distribuovaných systémech, není nutné okamžité zpracování, usnadňuje load balancing, je možný broadcast, zprávy mohou být persisted), příklad je například RabbitMQ případně Kafka. Musíme například zaručit idempotenci, pokud by dorazilo více stejných zpráv.


#### REST (Representational State Transfer)
- nejpoužívanější styl/způsob tvorby rozhraní webových aplikací (ne protokol), vychází z HTTP, požadavek má syntax `<metoda> <uri>`
- zdroje identifikovány URI, mohou mít různou podobu (JSON, XML, HTML, PNG...)
- užívá HTTP metod
    - **GET** - pro získání dat
    - **HEAD** - pro získání metadat - hlavička je totožná s GET, ale v odpovědi není přítomno tělo
    - **POST** - požadavek, aby cílový zdroj zpracoval data obsažená v těle. Obvykle se používá pro akce/přidání nového prvku do kolekce (login, přidání příspěvku...). V případě tvorby prvku bývá pravidlem vrátit nově vytvořené ID v odpovědi
    - **PUT** - jako post, ale součástí požadavku je ID. Prvek s tímto ID má být upraven novými daty (v těle), nebo vytvořen právě s tímto ID
    - **PATCH** - jako put, ale v těle nemusí být všechna pole upravovaného prvku - změnit se mají jen ta pole, která jsou přítomná
    - **DELETE** - požadavek k odstranění dat
    - dále existují **CONNECT**, **OPTIONS** a **TRACE**

*safe* metody nemění stav na serveru (get, head, options, trace)

*Idempotentní* metody splňují vlastnost, že vícero identických požadavků má stejný efekt, jako jediný požadavek (všechny, kromě POST, PATCH (není zcela standardizované chování) a CONNECT) 

RESTové služby jsou bezstavové (pro vyhodnocení požadavku by nemělo být nutné znát nic, co není v požadavku obsazeno, e.g. namísto `GET /nextPage` se použije `GET /pages/2`)

Některé REST metody jsou kešovatelné, v komunikaci mohou být prostředníci (třeba cache, proxy, load balancer..), o kterých klient neví

**Best practices**
- konzistentní pojmenovávání zdrojů
- vztahy řešíme pomocí URI (e.g. `GET /users/1/orders` vrací objednávky uživatele 1)
- je v cajku udělat alias (e.g. `/me`, `/trends`)
- používání správných metod, přemýšlíme v rámci CRUD operací
- filtrování a řazení řešíme pomocí query parametrů (`/users?active=true&sort=name`)
- verzování API
- metody, které vytvářejí/upravují zdroje by měly vracet výslednou podobu zdroje
- aktuálně je preference pracovat s JSON
- používání správných HTTP návratových hodnot

#### HATEOAS (Hypermedia as the engine of application state)
- jakýkoliv zdroj (URI) vrácený serverem může být předmětem další komunikace
- k entitám přidáváme href

#### WSDL (web services definition language)
- standardizovaný způsob popisu rozhraní webových služeb (jméno, lokaci, podporované protokoly, operace, formát zpráv..), používá se se SOAP

#### SOAP (simple object access protocol)
- komunikační protokol pro web services, umožňuje výměnu dat, vzdálená volání funkcí
- slouží jako jednotná vrstva mezi službami (aktuálně se používá spíš gRPC)

#### Java specifické věci

**Servlety** jsou komponenty umožňující zpracování požadavků a zaslání odpovědi (a.k.a. handler). 

**Java Web Containers** poskytují servletům runtime a starají se o další věci (e.g. sessions), může v nich běžet vícero web aplikací ve WAR (web archive). Alternativně je možné použít lehčí variantu, e.g. spring boot

**Java Server Pages** umožňují psát javu do html (server-side), obdobně jako php
