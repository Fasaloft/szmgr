# Analýza a návrh systémů

> Objektové metody návrhu informačních systémů. Specifikace a řízení požadavků. Softwarové architektury, komponentové systémy. Návrhové a architektonické vzory. Rozhraní komponent, kontrakty na úrovni rozhraní, OCL. Modely softwarových systémů, jazyk UML. Příklady z praxe pro vše výše uvedené. ([PA103](https://is.muni.cz/auth/el/fi/podzim2021/PA103/um/), PV167, [PV258](https://is.muni.cz/auth/el/fi/jaro2021/PV258/um/))

## Objektové metody návrhu informačních systémů.

Důležitý princip okolo kterého se vše točí je dekompozice systému. Nejsme schopní vše brát jako celek a musíme si najít nějakou dekompozici na různé komponenty a vztahy mezi nimi. Díky tomu jsme schopni vytvářet modely, ve kterých se dá mnohem lépe orientovat a vyznat.

**Dekompozice na úrovni objektově orientovaného modelování**
Definice objektového návrhu je tedy to, že část systému jsou nějaká *zapouzdřená data a spolu s nimi jsou propojené operace* nad těmito daty. Interní propojení se zde moc neřeší a je implicitní. *Propojení jednotlivých částí je volné* a závisí na definici rozhraní jednotlivých komponent.

Hlavním stavebním kamene je diagram tříd, nicméně využívají se zde skoro všechny diagramy z UML. Hlavní rozdělení těchto diagramů je:
- *Behaviour Diagram*
	- Activity
	- Interaction
		- Sequence 
		- Communication
	- State Machine
	- Use case
- *Structure Diagram*
	- Class
	- Deployment
	- Component
	- Object

**Objektově orientované paradigma**
- dekompozice na malé udržitelné části
- hlavní je dodržovat zapouzdření
- snažíme se cílit na znovupoužitelnost na úrovni komponent
- používáme dědičnost a abstrakci
- rozdíl object vs. třída - instance za běhu a statický předpis v době návrhu
- objekty vytváří jiné objekty a posílají si zprávy 

**Dědičnost** - může být fajn jako návrh, ale v dnešní době moc nechceme používat, spíše se přikláníme k použití *dependency injection* jako asociace, což nám poskytuje více volnosti

**Kompozice** - faktura má položky, pokud zahodím fakturu, nemám žádné položky, tedy kompozice mi říká, že je zde silná závislost a položka nemůže existovat bez celku. Značíme plnou šipkou.

**Agregace** - počítač může využívat tiskárnu, ale pokud počítač zahodím, tiskárna pořád bude existovat. Tedy využívám jiný objekt, ale není na mě kompletně závislý. Značíme prázdnou šipkou.

**SOLID** - S objektovými metodami velmi úzce souvisí SOLID principy. Chceme je tedy používat i v rámci návrhu systému.

**Konflikty s ERD** - pokud modelujeme čistě podle objektového přístupu, některé věci nejde úplně dobře přenést do entitně relačního schématu.  Nejde zde například potřeba trochu jinak modelovat m-n vazby, případně obousměrné vazby. Tak= dědičnost databáze nepodporují a tedy špatně se s ní pracuje.

Při modelování systému je dobré definovat si jednotný jazyk, který reflektuje skutečnou terminologii pro danou doménu problému. Podle toho volíme jména funkcí/tříd, aby bylo pokaždé všem (od doménových expertů po vývojáře) jasné, o čem se mluví. Podstatná jména používaná v jednotném jazyce obvykle v kódu reflektují třídy/rozhraní, slovesa zase metody/funkce.

Objektové paradigma si dobře rozumí s principy abstrakce, což lze aplikovat nejen na úroveň objektů, ale i *komponentů* - základních stavebních jednotek, ze kterých se skládá architektura systému.

Mezi **metody** se řadí:
- modelování domény pomocí [UML](./dev_1_analyza_a_navrh.md#modely-softwarových-systémů-jazyk-uml)
- v různých částech vývoje se zabýváme různými úrovněmi detailů UML diagramů
- dekompozice systému do menších, koherentních částí
- aplikace návrhových a architektonických vzorů, které popisují řešení na dobře známé a často se opakující problémy v (nejen) objektovém světě.


---

## Specifikace a řízení požadavků.

Požadavky na systém se dělí (obvykle je mezi kategoriemi tenká hranice podle formulace) na:
- **Funkční (functional) požadavky** - jaké funkce zákazník od systému očekává, jedná se o business logiku, uživatelské požadavky, řeší se programově, v implementaci
- **Nefunkční (non-functional/quality) požadavky** - jaké technické nároky jsou na systém, použité technologie, OS, garance dostupnosti (availability), response time, internacionalizace a lokalizace, řeší se návrhem, architekturou i kódem

**Řízení požadavků**
- porozumění doméně problému
- sběr požadavků od stakeholderů - klíčem je ptát se PROČ, ne CO a JAK 
- použití analytických diagramů (Martin Fowler)
- specifikace požadavků 
	- úprava do jednoznačné/formální podoby (use case)
	- koncepční diagramy tříd
	- je jasné, v jakém momentě můžeme považovat za splněný
- validace požadavků - ověření, že formalizované požadavky odpovídají skutečným potřebám
- prioritizace požadavků - umožňuje soustředit se na kritické části (dle potřeb zákazníka)

**Dobře specifikovaný požadavek**
- reflektuje skutečné potřeby zákazníka
- je v něm obsaženo PROČ (abychom mohli vybrat nejvhodnější řešení)
- má jasné *kritérium splnění*, je *měřitelný a testovatelný*
- má prioritu a je úplný

Obecně platí, že *čím později se požadavek změní, tím nákladnější bude jeho implementace*.

Požadavky se modelují pomocí *use case diagramu,* uchovávají se v *use case dokumentu* s nějakou identifikací, názvem, aktory, popisem a třeba i pre a post conditions a dalšími parametry.

Požadavky jsou také formalizovány v jednoduché formě pomocí **user stories** - krátké, výstižné popisy (As *WHO* I want to *WHAT* So I can *WHY*), srozumitelní zákazníkovi (+ obsahují akceptační kritéria, prioritu, story pointy).

Pro **určení priority požadavku** lze použít například:
- klasické ohodnocení 1-10
- binární strom - požadavky jsou uchovávány v uzlech. Vkládaný požadavek srovnáváme s uzly od kořene. Pokud je vkládaný požadavek prioritnější, jdeme doprava. Jinak jdeme doleva. Vložený požadavek bude listem stromu.
- MoSCoW - požadavky dělíme na Must, Should, Could a Won't

**Nefunkční požadavky** 
Platí vždy, že je třeba je brát v potaz i s nově příchozími functional požadavky, tedy máme pro ně vyhrazené místo, kde jsou důkladně popsány. Můžeme na konkrétní NFR poukázat v user stories, tedy v jedné story může být:
- FR jako uživatel chci mít přístup k aktuálním datům senzoru
- NFR systém poskytne odezvu do vteřiny
- NFR data ze senzorů se do systému dostanou nejpozději minutu po naměření


---

## Softwarové architektury

SW architektura určuje, jakým způsobem je systém strukturován, jakým způsobem je dělen na komponenty/moduly a jak mezi sebou jednotlivé komponenty/moduly interagují a jak jsou jednotlivé části systému nasazeny na HW. Tady se dá popsat jako struktura, která se velmi těžko pokud vůbec dá po implementaci změnit.

SW architektury (vyšší úroveň abstrakce) a architektonické vzory (nižší úroveň abstrakce) jsou obecná řešení architektur systému.

**MVC/MVP/MVVM pattern** - rozdělení na části, které zpracovávají dotazy, které pracují s daty a které vytváří UI pro uživatele

**Klient-Server** - klient je prezentační vrstva, server odpovídá na požadavky klienta

**Peer-to-Peer** - každý uzel je zároveň klient a zároveň server

**Layered architecture** - vrstvená architektura používá architektonický vzor Repository, snažíme se o abstrakci a rozdělení zodpovědnosti

**SOA** - zodpovědnou za určitou část řešené určitou službou, sdílí se databáze

**Microservices** - speciální případ SOA, hodně loosely coupled, nesdílí se DB


---

## Komponentové systémy

##### Komponentové systémy
Skládání jednotlivých komponent dohromady a provazování jejich komunikace. Jde o nějaké konkrétní realizování softwarové architektury. Díky použití komponent tak při vývoji softwarové architektury nemusím znát jejich interní reprezentaci, ale zajímá mě jen jejich úloha a rozhraní.

##### Komponenty
Jsou to spustitelné softwarové jednotky, která mají definované komunikační rozhraní, do vnitřního fungování nevidíme/nezajímá nás. 

Komponent by měl poskytovat logicky související funkcionalitu, funguje jako vrstva abstrakce.  Mohou být vyvíjeny nezávisle na jiných komponentech, jsou nahraditelné (stačí splnit rozhraní a jeho kontrakt), znovupoužitelné. Komponenty mohou mít vnitřní stav, ten však může dělat problém u škálování (parcelizací komponent), mohou být asynchronní, mohou se interně skládat z dalších komponent.

Pokud systém vystavuje rozhraní používaná i někým jiným (klient), je fajn nějakým způsobem verzovat rozhraní. Díky tomu se předejde problémům při přidávání změn, nějakou dobu totiž můžeme podporovat vícero rozhraní, než se klient aktualizuje na novou verzi.

Komponenta se od třídy liší od třídy tím, že v rámci komponenty máme více tříd, případně objektů a není zde viditelný zdrojový kód. Většinou má složitější životní cyklus. Třída na rozdíl od toho může mít i více rozhraní a je celkově otevřenější.

Komponenty mohou být stavové a bezstavové, kdy ty bezstavové jsou lepší kvůli lepší škálovatelnosti. Také mohou být dynamické, tedy se automaticky instancovat za běhu, případně statické, které mají pevný počet.

Komponenty můžeme vnímat jak jako runtime, tak jako design time. 

Komponenty mohou mít prvky:
- **Interface** - specifikace služeb, které vyžaduje nebo poskytuje
- **Port** - kam se dá připojit, můžeme mít stejné rozhraní na různých portech
- **Interní struktura** - většinou blackbox, nezajímá nás



---

## Rozhraní komponent, kontrakty na úrovni rozhraní

**Rozhraní**
Aby mohl komponent komunikovat se svým okolím (být volán a případně vracet data), potřebuje nějaké veřejné rozhraní, kterému se říká **signatura**. Skládá se z poskytovaných operací (funkcí/metod) a jejich vstupních a výstupních parametrů.

Rozhraní musíme velmi dobře dokumentovat a musíme mít specifický kontrakt.

**Kontrakt**
U rozhraní nás zajímají i další omezení, které mohou upravovat (správné) používání rozhraní (*e.g. uživatel se může registrovat jen jednou*). Signatuře a omezení se souhrnně říká **kontrakt**. Kontrakt popisuje poskytnutou funkcionalitu za předpokladu, že dodržíme předem stanovené podmínky. 

Součástí kontraktu (v kontextu struktur/objektů) můžou být:
- **preconditions** 
	- co musí platit před vyvoláním dané metody, aby metoda proběhla správně 
	- e.g. máme dost peněz na účtu
- **postconditions** 
	- co musí platit po skončení dané metody, i.e., co metoda poskytuje 
	- e.g. proběhne platba, z účtu se nám odečte příslušná platba
- **invariants** 
	- co vždy musí platit, váže se obvykle k objektům, nejen metodám 
	- e.g. na debetním účtu není možné jít do mínusu

Pro definici kontraktů můžeme používat
- **běžný jazyk** - většinou moc neformální a nejasné
- **matematické notace**
- **OCL** (object contraint language) 

---

## OCL (Object Constraint Language)
Je deklarativní jazyk, silně typovaný jazyk, který umožňuje popis kontraktů a jejich constraintů (omezení domén hodnot), včetně jejich zavedení do UML, a může být použit i pro jejich vynucování (e.g. generování kódu na základě kontraktu popsaného v komentáři/anotacích).

Při definici kontraktů objektů s dědičností nesmíme porušit *Liskov substitution principle*, dědic může invarianty a postconditions pouze utahovat, ne je rozvolňovat (co platilo pro rodiče, musí platit i pro potomka). Naopak je to u preconditions, kde může dědic podporovat více vstupů než předek.

V rámci UML se každý klasifikátor (třída nebo atribut) stává typem v OCL. Má taky základní typy kolekcí a stavíc *contraints*, které pak propojuje v rámci *kontextu* k elementům UML.

##### Invariants
- je to boolean výraz, tedy musí být splněný v rámci celého životního cyklu objektu
- váže se na nějaký kontext, tedy spíše ke třídě
- za klíčovým slovem `inv` můžeme přidat název

Příklady
`context Flight inv flightDuration: duration < 4`
`context Car inv: self.speed < 240`

##### Preconditions
- musí být splněné před spuštěním operace
- specifikuji kromě třídy i její metodu
- mohu se odkazovat na vstupní hodnoty, případně atributy

Příklady
```
context Flight::shiftDepart (t:Integer) 
	pre: t>0
```


##### Postconditions
- musí být pravdivé po ukončení operace
- přes @pre se mohu odkazovat na stav před a po ukončení operace

Příklady:
```
context Flight::shiftDepart (t:Integer): Time 
	post: result = departureTime + t

context Flight::shiftDepart (t:Integer): Time 
	post: result = departureTime@pre + t + duration

context Stack::pop()
	pre neniPrazdny: self.len() > 0
	post vraciVrsekZasobniku: result = self@pre.top()
```

##### Dědičnost
Pro jednotlivé typy v OCL musíme umět definovat dědičnost, která ale nesmí porušit Liscov substitution princip.

**Invariant**:
- mohu jen *zesilovat*, ale ne zeslabovat, tedy utahuji podmínku
- `context Flight inv: duration < 4`
- `context JetFlight inv: duration < 2`

**Precondition**
- podtřídy se mohou precondition jen *oslabovat*
- `context SuperClass::foo(i: Integer) pre: i > 1000`
- `context SubClass::foo(i: Integer) pre: i > 0`

**Postcondition**
- postcondition může být jen *posílený*
- `context SuperClass::foo() : Integer post: result > 0`
- `context SubClass::foo() : Integer post: result > 1000`

##### Kolekce
Celkem podporuje OCL tyto tři kolekce:
- **Set** - neuspořádaná množina bez duplicit
- **Bag** - neuspořádaná množina s duplicitami
- **Sequence** - uspořádaní množina s duplicitami

S kolekcemi se dá pracovat funkcionálně:
- `contextAirport inv: self.arrivingFlights -> collect(airline) -> notEmpty`
- `contextAirport inv: self.departingFlights -> forAll(departTime.hour > 6)`
- `contextAirport inv: self.departingFlights -> exists(departTime.hour < 6)`

V OCL lze provádět i množinové operace (union, intersection...), používat booleovské operátory (or, and, implies...) a spoustu dalšího (proměnné, cykly...)

Také se mohu odkazovat na stavy objektu:
- `context Bottle inv.`


---

## Návrhové a architektonické vzory.

##### Obecně o návrhových vzorech
Návrhový vzor je obecné řešení k často se opakujícímu problému řešenému při návrhu softwaru, není potřeba kompletně vymýšlet vlastní řešení. Slouží nejen jako obecný návod pro implementaci, ale umožňují snadnější komunikaci v rámci týmu (e.g. tady použijeme Strategy pattern). Vzory je třeba používat s rozvahou, občas můžou být zbytečně obecné.

##### Problémy
Není úplně pravda, že čím více vzorů použijeme, tím lepší, taky je potřeba přemýšlet, když vzor používáme, zda opravdu sedne na takové místo, nebo to tam je násilím. Občas vzory mohou vypadat hodně podobně, ale je potřeba jim dobře rozumět, abychom je rozlišili.

##### Rozdělení
Vzory můžeme klasifikovat podle GoF knihy na:
- **Creational patterns**
	- Factory method, Abstract factory, Builder, Prototype, Singleton
- **Structural patterns**
	- Adapter, Bridge, Composite, Decorator, Facade, Flyweight, Proxy
- **Behavioural patterns**
	- Iterator, Memento, Observer, State, Strategy, Visitor


### Creational patterns

#### Singleton
Zajišťuje, že daný objekt existuje v systému jen jednou (globální stav). V OO jazycích se řeší pomocí třídy s private constructorem a se statickou metodou `instance()` poskytující přístup k objektu drženému ve statickém atributu. 

Metoda `instance()` se obvykle stará i o inicializaci statického atributu

##### Aplikovatelnost
- chci mít danou instanci pouze jednou a chci mít kontrolu nad přístupem
- typicky třeba když dělám pool databáze tak tam chci použít tento pattern

##### Důsledky
- Singleton je mnohdy považován za antivzor, protože vytváří globální stav
- blbě se to testuje, může být nutné zamykání globálního stavu pro thread safety
- narušuje se single responsibility principle (singleton třída ovládá svou tvorbu)

![600](img/20230603121311.png)


#### Factory method
Stará se o tvorbu konkrétních instancí objektů dle instance továrny.

Příklad: máme rozhraní `VehicleFactory` a `Vehicle`. `CarFactory` bude dělat `Car`, zatímco stejné volání metody u `PlaneFactory` vytvoří `Plane`. 

##### Aplikovatelnost
-  pokud potřebujeme flexibilní a rozšiřitelný způsob vytváření objektů
- pokud chceme oddělit logiku tvorby objektu od zbytku
- nevýhodou je nutnost tvorby nové Factory třídy a rozhraní.

![600](img/20230604152821.png)


#### Abstract factory
Podobná factory method, ale je zodpovědná za více produktů. Instance této factory zajišťuje tvorbu vzájemně kompatibilních produktů.

Příklad: Můžeme vyrábět celé auto, kdy potřebujeme vyrábět kompatibilní díly pro určitou značku. `AbstractFactory` tedy bude `SkodaFactory` a budeme mít produkty jako je `wheel`, `engine`, `roof` apod.

##### Aplikovatelnost
- chci mít od určitého druhu kompatibilní třídy
- konfigurovatelnost - používá se například u UI pro různé systémy
- většinou přidání nového produktu je docela obtížné, protože musí být doimplementováno

![600](img/20230605121553.png)


#### Prototype
Doslova trait `Clone`, vytvoří identickou kopii nějakého již existujícího objektu. Hodí se, pokud inicializace objektu je náročná, nebo neznáme konkrétní instanci (pracujeme s abstrakcí přes interface).

##### Aplikovatelnost
- pokud je časově náročné vytvářet jednotlivé instance
- někdy je klonování jednodušší a máme jistotu, že objekty budou stejné

![600](img/20230604183448.png)


#### Builder pattern

Ke konfiguraci objektu při inicializaci používáme (deklarativním způsobem) metody příslušného `Builder` objektu, každá se stará o jeden aspekt. 

Příklad: Inicializace http požadavku, případně string builder.

```rust
let request = HttpRequest::get("www.mysite.com/content")
    .header("Authorization", "Bearer 8sa96d41a5s3fbwn")
    .queryParam("offset", 42)
    .build();
```

##### Aplikovatelnost
- pokud máme nějaké komplexní objekty, které můžeme skládat postupně
- umožňuje to přehlednější stavbu než teleskopické kontruktory

![](img/20230604183525.png)


### Structural patterns

#### Composite
Umožňuje tvorbu stromových struktur a poskytuje jednotné rozhraní k operaci na podstromu definovaném svým kořenem.`Component` je buď list `Leaf`, nebo uzel `Composite` obsahující potenciálně další `Component`.

##### Aplikovatelnost
- pokud chceme mít hierarchii s jednotnými akcemi
- stavební prvky grafických rozhraní

Je snadné přidávat nové typy a nemusíme řešit, co máme za uzly, prostě jen aplikujeme operaci.

![600](img/20230603143753.png)


#### Adapter
Taky by se dal nazvat wrapper - zapouzdříme/poskytneme rozhraní nekompatibilní jednotce tak, aby se dala použít v našem systému.

##### Aplikovatelnost
- pokud chci integrovat knihovny
- můžeme adaptér použít k převodu mezi formáty (XML - JSON)
- dá se díky němu připojovat nové komponenty na staré systémy

Adaptér lze implementovat ve všech populárních jazycích jako wrapper, je možná i implementace class adaptéru v jazycích podporujících mnohonásobnou dědičnost.

Většinou ale nejde adaptovat i podtřídy a umožňuje nám to měnit chování adaptovaného, což je bráno obecně jako nevýhody.

![600](img/20230603161229.png)


#### Bridge
Používá se k rozbití tightly coupled jednotek (nebo skupiny jednotek) pomocí abstrakcí (ty mohou mít vícero implementací, ale často nám bridge pomůže jen díky vytvoření abstrakce).

##### Aplikovatelnost
- změny v konkrétních implementacích neovlivňují klienta
- chceme používat abstrakce a implementace
- ve fullstack aplikaci využívající templating rozbijeme na frontend a backend API.

![600](img/20230604142514.png)


#### Decorator
Umožňuje rozšířit třídu, přidat k ní různé metody/atributy na základě použitého dekorátoru, dynamicky je přidávat/odebírat. Obdobně jako Adapter může obalit původní komponent, ale nemění rozhraní komponentu.

##### Aplikovatelnost
- chceme za běhu měnit chování objektu
- dynamicky přidáváme nějaké další funkcionality k objektu

Je více flexibilnější než dědičnost, ale při hodně objektech to může být docela chaos.

![600](img/20230604142455.png)


#### Proxy
Prostředník mezi objektem a volajícím, transparentně předává zprávu (a může provádět další operace, hlídat přístup k objektu, provést alokaci objektu on-demand...)

##### Aplikovatelnost
- pokud potřebuje kontrolovat, případně trackovat volání akcí
- pokud leží daný objekt na jiné síti a já zprostředkovávám volání

![](img/20230605125209.png)


#### Facade
Poskytuje jednotné (a jednoduché) rozhraní složitějšímu subsystému.

##### Aplikovatelnost
- chceme jednoduché rozhraní pro nějaký komplexní systém
- chceme jednodušší vazby mezi klientem a subsystémy

![600](img/20230605125311.png)


#### Flyweight
Sdílený objekt použitý na vícero místech - sdílený stav je uchováván v objektu, kontextuální stav se dodá skrz parametry volané metody. Slouží k úspoře paměti a/nebo výpočtu (pokud je inicializace drahá). Rozlišujeme mezi sdíleným a specifickým stavem. Tedy pro textový editor mám pro všechny znaky A uloženou jednu nějakou vizualizaci, což je tedy sdílený stav. Na druhou stranu pozice daného znaku je již specifická a nemůže být sdílena, jde tedy o specifickou vlastnost.

##### Aplikovatelnost
- používáme velké množství malých objektů
- cena za uložení je vysoká

Příkladem je DB pool, případně nějaký textový editor. Šetříme paměť, více vytěžujeme výpočetní výkon při hledání.

![](img/20230605130130.png)


### Behavioral patterns

#### Iterator
Poskytuje jednotné rozhraní k průchodu prvky kolekcí. Je to samostatný objekt (specifický pro danou strukturu), má metody jako `current()` a `next()` umožňující přístup k prvku, nebo posunutí interního ukazatele iterátoru na další prvek.

##### Aplikovatelnost
- nechceme zobrazovat interní strukturu
- chceme paralelní procházení, díky více instancím
- implementace `for-in/foreach`.

![600](img/20230603144800.png)


#### Strategy
Poskytuje rozhraní k výpočtu/operaci, které může klient použít bez znalosti konkrétní implementace a jejích detailů. Díky tomu je možné konkrétní implementace pro výpočet snadno měnit, nebo jednotně používat funkcionalitu objektů s rozdílnými implementacemi. Klient přistupuje přes `Context`, který se stará o případnou volbu strategie. Konkrétní strategie lze měnit za běhu. Díky tomuto přístupu například eliminujeme switch case. 

##### Aplikovatelnost
- máme nějaké třídy, které se liší pouze v implementaci jedné metody
- máme různé varianty a přístupy k výpočtu algoritmu
- libovolné použití přístupu přes rozhraní, třeba výpočet trasy (pro auto, pro cyklistu)

![600](img/20230603153352.png)

#### State
Obdobný jako Strategy, výběr implementace děláme na základě aktuálního stavu, který je možné měnit za běhu. O konkrétní stav (a výběr implementace) a jeho přeměny se stará `Context`, díky čemu izolujeme a můžeme jednoduše kontrolovat přechodu stavu v systému. 

##### Aplikovatelnost
- pokud se za běhu mění stavy objektu a jemu se na základě toho mění logika
- příkladem je telefon a jeho tlačítka pokud je vypnutý, zapnutý nebo zamčený

Na rozdíl od `Strategy`
- daná implementace je vybrána na základě vnitřního stavu
- řešíme přechody stavu, stavy se můžou nahradit jiným stavem
- stavy mohou mít referenci na kontext
- ne jenom specifický úkol, ale poskytujeme implementaci pro většinu věcí co `Context` nabízí

Příklad vypínač má dva stavy (concrete state), Vypnutý Vypínač a ZapnutýVypínač. Interface Vypínač má metodu přepni(), čímž se změní stav (VypnutýVypínač na ZapnutýVypínač a opačně)

![600](img/20230603154910.png)


#### Memento
Uchovává předchozí stavy objektu, díky čemuž je možné přenést objekt do dřívějšího stavu. Používá se pro případy, kdy přímý přístup do atributů třídy není možný (private atributy).

##### Aplikovatelnost
- chceme si ukládat předchozí stavy objektu
- nechceme aby se ven dostávaly implementační detaily

Příklad: použití při implementaci UNDO.

![600](img/20230605132549.png)


#### Observer
Umožňuje tvorbu mechanismu pro notifikace. Observery se registrují ke sledování Subjektu (ukládáme si reference observerů do vektoru). V momentě, kdy se subjekt změní (a měly by být observery notifikovány), stačí zavolat metodu notify, která projde observery a každého notifikuje (obvykle zavoláním metody).

##### Aplikovatelnost
- pokud máme nějaké dvě třídy, které na sobě závisí
- chceme efektivnější metodu než pooling

![600](img/20230605162806.png)


#### Visitor
Poskytuje jednotné rozhraní pro spuštění nějaké shodné akce nad objekty. Každý objekt má implementaci odlišnou, ale signatura pro všechny objekty je shodná (e.g. serializace různých struktur, bere Self, vrací String). Namísto abychom na základě typu struktury volali příslušnou metodu (`if let Vehicle::Car(_) = my_data { return serialize_car(my_data); }`), implementujeme metodu poskytnutou rozhraním (jen `serialize(&self)`). V diagramu je to metoda `accept(v: Visitor)`.

##### Aplikovatelnost
- pokud máme více různých tříd nad kterými musíme vykonat nějakou operaci
- nevýhodou je, že porušuje zapouzdření
- pokud nad různými třídami máme různé operace, které je potřebna provést

E.g. serde

![600](img/20230605165644.png)

## Modely softwarových systémů, jazyk UML.

Modely softwarových systémů popisují systém vždy z nějakého zjednodušeného pohledu (model je už z definice abstrakce). Různé modely se zabývají různými aspekty/fázemi vývoje systému. Důležité však je, aby byly modely systému vzájemně konzistentní. Obecně lze rozlišovat na modely popisující strukturu a modely popisující chování.

**UML (Unified Modeling Language)** je standardizovaný modelovací jazyk umožňující jednotný způsob vizualizace návrhu systému. Pro snadné verzování je fajn PlantUML (píšeme UML jako deklarativní kód, ze kterého generujeme příslušné diagramy). UML se dělí na základní typy a to je strukturální a behaviorální.

### Context diagram

Popisuje kontext a prostředí, v jakém systém má fungovat. Jsou zde znázorněny interakce s externími systémy a skupinami uživatelů.

![](img/20230607124347.png)

Neřešíme části, se kterými přímo neinteragujeme. Ty jsou vidět v [Ecosystem map](./dev_1_analyza_a_navrh.md#ecosystem-map). 

### Use case diagram

Zahrnuje všechny (uživatelé i jiné systémy), kteří budou systém používat ve formě actorů. U každého actora vidíme dostupné akce (use case) a případně vazby mezi akcemi.

| ![](img/20230607130528.png) | ![](img/20230607130605.png) |
|---|---|

### Conceptual class diagram

Diagram tříd, ale neřešíme datové typy ani metody. Zajímají nás klíčové entity (struktury/třídy), jejich data plynoucí z požadavků, a vazby mezi entitami (kontext). Pomáhá ujasňovat terminologii.

### Class diagram

Statická reprezentace systému ve formě tříd, zobrazuje jejich metody, atributy a vzájemnou provázanost. Vztahy mají kardinalitu

**Asociace** - klasická šipka (nebo čára pro oboustranný vztah), popisuje vztah daných tříd
**Agregace** - bílý kosočtverec, třída obsahuje jinou třídu (u ní je kosočtverec)
**Kompozice** - černý kosočtverec, třída (s kosočtvercem) je nedílnou součástí jiné třídy

![](img/20230608120634.png)

### Object diagram

Zachycuje systém za běhu v určitém čase, zobrazuje konkrétní objekty a jejich vazby.

![](img/20230608121047.png)

### Activity diagram

Popisuje workflow systému/komponentu (dle úrovně abstrakce), jednoduchý na pochopení i pro zákazníka.

![](img/20230609000854.png)

### Sequence diagram

Popisuje interakce v čase mezi jednotkami (třídami/komponenty/actory) systému

![](img/20230609001314.png)

### Deployment diagram

Popisuje jednotlivé komponenty systému a jejich komunikační toky, včetně použitých technologií.

![](img/20230609001416.png)

### Component diagram

Popisuje komponenty a jejich kompozici v sýstému.

Třídní/lollipop notace

![](img/20230606160621.png)

Komunikační rozhraní koponentů se nazývají porty, přímé spoje connectors.

![](img/20230606164944.png)

## Notes

**Verifikace vs validace** - validace ověřuje, že náš model odpovídá požadavkům, verifikace ověřuje, že naše implementace odpovídá našemu modelu, že je implementace kvalitní. E.g. u mostu by se validovalo, že je postavený v místě, kde je potřeba. Verifikovalo by se, že je postavený správně.

**Motivace objektových metod/návrhových vzorů** - systémy bývají složité, špatně se udržují a je náročné měřit/zajistit kvalitu, často se mění nároky. Pomůže dekompozice systému do menších koherentních částí, které se lépe udržují/mění, snadněji se měří kvalita

**Problém s cyklickou vazbou objektů** - e.g. v metodě toString() je potřeba vhodně řešit, abychom se necyklili. Proto může být vhodnější definovat si pro takové případy speciální objekty s jasnou hierarchií a bez cyklů

**Interface Definition Language** - popisuje rozhraní formou, která je nezávislá na použitém programovacím jazyce (e.g. OpenAPI Specification pro REST, protocol buffer pr gRPC, Web Service Definition Language pro SOAP, CORBA IDL). Obvykle je možné pomocí IDL schématu vygenerovat v daném programovacím jazyce kód/struktury, který poskytovatel implementuje a uživatel používá. Více v [otázce 7](./7_distribuovane_systemy.md).

**Event list** - seznam všech událostí, které mohou v systému nastat

### Ecosystem map

Znázorňuje celý kontext (včetně částí, se kterými přímo nekomunikujeme), ve kterém náš systém funguje.

![](img/20230607124544.png)

### Analytické vzory
Návrhové vzory nabízí řešení na často řešené problémy v návrzích systému. Tato řešení jsou místy až příliš sofistikovaná, takže se doporučuje složitější návrhové vzory používat z rozvahou, abychom problém *neoverengineeringovali*.

Accountability vzory *(přijdou mi ve slajdech popsány složitější, než jsou, proto popisuju koncepty/zapamatovatelné aspekty, zbytek si člověk dokáže odvodit. Odkazy vedou na příslušnou část s diagramem.)*
- [Party](./dev_1_analyza_a_navrh.md#party) - společný název (abstrakce) pro osobu či firmu, obvykle má kontaktní údaje (adresu, telefon, email...)
- [Organization Hierarchies](./dev_1_analyza_a_navrh.md#organization-hierarchies) - řešíme problém reprezentace organizace skládající se z často měnících se hierarchií organizačních jednotek (e.g. Korporace, Region, Pobočka, Oddělení... typy jednotek mohou být také předmětem změn). Řešením je stavební blok `Organizace`, která má 0..1 rodiče `Organizace` a  0..n potomků `Organizace` (rekurzivní vazba). Jednotlivé typy oddělení pak mohou dědit od `Organizace`.
- [Organization Structure](./dev_1_analyza_a_navrh.md#organization-structure) - To samé co organization hierarchies, ale přidáváme k tomu `TimePeriod` (pro verzování v čase), `Typ Organizační Struktury`, který může mít `Pravidla` zajišťující, že třeba oddělení nebude nadřízené divizi.
- [Accountability](./dev_1_analyza_a_navrh.md#accountability) - Organization Structure, ale Organizaci nahradíme Party (a vztahu říkáme accountability). Je tam opět `TimePeriod`, ale `Typ Organizační Struktury` se jmenuje `Accountability Type`. `Pravidla` pro vazby zahazujeme
- [Accountability Knowledge Level](./dev_1_analyza_a_navrh.md#accountability-knowledge-level) - Accountability, ale `Pravidla` pro vazby mezi jednotlivými `Party`s zase přidáme. `Pravidla` jsou definována pro jednotlivé `Accountability Type`s, každé definuje povolenou kombinaci `Party Type` potomka a rodiče v hierarchii. Úrovni, kde popisujeme pravidla (a kde tím pádem jsou i `Accountability Type`s a `Party Type`s) říkáme knowledge level, existuje jen pro zajištění správné kompozice (ale nemá moc význam pro day-to-day operace).

Příklad pro aplikaci accountability je ve [slajdech (str 35+)](https://is.muni.cz/auth/el/fi/podzim2021/PA103/um/02-03-Analysis-patterns.pdf#page=35).

Observations & measurements
- [Quantity](./dev_1_analyza_a_navrh.md#quantity) - kvantita má hodnotu a jednotku (v Rustu bychom použili Newtype pattern konkrétní jednotky a pomocí traitů implementovali funkcionalitu)
- [Conversion Ratio](./dev_1_analyza_a_navrh.md#conversion-ratio) - převedení jedné jednotky na jinou, samo o sobě funguje jen pro lineární vztahy
- [Compound Units](./dev_1_analyza_a_navrh.md#compound-units) - Jednotka může být buď `Atomic Unit` (e.g. kilometry), nebo `Compound Unit`, která má aspoň jeden `Unit Reference` obsahující mocninu (e.g. kilometry za hodinu). 
- [Measurement](./dev_1_analyza_a_navrh.md#measurement) - Reprezentuje výsledek měření. Každé měření bylo někým vykonáno (`Person`), zkoumalo nějaký měřený fenomén (`Phenomenon Type`) a zjistilo nějakou hodnotu, včetně jednotek (`Quantity`)
- [Observation](./dev_1_analyza_a_navrh.md#observation) - výše popsaný `Measurement` je typ `Observation`, stejně jako `Category Observation` umožňující zaznamenávat nekvantitativní měření s nějakou kategorickou hodnotou (e.g. počet lidí s danou krevní skupinou), kde nás zajímá konkrétní `Phenomenon` (e.g. A+), který je součástí `Phenomenon Type`.
    - je možné přidat i způsob měření `Protocol`, či sledovat přítomnost/nepřítomnost kategorického jevu, který může mít závislosti na (pod)jevech modelovaných pomocí `Observation Concept` (e.g. diabetik typu 2 je obecně diabetik)

### Diagramy analytických vzorů

#### Party
![](img/20230602212700.png)

#### Organization Hierarchies
![](img/20230602212810.png)

#### Organization Structure

![](img/20230602221810.png)

#### Accountability
![](img/20230602223147.png)

#### Accountability Knowledge Level
![](img/20230602224136.png)

#### Quantity
![](img/20230603105247.png)

#### Conversion Ratio
![](img/20230603105928.png)

#### Compound Units
![](img/20230603110857.png)

#### Measurement
![](img/20230603111248.png)

#### Observation
![](img/20230603112121.png)

Včetně způsobu měření a logickými vazbami mezi (pod)jevy
![](img/20230603112705.png)
