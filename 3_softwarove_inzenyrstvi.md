# Softwarové inženýrství

> Životní cyklus SW, proces vývoje a řízení softwarového vývoje. Metodika (Rational) Unified Process (UP, RUP), agilní metodiky a principy agilního vývoje SW. Nasazení a provoz softwarových systémů. Údržba softwarových systémů, znovupoužitelnost. Příklady z praxe pro vše výše uvedené. [PA017](https://is.muni.cz/auth/el/fi/podzim2020/PA017/um/cz/)

## Životní cyklus SW, proces vývoje a řízení softwarového vývoje

##### Definice co je to software

> Software je tvořen celkovým souhrnem počítačových programů, procedur, pravidel a průvodní dokumentace a dat, která náleží k provozu počítačového systému.

Kdybychom nějak chtěli definovat co je to *vývoj softwaru* tak je to proces, kdy měním *uživatelovy potřeby* na *požadavky na software*, které se mění na *návrh softwaru*. Ten se poté implementuje na *kód* a v poslední řadě na je otestovaný a zdokumentovaný, případně certifikovaný změněn na *operační použití*.

##### Základní aktivity vývoje SW
- **Specifikace** - definuji omezení, definuji funkcionality a nároky
- **Vývoj** - na základě specifikace tak implementuji SW
- **Validace** - software se testuje a kontroluje zda splnil očekávání a vyhovuje uživateli
- **Evoluce** - software se mění a rozvíjí na základě dalších požadavků zákazníka

##### Viditelné znaky při vývoji softwaru
- **Artefakty** - zdrojové soubory, data, dokumentace, výpisy
- **Procesy** - pracovní postupy, pravidla a interakce mezi členy

##### Charakteristiky vývojových procesů
- **Srozumitelnost** - je proces snadno srozumitelný a pochopitelný?
- **Viditelnost** - je postup vývoje nějak dobře viditelný zvenku?
- **Spolehlivost** - umožňuje mi odchytat a detekovat chyby než způsobí problémy?
- **Přijatelnost** - přijali ti, co vyvíjí software daný proces?
- **Robustnost** - když nastane problém, může i dále pokračovat?
- **Udržovatelnost** - umí se dobře přizpůsobit měnící se firmě?
- **Rychlost** - jak rychle lze proces realizovat, aby se dostal produkt k zákazníkovi?
- **Podporovatelnost** - existují nástroje, které mi zlepší práci s procesem?


### Životní cyklus SW

Existuje několik základních životních cyklů. Každá z nich má nějaké výhody a nějaké nevýhody. Vždy nějakým způsobem obsahuje fáze analýza, návrh, implementace, testování a provoz (včetně nasazení). Rozdíly jsou v tom, zda a jakým způsobem dělíme projekt na uchopitelnější části. Důsledkem toho jsou i různé způsoby, jakým se vývoj řídí.


##### Model životního cyklu: Vodopád
Velmi oblíbený model mezi manažery. Může jít o nejlevnější způsob vývoje SW pokud jsou věci dobře, nicméně věci většinou dobře nejdou a tento model většinou není moc robustní.

Tento model se skládá z kroků:
- **Analýza**
	- sběr požadavků klienta je klíčový pro tento proces a měl by být kvalitní
	- je důležité rozlišovat mezi tím, co říká že potřebuje, a co skutečně potřebuje
	- zajímá nás *co* a *proč*, často ale klient zmiňuje *jak*. V takových případech je důležité se ptát *proč*. Může jít o legitimní důvod, ale také třeba o nevědomost.
	-  výstupem například studie proveditelnosti, dokument požadavků
- **Návrh**
	- návrh architektury, jednotek, výběr technologií, plán testování
	- výstupem například diagramy, wireframy, prototypy
- **Implementace**
	- tvorba systému dle návrhu
	- výstupem jsou zdrojové soubory
- **Testování**
	- ověření, zda splňuje SW definované požadavky
	- výstupem jsou protokoly o testování systému apod.
- **Provoz**

Výhody:
- snadný na řízení
- pokud vše jde hladce, je to nejlevnější způsob

Nevýhody:
- většinou všechno nejde hladce
- špatně se reaguje na změny (musíme se vracet do předchozích fází modelu)
- zákazník předem nedokáže přesně a úplně definovat, co potřebuje
- v praxi nejsou kroky v tomto pořadí dodržovány (testovat chceme ideálně při vývoji, něco chceme ukázat netrpělivému zákazníkovi...)


##### Model životního cyklu: Inkrementální model
Jde prakticky o modifikaci velkého vodopádu na několik menších vodopádů. Projekt se rozděluje na inkrementy a každý z nich se podle priority vyvíjí a dodává postupně. Po nasazení tak vytvoříme verzi SW, dostaneme zpětnou vazbu od zákazníka a vyvíjíme další verzi.

Dochází zde k vývoji podle obrysové specifikace. Tedy navrhne se na začátku jak by systém měl vypadat a dále se rozvíjí po částech. Na toto většinou potřebujeme kvalitní a menší týmy, dokumentace většinou moc není protože se hned zahazuje a je zde tedy špatná viditelnost procesu.

Výhody:
- systém je dodáván po částech, celkové náklady jsou distribuovány
- není potřeba vytvářet velký tým, protože práce je dodávaná po částech
- uživatel vidí systém v raných fázích projektu. Lze rychle reagovat na zpětnou vazbu uživatele
- o nutnosti změny se dozvíme dříve a její zavedení bude levnější (není třeba vše překopávat, přidáme inkrement se změnou)

Nevýhody:
- náklady na vývoj jsou vysoké kvůli dodávce systému po částech
- model vyžaduje náročné plánování k distribuci práce
- pro připojení modulů vyvinutých s každou fází je nezbytné důkladně popsat rozhraní


##### Model životního cyklu: Spirála
Jde o kombinaci iterativního přístupu a vodopádu. Zatímco inkrementální model tak je navržený na začátku a vyvíjen postupně, spirála klade důraz na opakování, kdy na konci každého cyklu je kladený důraz na analýzu rizik, zpětnou vazbu a plán dalšího vývoje.

Fáze: *Analýza, Návrh, Implementace, Testování, Zpětná vazba, plán dalšího cyklu*
	
Ve srovnání s inkrementálnímu modelu nemusíme mít po každé iteraci hotovou část nasazeného systému (inkrement je třeba ve formě jasných požadavků, návrhu systému, nebo tak). Cykly aplikujeme i na jednotlivé fáze vodopádu. V tomto modelu lépe pracujeme s nejistotou, ale trvá to déle než u vodopádu například.


##### Model životního cyklu: Prototypování
Vytvoříme prototyp systému, abychom porozuměli, jakým způsobem chce zákazník systém používat a co od něj očekává. Po analýze prototypu ho **zahodíme** a začneme práci na reálném systému, kde využijeme vhodný model


##### Model výzkumník
Navrhni systém a implementuj ho. Vyhovuje? Super. Nevyhovuje? Zpět k návrhu/implementaci. Takovýto přístup nelze pořádně řídit, neexistuje dokumentace, řešitelé jsou obtížně nahraditelní, jde o experimentování.


Nezávisle na modelu je důležité nastavit správnou komunikaci, definovat a používat jednotný jazyk. Pokud chceme cokoliv řídit, je potřeba mít informace o aktuálním stavu, dodržování plánu, očekávaných změnách, problémech...

Hlavní metodiky řízení softwarových projektů jsou 
- **prediktivní metodiky** (e.g. RUP) 
- **agilní** (e.g. SCRUM).


---

## Metodika (Rational) Unified Process (UP, RUP)

*Unified process* je pouze obecný rámec. *Rational unified process* do toho přidává odpovědnosti v týmech, role, konkrétní postupy a podobně. Vyžaduje velké plánování předem.

Hlavní rysy
- *iterativní* a *inkrementální*
- *prediktivní* - musíme tedy znát výsledek než začneme a máme pevné požadavky, pokud se nestíhá nebo je problém, zvýší se zdroje, ale cíl je daný a musíme ho dokončit
- *rigidní* - jsou zde velké důrazy na procesy
- *řízený riziky* - reaguje na změny, riskantní věci se řeší na začátku každé fáze
- *architektura je středobodem* - existuje architektonický tým, se kterým ostatní týmy konzultují případné nejasnosti/problémy, slouží jako centrální komunikační uzel
- pevná *kontrola nad procesy* a týmem, typicky kdo, co, kdy a jak je pevně definované
- vhodný, pokud potřebujeme *pořádnou dokumentaci* (UML diagramy)
- hodí se pro *velké a heterogenní produkty*, velké týmy
- můžeme použít různé životní cykly

##### Výhody:
- zákazník není při vývoji potřeba
- definice produktu je zakotvena v kontraktu
- zákazník přesně ví co dostane
##### Nevýhody
- pracujeme s fixními termíny, rozpočtem i funkcionalitou
- v reálu se termíny a rozpočet může lehce měnit v závislosti na vývoji
- dodatečné změny v požadavcích jsou problém
- potřeba více času k plánování
- složitý kontrakt, je třeba myslet na všechno (exhaustive kritéria přijetí, penále...)

##### Jednotlivé fáze
Každá fáze si  prochází postupně celým cyklem workflows. Jen se liší poměry práce. Délka práce na jednom cyklu by měla být od 1 měsíce do 3 měsíců. Více jak 3 měsíce už se nedoporučuje.

![|600](img/20230523215135.png)

Postupné skupiny iterací
- **Inception** (Zahájení) (1 iterace)
	- řešíme proveditelnost, zachycujeme klíčové požadavky, rizika
	- popis významných požadavků s dopadem na architekturu
	- identifikace dalších systémů, se kterými máme komunikovat
	- na konci známe cíle, hrubou architekturu
	- co se používá pro podobné systémy? s čím máme zkušenosti?
	- určení použitých technologií
	- určení orientační ceny, časového plánu a rizik
	- diagramy - *Activity diagram*
	- výstup - cíle
- **Elaboration** (Příprava) (2 iterace)
	- řešíme požadavky, architekturu
	- na konci máme architekturu, návrh systému reflektující požadavky
	- mohou se dělat prototypy, implementovat rozhraní pro externí systémy
	- zkouší se technologie
	- diagramy: *Class diagram*, *Use case diagram*, *Sequence diagram*
	- výstup: základní architektura, podepsání specifikace zákazníkem, upřesněné plány
- **Construction** (4 iterace)
	- tvoříme systém, testujeme, nasazujeme
	- na konci máme beta verzi, relativně stabilní a otestovanou, připravenou k použití
	- diagramy: *komponentový diagram*, *class diagram*, *objektový diagram*
	- výstup: implementovaná funkcionalita
- **Transition** (2 iterace)
	- hledáme a opravujeme chyby, děláme manuály, poskytujeme konzultace
	- testování s uživateli (beta, na základě feedbacku děláme změnové požadavky)
	- akceptační testy
	- výstup: release produktu

 Workflows v rámci vývoje
- **Business modelování** - activity diagram
- **Požadavky** - use case diagram
- **Analýza a návrh** - sequence, class, activity diagrams
- **Implementace** - class, object, component, diagrams
- **Testování** - use case, class, activity diagrams
- **Deployment** - deployment diagram


---

## Agilní metodiky a principy agilního vývoje SW

Trochu opačný přístup, kdy se více dbá na lidi a na flexibilitu. Tedy pokud dojde k problému, raději budeme na tuto událost nějak reagovat, než se jí nějak dopředu snažit bránit.

Velký rozdíl je v tom, že máme nějaké fixní zdroje a čas. Funkcionality je tedy více variabilní a nemusí se stihnout implementovat vždy vše ve smluveném času. Máme jednoduchou dokumentaci, protože systém se často mění, komunikujeme intenzivně se zákazníkem a snažíme se minimálně plánovat předem. Metodika je také dobrá pokud potřebujeme mít brzo nějaký hmatatelný produkt, který se ukáže zákazníkovi.

> Postavili jsme dům a plot, v rozpočtu zbývají zdroje na garáž, nebo bazén. Co z toho chcete?

##### Základní prvky
- *Individualita* a *interakce* mají přenost přes procesy a nástroji - více zkušení lidé
- *Fungující software* má přednost před velkou a obsáhlou dokumentací
- *Spolupráce se zákazníkem* má přednost před nějakou velkou smlouvou na začátku
- *Reakce na změnu* má přednost přes plněním plánu

##### Společné rysy všech agilních metodik
- *Iterativní* a *inkrementální* vývoj v krátkých iteracích - dodáváme zákazníkovi po částech a zahrnujeme zákazníka do vývoje, aby měl neustále přehled co se vyvíjí, mohl testovat nové inkrementy a na konci věděl přesně co dostává.
- *Komunikace mezi zákazníkem a vývojovým týmem* - čím je zákazník blíže týmu tím lepší. Může poté oponovat a zasahovat do návrhů, případně testovacích scénářů a poskytuje cenou zpětnou vazbu.
- *Průběžné automatizované testování* - ověřujeme průběžně funkcionalitu a implementované části vůči sadám testů. Při každé změně tyto testy pouštíme abychom zachovali integritu celého systému.


Mezi konkrétní metodiky se řadí například *Extreme programing*, nebo *SCRUM*.

### Extreme programing
Většinou pro velmi malé týmy, kde se musí rychle vyvíjet produkt, jehož zadání se často mění, je velmi nejasné a podobně. Nejsou zde žádné věci kromě kódu. To je zdroj veškerých informací. Velmi malé inkrementy, jednoduchost, rychlá zpětná vazba.

Tento přístup pracuje hlavně s:
- *Malé přírůstky* - velké integrace selhávají, přidávejme tedy malé inkrementy
- *Jednoduchost* - obtížné, protože to jde proti programování, kde je potřeba plánovat, ale máme tým zkušených lidí, kteří ví kde složitost přidat a kde použít jednoduchost.
- *Rychlá zpětná vazba* - provedeme akci, zkontrolujeme stav systému, vyhodnocujeme a jde se dál. Vše v rychlém sledu
- *Kvalitní práce* je také předpoklad úspěšného projektu, jinak to členy týmu nebude bavit
- *Využití změny* - strategie, kdy se snažíme držet neustálou flexibilitu, abychom dobře reagovali pokud přijde změna.

Používá se extrémní přístup ve formě:
- Osvědčily se *revize kódu*, pak programujme velmi často párově
- Osvědčilo se *testování*, pak testujme všude za každou cenu
- Osvědčil se *návrh*, pak každý den dělejme návrhy a refaktorujme

### Feature-Driven Development
Vyvíjí se po malých částech, kdy každá nová vlastnost přináší nějakou hodnotu uživateli systému. Měříme hlavně pokrok ve vývoji projektu a kontrolujeme vývojový proces. Typicky každé dva týdny tak přibude nová vlastnost systému.

Celkem je 5 částí, kdy první 3 jsou plánovací a jsou sekvenční. Ty další jsou poté již iterativní.

![|600][img/feature-driven-development.png]

### SCRUM
*Nejčastěji využívaná* agilní metodika. Je opět *iterativní* a *inkrementální*, která *jednoduchá* a předpokládá *použití dalších nástrojů*, případně procesů. Je vhodná pro menší týmy *do 15 lidí* a volíme ji, pokud týmy jsou schopné vést *samostatnější práci* a potřebujeme rychle vytvořit nějaký produkt, který předáme zákazníkovi.


##### Role
- **Product owner** - reprezentuje zákazníky a zúčastněné strany, má největší přehled o požadavcích na produkt, spravuje product backlog, hlavní komunikace je komunikace s týmem, zákazníkem a stanovuje priority
- **Scrum master** - zodpovědný za dodržování metodiky, řeší procesy a odstraňuje překážky, snaží se o hladký průběh bez komplikací
- **Tým vývojářů** - 3-9 lidí, soběstačných, samo organizujících se. Jsou to analytici, návrháři, programátoři a testeři. Hlavní zodpovědností je dodat produkt

##### Artefakty
- **Product backlog** 
	- obsahuje veškerou zbývající požadovanou funkcionalitu ve formě *user stories*
		- user story obsahuje *story points*, které určují odhad náročnosti
		- náročnost se dá například vyřešit přes *planning poker*
		- také obsahuje seznam rizik
		- akceptační kritéria (Given ... When ... Then ...)
		- prioritu (MoSCoW), podle náročnosti, přínosu, rizika
		- náročnost většinou jako fibonacciho posloupnost
	- tvořen celým scrum týmem, spravuje ho product owner
	- v praxi jde o tabuli (reálnou/virtuální) se sticky notes
- **Sprint backlog** 
	- část product backlogu (množina user stories), která se má provést v daném sprintu
	- stories jsou rozděleny na jednotlivé úkoly, u každého je určen časový odhad v hodinách
	- úkol má fáze Todo, In progress a Done
	- úkoly si k práci vybírají vývojáři dle vlastního uvážení, může se měnit i priorita
	- žádné úkoly (ani user stories) nemohou být v rámci sprintu přidány/odebrány
	- spravován týmem vývojářů
- **Product increment**
	- všechny předměty product backlogu, které se splní během sprintu
	- tvořen týmem vývojářů, testován zákazníkem, a schválený product ownerem
	- je nutné, aby byl použitelný a byl splněn (dle definice scrum týmu)
	- stav produktu poté co dokončím sprint

##### Událost (Eventy)
- **Project planning**
	- tvorba PMBOK (product management body of knowledge)
	- tvorba product backlogu
	- výběr klíčových strategií (komunikace, rizika, řízení změn, kvalita...)
- **Sprint planning**
	- probíhá na začátku sprintu, cca 8 hodin
	- účastní se celý scrum tým
	- vytyčuje se cíl nadcházejícího se sprintu (co chceme udělat)
	- vybíráme věci z product backlogu a přiřazujeme jim úkoly
- **Sprint**
	- iterace soustředěná na vývoj funkcionality v sprint backlogu
	- cílem je vytvořit použitelný a potenciálně vydatelný product inkrement
	- pracuje na něm celý scrum team
	- product owner řeší komunikaci, vývojáři vyvíjí, scrum master sleduje dodržování procesů
	- analýza, návrh, implementace, testování
	- maximálně 1 měsíc, většinou ale na 14 dní, všechny sprinty trvají stejnou dobu, 
	- po sprintu sledujeme [team velocity](./3_softwarove_inzenyrstvi.md#team-velocity), máme lepší odhad pro budoucí plány a upravujeme díky tomu rozsah backlogu
- **Daily scrum (standup)**
	- 15 minut každý den, účastní se vývojáři a možná i scrum master
	- co jsem dělal včera, co budu dělat dneska, narazil jsem na nějaké problémy?
- **Sprint review**
	- 4 hodiny, účastní se celý scrum team a také třeba zákazník, uživatel
	- proběhne předvedení inkrementu
	- proberou se případné problémy, změny, odpovídá se na případné otázky zákazníka
	- proberou se případné změny product backlogu
	- případně se přepočítá předpokládané datum dokončení
	- probere se, co by se mělo dělat dál, upraví se priorita/pořadí v product backlogu
- **Sprint retrospective**
	- 3 hodiny, účastní se scrum team
	- řeší se procesy - rozložení práce, splnil se cíl, je třeba něco upravit?
	- řeší se vztahy - klapalo to? potřebuje někdo užší spolupráci?
	- řeší se nástroje - dobrá komunikace? dostatečná transparentnost? 
	- řeší se lidi - měl někdo trable? někoho pochválíme?
	- co nefungovalo, co můžeme zlepšit
	- ideálně se vymyslí jedno zlepšení procesů, které se v příštím sprintu bude používat
	- případně se upraví klíčové strategie, rizika
- **Project retrospective**
	- uzavření projektu s týmem
	- řešíme z čeho jsme se poučili, co se povedlo a nepovedlo

##### Výhody
- flexibilní, nejsou potřeba velké specifikace na začátku
- zákazník má rychle s tím pracovat, můžeme se adaptovat na změny

##### Nevýhody
- potřebujeme nějaký čas i od zákazníka
- špatně se odhaduje cena a nějaké termíny
- aplikace většinou potřebuje hodně refaktorovat v průběhu

##### Ukončení SCRUM
SCRUM může skončit, když
- product backlog je prázdný (vše hotovo)
- pokud je zbytek product logu považován za nedůležitý zákazníkem
- dojde čas/peníze
- udělali jsme poslední sprint a je sice co spravovat, ale defekty jsou přijatelné
- product owner/stakeholder se rozhodne ukončit projekt


Návrh a architektura se mohou dělat průběžně pro jednotlivé user stories, nebo se do procesu zavádí jako standard. Kontrakt je obyčejně na počet lidí a na období. Těžko se určuje výsledná cena a termíny. Zákazníka většinou zahrnujeme do procesu, což je nějaký overhead.

##### SCRUM termíny

**Burndown chart a Team velocity**
- Ukazuje kolik práce zbývá a jak si vedeme oproti plánu
- Team velocity jsou dokončené story pointy za sprint, je vidět v Burndown Chartu
- Velocity je jednoduše jen počet dokončených story pointů vyděleno počtem sprintů

![600](img/20230525221638.png)

**Planning poker**
Pro každé story každý z týmu provede odhad, odhady se zveřejní najednou. následuje diskuze, dokud se na bodech za dané story všichni neshodnou (doporučené použité body jsou podle fibbonacciho posloupnosti)


---

## Nasazení a provoz softwarových systémů

##### Nasazení
Jedná se všechny kroky, procesy a aktivity, pro zpřístupnění a systému a nebo jeho verze uživatelům. Zahrnuje to instalace našeho softwaru, konfiguraci, integraci se systémy i testování, abychom zabezpečili fungování softwaru v novém prostředí.

Tyto prvky nasazení mohou být manuální, případně automatické. V moderním vývoji se klade důraz právě na automatizované nasazení. V *DevOps* tak právě Operations část se zabývá zkrácením procesu nasazení a jeho automatizací. V *Continuous Delivery* se tedy hlavně řeší automatizované testy, produkční prostředí a automatizovaný deployment. Pro automatizaci používáme například *Kubernetes*.

Do nasazení se dá přidat i školení uživatelů, pro předejití neúspěchu z neochoty a neznalosti uživatelů. Také kontrola dokumentace, která může zaostávat a být neaktuální. V neposlední řadě tak se dá také provádět customizace pro specifické zákazníky.

Různé druhy prostředí:
- *development* - pro developery, nestabilní, čistě pro vývoj aplikace
- *testing* - pro testování, mnohem stabilnější, může být přístupné zákazníkovi
- *staging* - testování deploymentu před nasazením na produkční server
- *production* - nasazená aplikace pro uživatele

##### Provoz
Jde o vše co zahrnuje udržování a podporu po nasazení softwaru. Jedná se specificky o monitorování výkonu, aktualizace, obnova a zálohování a poskytnutí technické podpory. Je to důležité pro udržení systému v kvalitním provozu a minimalizovat výpadky.


---

## Údržba softwarových systémů
Jedná se o modifikaci softwarového produktu po předání zákazníkovi. Typicky je to za účelem *opravy chyb*, *zvýšení výkonu* nebo *přizpůsobení měnícímu se okolí*. Většinou na právě údržbu jsou výdaje mnohokrát větší než na samotný vývoj.

##### Faktory ceny údržby
- *Stabilita týmu* - měnící se tým se musí naučit se systémem
- *Smluvní zodpovědnost*
- *Kvalita a um zaměstnanců*
- *Věk a struktura programu* - čím starší, tím horší

Čím déle systém udržujeme, tím více nás to stojí. Máme více zásahů do systému, změn funkcionalit, nové školení a podobně. V určitém bodě je tedy už levnější přepsat software než ho udržovat. Údržbu můžeme také zařadit jako samostatný projekt a mít na to specializované týmy. 

V závěru je fajn si udělat analýzu toho, co (ne)fungovalo, co zlepšit...
- dosažená produktivita a kvalita
- použitý proces, odchylky, důvody
- plán vs realita a důvody (čas, peníze, chyby, FP/LOC...)
- rizika (plán vs realita, jak jsme řešili rizika a problémy)
- pracnost (i dle etap)
- souhrn defektů
- kauzální analýza - analýza odchylek výkonu u použitého procesu (jak a proč)
- použité technologie a jejich hodnocení
- popsat v dokumentu tým a jednotlivce, na které je možné se případně obrátit (třeba když se řeší problém v dalším projektu)
- aktiva procesu - co vzniklo a může být použito i v jiných projektech (knihovny, checklisty)

##### Lehmatovy zákony
V rámci údržby se projevují zákony, které popisují problémy s přidáváním funkcionalit do existujícího softwaru. Ukazuje to na problém s cenou údržby v konečném důsledku, kdy je lepší všechno přepsat.

**Zákon trvalé proměny**
>Systém používaný v reálném prostředí se neustále mění, dokud není levnější systém restrukturalizovat, nebo nahradit zcela novou verzí.

**Zákon rostoucí složitosti**
> Při evolučních změnách je program stále méně strukturovaný a vzrůstá jeho vnitřní složitost. Odstranění narůstající složitosti vyžaduje dodatečné úsilí.

**Zákon vývoje programu**
> Rychlost změn globálních atributů systému se může jevit v omezeném časovém intervalu jako náhodná. V dlouhodobém pohledu se však jedná o seberegulující proces, který lze statisticky sledovat a předvídat.

**Zákon invariantní spotřeby práce**
> Celkový pokrok při vývoji projektů je statisticky invariantní. Jinak řečeno, rychlost vývoje programu je přibližně konstantní a nekoreluje s vynaloženými prostředky.

**Zákon omezené velikosti přírůstku**
> Systém určuje přípustnou velikost přírůstku v nových verzích. Pokud je limita překročena, objeví se závažné problémy týkající se kvality a použitelnosti systému.

##### Brooksův zákon
Náklady na začlenění nového pracovníka do týmu jsou zpravidla větší než jeho přínos.

> Přidání řešitelské kapacity u opožděného projektu může zvětšit jeho zpoždění.  


---

## Znovupoužitelnost
Hlavně chceme znovupoužitelnost, protože můžeme několikanásobně ohodnotit vyvinuté komponenty.

##### Úrovně
- *Abstrakce* - analytické prvky
- *Objekty* - třídy
- *Komponenty* - kolekce tříd
- *Systém* - celý systém a platformy

##### Reuse oriented software
Jedná se o model vývoje softwaru, který se zaměřuje na systematické znovupoužívání některých částí. Díky tomu se může doprogramovat jen GUI, případně adaptéry a proxy, ale mnoho komponent z minulosti může být už využito. Tento přístup se hodně používá u budování business systémů.