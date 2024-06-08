# Zpracování dat.

> Základní pojmy a principy datových skladů, datové analytiky a business intelligence. Životní cyklus datového skladu. Analytika velkých dat, jazyky pro realizaci analytických úloh, analytika na úrovni databází. Pokročilé techniky zpracování dat, výkonnostní aspekty zpracování velkých dat. Příklady z praxe pro vše výše uvedené. ([PA220](https://is.muni.cz/auth/el/fi/podzim2021/PA220/um/), PA036)

## Základní pojmy a principy datových skladů, datové analytiky a business intelligence.

**Business intelligence** 
- procesy a nástroje pro sběr, analýzu a prezentaci/vizualizaci 
- účelem je asistence při tvorbě informovaných rozhodnutí v podnikovém řízení
- umožňuje transformaci dat do informací
- jádrem je datový sklad

**BI vs AI**
- AI dělá rozhodnutí za lidi
- BI pomáhá na základě dat dělat správná rozhodnutí

**Hlavní problémy, které je potřeba řešit**
- data máme v různých systémech
- data jsou většinou nekonzistentní, mají různé jednotky a různé struktury
- data jsou navržena pro business použití a ne pro analytické využití

##### Data warehouse
- pro nějakou organizaci je to jedno místo, kde se shromažďují všechny data
- máme na to dedikovaný jak SW tak HW
- data musí projít nějaký procesem integrace, validace a čištění než je zahrneme do skladu
- chceme data orientovat pro analytiku a ne pro operační využití

Definice: *Datový sklad je jediným konzistentním zdrojem pravdy z různých zdrojů. Je dostupný v takové podobě, že ji uživatelé dokážou pochopit a použít pro business výhody.*

Požadavky: *konzistence*, *dostupnost*, *bezpečnost*, *akceptovatelnost*

Datové sklady mají vlastnosti:
- jsou *subject-oriented*, tedy máme propojená data k jedné entitě a ukládáme je společně
- *integrované* - z několika systému máme data v nějaké konzistentní podobě
- *nevolatilní* - nepřepisujeme data ani je nemodifikujeme, jen nahráváme
- *časově proměnlivé* - změny v datech zaznamenáváme a držíme několik let


##### OLTP (Online Transaction Processing)
Jsou to běžné databáze, které jsou využívané zejména aplikacemi pro denní business operace. Jsou optimalizovány zejména na klasickou transakční práci, takže například používám normálové formy, aby při operacích bylo co nejméně zamykání a data se s vysokou výkonností mohly modifikovat, přidávat a odebírat.

**Klíčové charakteristiky**
- způsob ukládání dat v db pro transakční zpracování
- data v databázi se mění, cílem je zajistit konzistenci a umožnit CRUD
- nutné zamykání tabulek/řádků pro zajištění konzistence
- vhodné pro uložení dat v operativním provozu podniku (zajímá nás, co máme na skladě)
- normalizovaná forma (žádná redundance, public klíče pro případné spojování dat)
- používané dotazy známe dopředu, většinou zadrátované v kódu
- rychlé odpovědi na základní dotazy
- vysoká dostupnost a vyřešený konkurenční přístup

##### OLAP (Online analytical processing)
Databáze orientované na analýzu velkého množství dat. Nejsou zde žádné modifikace dat, zaměřujeme se hlavně na čtení a konzistenci z různých systémů. 

**Klíčové vlastnosti**
- způsob ukládání dat pro analytické zpracování
- data v databázi se nemění, pouze přidává
- zamykání není třeba, data se nemodifikují 
- pracujeme s mnohem větším objemem dat
- vhodné pro dlouhodobé uložení dat
- reflektuje historii dat z produkční databáze a jejich vývoj v čase
- denormalizovaná forma, hodně indexů, snažíme se minimalizovat nutné joiny
- nevadí datová redundance
- data nemusí být okamžitě dostupná
- data mohou být někdy i předagregovaná, abychom zrychlili dotazy
- máme multi-dimenzionální struktur
- jsou orientovaná na to poskytnou odpovědi na komplexní dotazy


##### Architektury DW

**Datový sklad**
- OLAP
- oddělení od OLTP, abychom nezatěžovali produkční db
- obvykle 1 db fungující jako centrální zdroj pravdy pro analýzu a reporting
- data ve skladu se nemění, pouze přidávají, je vidět vývoj dat v čase
- může obsahovat data z vícero zdrojů
- vyžaduje, aby byla zdrojová data očištěna a konzistentně uložena
- lze využít standardní databázi (e.g. postgres)
- lze využít specializovaná řešení (e.g. Google BigQuery, Teradata, Clickhouse)
- cílem je umožnit a zjednodušit analýzu dat

**Data mart**
- malý data warehouse, soustředí se na jednu zájmovou jednotku (e.g. objednávky)
- cílem je dekompozice za účelem zvýšení efektivity nebo omezení přístupu do jednotlivých částí datového skladu
- mohou být dvě podoby
	- samostatné fyzické *data marts* - je zde redundance, nemáme jednotný zdroj pravdy
	- logické *data marts* - jeden velký sklad a marts jsou jen pohledy, mnohem lepší konzistence

**Data Cube** 
- obsah DW, umožňuje pohled na data z různých dimenzí (rozměrů kostky, obvykle 4-15)
- skládá se z buněk (cells) - každá je kombinací hodnot dimenzí. No data = prázdná buňka. 
- **Dense/sparse cube** - hodně/málo neprázdných buněk v data cube


##### Budování DW
Hodně nám při budování pomůže 7W. Tedy *who*, *how*, *what*, *where*, *when*, *why*, *how* *many*

**Top Down**
- takový trochu vodopádový přístup
- získáme všechny požadavky, všechno naplánujeme a vymyslíme
- děláme implementaci naráz, je to náročné a nákladné
- většinou dlouho není nic vidět a nemáme zpětnou vazbu

**Bottom up**
- obecně lepší přístup
- inkrementálně přidáváme jednotlivé data marts
- máme rychlou odpověď od uživatelů, kteří vidí nějaký výsledky
- nejsou zde velké počáteční investice
- každý data mart máme pro nějakou skupinu uživatelů


##### ETL (Extract, Transform, Load) proces
V průběhu života do skladu přibývají data z OLTP, které je vždy třeba. Tento proces může běžet jako iniciální, tedy úplně první přidání dat, ale také periodicky, třeba vždy po konci dne přidat nová data. Často se ale spouští manuální na vyžádání.

**Extract** 
- z datových zdrojů (e.g. produkční db)
- zde je potřeba udělat adaptér na každý možná zdroj dat

**Transform** 
- odstranit duplicity
- upravit, aby odpovídala jednotnému stylu v DW, učesat do formátu používaném v DW
- vyčistit od nekompletních dat/chyb (spelling errors)
- občas může být třeba rozbít data na vícero sloupců (name => first name, last name)
- lze částečně automatizovat, ale mnohdy jsou třeba manuální zásahy
- obvykle nevkládáme přímo do DW, ale do staging table
- je fajn dělat po částech, ať se do toho nezamotáme

**Load**
- nejprve aktualizujeme dimenze (abychom měli k dispozici foreign keys)
- poté aktualizujeme fakta
- většinou se upsert nedoporučuje, protože je docela drahý, lepší je rozdělit příkazy
- je fajn naplňovat po velkých částech 
- po vložení přepočítat indexy/materializovaná views, najednou a ne postupně
- může pomoct, když vkládáme předřazená (presorted) data
- paralelizace (jednotlivé dimenze, lze například přidávat souběžně)

##### Schémata v DW

**Hvězdicové schéma/dimenzionální modelování** 
- středobodem je vždy nějaký subjekt (obsahující fakta e.g. prodej) s *tabulku faktů*
- fakta obsahující konkrétní záznamy měření, jsou *atomické*
- k faktům vážeme pomocí referencí (foreign key) *tabulky dimenzí* 
- dimenze jsou často odpovědi na otázky KDO, KDY, KDE, JAK...
- dimenze jsou obvykle detailní (denormalizované) pro snadnou analytiku
- redundance nevadí, e.g. datum dělíme na den, měsíc, rok, den v týdnu, kvartál...
- čím více dimenzí máme, tím konkrétněji se můžeme DW dotazovat (máme kontext)
- tabulky dimenzí obvykle předvyplníme (pro datum třeba 20230621)
- rozlišujeme dimenze data a času
- stěžejní data (to, co nás zajímá) bereme fakta
- dimenze jsou popisná data k faktům podle kterých je možné seskupovat
- reference jsou jen v tabulce faktů
- ID pro tabulky (surrogate keys, int) dimenzí si generujeme sami

- **typy faktů**
	- *transakční*
		- událost spojená s hodnotou (e.g. nákup)
	- *snapshot* 
		- zachycující nějakou aktuální hodnotu (e.g. naplněnost skladu)
		- většinou null hodnoty při nějaké neaktivitě
	- *bez hodnoty* 
		- fakt nemá žádnou numerickou hodnotu
		- obvykle jde o nějakou událost (e.g. click na určitý prvek)
- za fakta se považují i
	- odvozená data (e.g. kumulativní hodnoty za nějaké období)
	- data kombinovaná z vícero procesů (e.g. prodeje a jejich předpovědi pro dané období)

**Snowflake schema** 
Je to podobné jako hvězdicové, ale umožňujeme mít u dimenzí další dimenze. Většinou se nepoužívá, protože to způsobuje performance problémy.

##### Klíčové pojmy

**Granularita** popisuje, z jaké úrovně se na fakta díváme (e.g. zajímá nás, kolik se prodalo daného produktu? Za jeden den? V konkrétním obchodě?). Nejnižší granularita je jeden fakt (ukládáme opravdu fakty, nebo třeba jen agregovaná data?).

**Měření/Measure** - aspekt faktu, který nás zajímá, lze agregovat (e.g. cena prodeje). Některé hodnoty měření lze sčítat (e.g. tržby), některé jen v některých dimenzích (e.g. zůstatek na pokladnách, nelze sčítat v čase), některé vůbec (e.g. cena za jednotku produktu nebo průměrná cena za období...)

**Conformed (přizpůsobivá?) dimension** - dimenze, která má stejné hodnoty a význam pro data pocházející z vícero zdrojů. E.g. čas je obvykle conformed dimenze, většinou kritické, abychom dobře s daty pracovali

**Surrogate keys** - námi vytvořené unikátní klíče, abychom pracovali s cizími klíči na dimenze. Jde většinou o best practise, než se spoléhat na klíče z OLTP.


Na datový sklad/data marty jsou obvykle napojeny další **vizualizační aplikace**
- Grafana
- Kibana
- PowerBI


---

## Životní cyklus datového skladu.

##### Jednotlivé kroky

**Určení cíle a plánování** 
- co od systému očekáváme, jaký rozsah dat nás zajímá
- odhad ceny, rizik, prioritizace subjektů (=> datamartů)

**Návrh infrastruktury** 
- volba vhodných nástrojů a technologií
- architektonických řešení

**Návrh a vývoj data martů** 
- iterativně tvoříme data marty, každý zapojujeme do DW systému
- **volba procesu** 
	- včetně modelování procesu (třeba UML diagramem) e.g. prodeje
- **určení granularity** 
	- e.g. prodej jednoho produktu jednomu zákazníkovi, na jedné pobočce v jeden moment
- **identifikace dimenzí** 
	- vychází z granularity, můžeme dimenze rozšířit o další jevy (den v týdnu, slevové akce)
- **identifikace faktů** 
	- všech sloupců, které budou v tabulce faktů
	- e. g. cena jednotky produktu, prodané množství
- příprava ETL pro data mart
- první data mart je většinou kritický pro úspěšnost projektu a je základem celého DW

![600](img/20230610173720.png)

##### Změny dimenzí
Dimenze se mohou v průběhu života DW měnit (změní se třeba region, pod který spadá pobočka), nicméně měli bychom uvažovat, že chceme třeba tyto změny historicky držet.

Možnosti implementace změny
- **Typ 00 - Ignorování**
	- prostě změny ignoruji, většinou nechceme dělat
- **Typ 01 - Přepis** 
	- nahradíme stará data novými, je to jednoduché, ale ztrácíme informaci o historii
- **Typ 02 - Přidat řádek**
	- všechny historické hodnoty zachováme
	- přidáme nový řádek a používáme sloupce `valid_from` a `valid_to`
	- většinou docela komplexní na implementaci
- **Typ 03 - Přidání sloupce** 
	- přidáme sloupce například `prev_name`, kde si držíme předchozí hodnotu
	- pokud by ale došlo k další změně tak je to zase problém
- **Typ 04 - Přidání mini-dimenze**
	- pro často měnící se atributy je můžeme vytáhnou do dimenze bokem
- **Typ 05 - Kombinace Type 04 s odkazem**
	- můžeme se odkazovat z dimenze na aktuální dimenzi pro daný atribut
- **Typ 06 - Kombinace 01, 02, 03**
	- většinou lepší pro dohledávání informací zpětně


---

## Analytika velkých dat, jazyky pro realizaci analytických úloh, analytika na úrovni databází.

##### Big data
Jedná se o data, které kvůli své rychlé a kontinuální tvorbě, velkému objemu, či složitosti, *vylučují zpracování tradičními analytickými způsoby*. 

Povaha velkých dat:
- *velký objem* - každých 5 let se objem zdesetinásobí
- *různorodost* - máme textová, multimédia
- *rychlost* - máme velké toky dat
- *pravdivost* - máme mnoho zdrojů odkud čerpat, ale potřebujeme zdroj nějaké pravdy
- *hodnota* - snažíme se z nich získat něco přínosného

Problémy:
- *rychlý příchod dat*
	- vyžaduje kontinuální zpracování
	- nepoužíváme batch processing, je potřeba stream processing
	- pro distribuované zpracování velkého předání dat mezi systémy třeba Apache Kafka
- *velikost dat* 
	- lze zvládat pomocí distribuovaných databází/souborových systémů
	- obvykle NoSQL databáze, nebo Hadoop Distributed File System
- *složitá data*
	- zvládání komplexních vztahů, či data typu video
	- je nutné použít specializované nástroje (pro vztahy třeba grafovou databázi).

Přístupy ke zpracování (nejen) velkých dat
- **batch** 
	- jednou za čas aktualizujeme náš DW, doplníme nově vzniklá data
- **stream** 
	- průběžně vkládáme data tak, jak vznikají 
	- důležité je udržovat konzistentní formát dat,
	- snadněji se škáluje

Úložiště
- *horizontální škálování* je pro nás ve velkých datech lepší než to vertikální
- můžeme použít některé platformy jako jsou
	- *HDFS & MapReduce* - Hadoop
	- *column storage* - Vertica, Clickhouse
	- *NoSQL* - HBase
	- *distributed stream processing* - Storm

Konkrétní řešení
- **HDFS**
	- soubory jsou nasekané do bloků a ty se replikují
	- máme jeden master node a potom data nodes
- **Distribuované výpočet (mapReduce)**
	- dostanu data, kterým přidělím díky *map* klíče 
	- podle klíčů poté rozdělíme na skupiny
	- nad každou skupinou provedeme *reduce*

##### Analytika velkých dat
Máme multi-dimenzionální modely, které jsou vhodné pro dotazování na konkrétní analytické dotazy. Většinou tedy fakta znázorňujeme jako kostku a snažíme se nějakým způsobem transformovat data abychom dostali odpovědi. Kostky mohou mít různé množství volných buněk.

Přístupy k implementaci analytických databází:
- **Relational OLAP (ROLAP)** 
    - data ukládáme v relační databázi (e.g. postgres)
    - dimenze simulujeme pomocí star schema, pro dotazování používáme standardní SQL
    - (+) není potřeba specializovaný systém
    - (+) dobrá flexibilita
    - (-) response time
    - (-) zabírá 3-4x více místa, než MOLAP (v případě dense cubes)
- **Multidimensional OLAP (MOLAP)**
    - data ukládáme ve speciálních multidimenzionálních strukturách
    - ukládá se na menší prostor na disku
    - e.g. in-memory db, nebo multidimenzionální pole/matice
    - používáme přímou adresaci na disku
    - rychlejší queries než ROLAP, zabírá míň místa (není potřeba ukládat foreign keys)
    - horší flexibilita (při přidání hodnoty do domény dimenze je nutné přidat velké množství buněk, u ROLAP jde o jeden řádek v tabulce dimenze)
    - je potřeba specializovaný systém
    - mnohdy bývá součástí/add-on databázového řešení (MS SQL Server, Oracle...)
- **Hybrid OLAP (HOLAP)**
    - kombinace MOLAP a ROLAP
    - čistá data uložena v ROLAP
    - agregace uloženy v MOLAP
    - (+) *flexibilita*, *rychlost*
    - (-) vyšší složitost systému



##### Jazyky pro realizaci analytických úloh
- tradičně jde o SQL, nebo jeho deriváty, které jsou rozšířené mezi analytiky
- pro pokročilejší zpracování lze využít model MapReduce (a Hadoop), ve kterém je možné specifikovat transformační uzly v jakémkoliv programovacím jazyce
- NoSQL databáze mohou mít vlastní rozšíření SQL, nebo úplně jiný přístup k analytickým dotazům (e.g. mongo má knihovny pro různé jazyky)

Druhy *SQL dotazů* specifické pro analytiku

**Slice** 
- v rámci jedné dimenze vybíráme konkrétní hodnotu
- zobrazujeme pouze data s touto hodnotou dimenze
- v SQL pomocí WHERE
- e.g. kolik se prodalo laptopů?

**Dice**
- jako *slice*, akorát pracujeme s intervaly/vícero hodnotami jedné dimenze
- e.g. prodeje od-do, prodeje laptopů a telefonů
- tako můžeme pracovat s hodnoty vícero dimenzí (prodeje laptopů v říjnu)

**Roll-up** 
- provádíme agregaci dat
- v SQL pomocí agregačních funkcí (GROUP BY a třeba SUM)
- *dimenzionální* 
	- můžeme vynechat nějakou dimenzi
	- kolik jsme prodali za celý čas? kolik ve všech pobočkách?
- *hierarchický* 
	- můžeme se dívat z pohledu vyšší úrovně nějaké dimenze 
	- kolik jsme prodali v jednotlivých regionech, které se skládají z vícero poboček?
- oba přístupy lze kombinovat 

**Drill-down**
- opak roll-up
- jdeme z abstrakce do většího detailu (je nutné, aby nějaká detailnější data existovala)
- obvykle děláme drill-down z nějakého materializovaného pohledu
- opět zase buď přidám dimenzi, případně se snížím v hiearchii

**Pivoting** 
- přeskládání a agregace dat za účelem vizualizace
- snažím se nějak prokřížit více dimenzí
- nejjednodušší variantou je **kontingenční tabulka** (cross table)
- ve které se zaměřujeme na dvě dimenze: 
	![400](img/20230611214059.png)
- v SQL se dříve muselo provádět pomocí sjednocení (union)
- nyní je v SQL možné použít pro toto příkazy vypsané níže
- `GROUP BY ROLLUP(year, band)` 
	- vrací *polovinu* kontingenční tabulky
	- vrátí data, agregaci pro každý rok a celkovou agregaci
		![500](img/20230611215146.png)
- `GROUP BY CUBE(year, band)`
	- vrací celou *kontingenční tabulku*
	- vrátí data, agregaci pro každý rok, pro každou skupinu a celkovou agregaci
        ![500](img/20230611215253.png)
- `GROUP BY GROUPING SETS(...)` 
	- umožňuje větší kontrolu nad agregací dat
	- lze mimo jiné realizovat příkazy ROLLUP, CUBE
        ![500](img/20230611215834.png)
- kromě takového groupování se v SQL ještě využívá například
	- *window* - můžeme vytvářet různé agregace přes OVER
	- *ranking* - *row number*, *RANK*, *DENSE_RANK*

---

## Pokročilé techniky zpracování dat, výkonnostní aspekty zpracování velkých dat.

Pro zajištění rychlosti dotazů v OLAP se používá redundance v podobě
- materializovaných pohledů (vkládáme jednou za čas, takže to není problém)
- indexů
- denormalizovaného schéma
- optimalizací dotazů

##### Indexování

**Indexy** 
- umožňují rychlejší získání dat, která nás zajímají, pomocí předpočítaných výsledků
- omezují prostor nutný k prohledání při čtení dat
- obvykle se používají [B+ stromy](./5_databaze.md#indexování), které jsou ovšem limitované pouze 1 dimenzí
- další jsou například *hashování*, případně speciální jako je *bitmapový index*
- pokud bychom chtěli multidimenzionální indexy, musíme použít *UB*, nebo *R stromy*


**UB stromy** 
- multidimenzionální data jsou linearizovány pomocí Z-křivky
- následně indexujeme pomocí B* stromu
- B* jsou jako jako B+, akorát tam jsou jiná pravidla pro rebalancování
- linearizace Z-křivkou poskytuje dobrý výkon pro intervalové dotazy 
- také zajišťuje, že data, která si byla blízká původně si budou blízká i po linearizaci
- indexovat do linearizovaných dat lze pomocí konverze souřadnic na binární číslo
- poté jen prokládání bitů souřadnic
- díky tomu, že jsou souřadnice ve výsledku u sebe tak je to super na range queries

| ![300](img/20230611224138.png) | ![300](img/20230611224906.png) |
| ------------------------------ | ------------------------------ |
![600](img/20230611224805.png)


**R stromy** 
- obdélníky, popsány v [otázce 5](./5_databaze.md#indexování), špatně se škálují do mnoha dimenzí   
- data máme jen v listech a uzly jsou reprezentovány jako obdélníky
- záleží na tom jak se budou ty obdélníky vypadat, může to totiž občas vyjít dost neefektivně

**Bitmap indexy** 
- vhodné pro dimenze s málo variantami (e.g. pobočky)
- pro každou variantu uděláme bitové pole o délce tabulky faktů
- index v poli odpovídá řádku v tabulce faktů
- u pole nastavíme 1 pro indexy, ve kterých varianta platí, jinak 0
- výhodou je, že se snadno používají bitové operace (AND, OR)
- při mazání v tabulce faktů je třeba buď upravit všechny bitmap indexy, nebo v tabulce faktů použít *tombstone* hodnotu (považujeme za prázdnou).

**Range-encoded bitmap indexy** 
- vyžadují, aby měla dimenze seřazené varianty (pokud chceme hledat pomocí intervalů)
- opět má každá varianta bitové pole délky tabulky faktů
- pokud je varianta pro daný fakt pravdivá, nastavíme ji na hodnotu 1
- všechny následující varianty v pořadí se také nastaví na hodnotu 1 (jinak 0). 
- hodnota neznamená e.g. *narodil se v měsíci*, ale *byl už na živu v měsíci*
- při intervalovém dotazu pak stačí provést `<lower> AND (NOT <upper-exclusive>)`.
	![600](img/20230612104455.png)


##### Partitioning
Dělení dat (tabulky) na více (nepřekrývajících se) částí, pokud dat máme tolik že to už vytváří velmi pomalou výkonnost. Většinou dělíme na nepřekrývající se části a buď horizontálně nebo vertikální.

**Přístupy**
- *logické* 
	- dělíme dle data/organizační jednotky/kategorie
	- případně podle kombinace těchto faktorů
- *fyzické* 
	- distribuce dat na různé výpočetní uzly
	- umožnění paralelního zpracování na více strojích
- může být implementováno přímo v databázovém systému, případně si ho zajistíme na aplikační úrovni (náročnější)

**Typy dělení**
- *horizontální* 
	- tabulku dělíme na vícero tabulek se stejnými sloupci
	- obvykle podle intervalu (často časová dimenze, případně nějaká, co se často nemění)
	- dá se taky rozdělovat podle nějakého otisku hashovací funkce
- *vertikální* 
	- část sloupců přesuneme do jiné tabulky (a.k.a. row splitting, vztah 1:1)
	- dává smysl když určité sloupce nepoužíváme často

**Důsledky**
- data používaná společně by měla být uložena společně
- fajn pro škálování, části lze nezávisle prohledávat na více strojích
- nevýhodou je vyšší složitost systému, při vertikálním dělení jsou drahé joiny
- doporučuje se dělat partitioning, když má tabulka >100 milionů řádků/je větší než 2GB

##### Optimalizace JOINů
Většinou si můžeme k performance dotazu hodně pomoci i zamyšlením se nad tím, jak jdou udělat joiny. 

JOINy jsou
- *komutativní* - nezáleží na pořadí operandů
	- `A JOIN B = B JOIN A`
- *asociativní* - nezáleží na závorkách, když chceme použít víc operandů
	- `(A JOIN B) JOIN C = A JOIN (B JOIN C)`
pořadí JOINů lze tedy přeskládat, abychom získali rychlejší provedení SQL dotazu

Obvykle optimalizace provádí databázový systém. Většinou u složitých zkoušet všechno je hloupost, protože je toho hrozně moc na v nabídce, takže tam se mohou použít nějaké genetické algoritmy, tedy přistupujeme k tomu heuristicky. Pokud jsou to jednoduché dotazy, je možnost otestovat všechny varianty.

Pokud ale náhodou uživatel ví jak je to nejlepší, můžeme plán vynutit. To může být v analytických dotazech mnohdy lepší. Pokud jsou dimenze dost restriktivní (filtrují hodně faktů), může být vhodné udělat cross join dimenzí.

Obecně je výhodné se vyhýbat cross join v OLTP, nicméně v OLAP se s tím dá pracovat. Mohu tedy při joinech použít 2 přístupy
- *intersect of partial joins* 
	- sales (2 mil záznamů)
	- indexuji cizí klíče a jednou filtruji podle lokace, poté podle času a podle produktu
	- z těchto 3 výsledků poté udělám průnik
- *cross join*
	- snažím se minimalizovat počet průchodů v tabulce faktů (je obrovská)
	- prvně tedy seskládám všechny dimenze a až poté jdu dělat join


##### Pohledy
**View**
Klasický pohled připomíná funkce v programovacích jazycích.
- pojmenovaný dotaz
- při dotazu nad view se automaticky provede selekce dat

**Materializovaný pohled**
- funguje jako klasický pohled, ale má předpočítaný výsledek, uložený v tabulce
- funguje jako cache, takže dotazy na materializovaný pohled jsou rychlejší
- při změně dat se musí data materializovaného pohledu přepočítat/rozšířit 
- lze to sice odložit, ale pak máme nekonzistenci
- nicméně naštěstí nekonzistence u OLAP není zas takový problém, jako u OLTP
- vhodné pro často používané a drahé dotazy/části dotazů

**Výběr MV**
- *statický* 
	- admin se podívá a vymyslí pohledy, většinou aby se ušetřilo při hodně dotazech
	- pohledy jsou tedy manuálně vytvřené
- *dynamický*
	- monitoruji časté dotazy a na základě nich adaptuji OLAP
	- předpočítávání je tedy automatické

**Výpočet MV**
- *kompletní* - většinou hodně drahé
- *inkrementální* - nejde vždy a není úplně snadné
- *okamžité* - sice máme konzistenci, ale zase pomalou DB
- *odložené* - dobře škáluje, nicméně je tam dočasná nekonzistence, než se dopočítá


---


**Sloupcové databáze** - na rozdíl od řádkových databází (e.g. Postgres), kde jsou uloženy vedle sebe data náležící jednomu řádku ukládají sloupcové databáze (e.g. BigQuery, S4HANA) vedle sebe data z jednoho sloupce. Díky mohou být sloupcové databáze rychlejší pro čtení dat.

**In-memory databáze** - namísto uložení dat na pevném disku držíme data v RAM -> rychlejší přístup, ale mnohem vyšší cena. E.g. S4HANA

**Distribuované databáze** - umožňují horizontální škálování, svou distribuovaností umožňují fault-tolerance (díky replikaci dat), e.g. Hadoop Distributed File System, Apache Cassandra.

**NoSQL (not only sql)**
Obvykle nebývají ACID (a nepoužívají joiny), díky čemuž mohou být rychlejší. Větším problémem je udržení konzistence dat. Některé poskytují distribuci dat na více výpočetních uzlů out of the box (mongo, cassandra)

Příklady:
- key-value stores 
	- data ukládáme/hledáme pomocí klíče
	- snadno se používají jako cache e.g. Redis
- dokumentové databáze 
	- data ukládají ve formě dokumentů (každý má klíč, podle kterého se referencuje)
	- jinak je to klasická struktura a kolekcí dokumentů
	- e.g. Mongo, Firebase
- grafové databáze 
	- snadno modelují entity a vztahy, e.g. Neo4j


### Apache Hadoop
- **platforma pro paralelní/distribuované zpracování velkých datasetů**
- batch processing
- vysoká dostupnost zajištěna replikací dat
- využívá **Hadoop Distributed File System (HDFS)** 
    - distribuovaný souborový systém vhodný pro immutable data
    - abstrahuje distribuovanost, uživatel pracuje s daty jednotným způsobem
    - high availability díky replikaci, data rozdělena do bloků (defaultně 128MB), každý je v HDFS replikován (defaultně 3x, každá replikace na jiném stroji)
    - jeden stroj je **name node** (master), ostatní **data nodes**
    - Master má přehled o mapování souborů na bloky a jejich lokaci na data nodes (tato data jsou taky replikována)
    - pro získání dotazu klient kontaktuje mastera (zjistí, kde má hledat data) a následně kontaktuje příslušné data nodes.
    - datové bloky jsou write-once (díky čemuž nemusíme řešit zamykání a dosahujeme vyšších rychlostí čtení)
- spolu s HDFS využívá modelu **MapReduce**
    - umožňuje paralelní zpracování dat
    - uživatel definuje jen použité map a reduce funkce (může jich být vícero)
    - postupně probíhá Map, Grouping a Reduce fáze
    - **Map** - transformace dat (filtrování, sorting). Bere vždy jednu položku dat (e.g. řádek) a vrací 0-1 key-value pár. Tímto způsobem zpracuje všechna data
    - **Grouping** fáze - děje se automaticky po map fázi, seskupuje data se stejným klíčem (vznikne key-list) a předá data se stejným klíčem jednomu reduceru
    - **Reduce** - agregace dat podle klíče, sumarizace výsledků Map operací. Bere key-list (obsahující všechny hodnoty pro daný klíč) a vrací key-list (obsahující 0-n výstupních záznamů).
    - E.g. word count - map bere řádek a vrací několik (dle výskytu na řádku) dvojic `(slovo, 1)`. Reduce sečte `1` pro daná slova a vrací `(slovo, součet)`. 
    ![600](img/20230612201616.png)

### Apache Hive
- distribuovaný data warehouse postavený nad Hadoop (a HDFS)
- poskytuje SQL-like (HiveQL) rozhraní pro dotazy, které je převedeno do MapReduce dotazů (je možné dělat i vlastní map reduce skripty)
- umožňuje používání strukturovaných dat (struktury, seznamy, mapy)
- umožňuje serializaci/deserializaci dat do/z různých formátů (xml, csv, json...)
- vhodný pro dlouho běžící ETL jobs
- pokud chceme low latency/interactive queries, je vhodnější použít Apache Impala (SQL query engine nad Hadoopem)

### Stream processing
- nezpracováváme balík dat, ale kontinuální stream
- Apache Spark (real-time výpočty, skládá se ze zdrojů dat a acyklicky propojených zpracovávajících uzlů)
- Apache Storm (analytický engine pro large-scale data processing, umí batch i stream processing)

## Notes

### Příklad architektury Data Warehouse pro Big Data

![](img/20230612205443.png)
