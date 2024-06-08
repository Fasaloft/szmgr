# Kvalita kódu

> Kvalita ve vývoji softwarových systémů, atributy kvality a softwarové metriky. Taktiky pro zajištění kvality na úrovni jednotlivých atributů kvality. Principy Clean Code a SOLID, refaktoring kódu. Testování kódu, jednotkové testy, integrační testy, uživatelské a akceptační testy. Ladění a testování výkonu. Proces řízení kvality ve vývoji softwarových systémů. Příklady z praxe pro vše výše uvedené. [PV260](https://is.muni.cz/auth/el/fi/jaro2023/PV260/um/lectures/), PA017, PA103

## Kvalita ve vývoji softwarových systémů

- důležitý aspekt při vývoji sw systémů, 
- kvalita je často definována jako **schopnost produktu dostát požadavkům** => je důležité si určit, co jsou požadavky
    - **zákaznické požadavky** a.k.a. externí kvalita (použitelnost, přesnost/správnost, spolehlivost, bezpečnost, výkon..)
    - abychom dostáli těmto ^, je třeba, aby šel vývoj snadno, aby se produkt dal jednoduše dlouhodobě udržovat (byl snadný modifikovat/rozšířit), a aby nebyl zbytečně drahý (skrz náklady na provoz i cenu úprav). Toho docílíme dodržováním **interní kvality produktu** (modularita, jednoduchost jednotek, testovatelnost, přizpůsobitelnost změnám, čitelnost kódu, znovupoužitelnost, škálovatelnost, přenositelnost, udržitelnost, dodržování standardů...)
- špatná externí kvalita je často symptomem špatné interní kvality produktu (opravy chyb trvají dlouho, systém je pomalý... ale nemusí to být vždy pravda, třeba jen máme slabší UI)


---

## Atributy kvality

Abychom si mohli nějak zadefinovat kvalitu, potřebujeme nějaké atributy, abychom si k nim mohli dát nějaké požadavky. Každý software může mít jiné nároky na každý z atributů.

|     | Atribut            | Vysvětlení                                               |
| --- | ------------------ | -------------------------------------------------------- |
| 1.  | **Udržitelnost**   | Snadnost úprav, vývoj bez technického dluhu              |
| 2.  | **Výkonnost**      | Reakční doba systému (a efektivita využití zdrojů)       |
| 3.  | **Spolehlivost**   | Pravděpodobnost bezchybného fungování po určitou dobu    |
| 4.  | **Testovatelnost** | Snadné a efektivní testování systému                     |
| 5.  | **Škálovatelnost** | Adaptovat se na větší výkon pro zpracování více dat      |
| 6.  | **Bezpečnost**     | Odolnost vůči útokům a neautorizovanému přístupu         |
| 7.  | **Použitelnost**   | Snadnost používání systému a jednoduchost učení se s ním |
| 8.  | **Robustnost**     | Odolání nečekané události a zotavení se                  |
| 9.  | **Dostupnost**     | Kolik procent času je systém funkční a dostupný          |

### Code smells

Každý z atributů může mít nějaké typické chyby, které brzdí a omezují jeho kvalitu. 

##### Výkonnost
Nadbytečně pouštíme nějaké složité algoritmy a neděláme cachování výsledků. Máme dlouhé kritické cesty, které často blokují zdroje, případně je v aplikaci nějaké aktivní čekání apod.

##### Spolehlivost
Je potřeba kontrolovat všechny vstupy co dostanu a hlavně i výsledky, které se spočítají. Použití některých nových neozkoušených technologií také snižuje spolehlivost a pokud se používají výjimky, je potřeba je správně odchytávat a reagovat na ne.
##### Testovatelnost
Problémy se hlavně týkají držení globálního stavu, chybějící inversion of control, případně Demeterův zákon, který říká, že máme komunikovat jen s našimi sousedy. Chceme se dostat na to, že každá vrstva, třída nebo funkce má jeden účel, který se dá testovat a můžeme jít vložit s čím má pracovat. Tedy použití nějakých mockovaných tříd pro testovací účely.

##### Udržitelnost
Dávat si pozor na zbytečné ladění výkonu, které dělá kód méně čitelný. Pokud je někde velká flexibility, je zde i velká složitost. Zaměřovat se hlavně na jednoduchost, abstrakci a podobně.


---

## Softwarové metriky

### Rozdělení metrik

##### Přímé vs. Nepřímé
- **Přímé** metriky jsou ty, co můžeme měřit s konkrétními hodnoty a snadno se sbírají. Jde tedy o nějaké počet známých chyb v aplikaci, případně nějaké počty řádků kódu. 
- **Nepřímé** jsou na druhou stranu například nějaká  komplexita kódu, spokojenost zákazníků a podobně.

##### Interní vs. Externí
- **Interní** je například nějaká vnitřní charakteristika systému, procesu nebo zaměstnanců
- **Externí** je spíše spíše důsledkem nějakého vnějšího prostředí

##### Objektivní vs. subjektivní
- **Objektivní** jsou automatizované a nezpochybnitelné. Tedy počet řádků kódu apod.
- **Subjektivní** může být například čas strávený v aplikaci, spokojenost uživatele apod.

### Příklady různých metrik

Metriky se dají kategorizovat například podle těch, které se zabývají velikostí, pak také složitosti a některých, které jsou orientované na třídy.

Před sbíráním metrik je dobré si ověřit, že je reálně potřebujeme. Je nutné si dávat reálné cíle a nebýt paralyzovaný neustálým analyzováním, ale soustředit se na činnost.

##### Metriky pro určení velikost
Tyto metriky mohou ukázat nějaké úsilí, případně porovnání projektů, ale určitě to není nějak zásadní hodnocení ve smyslu kvality aplikace nebo kódu.

- **Lines of code** (LOC)
- **Commented Lines of Code** (CLOC)
- **Non-Commented lines of code** (NLOC)
- **Number of classes** (NOC)
- **Number of methods** (NOM)

##### Metriky pro určení složitosti
Složitost zejména koreluje se schopností dobře testovat a udržovat kód. Čím je složitější, tím je horší se v kódu vyznat a napsat správné testy. Většinou se bere jen syntaktická složitost a ne ta sémantická. Pochopitelnost stejné CC a funkcionality se může lišit v různě napsaných kódech.

- **Cyclomatic Complexity** (CC) - počet nezávislých cest ve zkoumané jednotce
- **Branch Count** (BC) - počet větví
- **Nesting Dept** (ND) - počet zanoření v kódu

##### Metriky pro objektově orientovaný přístup
Typicky se používají v objektově orientovaném přístupu, protože berou nějakou závislost různých metrik vůči třídám. Ukazuje to komplexitu dědění, komunikace mezi třídami a podobně, kdy se opět snažíme nějak zjednodušovat výsledný produkt.

- **Weighted methods per class** (WMC) - vážený počet metod na třídu
- **Depth of inheritance** (BC) - hloubky stromů dědění
- **Number of children** (ND) - počet potomků třídy
- **Coupling between objects** (CBO) - kolik jiných tříd využívá třída


---

## Taktiky pro zajištění kvality (pro jednotlivé atributy)

- **Udržitelnost (maintainability)** - refaktoring na koherentní jednotky, aby bylo místo nutné změny minimální a snadno lokalizovatelné, separace dat od logiky (aby bylo možné jednotku nahradit jinou), decoupling (závislosti na rozhraních, namísto na implementacích), oddělení rozhraní a implementace, obecně dodržování clean code
- **Výkonnost** - caching, paralelismus, asynchronní komunikace/zpracování, detekce a odstranění bottlenecků, odstranění adaptérů, zjednodušení komunikace separace dat od logiky, použití profileru, kontrola použití zdrojů
- **Spolehlivost** - detekce a náprava zdrojů nespolehlivosti, kontrolní mechanismy pro zajištění spolehlivosti, vhodné ošetření chyb, automatický reporting neočekávaných chyb, automatické restarty a obnovy, pravidelný ping (iniciuje volající služby), heartbeat (služba pravidelně reportuje stav), pravidelné snapshoty a rollback v případě pádu, transakce, kontrola vstupů na každé úrovni, odstranění single point of failure
- **Testovatelnost** - refaktoring na závislosti na abstrakcích, decoupling, separace dat a logiky, odstranění globálního stavu, obecně psaní clean code, použití dependency injection
- **Škálovatelnost** - refaktoring na jednodušší samostatně nasaditelné jednotky, extrakce dat pro umožnění paralelizace jednotek, extrakce a samostatné nasazení subsystému, distribuce a/nebo replikace dat (db bývá bottleneck, ostatní věci lze snadněji paralelizovat), je dobré používat stateless architektury, použití load balanceru, cachování, optimalizace databáze, monitorování systému
- **Bezpečnost** - detekce a oprava chyb. použití šifrované komunikace, automatické systémy pro detekci útoků
- **Použitelnost** - zlepšení UX, použití taktik pro zlepšení výkonnosti


---

## Clean Code

- je to sada principů, pomáhají zejména s **čitelností, pochopitelností a udržitelností kódu**
- proslavil se hlavně díky knize Clean Code od Roberta C. Martina (Uncle Bob)
- principů je hned několik - jednoduchost, malé funkce, pojmenovávání, konzistence, neopakování se, srozumitelnost apod.
- je dobré se hodně zabývat čitelností a srozumitelností kódu. Kód bývá mnohem více čten než psán, proto je důležité, aby byl srozumitelný, čas vývojářů je drahý

##### Princip: Smysluplné názvy
- jasné pojmenovávání reflektující doménu problému, dostatečně výstižné. V ideálním případě by mělo být sebevysvětlující a komentáře by neměly být potřeba
- důležitá je konzistence napříč codebase (ideálně stavěná na standardech daného jazyka)
- pokud má proměnná krátký rozsah, stačí kratší názvy, delší rozsah, tím více popisný název
- veřejné API většinou úderné kratší názvy, interní funkce více popisné

##### Princip: Malé funkce a třídy
- rozumná velikost jednotek - ideálně krátké funkce, jednoduché třídy.
- single responsibility principle - obsah jednotky by měl reflektovat její název

##### Princip: Vyhýbání se duplikaci: Don't repeat yourself (DRY)
- každá informace by měla být v systému jednoznačně definována na jediném místě
- dokumentaci generujeme ze kódu, abychom neměli více sources of truth
- definujeme schéma, ze kterého vygenerujeme jak SQL tabulky, tak struktury pro náš jazyk
- vytáhneme sdílenou funkcionalitu do vlastní funkce

##### Princip: Jednoduchost: Keep it simple stupid (KISS)
- jednoduchost před výkonem
- nejlépe fungují systémy, které jsou co nejjednodušší
- není důvod používat složité techniky na jednoduché problémy

##### Princip: You Ain't Gonna Need It (YAGNI)
- nezabýváme se tvorbou něčeho, co nebudeme potřebovat (e.g. neděláme přílišné abstrakce pro podporu možné budoucí funkcionality, pokud to není nutné)
- je lepší věc udělat jednoduše a pak ji snadno upravit, než ji udělat univerzálně, abychom pak zjistili, že nás nenapadl nějaký edge case a musíme to stejně celé přepsat. Vývoj postupuje po malých krůčcích.

##### Princip: Boy Scout Rule
- nech místo, na které si přišel lepší než si ho našel
- postupně zlepšovat každou část kódu


---

## SOLID

##### Single responsibility
- každá třída by měla mít pouze jednu zodpovědnost
- pro každou třídu by měl být pouze jeden důvod, proč by se měla změnit
- e.g. FileReader by se měl starat pouze o čtení ze souboru, ne o zpracovávání čtených dat. Pouze změna způsobu čtení ze souboru může zapříčinit, že musíme měnit FileReader
- nižší provázanost (coupling) tříd - míra spoléhání se na jiné třídy
- vyšší koheze (zaměřenost na jednu věc) - míra toho, jak souvisí různé zodpovědnosti
- Robert C. Martin: *Nikdy nesmí být více jak jeden důvod pro změnu třídy*

##### Open/closed principle
- Otevřeno pro rozšíření, uzavřeno pro modifikaci
- preferujeme přidávání nové funkcionality před změnou zdrojového kódu, co už máme
- menší šance, že něco rozbijeme, na nových třídách nic nezávisí
- používá se implementace rozhraní/abstraktní třídy
- dodržování OCP způsobuje vyšší komplexitu, takže je potřeba ho používat obezřetně a jen tam, kde se často mění/přidává funkcionalita
- dá se přistupovat tak, že se na začátku nepoužívá, první modifikace se povolí a při druhé se již přepíše na principy OCP
- vede to tedy k vyvarování se předčasné abstrakce

##### The Liskov substitution principle
- tříd by měly být nahraditelné jejich potomky, aniž by došlo k narušení chování systému
- všechny podtřídy by měly dodržovat kontrakty rodičů 
- nemělo by se odstraňovat chování rodičů
- problém je, když musíme explicitně ověřovat, o jaký podtyp se jedná - řeší *polymorfismus*
- pokud dvě třídy sdílí mnoho funkcionality, ale nejsou nahraditelné, je vhodné je upravit na podtřídy nové třídy obsahující sdílené chování
- pokud nemáme zastupitelný kód tak nefunguje polymorfismus

##### Interface segregation principle
- klienti kódu by neměli být závislí na metodách, které nepoužívají
- dělej malá a jednoduchá rozhraní namísto velkých složitých
- pokud potřebuji třídu převést na string, implementuji např. v Rustu pouze trait Display
- pokud je to možné, nechávejme klienta si definovat rozhraní
- pokud je to možná, nenuťme záviset klienta na věcech, které nepotřebuje

##### Dependency inversion
- moduly by měly záviset na rozhraních, ne na konkrétních implementacích
- nechci aby moduly vyšších úrovní záviseli na nižších úrovních
- snižuje se tím provázanost modulů, je možné poskytnout vlastní implementaci či mockovat
- modul by měl definovat na čem závisí a to by mu mělo být poskytnuto
- modul by si neměl vytvářet zdroje sám (e.g. repo si nemá tvořit připojení do databáze)
- typické řešení je *Dependency Injection*


---

## Refaktoring

Je to proces kdy měním vnitřní kód, aniž by se měnilo jeho vnější chování za cílem zlepšovat jeho vnitřní strukturu. Pokud chceme refaktorovat, musíme mít skvěle pokrytou funkcionalitu testy, které kontrolují nechtěné chyby v chování. Nedodáváme žádnou novou funkcionalitu.

Kód, který se dobře čte a udržuje nemusí být ten nejrychlejší/nejefektivnější (abstrakce mohou něco stát). Obvykle nám mírné snížení výkonu za vyšší čitelnost nevadí, ale nemusí to být vždy pravda.

**Refaktoring** (podstatné jméno) - je to systematické proces změn vykonaných uvnitř systému, aby byl lehčí na pochopení a jednoduší pro následné úpravy a to beze změny jeho vnějšího chování.

**Refaktoring** (sloveso) - je to restrukturalizování systému za použití série menších refaktorování beze změny jeho vnějšího chování

##### Techniky refaktorování
- **Extrakce funkce** - kus kódu funguje jako jednotka/potřeboval by komentář => vytáhni ho do funkce, dej tomu přiléhající jméno, bude možné to použít na více místech
- **Inline funkce** opak extrakce, vhodné pro triviální situace jako `isMoreThanFiveEven(x)`
- **Nahrazení metody objektem metody** - fajn, když funkce používá hodně lokálních proměnných, ze kterých se stanou se atributy struktury
- **Move method/field** - z jedné do jiné struktury, pokud to dává smysl (třeba doménově)
- **Extrakce/inline třídy** - z třídy obsahující množinu polí, která jsou related, vytáhneme nový objekt, který bude původní třída obsahovat/nebo naopak pro inline
- **Early return** - obecně chceme, aby funkce popisovala správný/bezchybný tok programu. Pokud při zpracování funkce objevíme chybu ve vstupních datech, hodíme tam return. V takových případech nepoužíváme `if-else`, ale `if return`
- **Rename** cokoliv
- **Nahrazení magických hodnot** - dáme číslo uvnitř programu do konstanty
- **Seskupení mnoha parametrů do struktury** - typicky pokud máme více jak 3 atributy
- **Sbalení hierarchie** - nahrazení nelišících se rodičů a potomků jednou třídou
- **Extrakce supertřídy** - pokud dvě třídy mají společné vlastnosti, vytvořme rodiče


---

## Testování

**Definice**: proces evaluace, zda systém splňuje specifikované požadavky

Většinou testování ukazuje chyby, ale ne bezchybnost, protože málokdy pokryjeme testy naprosto všechny možnosti. Testy by se také měli zabývat spíše konkrétními věcmi než několika věcmi naráz. Díky tomu by měl při chybě padnou je jeden konkrétní test a ne všechny. V nejlepším případě testy píše někdo jiný než autor napsané funkcionality.

Můžeme rozdělit mezi hlavní testování, jako jsou:
- **Whitebox (strukturální)** - vidíme zdrojový kód a můžeme vstupy testů cílit na spouštění kritických míst, například jde o unit, integration, performance testy
- **Blackbox (funkcionální)** - nevidíme co se děje uvnitř systému, pouze sledujeme vstupy a výstupy, jde tedy o například akceptační nebo systémové testy

##### Principy testování
- **Citlivost** - raději selžu pokaždé než někdy
- **Konzistence** - konzistentní výsledky i po několika pokusech
- **Redundance** - více způsobů testování má výší pravděpodobnost nalezení chyby
- **Omezení** - vhodné omezení mohou redukovat těžké problémy an jednoduché
- **Rozdělení** - větší komplexní test raději na menší testy
- **Viditelnost** - měření pokroku testování, přiblížení k cíli v harmonogramu apod.
- **Feedback** - držet si například nalezené chyby z minulých projektů apod.


Pokud při provozu narazíme na chybu, je důležité ji ihned přidat do testovacího scénáře. Také pokud chceme ověřovat, že testy fungují, mohou se dělat nějaké náhodné mutace v kódu a dívat se, zda testy popadají a odhalí je. 

Pokud se testují vstupy, je dobré si udělat nějaké kategorie a vybrat z každé z nich několik zástupců. Důležité je stanovit si, co jsou kritické funkcionality v aplikaci a ty pokrýt nejvíce testy a dbát na ně větší důraz. Testování také zjednodušují nevalidní stavy jako v automatech a podobně.

##### Pokrytí testy
- můžeme sledovat různá kritéria
	- **line coverage** - řádky kódu
    - **function coverage** - pokryté funkce, jde o to, zda byla aspoň jednou zavolána
    - **branch coverage** - pokryté logické větve programu
    - **condition coverage** - každá boolean podmínka byla vyhodnocena jako true i false
- pokrytí znamená, že danou cestou kódu prošel aspoň jeden test, metrika je obvykle v procentech
- mnohdy není 100% pokrytí možné a zároveň 100% pokrytí neznamená bezchybnost
- některé části kódu je mnohem těžší pokrýt, než jiné


---

## Druhy testů
### Jednotkové (unit) testy  (whitebox)
- validace, že se izolovaná jednotka kódu (funkce/třída) chová tak, jak bychom očekávali
- testy jsou automatizované, rychlé, jednoduché, čitelné, deterministické, každý testuje jednu jedinou věc a mohou běžet paralelně, protože na sobě nezávisí
- izolujeme jednotku od zbytku systému pomocí **test doubles**
    - *dummy objekt* - nikdy se nepoužije, ale je potřeba třeba jako parametr
    - *fake objekt* - obsahuje implementaci na předepsané chování
    - *stub* - vrací vždy stejnou věc, jednoduchý mock
    - *spy* - kontrolujeme, kolikrát se volal, případně s jakými parametry
    - *mock* - předprogramovaný objekt (pro parametr A, vrať B)
- fáze testování rozdělené do *AAA*, kdy Act by mělo být co nejkratší
	- **arrange** - příprava na testování,
	- **act** - provedené testovaného chování,
	- **assert** - ověření vrácených hodnot vůči očekávaným
- e.g. cargo test, jest, junit

### Integrační testy (blackbox, whitebox)
- sledují, zda spolu jednotky interagují tak, jak bychom očekávali
- může jít například o testování komunikace repository s databází
- pomalejší, větší a složitější, než unit testy
- pro testování UI použijeme *Playwright* (dřív se používalo *Selenium*)

### Systémové testy (blackbox)
- ověření, že systém splňuje specifikované funkční požadavky
- testují použitelnost, kapacitu, výkon, splnění funkcionality, bezpečnost apod.
- benchmarking, penetrační testování, uživatelské testy...
- lze automatizovat pomocí programem ovládaným prohlížečem (Playwright)

### Akceptační testy (blackbox)
- ověření, že systém splňuje business požadavky a je připraven k vydání
- může být ve formě odškrtávání políček s požadavky na systém, které zákazník předem určil
- prováděny se zákazníkem
- testování použitelnosti, kompatibility s OS apod.

### Další testy
- **Regresní testování** - je to skupina testů, kterou sledujeme, zda změny v systému nepřinesly odhalení chyb
- **Smoke testy** - většinou velmi jednoduchý a krátký test, kdy sledujeme, zda vybrané kritické funkce fungují v novém prostředí. Pokud ne, nemá vůbec cenu nasazovat a testovat další věci
- **Sanity testy** - jako smoke, ale spouští se pro ověření nápravy chyb/přidání funkcionality, jsou více podrobnější než smoke testy, ale také mají za úkol před regresními testy ověřit, zda vše funguje tak jak má a ušetřit tím zdroje a čas
- **A/B testování** - používáme dvě varianty a sledujeme, která je úspěšnější (hlavně UI)
- **Fuzzing** - posílání na vstup nevalidních a náhodných hodnot a monitorování reakce programu na tyto nečekané vstupy. Testuje se tím také bezpečnost softwaru.
- **Property-based testing** - testujeme vlastnosti, které jsou pravdivé. Nemusíme tedy pro každý vstup psát vlastní test, ale více vstupů se testuje naráz. Jde o vlastně generování definovaných vstupů

### Test-driven development (TDD)
- skládá se z tří fází, red, green, blue, které iterativně aplikujeme. V každé části se snažíme docílit pouze jedné věci
- **red/test** - vytvoříme test, která padá, pro co nejmenší část funkcionality
- **green/write** - implementujeme funkcionalitu co nejjednodušeji tak, aby testy prošly
- **blue/refactor** - upravíme implementaci tak, aby odpovídala standardům

### Behaviour-driven development (BDD)
- se zákazníkem sepíšeme chování systému jako jednotlivé scénáře
- scénáře slouží vývojářům i testerům jako jednotky
- e.g. gherkin, cucumber - konstrukty given, when a then (jako AAA) se používají pro definici scénářů v english-like jazyce srozumitelném zákazníkovi, tyto scénáře se pak objevují i v testech


---

## Ladění a testování výkonu

Cílem je identifikace a řešení případných problémů týkajících se rychlosti, odezvy a propustnosti systému, nalezení hranic. Důležité je provádět tyto testy nad daty, které se vyskytují na produkční aplikaci a také na HW, který je použitý v produkci, jinak to nedává smysl.

Výkon lze obecně zvýšit za cenu dalších atributů (například maintainability), proto je nutné volit správný kompromis pro náš případ.

Základní rozdělení je na:
- **Load testing** - zátěžové testy, sledujeme jak systém zvládá dlouhodobější zátěž
- **Stress testing** - sledujeme, jak se systém reaguje na mnoho požadavků v krátkou dobu

Běžící systém je také vhodné dlouhodobě monitorovat, abychom odhalili další slabá místa. Pokud díky testování zjistíme chyby, použije se profiler, případně také flame chart, kdy se zjistí jaké části zabíraly nejvíce času a které je potřeba optimalizovat.

Testování například webových stránek simuluje mnoho uživatelů v jeden moment. U databázových systémů jsou testovány rychlosti zápisu a škálovatelnost při vyšším zatížení a podobně.

##### SW Profiling
Jde o dynamickou analýzu programu pro měření například časové či paměťové složitosti, případně také měří trvání mezi voláním jednotlivých funkcí.

##### Ladění
Metodický postup pro hledání a snižování chyb v systému. Ladění se sbírá díky výpisům z nějakých ladících nástrojů, například jde o Valgrind, debugger apod.

Mezi techniky ladění může patřit výpisy na konzoli, krokování za použití debugerru a nebo logování, které je možné používat i za běhu v produkci.


---

## Proces řízení kvality ve vývoji softwarových systémů

**Software quality management (SQM)** - je to kolekce několika procesů, které se starají a zabezpečují, aby SW produkt a jeho služby společně s jejich životním cyklem splňovali stanované kvality organizace a dosahovali spokojenosti zákazníka.

**SQM** zejména definuje tyto věci:
- *Procesy* a jejich zodpovědné osoby
- *Požadavky* na jednotlivé procesy
- *Měření* procesů a jejich výstupy
- *Zpětnou* vazbu celého životního cyklu SW produktu

SQM dále zahrnuje kategorie:
- *Plánování kvality SW* - specifikace funkčních i nefunkčních požadavků, stanovení hodnotících kritérií, rizik, určení metrik, podrobný popis a rozvržení aktivit k zajištění kvality
- *Zabezpečení kvality SW* (assurance) - definice a kontrola procesů, které povedou k zajištění  kvality a prevenci defektů (mimo jiné nastavení CI/CD)
- *Kontrola SW kvality* - kontrola, zda produkt/jeho části splňují požadavky (včetně požadavků na kvalitu) a jejich vývoj se řídí definovanými procesy, monitoring zda se držíme procesů a vytyčených cílů
- *Zlepšení kvality procesu* - snaha zlepšit procesy, abychom docílili zlepšení kvality

Podle ISO standardu existuje 6 úrovní procesu, podle kterých se hodnotí vyspělost organizace:
- úroveň 0 - nedokončený proces
- úroveň 1 - vykonaný proces
- úroveň 2 - řízený proces
- úroveň 3 - zavedený proces
- úroveň 4 - předvídatelný proces
- úroveň 5 - optimalizovaný proces

**Capability Maturity Model** definuje úrovně vyspělosti organizace v kontextu zajištění kvality
- *úroveň 1 Výchozí* - chaos, nepředvídatelná cena, plán
- *úroveň 2 Řízený* - intuitivní, cena a kvalita jsou proměnlivé, plán je pod vědomou kontrolou, neformální metody & procedury
- *úroveň 3 Definovaný* - orientace na kvalitu, spolehlivé ceny a plány, stále nepředvídatelný výkon systému kvality
- *úroveň 4 Kvantitativně řízený* - měření, promyšlená a statisticky řízená kvalita produktu
- *úroveň 5 Optimalizující* - automatizace a zlepšení výrobního procesu, prevence chyb, inovace technologie


---

## Notes

### Prevence problémů kvality
- následování best practices a konvencí, obecných (SOLID, clean code) i pro danou technologii/jazyk (eslint, cargo fmt)
- využití principů návrhových vzorů
- techniky jako TDD, párové programování, code reviews
- použití procesních standardů (ITIL), agilních technik (scrum, kanban)
- automatizované testování, CI
- komunikace, jednotný jazyk
- fail-fast přístup - snažíme se detekovat problém ve vstupech, namísto abychom klidně akceptovali cokoliv a pak se divili při neočekávaném chování
- design by contract - naše metody (zvlášť při tvorbě) mohou vyžadovat splnění určitého kontraktu (lze vynutit asserty), aby mohly poskytnout garance o výstupech. Je možné použít podmíněnou kompilaci a mít kontrakty třeba jen ve vývojovém prostředí (tím se ale můžeme připravit o přesné určení místa problému na produkci) 

Nonfunkcionální problémy kvality se řeší architekturou. Pro prevenci těchto problémů je možné vytvořit model systému a na něm si simulačně ověřovat požadavky (e.g. schopnost obsloužit určitý počet požadavků za určitý čas) a případně odvodit nároky na jednotlivé komponenty (třeba maximální dobu zpracování požadavku v daném komponentu).

Pro ověření kvality je také  možné použít formální verifikaci (používá se třeba pro dokazování správnosti algoritmů).

### Detekce problémů kvality
- code reviews (vzájemné mezi vývojáři), inspections (formální, je fajn použít formulář; ukazuje to přípravu, na nic se nezapomene a zároveň se odfiltrují zbytečnosti, nelpíme na stylu, řešíme správnost, dodržování standardů...)
- (automatizované) testování (rust\cargo test)
- statická analýza (rust\cargo clippy, borrow checker, sonarqube) - nespouštíme kód

### Špatný kód
- pomíchané úrovně abstrakce
- nízká koheze (megatřídy, dlouhé funkce..)
- kruhové závislosti (je pak závislost na implementaci, blbě se sleduje flow a vztahy, blbě se to testuje, udržuje a škáluje)
- duplikace kódu
- spousta parametrů
- blbé názvy
- dělání věcí příliš "chytře", když to není nutné
- nedodržování standardů/vhodných konstruktů jazyka
- magické konstanty

#### Code smells a řešení

!Jednotlivé taktiky mohou být vzájemně v rozporu, je potřeba si určit, čeho chceme docílit! (e.g. udržitelnost vs výkon)



### Sledování problémů kvality
- issue tracking
- správa technického dluhu (tracking, vyhrazení času na jeho nápravu)
