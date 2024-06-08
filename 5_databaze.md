# Databáze
> Principy ukládání dat, databáze a souborové systémy. Kódování a komprese dat. Architektura relačních databází, dotazovací jazyk SQL a jeho části (definice, manipulace, transakce). Jazyk definice datového schématu, DDL. Jazyk manipulace s daty, DML. Relační algebra, integritní omezení, řízení transakcí. Indexování, hašování. Příklady z praxe pro vše výše uvedené. ([PV003](https://is.muni.cz/auth/el/fi/jaro2022/PV003/um/) || PV062)

## Principy ukládání dat, databáze a souborové systémy

**Persistence** - je nějaká schopnost programu si udržet data mezi jednotlivými sezeními, restarty a spuštěními. Používají se na to souborové systémy, databáze nebo cloudové uložiště.

Pro zajištění persistence jsou zde 3 základní přístupy
- *Souborový systém* - ukládáme jako soubory, pro strukturovaná data například jako XML, případně jako nestrukturovaná data jako klasické soubory
- *Relační databáze* - ukládáme do relačních databází, případně Relational database management system (RDBMS) díky tabulkám a vztahům mezi tabulkami. Pro dotazování používáme SQL.
- *NoSQL* - například MongoDB nebo Cassandra, kdy ukládáme spíše nestrukturovaná data s lepším důrazem na škálování a strukturování

#### Databáze
- uspořádaná množina dat, se kterými jde pracovat
- jedná se o kolekci relací, vztahů, integritních omezení, indexů, triggerů a podobně
- nezávislý na aplikaci, jednotné rozhraní pro všechny
- snadné zabezpečení, konzistence, **souběžný přístup**
- snadná čitelnost, dokumentovatelnost
- relační systémy korelují s ERD
- **deklarativní přístup**
- obtížná implementace složitějších struktur (záleží však na systému)
- relačních databázích platí, že umožňují ACID [transakce](./5_databaze.md#řízení-transakcí). 

##### Relační model
- správa dat pomocí jazyka, kde všechny data reprezentujeme jako množinu n-tic
- právě tyto *n-tice jsou seskupené do relací*, což nám reprezentuje tabulky
- účelem právě relačního modelu je poskytnout nějakou deklarativní metodu pro specifikování dat a dotazování
- *struktura* - tabulky, *operace* - dotazování, *modifikace* - SQL a relační algebra

##### RDBS
- *typy datových elementů* 
	- klasické základní datové typy, většinou pevné délky
	- variabilní délka se řeší třeba přidáním délky na začátek
- *záznam*
	- seznam nějak souvisejících datových elementů
- *schéma záznamu*
	- popisuje strukturu (pořadí, typ atributů, počet)
- *sloupcové relace*
	- lepší pro efektivní čtení a vyhledávání
- *řádkové relace*
	- efektivnější když přistupujeme k celým záznamům
	- řeší se zde problém variabilní délky, kde potřebujeme oddělovač
	- můžeme mí seřazené záznamy, které mají lepší dotazování, ale horší modifikace

##### Důvody vzniku 
- redundance, nekonzistence dat a bezpečností problémy
- problémy s přístupem, souběžným přístupem k datům a atomicitou aktualizací 
- problémy se zaručením integrity dat

**Výhody**
- integrita dat a konzistence
- skvělý dotazovací jazyk
- škálovatelnost

**Nevýhody**
- komplexita
- vyžaduje větší výkon
- může zde být nižší flexibilita, kvůli databázovému schématu


#### Souborový systém
- sada nástrojů od operačního systému
- umožňuje přístup a správu dat na disku
- menší systémové nároky, jednodušší
- náročné zajištění konzistence, nutnost řešení zamykání souborů
- je zde problematický transakční přístup
- náročnější správa přístupových práv a tedy nějakou bezpečnost
- nutnost konzistentně řešit formát dat
- horší čitelnost & dokumentovatelnost datového modelu
- operační systém slouží jako abstrakce pro aplikace, umožňuje jednotný přístup

V rámci souborových systémů rozlišujeme dva typy souborů
- *Fyzické soubory* - ty co jsou uložené na hard disku, po otevření se vytvoří FD
- *Logické soubory* -  jen file descriptor, který používá proces, je v operační paměti

Pro aplikace se hodí na ukládání velkých souborů (obrázky, video, statická stránka), které je nepraktické uchovávat v databázi. Je nutné dávat pozor, abychom neposkytli přístup jinam než chceme. Nicméně v praxi je dobré na tohle využít CDN.

**Výhody**
- jednoduchost
- velký flexibilita
- přímý přístup

**Nevýhody**
- horší škálovatelnost
- většinou nějaká redundance pokud chceme mít na více místech
- není zde úplně vyřešena integrita


---

## Kódování a komprese dat

#### Kódování dat
Kódování dat má za cíl konvertovat data na nějakou binární reprezentaci, která se dá ukládat. Snaží se přitom zaměřovat na balanc mezi efektivním využitím úložiště a integritou dat.

Hlavní typy kódování:
- *Fixní šírka*
	- každý znak je na fixní šířku bajtů
	- je super z hlediska jednoduchosti a práce s daty
	- má redundantní a nevyužité místo vůči entropii dat
- *Variabilní*
	- snaží se přizpůsobit datům
	- většinou máme nějaké oddělovače, je trochu složitější správa dat
	- složitější na implementaci
- *Slovníkové kódování*
	- máme slovník a jen se na něj odkazujeme
	- obzvlášť efektivní pro určité enum hodnoty v rámci sloupců a podobně


#### Komprese
Techniky s cílem transformace informací do formátu, který je efektivní na ukládání či přenos. 

*Komprese* - kóduji zprávu `O(x)` na `L(x)`, kdy `L(x)` by mělo být menší než `O(x)`
*Neurčitost zprávy* - `H(x)` nejde zakódovat na nižší počet, aby bylo stále bezztrátové
*Kompresní poměr* - `L(x)/O(x) => 0.75/1`, tedy o 25% kratší zpráva
*Kompresní faktor* - `O(x)/L(x)`
*Kompresní zisk* - `O(x) - L(x) / O(x)`
*Redundance zprávy* - `R(X) = O(X) - H(X)`
*Redundance komprimované zprávy* - `R'(X) = L(X) - H(X)`

Druhy kompresí
- *statistická komprese* - nemění se procedura komprimování
- *adaptivní komprese* - dynamicky se mění

- *fyzická* - zadrátovaná a nekouká se na význam dat, které komprimuje
- *logický* - většinou ztrátová, snaží se používat rysy dat

Máme dva základní druhy
- *Bezztrátová komprese* 
	- z komprimovaných dat jsme schopni plně rekonstruovat původní data (e.g. png, zip)
	- jako příklady je například Huffmanovo kódování
- *Ztrátová komprese* 
	- část komprimovaných dat je ztracena (e.g. jpeg, mp3)
	- jsme schopni dosáhnout větší komprese
- *Sloupcové komprese*
	- zaměřujeme se hledání vhodných kompresí nad sloupci a ne nad řádky
	- většinou jsou dobré využití slovníkových kompresí

##### Vybrané metody 

**Základní**
- Run length Encoding
	- pro repetetivní znaky ve zprávách
	- udávám počet a znak `AAAABBCC -> 4A3B2C` 
- Bitová komprese (například Bit-Packing)
	- technika pro možnost zabalení více druhů hodnot do jednoho slova
	- teoreticky pokud bych měl A a B každý na 2B tak to mohu sloučit a dát to na 4B
	- tím pádem nemusím použít třeba 2x integer

**Statistické**
- [Huffmanovo kódování](https://www.youtube.com/watch?v=iEm1NRyEe5c) 
	- na základě frekvence určíme pro každý symbol kódovací znak
	- kódovací symboly jsou prefixové, takže nemusíme mít oddělovače
	- kód má minimální redundanci, proměnlivá délka kódu symbolů
	- seřadíme znaky podle frekvence do prioritní fronty ve formě uzlů
	- u každého znaku máme uvedenou frekvenci a postupně tvoříme strom
	- cílem je dostat se k hodně frekvenčním znakům na minimum bitů
    
- [Shannon-Fano](https://www.youtube.com/watch?v=dJCck1OgsIA) 
	- podobný jako Huffman, nemusí být optimální
	- jdeme od kořene a sekvenci symbolů seřazených dle frekvence dělíme na poloviny
	- při každém dělení značíme `0` a `1`
	- jakmile je ve vytvořené polovině jen 1 symbol, už není co dělit.

**Slovníkové metody**
- *LZ77*
	- postupně klouzavým způsobem určité délky vzoru ukládám do slovníku
	- držím si tedy počátek vzoru, délku vzoru a další slovo
- *LZ78*
	- vytvářím kompletní dynamický slovník pro celou zprávu
	- dodávám ho zvlášť a odkazuji se na něj
	- modifikace u *LZW*, kdy se některé hodnoty už přednastaví


---

## Architektura relačních databází

Je potřeba si rozlišit pojmy DB a DBMS.
- **databáze (DB)**
	- je to kolekce dat, jedná se o skutečná dat uložena na disku
	- žádná interakce s daty, jen uložiště
	- nejsou zde žádné nástroje pro správu
- **database management system (DBMS)**
	- jde o software, který komunikuje s databází
	- poskytuje správu dat, manipulaci, práva přístupu apod.
	- poskytuje SQL pro komunikace
	- umožňuje zálohování, transakční zpracování a podobně

Dělení databázových podle architektury
- **centrální architektura** - DB i DBMS na jednom počítači a komunikují přes terminály
- **architektura klient-server** - DB i DBMS na jednom serveru odpovídající na dotazy
- **architektura distribuovaných databází** - DB je na více serverech, ale tváří se jako jedna

Nějaká jednoduchá architektura by mohla vypadat taky jako:
- **databázový server** 
    - přijímá, zpracovává a odpovídá na požadavky
- **relační databázový systém** 
    - autentizace, autorizace
    - aplikace pracující nad samotnou databází
    - umožňuje tvorbu tabulek/indexů... manipulaci s daty, jejich čtení...
    - zajišťuje integritu dat
    - vyhodnocuje a zpracovává SQL queries, provádí vnitřní optimalizace
    - může dělat kešování
- **databáze** - samotné místo, kde jsou data uložena

RDBMS může obsahovat techniky pro administraci přístupových práv (omezení určitých operací, viditelnost dat až na row/column level...).

Pokud se otázkou myslí *Z jakých prvků se relační databáze skládají*, pak by bylo fajn mluvit o tabulkách, sloupcích, jazyku SQL pro jejich definici (DDL, data definition language) a manipulaci (DML, data manipulation language), indexech, (materializovaných) views...


---

## Dotazovací jazyk SQL a jeho části

Dotazovací jazyk SQL vychází z [relační algebry](./5_databaze.md#relační-algebra). Je to neprocedurální jazyk, nerozlišuje velká a malá písmena a je standardizovaný, nicméně některé speciální funkce mohou dodávat různé databázové systémy podle potřeby.

Můžeme rozdělit na základní prvky jako je:
- **Příkaz** - řetězec znaků v syntaxi SQL (SELECT, DELETE, UPDATE)
- **Dotaz** - příkaz, který vrací relaci dat (SELECT)
- **Klauzule** - jednotlivé komponenty příkazů
- **Predikát** - podmínka, která se využívá v příkazech, musí být podle 3 hodnotové logiky
- **Výraz** - konstanta nebo funkce, vracející skalární hodnotu

Obsahuje konstrukty pro definici datového schématu, pro manipulaci s daty a pro transakční zpracování (viz další sekce). V některých systémech má prostředky pro procedurální programování, **PL/SQL** (třeba Oracle). Při práci s SQL používáme prepared stetements, abychom zabránili *SQL injection*.

##### Trigger
SQL může obsahovat triggery, tedy dodatečné akce, které se mají vykonat při určitém příkazu (INSERT, UPDATE, DELETE). Používají se třeba pro udržování history table.

Vždy musíme specifikovat za jaké podmínky a kdy se má spustit a jaké akce má provést. Mohou nastat i problémy cyklení při provolávání apod. Triggery mohou být jak DML (při přidání řádku), tak DDL (při přidání tabulky).

```postgresql
CREATE TRIGGER aktualizuj_platy
ON lidé FOR DELETE
AS DELETE FROM platy WHERE platy.osoba_id = lide.id
```

##### Agregační funkce
Při použití GROUP BY vytvářím skupiny, nad kterými se poté používají v SELECT různé aritmetické a statistické funkce. Používané s `GROUP BY sloupec/sloupce`. Pokud nepoužijeme `GROUP BY`, počítají se agregační funkce ze SELECTu. Lze použít `HAVING ...`, což je `WHERE`, ale s použitím agregačních funkcí.
- COUNT - vrátí počet hodnot v určeném sloupci, v kombinaci s DISTINCT i unikátní hodnoty
- AVG, SUM, MIN, MAX - další klasické funkce pro agregování dat


##### Uložené procedury
Jsou to objety v databázi, které neobsahují data, ale jsou to programy, které vykonávají nějaké akce nad daty. V rámci Oracle je to například PL/SQL, v rámci MS SQL například T-SQL.

Výhody uložených procedur jsou v optimalizaci, kdy po první provedení je plán uložen a další provedení jsou už rychlejší. Můžeme mít nějaké zabezpečení, kdy povolíme určitým uživatelům pouze přístup k procedurám.

Příklad:
```plsql
CREATE OR REPLACE PROCEDURE get_employee
	(p_empid in employees.employee_id%TYPE,
	 p_sal OUT employees.salary%TYPE,
	 p_job OUT employees.job_id%TYPE) IS
 BEGIN
   SELECT sal,job_id INTO p_sal, p_job
   FROM employees
   WHERE employee_id = p_empid;
 END;

-- Usage
VARIABLE v_salary NUMBER;
VARIABLE v_job VARCHAR2(15);
BEGIN 
	GET_EMPLOYEE (120, :v_salary, :v_job);
END;
```


---

## Jazyk definice datového schématu, DDL.

Různé RDBMS podporují různé typy. Třeba TEXT v základu SQL definován není, ale v praxi je použití VARCHAR2 s fixní délkou příliš nepraktické.

Tvorba tabulky

```postgresql
CREATE TABLE Products (
	id          INT   PRIMARY KEY,
    cost        INT   NOT NULL,
    ean         INT   UNIQUE NOT NULL,
    name        TEXT  NOT NULL,
    description TEXT,
    created_by  INT   NOT NULL REFERENCES User(id)
    updated_at  DATETIME,
);
```

V praxi je lepší si generovat vždycky primární klíče - externí unikátní hodnoty nemusí být vždy zas tak unikátní/neměnné. Compound primary key je možný, ale opět bývá pomalejší. 

Generování hodnot ID se dřív používaly sekvence, dneska stačí `SERIAL`, nebo `AUTOINCREMENT`.

U cizích klíčů můžeme specifikovat `ON DELETE` `CASCADE` (se smazáním uživatele se smažou i jím přidané produkty), nebo `SET NULL`.

Modifikace tabulky
```sql
ALTER TABLE Products ADD picture TEXT;
ALTER TABLE Products DROP COLUMN description;
DROP TABLE Products;
```

V produkci použijeme migrační schéma obsahující UP a DOWN skripty, abychom mohli případně akce revertovat.


---

## Jazyk manipulace s daty, DML

Pro udělování oprávnění pracovat s daty v databázi.

```postgresql
GRANT ALL PRIVILEGES ON ALL TABLES IN SCHEMA schema_name TO username;
GRANT ALL PRIVILEGES ON ALL SEQUENCES IN SCHEMA schema_name TO username;
GRANT ALL PRIVILEGES ON DATABASE database_name TO username;
REVOKE DELETE, UPDATE ON ORDERS FROM customer1;
```


---

## Jazyk manipulace s daty, DML

Množina příkazů, které se používají pro výběr, vkládání, úpravu a mazání dat v tabulkách.

**Insert**
Kontrolují se integritní omezení, v případě autoincrement/serial klíče ho není nutné explicitně uvádět. Obvykle příkaz vrací vložená data (včetně vygenerovaných hodnot).

```sql
INSERT INTO Tabulka(sloupec_a, sloupec_b) 
VALUES (hodnota_a, hodnota_b);
```


**Update**
Update bez WHERE může provést update všeho. Kontrolují se integritní omezení

```sql
UPDATE Tabulka 
SET slopec_a = hodnota_a
WHERE ... --často klíč
```


**Delete**
Delete bez WHERE může provést smazání celého obsahu.

```sql
DELETE FROM Tabulka WHERE ...
```


**Select**
Výsledek selectu lze dát do závorek a použít namísto nějaké tabulky, data mají pořád tabulární strukturu. Mezi daty se stejnou strukturou lze provést množinové operace `UNION`, `INTERSECT`, `MINUS`.

U `WHERE` můžeme používat i příslušnost v množině hodnot `IN`, rozsahu `BETWEEN ... AND ...`, logické operátory `AND`, `OR`... U stringů `LIKE` kde `?` zastupuje znak a `%` několik znaků.

```sql
SELECT DISTINCT Tabulka.sloupec, B.sloupec 
FROM Tabulka JOIN TabulkaB AS B ON Tabulka.cizi_id = B.id
WHERE price > 0
ORDER BY sloupec ASC
```


**Pohled/View**
Uložený a pojmenovaný select, který se vykoná s provedením dotazu. View mají omezenou modifikaci dat (například nelze, pokud obsahuje agregaci, distinct, union...)


**Materializovaný pohled/view**
View, jehož výsledek se předpočítává. Vrací se pak hodnoty přímo z nové tabulky, ale s každou změnou je třeba materializované view přepočítat (rychlejší čtení, pomalejší zápis).


---

## Relační algebra

**Relace** je podmnožinou kartézského součinu domén. Toto se promítne do databáze tak, že domény jsou datové typy sloupců a tabulka (složená ze sloupců) obsahuje pouze takové kombinace hodnot (řádky), jaké jsou v relaci.

Relační algebra je dotazovací jazyk, který bere na vstupu jednu nebo více relací a vrací jednu relaci. Používá celkem 6 základních operací *selekce*, *projekce*, *sjednocení*, *rozdíl*, *kartézský* *součin* a *přejmenování*. Ta uzavřenost na relace je důležitá, i kdyby na vstupu měla jít pouze jednoatributová relace. Tedy i pokud si vypíšu počet řádků, tak mi to nevrátí číslo ale relaci.

**Selekce**
- označení jako Sigma `σ`
- příklad: $σ_P(r) = \{t | t ∈ r ∧ P(t)\}$
- `p` je predikát, `r` je relace
- použití: $σ_{A=B ∧ C < 5}(r)$
- vybere řádky podle parametrů

**Projekce**
- vyberou se zvolené sloupce relace
- píše se jako pí $Π$
- příklad: $Π_{F1, F2,…, Fn}(E)$
- $E$ je relace a $F_1, F_2, F_n$ jsou aritmetické výrazy s konstanty a atributy $E$

**Sjednocení**
- pokud mají stejnou aritu, můžeme použít sjednocení
-  $r ∪ s = \{t | t ∈ r ∨ t ∈ s\}$
- výsledkem je jedna relace

**Rozdíl**
- opět jako sjednocení, musím míst stejnou aritu a kompatibilní domény
- $r – s = \{t | t ∈ r ∧ t ∉ s\}$

**Kartézský součin**
- dvě relace na vstupu s předpokladem disjunktnosti, pokud nejsou musí se přejmenovat
- $r × s = \{t q | t ∈ r ∧ q ∈ s\}$

**Přejmenování**
- $ρ_{relaceB(attr_1, attr_2, attr_3...)}(relaceA)$
- přejmenování relace a jejich atributů
- v příkladu přejmenuji relaci A na relaci B a změním názvy všech jejich atributů
- přejmenování se typicky musí použít při agregačních funkcích, kde jsou mezivýsledky
- je potřeba přejmenovávat u společných atributů relací u kartézského součinu

**Agregační funkce**
- $_{G1, G2, …, Gn}𝓖_{F1A1, F2A2, …, FmAm} (E)$
- seznam před $𝓖$ jsou atributy, podle kterých seskupuji n-tice
- seznam za $𝓖$ jsou souhrnné funkce a názvy atributů
- je potřeba dávat pozor na null hodnoty, protože pokud všechny hodnoty budou null, výsledek taky bude null. Jediný COUNT tak vrací 0.

**Spojování relací**
- *Přirozené spojení* (Natural join)
	- příklad jako: $r ⨝ s$
	- dá se vyjádřit jako relační algebra projekce, selekce a kartézského součinu
	- spojím dvě tabulky na základě stejných společných atributů
- *Vnější spojení* (Outer join)
	- podobné jako přirozené, jen dodáváme null hodnoty pro prázdná místa
	- díky tomu nemáme ztrátu žádné informace
	- podrozdělení na *Levé spojení*, *Pravé spojení*, *Úplné spojení*

Existují dotazy, které nejsme schopní vyjádřit relační algebrou, třeba tranzitivní uzávěr. Na to je totiž potřeba rekurze, která není v relační algebře.

*Tranzitivní uzávěr nad relací získáme tak, že se díváme na prvky množiny v relaci. Pokud je `a` v relaci s `b` a `b` v relaci s `c`, pak (aby bylo dosaženo tranzitivity) tranzitivní uzávěr obsahuje relaci `a` s `c`.*


---

## Integritní omezení

Součástí DDL, jazyku definice dat. Určitým způsobem omezují, jakých hodnot mohou pole nabývat. Díky těmto omezením máme vždy konzistentní data v databází a je to hlídáno přímo na úrovni databáze když vkládáme data.

Přehled integritních omezení:
- `NOT NULL` - povinnost 
- `UNIQUE` - unikátní hodnota v rámci sloupce
- `FOREIGN KEY .. RERERENCES ..(..)` - kontrola reference na jinou tabulku
- `CHECK(price>0)` - kontrola řádku, který vkládám podle nějaké podmínky

Příklad přidání omezení:
```postgresql
ALTER TABLE tabulka ADD CONSTRAINT nazev NOT NULL (id);
ALTER TABLE tabulka ADD CONSTRAINT nazev CHECK (id>0);
```


---

## Řízení transakcí.

Transakce se používají pro sekvenční práci nad daty a nechci aby se mi data mohly dostat do nekonzistentního stavu. Transakce v RDBMS mají ACID vlastnosti
- **Atomicity** - příkazy se v transakci provedou všechny nebo žádný
- **Consistency** - po vykonání transakce ke databáze v konzistentním stavu, není porušeno žádné integritní omezení
- **Isolation** - transakce je izolovaná od ostatních transakcí, je možné nastavit úrovně transakce, dle toho může transakce skončit chybou (pokud došlo k modifikaci stejného objektu, jaký modifikovala jiná transakce), nebo se využijí zamykací mechanismy
- **Durability** - data jsou po vykonávání transakce persistentně uložena

Transakce se potvrzují příkazem `COMMIT`, vrací příkazem `ROLLBACK` na stav před započením transakce, či po poslední `SAVEPOINT`. K nekonzistenci by mohlo teoreticky dojít, pokud by nastala chyba v DB systému, výpadku hardware a nebo nějaké interní chybě v transakci.

Úrovně izolovanosti transakce
- *Read uncommitted* - hned jak transakce provádí změny je možné je vidět, tím pádem nevím, jestli data která čtu nebudou později zrušena, tomu se říká *dirty read*
- *Read committed* - mohu číst jen commitovaná data, nicméně jedna transakce může v různé časy vidět různé hodnoty, pokud jí pod ruce sahá a edituje jiná transakce, tomu se říká *repetable read*
- *Repetable read* - je zaručené, že nedojde k opakovanému čtení, ale mohou se vyskytovat takzvané *phantom read*, kdy stále mohou přibývat nové řádky
- *Serializable* - nejvyšší a nejvíce robustní izolace, kdy skutečně jedna transakce běží po druhé a nedochází k žádným problémům výše

Transakce mají 5 stavů: *aktivní*, *částečně potvrzená*, *potvrzená*, *chybující zrušená*

Atomičnost transakce
- musíme zajistit, že se provedou všechny nebo žádný příkaz
- *UNDO* - zapisujeme operace do žurnálu, abychom při chybě uměli vrátit databázi zpět do stavu před zahájením transakce. Do žurnálu zapíšeme data a po uložení na disk přidáme potvrzovací *commit*. Pokud najdeme *commit* nebo *abort* tak se neděje po recovery nic, pokud bychom našli *start* a žádný abort nebo *commit*, pak se změny vrátí. U undo tedy zapisujeme *commit* až po zapsání dat na disk.
- *REDO* - operace se zapisuje, aby se provedla znovu pokud například vypadne proud. Commit se píše po skončení transakce a před zapsáním na disk. Při výpadku tak se provedou znovu všechny akce po posledním commit od nejstarších.


---

## Vyhodnocování dotazů

Vyhodnocování dotazu se skládá ze základních kroků:
- **Analýza** - překládáme a parsujeme dotaz do interní reprezentace, kterou následně přeložíme do relační algebry. Ověřujeme zde syntaxi a existenci jednotlivých relací
- **Optimalizace** - snažíme se najít nejlevnější provedení dotazu nad různými ekvivalentními dotazy, kdy jednotlivé ceny se vyhodnocují na základě statistických informací v katalogu databáze
- **Vyhodnocení** - provede se vykonání dotazu podle nejlevnějšího nalezeného a vrátíme výsledky uživateli

Měření nákladů na dotaz - abychom mohli nějak vypočítat cenu dotazu, bere v potaz vždy nějakou akci vynásobenou průměrnou dobou
- počet vyhledávání vynásobeno průměrnou dobou vyhledávání
- počet přečtených bloků vynásobeno průměrnou cenou čtení bloku
- počet zápisů bloků vynásobeno průměrnou cenou zápisu bloku


---

## Indexování

Index slouží ke zrychlení/zefektivnění častých dotazů nad tabulkou. Dotazy obsahující zvolený sloupec (či jejich kombinaci) budou rychlejší. Chceme indexovat, protože je to rychlejší než kdybychom procházeli data sekvenčně.

**Sekvenční soubor** - soubor s daty z tabulky, které chceme procházet
**Index** - soubor nějakých pomocných ukazatelů, ve stylu klíč a záznam

Dělení indexů
- **dense** - každý řádek je zaindexovaný, zabírá více místa, ale hledání je rychlejší
- **sparse** - pouze některé řádky zaindexované, zabírá méně místa, ale hledání pomalejší (je potřeba dohledat konkrétní řádek)

Příkaz pro vytvoření indexu v databázi:
```sql
CREATE INDEX my_index ON Products (Price)
```

##### Konvenční index
Jako v knihách, odkazy na řádky s danou hodnotou, je možné dělat více úrovní indexů, používat různá indexová uspořádání.

Vhodné pro *full scan* souborů, ale má náročné udržování při přidávání nových položek, protože nám někde mohou začít přetékat data a pak nemáme vyvážené odkazy.

Můžeme poté dělit dále na řídké index, husté indexy, případně na víceúrovňové indexy. Samozřejmě čím méně údajů v indexu, tím snažší údržba a paměťová náročnost, ale je pomalejší při dotazování. Víceúrovňové používají indexy z indexu.

Pokud bych neměl sekvenční soubor uspořádaný podle klíče, který indexuji, použije se sekundární index, který je uspořádaný a ukazuje na konkrétní hodnoty v tabulce.

##### B+ stromy
Není zde nutné sekvenční uspořádání dat v tabulce. Je to super na vyhledávání a hlavně se sám organizuje, takže jednotlivé vkládání a mazání dat nejsou až takový problém při výkonu jako u sekvenčních indexů. Používají se spíše B+ stromy, které mají hodnoty, tedy ukazatele do tabulky, uložené v listech. B stromy mají hodnoty i po cestě.

Jsou zde pravidla, že pro n je vnitřní uzel s maximálně n - 1 klíči a minimálně polovinou n klíčů, pokud nejde o kořen, které může mít minimálně 1 klíč a to samé platí o listech.

##### R stromy
Podobné jako B+ stromy, ale jsou vícedimenzionální, ve 2D fungují jako obdélníky. Data jsou v listových uzlech stromu. Rodič uzlu zahrnuje všechny své potomky (ve 2D jde o větší obdélník, který obsahuje potomky). Ideální je, aby zabíraly rodičovské obdélníky co nejméně prostoru - rodič totiž jako index redukuje oblast nutnou k prohledání (říká *hledej ve mně!*).

##### Bitmapový rastr
Pokud máme malý počet unikátních hodnot, můžeme sestavovat bitové vektory. Tedy ve výsledku index ve vektoru bitů říká, zda tam hodnota je nebo není a pro každý počet hodnot máme řádek tabulky indexu.

| Hodnota | Vektor   |
| ------- | -------- |
| foo     | 10010010 |
| bar     | 01001000 |
| baz     | 00100101 |
Dá se snadno pomocí bitových operací získávat různé konjunkce nebo disjunkce. Může to být nicméně paměťově náročné a špatně se aktualizují záznamy.

##### Indexování
Pokud chceme indexovat pro více atributů, můžeme:
- index pro jeden atribut a filtrovat
- nezávislé index pro každý atribut a poté nějaké sjednocení nebo průniky
- index v indexu, kdy indexuji už vytvořený index tabulky
- spojování klíčů, což jde o něco lépe v bitovém indexu


---

## Hašování

Cílem hašování je převést vstupní data libovolné délky na výstup jednotné délky (fixed-length řetězec, nebo číslo), hash. 

Z otisku by nemělo být možné odvodit vstup (**jednosměrnost**), pro každý vstup bychom měli být schopni deterministicky (vstupem jsou pouze data) určit jediný otisk. Zároveň může být (dle použití) cílem minimalizovat riziko kolize, tedy že dva vstupy mají stejný otisk (nelze se tomu ale vyhnout, protože musíme být schopni mapovat nekonečno možných vstupů na omezený počet výstupů daný délkou).

V rámci databází bereme to, že otisk nám určuje nějakou sekci dat, ve které je poté jednodušší vyhledávání. Ideálně tedy chceme aby hashovací funkce rozdělovala do sekcí záznamy rovnoměrně.

Bezkoliznost je jeden z kritických charakteristik hashovací funkce
- **slabá** - pro vstup A nejsme schopni v rozumném čase nalézt vstup B, se stejným otiskem
- **silná** - nejsme schopni v rozumném čase najít dva rozdílné vstupy se stejným hashem 


Hlavní dva druhy adresací:
- **Přímá adresace** - odkazuji se přímo na daný záznam
- **Nepřímá adresace** - odkazuji se například na další indexy (sekundární indexy)

Dva druhy hashování
**Statické hashování** 
- generujeme omezené množství hodnot a kolizní hodnoty řešíme přetoky
**Dynamické hashování** 
- funkce roste s počtem dat a generuje větší počet hodnot. Přidáváme tedy další sekce podle vyšších bitů

Pokud najdeme kolizi, můžeme to řešit dvěma způsoby
- *Uzavřené hashování* - vytváříme fixní adresy, při přetečení tak zřetězujeme data do přetokových oblastí
- *Otevřené hashování* - použijeme další, tzv. kolizní hashovací funkci

**Rozšiřitelné hashování** - využíváme první bity adresy, pokud máme plnou sekci tak ji rozštěpíme, pokud máme plný adresář tak se zdvojnásobí, vede to k méně plýtvání místem, ale je zde další vrstva nepřímosti.

**Linearání hashování** - když přijdu na kolizi tak zkusím další slot a pokud je volný tak dám prvke tam. Opakuji takhle dokud nenajdu volné místo. Když pak vyhledávám tak zkouším možné pozice a porovnávám prvky, jestli je to ten co jsem hledal.

**Cuckoo Hashing** - pokud najdu kolizi tak použiji druhou hashovací funkci pro nalezení další volné pozice pro prvek, který už na pozici byl

**Perfect Hashing** - snaží se úplně eliminovat kozice kdy má dvě úrovně hashování. Většino udobré pokud dopředu známe klíče a můžeme sestavit perfektrní hashovací funkci

Pro různé účely používáme různé algoritmy, jde o balanc rychlosti (u hesel může je kýžená pomalost) a bezpečnosti/pravděpodobnosti kolize.
- **MD5** - relativně rychlý, není bezpečný (lze rychle najít kolize i na běžném počítači). 
- rodina Secure Hashing Algorithm, za bezpečnou se aktuálně považuje **SHA-2** (SHA256, SHA512, SHA-384...)
- **Argon2** - v současnosti doporučovaný pro hašování hesel
- otiskem (hloupým, ale rychlým) může být třeba i délka vstupu, modulo apod.
