# Projektové řízení
> Plánování, řízení rizik, role modelů v projektovém řízení. Ganttovy diagramy, síťová analýza, metoda kritické cesty (CPM), Program Evaluation and Review Technique (PERT). Mezinárodní standardy a metodiky projektového řízení (PMI Project Management Body of Knowledge, PRINCE 2). Příklady z praxe pro vše výše uvedené. [PA179](https://is.muni.cz/auth/el/fi/jaro2022/PA179/um/)

## Projektové řízení

Definice záleží od standardu, ale jde o nějakou *sadu metod, technik, nástrojů a kompetencí*, které se *aplikují na projekty*, aby byly *projekty úspěšné* a *naplnili svůj cíl* a pomáhaly udržet rovnováhu mezi *cenou*, *časem* a *scopem*.

##### Projekt
Opět není jasná definice, ale jsou tam vždy tyto základní vlastnosti:
- **Časově ohraničený** 
	- většinou úsilí s daným startem a koncem
	- má svůj vlastní životní cyklus (pre-project, initialization, execution, closing)
- **Unikátní**
	- každý projekt je jiný a má svoje specifika
	- není tam moc velká rutina
	- máme jiného zákazníka, jiný tým a podobně
- **Řízený změnami** 
	- dochází ke změnám, ale s tím se počítá
	- projekt má mít přínos pro zákazníka
- **Nejistý** 
	- je zde nějaké riziko a nejistota
	- s rizikem se počítá, jsou na to strategie
	- řeší se přes správy rizik a podobně

Kromě toho ještě projekt dělá vše aby dosáhl cíle a bojuje s *projektovým trojimperativem*, což je trojúhelník cena, čas, rozsah. Myšlenka je, že nikdy nemohu mít vše naráz.

V projektech se mi mohou vyskytovat opakovatelné prvky, tedy procesy. Většinou jsou řízené událostmi a jsou dobře definované a vizualizované různými flow charty a podobně.

Řízení projektů je typicky díky standardům, jako jsou PRINCE2, PMBOK, IPMA.

Projekt je například *přistání na měsíci*, *stavění domu* nebo *vytváření informačního systému*.
##### Proces
Je to nějaký samostatný proces činností, které na sebe navazují a na základě vstupních požadavků vytvářejí výstup. Jsou opakované, lehce monitorované, měřitelné, odladěné a vyzkoušené.

Procesy se také mohou používat v různých projektech. Mezi příklady patří například *přistání na letišti*, *linková výroba auta*, nebo *instalace softwaru*.

##### Proces vs. Projekt

| Projekt                        | Proces                              |
| ------------------------------ | ----------------------------------- |
| Unikátní                       | Opakovatelný                        |
| Provedený poze jednou          | Má několik instancí                 |
| Plánovaný                      | Řízený událostmi                    |
| Vizualizovaný Gantt chartem    | Vizualizovaný Flow chartem          |
| Snažíme se ho držet v kolejích | Optimalizujeme, měříme, vylepšujeme |

##### Program
Je to nějaká skupina projektů v rámci společnosti, která je nějak provázaná a řízená dohromady, aby se dosáhlo cílů, které sdílí projekty. 

Při řízení programů:
- **Plánování** - s ohledem na to, jak to ovlivní jiné projekty
- **Odstraňují se omezení** - hlídají se konflikty a předchází se jim
- **Správa rizik** - spravují se rizika programu


##### Portfolio
Skupina projektů a programů, řízená k dosažení dlouhodobých strategických cílů, tedy co dlouhodobě nabízíme jako společnost.

Při řízení portfolia
- **monitoring** - monitorováním jednotlivých programů
- **prioritizace** - výběrem a prioritních programů a projektů


---

## Plánování

Při plánování projektu je potřeba se rozhodnout nad přístupem k řízení a tím pádem i výběrem standardu pro řízení projektu. Berem tedy do úvahy, zda známe dopředu všechny požadavky, nebo budou přibývat. Jak velký a zkušený tým máme, délka projektu, kooperace v týmu, jestli má být produkt rychle v iniciální verzi doručený, nebo až na termín ukončení.

Rozlišujeme tedy mezi tím, že máme sadu specifikací a atributů a snažíme se na to napasovat nějaké Project management a SW Development.

##### Project management standards
- **PRINCE2** (Project in controlled environments)
	- **PMBOK** (PMI - Project management body of knowledge)
- **ICB** (IPMA - Individual competence baseline)

##### Procesy pro vývoj SW
- **Unified process**
- **SCRUM**

### Agilní plánování
Předpokládejme, že volíme agilní přístup pro projekt. Pak tedy zvolíme *IPMA* nebo *PMBOK* a *SCRUM*. Díky PMBOKu vytvoříme *project charter*, *strategie*, *řízení rizik*, *definování kvality*, *komunikaci* a v poslední řade *kompetence* lidí. *SCRUM* na druhou stranu vytváří *proces vývoje*, udává *role*, *události* a *artefakty* a třeba také *continuous improvement a integration*.

Projekt poté rozdělujeme na části - **Planning**, **Sprinting** a **Closing**

##### Planning
Fáze před samotnými sprinty, kde se většinou vykrade nějaký PMBOK, aby se projekt náležitě zahájil a zdokumentovat. Můžeme rozdělit na základní sekce:

**Vytvoření Project charteru**
- Definuje ho PMBOK a v základu nám říká několik otázek na které odpovíme
- *BUSINESS CASE* (proč) - Proč děláme projekt, důvody, benefity a největší risky a výdaje
- *OUTCOME* (co) - jednoduchý popis aplikace, hlavní cíle a požadavky
- *STAKEHOLDER* (kdo) - zapsat klíčové členy týmu interních i externích
- *APPROACH* (jak) - jak se bude řídit projekt, standardy, životní model, nástroje
- *SCHEDULE* (kdy) - klíčové milníky projektu

**Management klíčových strategií**
- *Strategie komunikace* - přímo s klientem, rychlé meetingy, reporty a podobně
- *Risk management* - strategie pro risky typicky z IPMA, PMBOK
	- Identifikace základních rizika
	- Ohodnocení - pravděpodobnost a dopad
	- Odpovědi - Tranfer/Avoid/Reduce/Accept
	- Monitorování - konkrétní člověk odpovědný za kontroly
	- Vytvoření registru risků
	- Nejčastější risky jsou nedostatek lidí, nerealistické odhady cen, času
- *Change management* - jak postupovat u změn zákazníka, zpracování nových požadavků
- *Quality management* - stanovíme si cíle na kvalitu a zvolíme cíle, metriky a nástroje
	- Ve SCRUM se mohou definovat akceptační kritéria do user stories
	- Můžeme počítat Team velocity
	- Používat Burndown chart
	- Retrospektivu sprintu

**Management product backlogu**
- Přidáváme do product backlogu user stories
- Dáváme jim priority, pracnost a akceptační kritéria, související rizika

##### Sprinting
- *Spring planning* - z product backlogu vybíráme stories a definujeme cíl
- *Daily Standup* - transparentnost, progres
- *Sprint review* - představení inkrementu, kontrola product backlogu, dokončenost projektu
- *Sprint retrospective* - Zaměřený na komunikaci. týmu, měření výkonu, vylepšení
- *Aktualizace strategií* - Pokud je něco špatně, aktualizují se některé strategie

Do sprintu můžeme zahrnout i nějaké řešení týmových konfliktů, změny požadavků. U změn požadavků je velmi důležité rozhodnout, zda se bude sprint zastavovat nebo ne.¨

##### Closing
- *Dokončování produktu* - dohodnutí se na posledním sprint review
- *Přechod do operations* - vytváření uživatelské a technické dokumentace
- *Timeline retrospektiva* - co jsme se naučili, co se mělo stát a nestalo, co zlepšit



### Prediktivní plánování

Typickým příkladem, s čím nám pomáhá *PRINCE2* tak je *terminologie*, *role v týmu*, *reporting*, *projektová dokumentace* a *projektový plán*. Pokud k PRINCE zvolíme například *UP*, ten se zase zaměřuje na proces *vývoje produktu*, *sbíráním požadavků* a *produktovou dokumentací*. Zvolení těchto dvou přístupů vede k tomu, že bude velmi administrativní management s detailní dokumentací a rozsahem práce definovaným předem.

Celkově rozdělujeme v PRINCE2 fáze: **starting** , **initiation**, **delivery**, **closing**.

##### Fáze: Starting (Inception in UP)
- **Project brief (PRINCE)** 
	- je to nějaký základní dokument, který je velmi podobný Project Charter
	- definujeme role v týmu
	- definujeme přístup k řízení
- **Next stage plan (PRINCE)**
	- vytvoříme plán ze dne na den pro další číst projektu
	- identifikujeme aktivity, odhadneme délky trvání, vytvoříme Gantt chart
- **Analyze high level requirements (UP)**
	- specifikovat aktory systému, nějaké use case diagramy
	- popsat motivaci a jednoduchý popis produktu (většinou spolu s klientem)
- **Analyze and determine feasibility and outline architecture (UP)**
	- odhady na ceny, risky, plánování
	- vytvořit nějaký počáteční plán na řešení

##### Fáze: Initiation (Elaboration in UP)
- **Project initiation document (PRINCE)**
	- základní dokument celého projektu
	- detailní důvody projektu a popis produktu
	- struktura týmu
	- analýza rizik, přístup k řízení, vytvoření plánu projektu
	- kdo a kdy posílá reporty, jak se bude hodnotit kvalita
	- rozvrh Gantt chartu a odhady na ceny
- **Detailed requirements (UP)**
	- shromáždění většiny požadavků
	- vytvoření specifikace produktu a to jak pro vývojáře tak pro uživatele
	- vytvoření produktové dokumentace je důležité kvůli kontraktu
- **Stage report (PRINCE)**
	- vytvoření reportu z této fáze
	- obsahuje risky, výkon týmu, kvalitu produktu, situaci projektu apod.
- **Next stage plan (PRINCE)**
	- opět se navrhne a naplánuje další fáze

##### Fáze: Delivery (Transition, Construction in UP)
- **Robust architecture (UP)**
	- v UP je to pořád elaborace, nicméně už se to bere do delivery
	- definují se moduly, technologie, rizika architektury
- **Controlling stage (PRINCE)**
	- vede se dokumentace jak vypadá vývoj
	- vedou se aktualizace registrů risků a problémů
	- popisuje se kdo co dělal a kdo to kontroloval
	- dělá se sumarizace fáze, která se předává poté jako report pro project board
- **Managing product delivery (PRINCE)**
	- dělá se dokument kdo bude na čem pracovat
- **Managing stage boundary (PRINCE)**
	- Opět konec fáze, takže se generuje plán další fáze a report aktuální
	- Aktualizuje se plán projektu, risky, problémy, kvalita
	- Občas se může i aktualizovat business case

##### Fáze: Closing (Construction, Transition in UP)
- **System acceptance (UP)**
	- akceptace systému
	- máme již beta verzi, která se používá testujeme ji před přechodem do produkce
- **Transition phase (UP)**
	- dopisuje se dokumentace
	- probíhá trénink uživatelů
	- zapracováváme změny z beta testování
	- snažíme se vyrobit už systém, který bude akceptovatelný, takže spíše ladíme
- **Product acceptance testing (UP)**
	- vypisuje se protokol o akceptování
	- je to formální testování systému
- **Product handover (PRINCE)**
	- definuje se Service level agreement (SLA)
	- přesun odpovědnosti z vývoje produktu na nasazení a údržbu 
- **Zavření registrů a logů (PRINCE)**
	- archivace všech dokumentů, logů a registrů
- **Report o ukončení projektu (PRINCE)**
	- formální report, kde jsou obsažená i tvrdá čísla o projektu
- **Lessons learned report (PRINCE)**
	- méně formální report  pro budoucí doporučení, užitečných technik apod.



**Work Breakdown Structure**
- tvořená ze specifikace
- počítá se čas a cena jednotlivých **Work Packages** (součást WBS, nejnižší jednotka)
- náročnost a čas například pomocí [PERT](./4_projektove_rizeni.md#program-evaluation-and-review-technique-pert)
- vypisujeme závislosti, tvoříme rozvrh (gantt/network diagram)
- přiřazujeme odpovědnosti

![600](img/20230526000518.png)


---

## Řízení rizik

Rizika jsou nedílnou součástí vývoje produktu a proto na ně myslí každý standard pro řízení projektů. Je potřeba je nebrát na lehkou váhu a dobře zpracovat a řešit v rámci projektu. Je to soustavná činnost, která se snaží omezit pravděpodobnost jejich výskytu nebo snížit dopad.

**Riziko**: Nejistota vztahující se k výskytu ztráty

**Cíle analyzovaní rizik**: Eliminovat, snížit nebo odhalit potenciální rizika

##### Fáze řízení rizik
1. **Identifikace rizik**
    - čerpáme z předchozích zkušeností
    - snažíme se vymyslet potenciální rizika
2. **Analýza a zhodnocení rizik**
    - každé riziko způsobí náklady, můžeme pro něj odhadnout cenu
    - každému přiřadíme pravděpodobnost a kritičnost dopadu, určíme následky
3. **Ošetření a zvládnutí rizik**
    - *akceptování* - bohužel se stance, ale náklady na prevenci by byly vyšší než riziko
    - *vyhnutí se* - nastavení plánu, aby problém nemohl nastat (zvolím jinou technologii)
    - *přesuň* - problém pojistíme, nebo zahrneme do SLA
    - *sniž* - sniž pravděpodobnost/míru dopadu rizika, třeba důkladnějším systémem reviews
    - musím si dát pozor na to, aby náklady na řešení rizika nebyly vyšší než riziko samotné
    - musím brát v potaz, jak daná společnost rizika může zvládnout
4. **Stanovení monitoringu rizik**
    - stanovení odpovědnosti za monitoring rizik
    - určení, kde budou rizika definována, kdy budou revidována a upravována
5. **Vytvoření registru rizik**

##### Druhy rizik
- *ekonomická a finanční* - nedostatek financí
- *projektová rizika* - opoždění harmonogramu
- *technická rizika* - selhání některých technologií
- *sociální rizika* - odpor zaměstnanců k implementaci systému
- *provozní rizika* - výpadek provozu během implementace
- *bezpečností rizika* - ohrožení bezpečnosti dat, útok na systém

##### Modely řízení rizik
- **Centralizovaný** - máme ve společnosti výbor pro řízení rizik, který vytváří samostatné aktivity aby vyhodnocoval, monitoroval a vykazoval významná rizika
- **Decentralizovaný** - je to součástí každého rozhodnutí a vyžaduje to aktivní účast všech vedoucích zaměstnanců na jednotlivých úrovních řízení

##### Možné zdroje rizik
- uživatel - **nemožnost/neochota zapojit se**, odpor ke změnám
- požadavky - **špatně pochopené**, blbě definované, nejasné či neadekvátní, **přijdou změny** (mnohdy až v momentě, kdy mohou zásadně narušit vyvíjený systém) 
- složitost projektu - komplexní doména, použití nové/nezavedené technologie
- management - **neefektivní řízení**, špatně zvolená/použitá metodika/standard, **špatný odhad nákladů/zdrojů/času**, špatně určená komunikace, **nezkušený manažer**
- tým - nezkušenost, **málo lidí**, osobní konflikty
- firemní prostředí - nestabilní, změna vedení...
- **subdodavatelé** - opoždění, nedostatečná kvalita, komunikace...

##### Vyhodnocení rizika
Bere se v potaz pravděpodobnost a míra škody, kterou může riziko napáchat.
![500](img/20230525214112.png)
### Specifika prevence u agilního řízení rizik
Prevence:
- **Transparence a zpětná vazba**, abychom předešli nedorozumění v týmu
- **Používání user stories** - jsou snadno pochopitelné pro zákazníka, dají se dobře ověřovat
- **Jasná definice, co znamená "hotovo"**
- **Krátké iterace** - brzo zjistíme, co je případně blbě

## Role modelů v projektovém řízení

Těžko říct, co se tím myslí; v přednáškách PA179 žádná významná zmínka o modelech nebyla
Datové modely? Modelování komunikace, financí, rizik?

V řízení lze modely použít při plánování projektů pomocí [síťové analýzy](./4_projektove_rizeni.md#síťová-analýza), [metody kritické cesty](./4_projektove_rizeni.md#metoda-kritické-cesty-cpm).

Dále je možné modelovat procesy (komunikace), finance, rizika... a na těchto modelech hledat kritická místa, zkoumat co by kdyby...


---

## Ganttovy diagramy

Velmi důležitý nástroj pro plánování projektů, kdy reprezentujeme naplánované aktivity v rámci kalendáře. Díky tomu je vidět jak nákladná na čas každá činnost je a jak je rozložená práce v rámci delšího intervalu.

V základu jde jen o jednoduchý kalendář s řádky odpovídající úkolům
![](img/20230525192847.png)

Je možné rozšířit o *milníky*, *progress*, nebo omezení na *precedenční podmínky* a *zdroje*. 
![](img/20230525195955.png)

Obvykle minimalizujeme *makespan* (čas dokončení poslední úlohy a tedy i celého projektu).  Můžeme také zde využít zmíněné Precedence Diagramming Method:
- *Finish-to-start* - Aktivita B nemůže začít, dokud neskončí aktivita A.    
- *Finish-to-finish* - Aktivita B nemůže skončit, dokud neskončí aktivita A.
- *Start-to-start* - Aktivita B nemůže začít, dokud nezačne aktivita A.
- *Start-to-finish* - Aktivita B nemůže skončit, dokud nezačne aktivita A.


---

## Síťová analýza

Síťová analýza je soubor technik, který se používá na vyhodnocení a vizualizaci vztahů v aktivitách projektu. Pomáhá díky tomu pochopit posloupnosti a závislosti činností, identifikovat kritické cesty a efektivně řídit projekt. Pro analýzu se používají hlavně dvě techniky. Jedna je *Metoda kritické cesty* (CMP) a druhá je *Technika hodnocení a kontroly programu* (PERT). 

Používá se pro to síťový graf hranově/uzlově orientovaný - úlohy jsou na hranách/uzlech. Uzlově orientovaný umožňuje snadno modelovat precedenční podmínky, lze snadno použít pro metodu kritické cesty.

Vykonáním síťové analýzy nám pomůže v projektu:
- **Určit kritickou cestu** - identifikovat činnosti, které jsou nevyhnutelné k dokončení projektu
- **Odhadnou trvání projektu** - za základě nevyhnutelně serializovaných činností
- **Identifikovat potenciální překážky** - mohlo by vést ke zpoždění projektu
- **Identifikovat činnost pro paralelní práci** - efektivní využití času
- **Přidělovat efektivně zdroje** - podle závislostí na zdroje a potenciální konflikty
- **Monitorovat a kontrolovat pokrok** - projektu porovnáním s naplánovaným harmonogramem

### Metoda kritické cesty (CPM)

Metoda pro identifikaci vzájemně závislých aktivit, které mají vliv (jsou kritické) na dobu dokončení projektu a nemohou být opožděny bez prodloužení dokončení projektu. Vypadá jako síťový diagram s aktivity a jejich trváním. Můžeme buď použít dopředný a zpětný průchod a dopisovat dodatečné informace. [Postup](https://www.youtube.com/watch?v=4oDLMs11Exs)

**Dopředný průchod**
- díky dopřednému průchodu umíme spočítat *nejkratší dobu trvání projektu*
- zapisujeme earliest-start a earliest finish (ES + duration  = EF)
- pokud mám 2 aktivity scházející se do 1, vezmu největší EF

**Zpětný průchod**
- opíšu u poslední aktivity EF na latest-finish (LF)
- vypočítám latest-start jako (LF - duration = LS)
- pokud mi opět více aktivit vede do jedné beru nejnižší LS
- podívám se na stejné hodnoty ES, LS a EF, LF a díky tomu znám *kritickou cestu*

Rozdíly mezi EF a LF nám řeknou o kolik se můžeme zpozdit, aby i tak to neohrozilo termín dokončení projektu.

![600](img/20230526101347.png)

### Program Evaluation and Review Technique (PERT)

Technika k odhadu času k dokončení tasku. Bereme **optimistický** odhad, **pesimistický** odhad a **nejpravděpodobnější** odhad. Pesimistické odhady mohou být klidně i desetinásobky optimistických. Jde o to vytvořit nějaký buffer, kdyby se něco pokazilo.

Výpočet je poté vážený, většinou (1 4 1), ale můžeme si dělat i vlastní poměry
`očekávaný = (optimistický + 4 * nejpravděpodobnější + pesimistický) / 6`

Podobně je to při hraní pokeru ve SCRUM, ale tady dělají odhady manažeři a ne vývojáři.


### Výpočet nákladů na projekt

Je více možností, ale může se to dělat ve formě
- určíme pracnosti aktivit a přiřadíme vývojáře a jejich cenu
- dodáme cenu za licence, za materiál, HR, PR a podobně
- pokud toto uděláme pro každý *Work package* pak získáme **Project estimate**
- K Project estimate se přidá **Contingency reserve**, což je suma na všechny projektová rizika
- Project estimate a contingency reserve tvoří poté **Cost baseline**
- Úplně k tomu všemu se pak přidá **Management reserve** na neurčené výdaje
- Toto vše je poté **Cost budget**


## Mezinárodní standardy a metodiky projektového řízení 
- standardy projektového řízení PRINCE2, PMBOK, IPMA ICB popisují obecnější způsob řízení
- metodiky softwarového vývoje (RUP, SCRUM) řeší řízení v rámci vývojového týmu, jsou specifické pro vývoj SW

![](img/20230525184623.png)

### PMI Project Management Body of Knowledge (PMBOK)
- **procesně orientovaný** standard, podrobně popsaná sada good practices
- snadno se používá jako handbook pro vhodné znalostní oblasti a nástroje/techniky při životním cyklu projektu
- vhodný, když manažer potřebuje tipy na nástroje a techniky, jaké by měl použít, ale aspoň trochu tuší co a jak
- 49 procesů (série aktivit s definovanými vstupy, výstupy, nástroji a technikami) dělených do
    - 5 procesních skupin, logické dělení procesů podle fází (inicializace, plánování, provedení, monitoring a řízení, uzavírání)
    - 10 vědomostních oblastí/disciplín projektového managementu, každá má vlastní procesy
        - Integrace - vytvoření Project charteru, Integrated change control apod.
        - Rozsah - sesbírání požadavků, definice, validace a řízení rozsahu funkcionalit systému, tvorba Work Breakdown Structure
        - Plán - definice a určení pořadí aktivit, odhady časů aktivit, tvorba a řízení plánu
        - Cena - odhad cen a rozpočtu aktivit nebo jednotek práce pomocí Work Breakdown Structure, řízení ceny a rozpočtu
        - Kvalita - plánování, řízení a kontrola kvality
        - Zdroje - odhad nepeněžních a lidských zdrojů, jejich získávání a řízení, tvorba a správa týmů
        - Komunikace - plán, správa a kontrola komunikace a informací o projektu
        - Riziko - identifikace, kvalitativní (míra dopadu) a kvantitativní (pravděpodobnost) analýza rizik, jejich monitoring, plán a procesy reagující na rizika
        - Dodavatelé - produkty a služby pocházející mimo náš tým, kontrakty, objednávky, SLA, výběr dodavatelů, monitoring výkonu dodavatelů
        - Stakeholdeři - zúčastněné osoby; jejich identifikace, plánování a správa zíkazníka do projektu

### PRINCE 2 (Projects IN Controlled Environment)
- standard pro řízení obecného projektu
- předepsaný postup, krok za krokem (spousta formulářů na vyplňování, checklisty)
- součástí není správa požadavků, rozpočtování
- vhodný pro
    - nutnost velkého reportování
    - nutnost kompletní projektové dokumentace
    - tým vyžaduje řád a kontrolu
    - manažery s málo zkušenostmi, hodí se mu podrobný popis postupu

- fáze (hrubě odpovídá UP inception, elaboration, construction a transition)
    - **Starting up** 
        - tvorba **Project brief**
            - řešíme feasibilitu, zachycujeme klíčové požadavky, rizika
            - popis významných požadavků s dopadem na architekturu
            - identifikace actorů
            - identifikace dalších systémů, se kterými máme komunikovat
            - na konci známe cíle, hrubou architekturu
            - co se používá pro podobné systémy? s čím máme zkušenosti?
            - určení použitých technologií
            - určení orientační ceny, časového plánu a rizik
        - plán další fáze
            - **Work Breakdown Structure**
            - identifikace aktivit, dependencí
            - odhad trvání aktivit, stanovení milestones
            - definice rolí a odpovědností
            - tvorba rozvrhu (Gantt/síťový diagram)
    - **Initiation** 
        - tvorba **Project Initiation Documentation** (dokument/vícero dokumentů)
            - obsahuje současný stav projektu, plány, Kdo, Co, Kdy, Jak, Proč, Za Kolik...
            - slouží k definici projektu, určení rámce...
            - schvaluje product board
            - detailní Business Case (důvody projektu, očekávání, cost-benefit analýzu, časovou škálu, ceny, rizika)
            - popis struktury managementu, rolí týmu
            - popis přístupu ke kvalitě, změnám, riziku, komunikaci
            - plán projektu
        - plán další fáze
    - **Delivery**
        - obvykle má více částí (iterací), každá max 3 měsíce, každá má definované měřitelné a ověřitelné milestones 
        - produktový manažer se stará o udržení ceny, termínů, rozsahu a kvality specifikované v PID
        - produktový manažer autorizuje, provádí reviews work packages, reportuje (pravidelně) status, změny, problémy a kvalitu výš, spravuje rizika a problémy
        - týmový manažer provádí týmové plánování (jednotlivých work packages), demonstruje kvalitu produktu, zajišťuje dodání work packages
        - mezi fázemi se hodnotí končící fáze a plánuje (zase WBS, gantt) další, aktualizuje se PID
    - **Close**
        - předání produktu (samozřejmě opět spousta protokolů), nasazení, uzavření všech dokumentů, PID, dokumentace, tvorba end report a lessons learned
        - případné předání projektu ops a maintenance týmu
        - tvorba SLA

- 7 principů (vše máme nějak zdokumentované)
    - **Kontinuální odůvodnění projektu** - proč to děláme? 
    - **Učení se ze zkušeností** -  co (ne)fungovalo
    - **Role a odpovědnosti** - přesně specifikovaná struktura týmu, vymezené práva a odpovědnosti
    - **Řízení po fázích** - po každé fázi děláme review Project brief, provádíme reporting vyššímu managementu
    - **Manage by exception** - řízení soustřeďujeme na části, které se nějak (negativně) vymykají. Nezasahujeme do toho, co funguje. Vytyčíme cíle a tolerovatelné odchylky v kvalitě, času, ceně a rozsahu, určíme zodpovědnosti za nepřekračování
    - **Důraz na produkt** - primární cíl je produkt, ne práce
    - **Přizpůsobení metodiky projektu** - není nutné PRINCE používat úplně doslovně, řádek po řádku. Ne všechny formuláře jsou vždy zcela relevantní

- 7 témat
    - **Business case** - obsahuje očekávané přínosy, rizika, časový a cenový rozsah, důvody projektu... Měl by být neustále aktualizován a držen validní po celou dobu projektu
    - **Organizace** - definice rolí a odpovědností, typy stakeholderů (dodavatel, business/zákazník, uživatel), 3 úrovně managementu (project board pro směrování projektu (obsahuje exekutivu, senior suppliera, senior usera), project manager pro řízení projektu, team manager pro dodávání produktu), manage by exception
    - **Kvalita** - monitoring, akceptační kritéria, určíme si strategii řízení kvality (nástroje, procesy), řešíme kvalitu produktu i manažerských výtvorů (plány, reporty)
    - **Plány** - plánujeme projekt i jednotlivé fáze, Gantt diagram, Work Breakdown Structure je základem plánování
    - **Rizika** - identifikace možných rizik, určujeme způsob reakce na dané riziko na základě ceny prevence, pravděpodobnosti a dopadu, uchováváme registr rizik
    - **Změny** - u požadavků na změnu řešíme prioritu, dopad, kritičnost, zkoumáme možnosti řešení, dle změny upravujeme záznamy a plán
    - **Postup projektu** - porovnáváme realitu s plány (čas, cena, kvalita, rozsah, rizika...), sledujeme zda stále projekt splňuje business case

- 7 procesů
    ![](img/20230525115631.png)
    - **Úplný začátek projektu** - nastínění business case, přiřazení klíčových vedoucích osob, studování "lessons learned" předchozích podobných projektů, získání autorizace product boardu
    - **Inicializace projektu** - příprava strategií řízení (rizik, kvality, komunikace, konfigurace), projektového plánu, konkretizace business case, založení dokumentace
    - **Řízení fáze** - řeší produktový manažer, monitoring, reportování významných událostí, řídíme exceptions, revidujeme a schvalujeme práci/nové části produktu
    - **Řízení dodání produktu** - to samé co řízení fáze, ale řeší to týmový manažer
    - **Směrování projektu** - vysokoúrovňová rozhodnutí, funguje po celou dobu projektu, plán nadcházející fáze, na konci projektu autorizujeme uzavření
    - **Řízení mezi fázemi (managing a stage boundary)** - plán nadcházející fáze, řeší produktový manažer, aktualizace business case a projektového plánu, report předchozí fáze
    - **Uzavření projektu** - řeší projektový manažer, evaluace, předání produktu, návrh board na ukončení

### IPMA ICB
*V otázce není, ale není na škodu znát*
- obecný standard pro vedení projektu
- narozdíl od většiny ostatních obsahuje podrobnou sekci o soft skills
- vhodný, když
    - projekt vyžaduje dobré soft-skills (komunikace, leadership, řešení konfliktů)
    - manažer je zkušený, zná procesy
    - není nutná spousta reportingu
- vhodné pro použití jako handbook pro různé manažerské kompetence
- kompetenční přístup, pro každou ICB popisuje požadované dovednosti a schopnosti, popis a metriky indikátorů kompetence
    > kompetence je aplikace znalostí (knowledge, informace & zkušenosti), dovedností (skill, schopnost aplikovat znalosti) a schopností (ability, použití dovedností efektivně, ve správný čas a na správném místě) k dosažení kýženého výsledku
    - kompetence perspektivy - metody a techniky pro interakci jedinců s prostředím
    - lidské kompetence - techniky pro jednání s jedinci/skupinami
    - praktické kompetence - metody a techniky pro úspěch projektu

### Metodiky
- popsány v [otázce 3](./3_softwarove_inzenyrstvi.md)

## Notes

Specifika IT projektů v porovnání s většinou průmyslových odvětví
- nepřesné/neznámé, časté a měnící se požadavky
- větší nutnost přizpůsobení produktu
- velká složitost
- náročné testování
- neustálý a rapidní vývoj technologií
- možnost globální spolupráce
- projekty mohou v rámci portfolia ovlivnit ostatní projekty (zvlášť při selhání)
- nutnost řízení rizik
- dokončené projekty je často třeba servisovat/poskytovat podporu 

IT Infrastructure Library (ITIL)
- best practices pro **řízení IT služeb**
- fáze
    - **Service strategy** - požadavky, strategie pro zajištění kýženého, finance, co vlastně budeme dělat
    - **Service design** - Service Level Agreement, řešení rizik, security & business compliance
    - **Service transition** - jak měníme stávající služby, řešení deploymentu, uložení získaných znalostí pro budoucí projekty 
    - **Service operation** - dokumentace pro uživatele/helpdesk, řešení incidentů/změnových požadavků/problémů, řešení identit a přístupu k systému
    - **Continual service improvement** - monitoring, logování, aktualizace běžící služby
