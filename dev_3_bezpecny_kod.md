# Bezpečný kód.

> Bezpečný kód. Metody autentizace a řízení přístupu. Biometrické metody autentizace, jejich dopady a problémy. Elektronický podpis a jeho použití. Autentizace strojů a aplikací. Zásady a principy bezpečného kódu. Typické bezpečnostní chyby na úrovni kódu, souběžnost, ošetření vstupů. Detekce bezpečnostních zranitelností, penetrační testování. Příklady z praxe pro vše výše uvedené. ([PV157](https://is.muni.cz/auth/el/fi/podzim2021/PV157/um/), PA193, PV276)

## Metody autentizace a řízení přístupu.

##### Klíčové pojmy

**Dostupnost (Availability)** - týká se hlavně toho, abych se ke službám a sítím dostali, tedy řešíme nějaké DoS útoky, používáme RAID, load balancing a clustering abych mu předešli

**Důvěrnost (Confidentiality) -** bráníme citlivá data před neoprávněným přístupem, zveřejněním nebo zachycením posílané zprávy. Šifrování, kontrola přístupu apod.

**Integrita (Integrita) -** snažíme se nějak uchovat přesnost a konzistentnost odesílané zprávy, abychom zajistili, že data která odešleme jsou nezměněna a spolehlivé během životního cyklu. Můžeme zde použít nějaké hashování, řízení přístupu apod.

**Zodpovědnost (Accountability)** - musíme umět dokázat, že uživatel akci opravdu udělal a je za ni zodpovědný. Tedy nemůže popřít, že třeba zprávu neodeslal.

**Účtování (Accounting)** - sledování využívání nějakých služeb za účelem nějaké správy a případně vyúčtování.

**Neodmítnutelnost (Non-repudation)** - záruka, že ani příjemce ani odesílatel nemůže popřít že odeslal nebo dostal zprávu. Máme teda nějaký důkaz o odeslání a přijetí.

**Safe** - neohrožujeme život nějaké vlastnosti nebo komponenty

**Secure** - zajišťujeme zabránění úniku informace, nějakému neautorizovanému použití případně kompromitování nějakých zdrojů

**Identifikace** - například otisk prstu. Na základně nějakých rysů se snažíme určit identitu z množiny identit.

**Authentication** - ujišťujeme se, že aktér je identifikován. Tedy máme jistotu, že ten s tím komunikujeme je přesně ten, který si myslíme. Je to tedy kombinace identifikace a poté důkazu. Třeba heslo je nějaký důkaz.

**Authorization** - řešíme, jestli je oprávněn vykonávat nějaké akce. Tedy prvně uživatele nebo entitu autentizujeme a poté autorizujeme na vykonávání nějakých akcí.

**Access Control** - je to nějaká kombinace autentizace a autorizace, kdy řídím přístupy k různým entitám v rámci systému. Jsou zde tedy zahrnuty role, práva a restrikce za účelem ochrany zdrojů.

**Certifikát** - jedná se o digitálně podepsanou zprávu, který obsahuje jméno vlastníka veřejného klíče a veřejný klíč samotný s jeho platností. Cílem je kryptograficky spojit veřejný klíč a jeho vlastníka.

**Certifikační autorita** - kdokoli si ji může zřídit, jedná se o nějakou autoritu, která certifikuje a zaručuje se za vydané certifikáty. Pro ČR to může být například *Česká pošta*, *eIdentity*, což jsou *Akreditované CA*, které prošli nějakou akreditací z hlediska *státních orgánů*.

**Zranitelnost** - nějaká slabina v naší aplikaci, systému, návrhu či implementaci, který by mohla porušit bezpečnost našeho softwaru.

**Hrozba** - nějaká okolnost nebo událost, která by vedla k poškození systému, případně úpravě údajů nebo odmítnutí služeb.

**Útok** - akt kdy naplním hrozbu. Tedy aktivně jsem využil nějaké hrozby a útočím nebo obcházím systém. Může být buď **aktivní**, kdy modifikuji například data, případně **pasivní**, kdy data získávám.

**Útok impersonací** - mohu odposlechnout z komunikace heslo, nebo jeho otisk a pak se vydávat za entitu při další komunikaci

**Klasifikace útočníků** - rozdělujeme na 3 třídy, podle úrovně ohrožení. Většinou mě zajímá jak jsou chytří, jaké mají dostupné vybavení a jestli znají systém na který útočí.
- Třída 1 - Chytří nezasvěcení útočníci (středně vybavení)
- Třída 2 - Zasvěcení insideři (specializace a zkušenosti)
- Třída 3 - Celé organizace s dobrou finančí podporou (týmy specialistů)

**PKI** - nějaká pomocná infrastruktura pro správu veřejných klíčů

**Obscurity** - většinou když se snažíme dělat bezpečnost na základě nějakých implementací a mechanismech, které jsou tajné. Obecně se ale považuje za slabou a měli bychom mít dobrou bezpečnost i za předpokladu, že útočník zná implementace a mechanismy.

**Firewall** - zařízení, které monitorují a kontrolují provoz na sítí a to jak příchozí tak odchozí

**SCAP** - (Security Content Automation Protocol) - jde o nějaký standard pro spravování hrozeb v rámci firmy, kdy si držím nějaké registry veřejně známých hrozeb, bezpečných konfigurací, případně i způsoby jak detekovat zranitelnosti


### Metody autentizace
- na základě **znalosti** (pin/heslo)
- na základě **vlastnictví** fyzického tokenu (klíč/čipová karta, řeší se i cena padělání)
- na základě **biometrie** (otisk prstu, který nikdo jiný nemá)
- na základě **fyzické/virtuální lokace** (rychlá změna fyzické lokace může být varovný signál, přihlášení z určitého počítače s certifikátem může stačit k autentizaci)

**Jednostranná autentizace**
Autentizaci můžeme vyžadovat jednostranně, tedy server může chtít, abych se autentizoval já jako uživatel, ale já vlastně nepotřebuji žádnou autentizaci serveru.

**Oboustranná autentizace**
Obě strany v procesu se vůči sobě autentizují. Může se to vyskytovat třeba v bankovních systémech. Potom zde vyvstává problém man-in-the-middle útoku.

Mohu teoreticky chtít kontinuálně během komunikace si ověřovat autentizaci, případně jen autentizace může proběhnout na základě výzvy, nebo klidně z iniciativy subjektu.

**Zero-knowledge protokoly** (protokoly s nulovým šířením znalostí)
Umožňují demonstraci znalosti tajemství, aniž bychom odhalili jakoukoliv informaci vedoucí k získání tajemství. Příkladem je například *Schnorrův protokol*. Mezi vlastnosti těchto protokolů patří:
- **úplnost/completeness** - poctivci vždy dosáhnou úspěšného výsledku
- **korektnost/soundness** - mizivá šance na úspěch nepoctivce

#### Autentizace tajnými informacemi
- cílem je autentizace uživatele
- v ideálním případě autorizovaným uživatelům nekomplikují fungování
- co nejvíce znesnadňují zneužití útočníky
- řeší se
    - ukládání
    - bezpečnost (kvalita/složitost) vs zapamatovatelnost
    - jak bude probíhat kontrola
    - postup v případě kompromitace (změna hesla)
- je nutné dodržet
    - informace by měla být opravdu tajná, neměla by být odvoditelná - ne rodné jméno
    - informace by měla být vybrána z velkého prostoru hodnot - čísla, písmena, symboly
    - informaci při autentizaci nepředáváme v čisté podobě (lze odposlechnout)
        - *šifrujeme*, v ideálním případě je šifrovaná celá komunikace
        - posíláme jen *haš* (lze sice přepoužívat, ale neodvodíme si původní heslo)
        - používáme *challenge-response*, pomocí kterého se tajné informace nešíří
- může jít o *pin*/*heslo*/*identifikaci* *obrazové informace*/*spojení bodů v určitém pořadí*

##### Hesla
- možnosti
    - **skupinová** (více uživatelů sdílí heslo) - mizivá bezpečnost
    - **unikátní** pro osobu, pomocí hesla se zároveň uživatel identifikuje
    - **kombinace** s uživatelským jménem, nemusí být unikátní
    - **jednorázová** 
	    - odděleným kanálem
	    - obvykle součástí 2FA, prokazujeme vlastnictví dalšího tokenu
- ukládají se jako **otisk** (pokud nepotřebujeme získat původní heslo)
	- ideálně včetně soli a pepře
	- šifrovaná (problém je, že teď musíme chránit místo hesla šifrovací klíč)
	- nikdy ne v otevřené formě
    - **salt** - náhodně vygenerovaná data, která se ukládají zároveň s otiskem a při hašování se přidávají k heslu, efektivně prodlužuje délku hesla a znemožní detekci stejných hesel dle shody otisků
    - **pepper** - data, která se při hashování ke vstupu, jsou však utajená narozdíl od soli a proto je neukládáme vedle haše
- *nucená expirace* hesla může mít za následek používání obecně slabších hesel
- dobrý kompromis mezi bezpečností a zapamatovatelností jsou hesla založená na frázích, nebo lokálním důvěryhodným správcem hesel 
- **nevýhody** - uživatel může být právě kritickým místem, může si dávat jednoduchá hesla, nebo si je někam zapisovat
- **výhody** - dobře se s nimi pracuje, uživatelé je znají, nepotřebujeme další HW

##### Útoky na hesla
- **cílený** (snažíme se zjistit heslo konkrétního uživatele)
- **plošný** (snažíme se zjistit heslo kohokoliv ze skupiny uživatelů)
- **online** (lze omezit počet pokusů)
- **offline** (kdy jsme se zmocnili souboru s haši/šifrovanými daty)
- **odpozorování** (vizuálně, phishing, nebo zachycení komunikace, sniffing)
- **slovníkový** (máme slovník často používaných hesel)
- **hrubou silou**
- **zneužití mechanismu na obnovu hesla** (mnohdy snadnější, než prolomení hesla)
- **analýza zdrojového kódu** nebo souborů verzovacího systému (často tam hesla nechávají vývojáři)
- použití **iniciálního hesla z manuálu** (e.g. často u routerů)
- krádež databáze/databáze, získání obsahu paměti/cache
- použití **rainbow tables** (přepočítané hodnoty a jejich haše)

**Jednorázová hesla**
- buď náhodně generovaná a zaslaná separátním (multifactor authentication)
- nebo **(Lamportův) řetězec haší**
    - na začátku se lokálně uloží heslo, který se 1000x zahashuje, výsledek dá serveru
    - při každé autentizaci uživatel pošle předchozí hash (číslo 999, 998...)
    - server prožene předaný hash 1x hash funkcí a porovná s posledním uloženým otiskem
    - pokud výsledek sedí, uloží si předaný hash jako poslední uložený
    - považuje uživatele za autentizovaného
    - útočník nemůže použít odposlechnutý hash, protože potřebuje předchozí hodnotu
- nebo přístroj (autentizační kalkulátor)
	- generující náhodná hesla na základě času
	- princip generování je znám službě, která autentizuje
	- je nutná synchronizace hodin
	- případně má autentizační kalkulátor klávesnici pro challenge-response

#### PINy
- obvykle velmi krátké -> omezujeme počet pokusů
- většinou používané s fyzickým předmětem
- někdy lze, ale mnohdy nelze měnit na přání zákazníka

#### Autentizační tokeny
- je to autentizace tím, že uživatel něco má
- mají nějaké fyzické vlastnosti a většinou obsahují nějaké tajné informace
- některé jsou schopné provádět nějaké kryptografické operace, ty symetrické jsou většinou v pohodě, na ty asymetrické kvůli náročnosti potřebujeme nějaký koprocesor
- druhy zabezpečení tokenů
	- **Fyzická bezpečnost** - nějaký fyzická překážka za účelem ztížit fyzický přístup
	- **Odolnost narušení** - vlastnost systému, který je chráněná proti modifikaci
	- **Detekce narušení** - automatická detekce pokusu o narušení
	- **Zjistitelnost narušení** - pokud je narušený token tak se to zanechá stopy
	- **Odpověď na narušení** - automatický reakce pokud je detekován pokus o narušení
- **výhody** - rychle vím, že jsem je ztratil, nedají se jednoduše zkopírovat a mohou samy o sobě přenášet nebo zpracovávat nějaké informace
- **nevýhody** - bez tokenu nerozeznám uživatele, musí být složitý a obtížně kopírovatelný a může přestat fungovat, případně potřebuji nějakou osobu, který ho umí používat

Útoky na tokeny
- **fyzické** - máme kartu u sebe a jdeme ji rozebrat
	- *invazivní útoky*, kdy poškodíme trvale token - preparace, čtení paměti, analýza návrhu
	- *semi-invazivní*, čip není trvale poškozen - ozařování, měření apod.
- **logické** - nevyžadují nějakou znalost struktury karty
	- *monitorování* - časová a výkonnostní analýza
	- *indukce chyb během činnost*
	- *útoky na API tokenu*

#### Autentizace pomocí symetrické kryptografie

Jak ověřit, že komunikuju s tím, kdo se mnou sdílí klíč? Mám 3 přístupy:
- použití **časového razítka**
- použití **náhodného čísla**
- použití **hashovací funkce** s klíčem *MAC*

Do zpráv je možné přidat identitu challengera, abychom předešli man in the middle útokům.

**Časové razítko**
- jednoduché, dá se napadnou rychlým zopakováním, případně změnou hodin
	- $A → B: E_K(t_A,B)$
- je to jednoduché, pro oboustrannou jen zopakuji

**Náhodným číslem**
- používám náhodné čísla, trochu horší na útoky
- mou podvrhnout generátor náhodných čísel, případně čekat na zopakování výzvy
	- $A ← B: r_B$
	- $A → B: E_K(r_B,B)$
- případně jde také modifikovat na oboustrannou
	- $A ← B: r_B$
	-  $A → B: E_K(r_A,r_B,B)$
	-  $A ← B: E_K(r_B,r_A)$

**Použití hashování s klíčem**
- předpokládá se nějaké použití MAC a klíče, který už A a B sdílí mezi sebou
	- $A ← B: r_B$
	- $A → B: r_A, h_K(r_A,r_B,B)$
	- $A ← B: h_K(r_B,r_A,A)$


#### Autentizace pomocí asymetrické kryptografie

Velmi podobně jako u symetrické, ale používám veřejné a privátní klíče. Tedy opět zde jsou varianty s *náhodným číslem* nebo *časovým razítkem*.

**Časové razítko**
- A vezme časové razítko a šifruji ho privátním klíčem
- B si rozšifruje pomocí veřejného klíče a podívá se zda jsou údaje pravdivé
	- $A → B: cert_A, t_A, B, S_A(t_A,B)$

**Náhodné číslo**
- pro jednostrannou autentizaci
	- $A ← B: r_B$
	- $A → B: cert_A, r_A,B, S_A(r_A,r_B,B)$
- pro oboustrannou autentizaci
	- $A ← B: r_B$
	- $A → B: cert_A, r_A,B, S_A(r_A,r_B,B)$
	- $A ← B: cert_B,A, S_B(r_B,r_A,A)$

#### Protokoly pro správu klíčů

Chci nějak ustanovit klíče pro symetrickou komunikaci, beru v úvahu například kolik stran se účastní procesu, tedy za máme nějakou 3 stranu, která něco řeší za nás, případně zda je to jen mezi dvěma entitami.

U protokolu nás zajímá hlavně **ustanovení klíče**, **přeposlání klíče**, případně **aktualizace klíče**. Také rovnou během procesu můžeme strany autentizovat.

**Aktualizace klíče**
- chceme nový klíč, ale máme pořád starý, tak ho použijeme a šifrujeme
- nový klíč lze předat zašifrovaný
- lze opatřit časovým razítkem, nebo spojit s náhodným číslem od parťáka
- díky tomu předejdeme budoucímu útoku přehráním
- opět můžeme buď přes časové razítko:
	- $A → B: E_K(r_A,t_A,B)$
- nebo můžeme přes náhodnou výzvu
	- $A ← B: n_B$
	- $A → B: E_K(r_A,n_B,B)$

**Diffie-Hellman protokol**
- spolu s kámošem se dohodneme na společném základu (malé prvočíslo `g` a velké číslo `n`)
- každý přidáme svou tajnou ingredienci, já `a`, kámoš `b`
- musí platit, že $1 <= a, b <= n$ 
- poté provedeme operace $x_a = g^a\ mod\ n$ a $x_b = g^b\ mod\ n$
- výsledek si vyměníme
- poté provedeme operace $K = (x_a)^b\ mod\ n$ a $K = (x_b)^a\ mod\ n$
- využijeme ekvivalence a kongruence modulo

**AKEP2 (Authentication Key Exchange)**
- používá se přenost klíče odvozením
-  $A → B: r_A$
-  $A ← B: (B,A,r_A,r_B), h_K(B,A,r_A,r_B)$
-  $A → B: (A,r_B), h_K(A,r_B)$
-  Nový klíč $W=h´_{K´}(r_B)$

**Shamirův protokol**
- Vyžaduje komutativní šifru a oba sdílíme nějaký svůj klíč $K_A$ a $K_B$
	- $A → B: E_{K_A}(X)$
	- $A ← B: E_{K_B}(E_{K_A}(X))$
	- $A → B: E_{K_B}(X)$
- na konci tohoto protokolu tak sdílíme oba údaj X, ale potřebovali jsme na to 3 zprávy

**Kerberos**
- kerberos používá symetrickou kryptografii a funguje jako centrální ověřená autorita
- ostatní entity ji využívají pro ustanovení klíčů pro symetrickou kryptografii
- cílem je vytvořit klíč mezi A a B
- počítá se s tím, že klíče pro komunikace s T již existují
- L – doba platnosti („lifetime“)
- Def.: $ticket_B = E_{K_{BT}}(k,A,L), auth = E_k(A, T_A)$
	- $A → T: A,B,n_A$
	- $A ← T: ticket_B, E_{K_{AT}}(k, n_A, L, B)$
	- $A → B: ticket_B, auth$
	- $A ← B: E_k(T_A)$

**Asymetrický přenost klíče**
- Opět zde využíváme nějaké techniky asymetrické kryptografie
- v rámci šifrování podepsaného klíče tak mohu přiložit i nějaké časové razítko
	-  $A → B: P_B(S_A(B, k , t_A))$
- šifrování a podpis mohu také rozdělit, kdyby z podpisu nešli získat data
- typicky X.509 funguje jako
	- $D_A = (t_A, r_A, B, P_B(k_1))$
	- $D_B = (t_B, r_B, A, P_A(k_2))$
	- $A → B: cert_A, D_A, S_A(D_A)$
	- $A ← B: certB, D_B, S_B(D_B)$

**Zero knowledge protokoly**
- příkladem je Fiat-Shamir
- umožňuje nám to pracovat s nějakým tajemstvím
- umím prokázat, že ho znám, aniž bych tajemství vyzradil
- většinou čím vícekrát provedu, tím menší šance, že jsem podváděl
- pracuje trochu podobně jako RSA


##### Symetrické šifrování
- dobrý pro dlouhé zprávy
- rozděluji na proudové šifry (RC4) a blokové šifry (DES, 3DES, AES)
- blokové šifry většinou pracují na nějakém principu, kdy buď šifruji každý blok zvlášť (ECB), což není moc dobré, místo toho spíše chci buď kombinovat nějak předchozí blok (CBC), případně mít nějaký nonce, který inkrementuji a přidávám ke zprávám.

##### Asymetrická kryptografie
- máme dva klíče, jeden na šifrování, jeden na dešifrování
- většinou o dost více výpočetně náročné, takže šifrovat takhle velká data je blbost

##### Hashovací funkce
- převádíme libovolně velký vstup deterministicky na nějaký výstup fixní délky
- příklad jsou MD5(prolomena), SHA-256 (aktuální), Bcrypt případně Argon2 na hesla
- vlastnosti:
	- jednosměrnost
	- bezkoliznost rozlišujeme na slabou a silnou
- používáme hodně v podepisování

##### Výpočetní bezpečnost
- například RSA je založeno na faktorizaci velkých čísel
- pokud máme čísla n, které je velké v tisících bitech tak je nesnadné najít v rozumném čase nějaká prvočísla, ze kterých se skládá

##### MAC (Message authentication code)
- slouží k zajištění integrity a ne důvěrnosti dat
- sdílíme si tajný klíč k
- je to vlastně hashování s klíčem


### Řízení přístupu

Bezpečnostní mechanismus pro umožnění uživatelům vykonávat v systému nějaké akce. Jsou vázána k subjektu (uživatel nebo proces) a k objektu (databáze, soubor).

**Pojmy**
- *vlastník dat* - zodpovědný za určitá data
- *správce dat* - zodpovědný za bezpečnost určitých dat
- *uživatel* - může vykonávat operace s daty dle svých přístupových práv

**Základní typy práv** 
Obvykle specifikovatelná pro každou jednotku dat, tedy soubory, nebo i buňky v tabulkách.
- **read** (může i kopírovat a zrádný člen skupiny tak udělat veřejnou kopii)
- **write** (modifikace)
- **execute** (spouštění programu)
- pokročilejší příznaky mohou být třeba append only soubor

**Politiky řízení přístupu**
- **volitelný přístup** (decentralizovaná správa řízení) 
	- vlastník dat/objektu rozhoduje
	- malá režie, o správu se starají vlastníci/správci
	- špatné vynucování/koordinace celosystémových pravidel
	- možnost problému, kdy někdo v souborovém systému tajný soubor zkopíruje a zveřejní ho omylem všem
- **povinný** (přístup/centralizovaná správa řízení)
	- o přístupu rozhoduje systémová politika
- **povinný a volitelný přístup lze kombinovat**
	- systém je pak flexibilnější, ale stále zaručuje bezpečnost u kritických objektů

**Access Control List (ACL)**
- ukládáme si nějakou matici přístupových práv
- matice je většinou řídká, proto ukládáme jen neprázné buňky
- každý objekt tedy má nějaký seznam přístupových práv, pro konkrétní skupiny
- *výhody*: mohu modifikovat a měnit práva na určité skupině
- *nevýhody*: obtížná správa a neefektivní kontrola, pokud uživatel změní pracovní pozici, špatně se mi kontroluje kam všude měl přístup

**Matice přístupových práv**
Práva bychom mohli ukládat i ve velké matici, kde máme jednu osu soubory, druhou uživatelé a přiřazovat práva, nicméně by to bylo hodně nepřehledné.

**Přístupová práva v operačních systémech**
Přístupy můžeme také omezovat *časem*, *místem* případně *typem služby*. Také se dá omezovat na základě role, skupiny případně hesla.

V **unix** systémech bývá obvykle nějaký **superadmin/root**, který má přístup ke všemu. Dobrou politikou je snaha o omezení práv tohoto uživatele a vytvoření skupin pro příslušné skupiny dat/objektů - pokud se hacker dostane k rootu, je vše v pytli.

**Moderní unixové** systémy (obvykle komerční verze) nabízí jemnější granularitu nad skupinami, právy uživatelů a podobně. Můžeme tedy mít právě append only soubory a podobně.

**Windows** nabízí mnohem jemnější práci s právy a umožňuje i dědičnost. Většinou ale stejně všechno podělá uživatel, protože se přihlásí jako Admin aby něco nainstaloval a až do konce session jako admin zůstane.

**SAML (Security Assertion Markup Language)**
- standard pro výměnu autentizačních a autorizačních dat v XML
- většinou se používal přes web
- typicky se díky němu řešilo SSO

**Good practices řízení přístupu**
- *separace oprávnění* 
	- potvrzení důležité operace vícero aktéry
	- příkladem jsou nějaké velké bankovní transakce
- *princip nejmenších privilegií*
	- každý má přístup jen k tomu, co nutně potřebuje a k ničemu jinému
- *defaultní akce je zamítnutí* 
	- by default tak všechno chci zakázat a explicitně povolovat
	- typicky třeba firewall

**Multi-level systems (MLS)**
- do systému mají přístup všichni uživatelé
- data jim zobrazujeme/umožňujeme používat objekty dle jejich úrovně
- nižším úrovním skrýváme to, co mohou vidět vyšší úrovně
- role jsou hierarchické, mohou být jako *Top secret*, *Secret*, *Classified*, *Unclassified*

**Role-based access control (RBAC)**
- uživatelům přiřazujeme role (i vícero)
- na role navazujeme oprávnění, které mohou být i docela dost jemné
- role jsou v každém systému jiné
- e.g. role v databázích


---

## Biometrické metody autentizace, jejich dopady a problémy.

> Automatizované metody identifikace nebo ověření identity na základě měřitelných fyziologických nebo behaviorálních (založených na chování) vlastností člověka

Systémy na základě fyziologických vlastností jsou většinou lepší, protože jsou opakovatelné a nepodléhají nějakým vnějším vlivům. Hlavní rozdíl při autentizaci a identifikaci je ten, že systém nám neřekne ano je to tento člověk, ale řekne nám, že s nějakou pravděpodobností je to tento člověk.

Výhoda je, že zároveň identifikujeme a autentizujeme. Nemůžeme ztratit ani zapomenout a většinou rychlé a docela dobré výsledky. Většinou musíme řešit, co když mají uživatelé nějaké postižení, případně jak nastavit FAR a FRR abychom měli bezpečnost a uživatelé byli spokojení.

Testování živosti většinou nese vyšší náklady a nemusí být nikdy na 100%.

Biometrická data je nejdříve třeba nasnímat (včetně kontroly kvality, extrakce charakteristik) a uložit, potom je možné je používat k autentizaci/identifikaci (pomocí srovnání charakteristik).

Na rozdíl od ostatních metod autentizace **musíme řešit variabilitu** uložených dat a nasnímaného vzorku, data nejsou nikdy zcela identická.
- velmi často závisí na
	- měřících podmínkách
	- samotném zařízení
	- stavu měřeného
	- schopnosti/motivace měřeného provést si měření správně
- 100% shoda může znamenat problém - útočník se dostal k uloženým datům
- řeší se **false acceptance** (bezpečnostní problém) a **false rejection** (nepohodlí uživatelů)
	![600](img/20230613154105.png)

Biometriky jsou vhodné jako doplňkové metody, pro přístup k tajnému klíči, autentizaci uživatele (ne dat/počítače)... ne pro použití jako samotný klíč.

Fáze při biometrické autentizaci:
- **Registrace vzorku** - získání biometrických dat, extrakce charakteristik, uložení vzorku
- **Autentizace a identifikace** - získání, extrakce charakteristik, srovnání, rozhodnutí

Rozdělení biometriky
- **fyziologické charakteristiky (statické)** - otisk prstu, geometrike ruky
- **behaviorální charakteristiky (dynamické)** - hlas, podpis, chůze

Charakteristiky biometrie
- **genotypické** - založené na genetice a neměnné (DNA, duhovka)
- **fenotypické** - ovlivněné vývojem - otisk prstu

**Otisk prstů**
- jedna z nejstarších metod
- snímače máme optické, kapacitní, ultrazvukové a tepelné
- vytváříme z otisku mapu markantů
- můžeme brát i geometrii ruky, ale ta není tak unikátní

**Dynamika podpisu**
- máme zařízení, které detekuje dynamiku psaní
- musíme mít specializovaný tablet

 **Oční duhovka**
- černobíle snímání, většinou velmi přesné

**Rozeznání obličeje**
- docela výpočetně náročné
- obličej se v čase mění a můžeme mít brýle, náušnice, pozadí a podobně

**Problémy biometrické autentizace**
- nikdy nejsou zcela bezchybné
- Failure to enroll - není možné získat biometrickou charakteristiku při registraci (e.g. někdo nemá prst, který chceme snímat)
- Failure to acquire/capture - není možné získat charakteristiku při autentizaci
- **False positive identification** - přijali jsme chybně (bezpečnostní riziko)
- **False negative identification** - zamítli jsme chybně (naštvanější uživatelé)
- **fenotypické charakteristiky** (e.g. geometrie ruky) se mohou v čase měnit
- **genotypické charakteristiky** (e.g. dna) je zase obtížné rychle vyhodnotit
- měření není dokonalé (prostředí, jiný měřák, nezkušenost/nespolupráce měřeného)
- měření může být nepříjemné
- metody mají různé charakteristiky rychlosti, spolehlivosti, příjemnosti, výpočetní náročnosti, míru vlivu prostředí...
- musíme řešit živost - jde skutečně o člověka, nebo o umělý prst? je daný člověk na živu?
- charakteristika může být použita ve více systémech, zveřejnění nesmí ohrozit soukromí
- biometriky nejsou tajné
- ochrana soukromí, legislativní omezení
- kvůli nepřesnostem/možným změnám/netajnosti není vhodné z biometrik generovat kvalitní kryptografické klíče

**Kontinuální autentizace** - subjekt kontinuálně sledujeme a snažíme se detekovat možné odchylky v chování, které by naznačovaly, že se jedná o útočníka, e.g. dynamika psaní na klávesnici

Forenzní systémy pro biometrickou autentizaci jsou přesnější, spolehlivější, dražší, mohou být pomalejší, vyžadují odborníky.


---

## Elektronický podpis a jeho použití.

Zajišťuje **autentizaci** (že zpráva pochází od daného autora) a **integritu** (že zprávu nikdo nepozměnil) **podepisovaných dat**. Nezajišťuje důvěrnost dat. Měl by obsahovat i datum/čas. 

Algoritmy jsou například **RSA, DSA**


**Průběh podepisování**
- vytvořím asymetrické klíče (veřejný, soukromý)
- veřejný klíč zaregistruju/vystavím, aby mohl být později použit k ověření
- pro každý podepisovaný dokument vytvořím hash (e.g. pomocí SHA-2)
- šifruju haš soukromým klíčem
- podepsané dokumenty je možné ověřit pomocí mého vystaveného veřejného klíče

Pozor, je rozdíl mezi elektronickým podpisem (podepsání na iPadu) a zarušeným elektronickým podpisem (jednoznačně přiřazený kryptograficky k entitě).

**Certifikát**
- spojuje veřejný klíč a informace o subjektu, který veřejný klíč poskytuje
- jde tedy o nějaké potvrzení identity
- certifikační autorita podepíše veřejný klíč a informace svým soukromým klíčem
    - vytváří se řetězec důvěry - pokud věříš autoritě, můžeš věřit i mně
- **certifikační autorita** 
    - zajišťuje, že daný subjekt opravdu vlastní soukromý klíč
    - autentizuje subjekt vystavující veřejný klíč (zajišťuje, že daný subjekt je tím, co tvrdí) 
    - potvrzuje platnost veřejného klíče daného subjektu svým podpisem
- bývá časově omezen

**Použití podpisu**
- autentizace dat (podpis zprávy, který si mohou ostatní ověřit)
- autentizace počítačů/tokenů díky mechanismu **výzva-odpověď (challenge-response)**
    - jestli jsi opravdu vlastníkem soukromého klíče, tak podepiš tato vzorová data
- autentizace osob pomocí schopnosti spustit aplikaci na počítači/tokenu
- digitální podpis neprovádí člověk, ale počítač
- pokud potřebujeme šifrovat, nejprve podepisujeme, potom šifrujeme

**Soukromý klíč je potřeba chránit**
- v případě vyzrazení se za nás může někdo vydávat.
- soukromý klíč bývá ideálně šifrován/blokován
- potřebujeme tedy zadání přístupového hesla/pinu

**Veřejný klíč musí mít zajištěnou integritu**
- nesprávný veřejný klíč, dá nesprávné výsledky
- vystavuje se certifikát, který spojuje klíč s naší identitou
- pomáháme si podpisu certifikační autoritou

**Infrastruktura pro správu veřejných klíčů (PKI)**
- **Certifikační autorita** 
	- poskytuje certifikační služby, vydává certifikáty a případně je zneplatňuje
- **Registrační autorita** 
	- registruje žadatele o vydání certifikátu, prověřuje jejich identitu (může být zároveň CA)
- **Adresářová služba** 
	- uchovává a distribuuje platné klíče (a seznam zneplatněných certifikátů)
- certifikační autoritu obvykle certifikuje nadřazená certifikační autorita
- tímto vším tvoříme řetězec důvěry

**Vystavení certifikátu**
- generování klíčových dat (e.g. key-pair pro asymetrickou kryptografii)
- doložení a ověření identifikačních informací (e.g. pro web předáme údaje o identitě a instalujeme *Certbot*, nebo nahrajeme určitý soubor, abychom dokázali, že máme nad serverem kontrolu)
- vydání certifikátu žadateli (včetně zveřejnění v adresářové službě) 

## Autentizace strojů a aplikací.

**Autentizace počítačů**
- na základě adresy (IP, MAC fyzická adresa)
    - MAC fyzická adresa 
	    - svázáním portu switch přepínače s určitou MAC adresou
	    - svázání IP adresy s MAC adresou
    - IP - řízení přístupu k webovým službám na základě IP adresy
    - problém může být, že MAC i IP adresy lze změnit
    - MAC ani IP nejsou tajné, je možné uvést cizí IP adresu
    - IP adresu mohu cíleně podvrhnout (Spoofing)
- na základě tajné informace (symetrická/asymetrická kryptografie/hesla)
    - heslo/tajný symetrický klíč/soukromý asymetrický klíč
    - hesla buď uložíme otevřené, nicméně pak se k nim každý dostane
    - můžeme je šifrovat a při startu počítače heslo zadat, pak záleží na kvalitě hesla
    - dá se použít taky HashiCorp Vault (secret manager)

**TLS/SSL** - protokol vyšší úrovně
- SSL je předchůdce TLS
- autentizuje strany pomocí certifikátu a challenge-response
- defaultně povinná autentizace pro server, volitelná pro klienta
- zajišťuje integritu a autenticitu dat
	- pomocí Message Authentication Code, MAC
	- k datům přidáme tajný klíč a celé to hašujeme
	- na rozdíl od podpisu neprovádíme šifrování otisku dat tajným klíčem
- zajišťuje důvěrnost
- nejprve proběhne iniciální handshake (autentizace pomocí asymetrické kryptografie)
- následně se stanoví symetrický kryptografický klíč, kterým je šifrována celá komunikace.
- je mezi TCP a aplikací, TLS nevidí do přenášených dat

**IPSec** - na síťové vrstvě, přidán do IPv4, v IPv6 už je defaultně
- pro každý IP datagram
    - zajišťuje autentizaci odesilatele
    - zajišťuje integritu dat (nezměněná data)
    - zajišťuje důvěrnost dat (symetrický šifrovací klíč známý oběma stranám)
    - zajišťuje ochranu před útokem přehráním (MAC v kombinaci se sekvenčním číslem)
- umožňuje transportní (end to end, nepodporuje NAT), nebo tunelovací režim (celý datagram beru jako data, přilepím tomu novou IP hlavičku)

**Secure Shell Host (SSH)**
- slouží k vzdálenému přihlášení k serveru
- můžeme také do `.rhosts` dát ověřené IP adresy, ale pozor na spoofing
- oproti telnetu je komunikace šifrovaná (symetrickou šifrou, klíč se stanoví po handshake)
- probíhá autentizace serveru i klienta (`ssh-keygen`, tak to bylo ono)
- používá se pro to třeba RSA, DSA (asymetrická kryptografie)
- mohu použít ssh-agent, kdy zadám heslo jednou a on si ho pamatuje

**Security Assertion Markup Language (SAML)**
- standard pro popis a výměnu autentizačních dat
- založený na XML, používaný pro webové aplikace
- umožňuje oddělení poskytovatele identity a poskytovatele služeb
- jinými slovy umožňuje Single Sign-On (SSO)
- SAML token obsahuje
    - subject (kdo je držitel tokenu, e.g. user id)
    - auth statement (způsob & čas provedené autentizace)
    - příslušnost ke skupinám, rolím, povolené operace

## Zásady a principy bezpečného kódu.

**Základní problémy, proč máme narušenou bezpečnost kódu**
- *Nevzdělaní vývojáři* - buď nezkušenost, nebo neznalost problémů
- *Legacy code* - starý kód, který je složitý a moc lidí mu nerozumí
- *Chybějící specifikace* - nejsou analýzy, nevíme jestli byla implementace úspěšná
- *Spoléhání se na 3rd party* - neudržované knihovny, které musím forknout aby je opravil
- *Ekonomika bezpečnost* - vím, že mám problém, ale nemám peníze na opravu
- *Problémy lidí* - dokud se na problém nepodívám, problém není

**Co to znamená bezpečný software**
- *používáme obecně dobrý vývoj a dodržujeme bezpečností praktiky*
	- vzděláváme se, testujeme, děláme code review
- *sémantický deployment, údržba a odstraňování chyb*
	- monitoring, fixy, detekce chyb na knihovnách 3 stran
- *použitelnost*
	- snažíme se jak pro uživatele tak pro developery
	- aplikace, případně API by mělo být srozumitelné, aby se nedalo použít nesprávně
- *automated and manual review*
	- continuous integration, penetrační testování, code reviews
- *používání nástrojů a řešení specifických problémů jazyku*
	- u C buffer overflow, u Java code injection
- *kryptografická primitiva*
	- použití knihoven a ne si věci implementovat sím

**Defensive programming** 
- kód by měl být psán tak, aby byl systém připraven pracovat v prostředí, kde mohou nastávat (nechtěné) chyby, dbáme tedy hodně na:
    - *ověřování vstupních dat*
    - *ošetření i těch situací, které* *přece nemůžou nastat*
    - *příprava systému na jednoduché testování* (dekompozice, závislosti na abstrakcích) a diagnostiku chyb (logování, explicitní ošetření chyb)
    - *logování událostí* (abychom dokázali detekovat, co se v systému dělo)

**Pro zajištění bezpečnosti kódy lze postupovat různými způsoby:**
- *použití bezpečnějšího jazyka*
	- některé chyby neumožňuje, nebo je aspoň dělá těžší na provedení e.g. Rust
    - případně použití striktnějšího modu překladače
- *spouštění aplikace v sandbox prostředí*
	- třeba kontejneru, aby případný útočník nezískal kontrolu nad celým strojem
	- můžeme sledovat co aplikace dělá a učit se z toho
- *důkladné testování statická a dynamická analýza, code reviews*
- *pro kritické věci (kryptografie) je dobré použít osvědčené knihovny*
- *závislosti (knihovny)*
	- je dobré pravidelně sledovat ohledně výskytu bezpečnostních slabin 
	- e.g. automatizovaně pomocí *dependabot*
- *použití bezpečných verzí funkcí* (u C/C++ třeba strncpy místo strcpy)
	- nepoužívání funkcí označených *obsolete*
- *kontinuální integrace*
	- automatizované spouštění testů, statické (případně i dynamické) analýzy
- *je klíčové dobře znát použitý jazyk a jeho typické slabiny*
- *pokud si můžeme vybrat, je lepší používat whitelisting než blacklisting (deny by default)*

Při vývoji kódu je dobré zajistit, aby byly chybové stavy nereprezentovatelné (třeba pomocí builder patternu a různých builder tříd).

## Typické bezpečnostní chyby na úrovni kódu, souběžnost, ošetření vstupů.

Seznamy běžných chyb
- **Common Weakness Enumeration (CWE)** 
	- obecně časté bezpečnostní chyby v programovacích jazycích
- **OWASP top 10** 
	- nejčastější bezpečnostní díry ve webových aplikacích 
	- OWASP mají i jiné zajímavé projekty zaměřené na bezpečnost

Je dobré se dívat i na časté chyby pro daný jazyk. Například:
- PHP má velmi často Cross Site Scripting
- Java CRLF Injection
- Pyton - kryptografické problémy

##### Typické chyby
- **Injection** 
	- vložení vlastních instrukcí do dat
	- jsou bez dostatečné kontroly vyhodnocována interpretem
    - e.g. SQL injection
- **Race condition** 
	- simultánní zápisy (nebo zápis a čtení) do sdílené paměti (ze stejného paměťového místa, ale i třeba ze dvou různých logicky závislých míst) 
	- řešením je sekvenční zpracování nebo zamykání
- **Buffer overflow** 
	- v paměti máme pole a za ním data
	- pokud provedeme zápis do pole a zapisovaná data jsou delší než pole (a neohlídáme si délku), mohou nám zapisovaná data přepsat i data za polem
	- ovlivňuje hlavně C/C++
- **Buffer overread** 
	- jako buffer overflow, ale se čtením - jsme schopní číst i data za polem
- **Stack exhaustion** 
	- vyplýtvání místa na zásobníku, typicky kvůli velké rekurzi
- **Heap exhaustion** 
	- vyplýtvání místa na haldě, není možné alokovat další paměť
	- může být způsobeno memory leaky, nebo velkou paměťovou náročností programu
- **Type overflow** 
	- přetečení hodnoty
	- například int overflow; způsobeno `i64::MAX + 1`, výsledek je 0
	- kontrola hodnot, nebo speciální operace (tedy třeba hodí výjimku při přetečení)
- **Off-by-one error**
- použití neinicializované paměti (po malloc), nebo uvolněného ukazatele (po free)

Můžeme poté také rozlišovat jako **side-channel attacks**, kdy se nesnažím přímo nějak prolomit kryptografii, ale třeba u tokenů se snažím dělat nějakou analýzu spotřeby proudu, pokoušet se ukrást cache, kde mohou být uložená nějaké klíče a citlivá data, můžu také zkoušet nějak skenovat HW a podobně. Jde o to, že spíše využíváme nějaké side-effekty chování systému než to, že jdeme na přímo po kryptografii.

**Souběžnost** a.k.a. race condition
- špatné načasování operací (nebo jejich pořadí) způsobí nečekané stavy systému
- máme současně běžící programy
- každý chce přečíst hodnotu ze sdílené paměti a zvýšit ji o 1. 
    ```
    Procesy A a B chtějí inkremetovat sdílený čítač, každý o 1
    A čte hodnotu 5
    B čte hodnotu 5
    A inkrementuje načtenou hodnotu 5+1=6
    B inkrementuje načtenou hodnotu 5+1=6
    A zapíše 6
    B zapíše 6
    Oba procesy inkrementovaly čítač, který se reálně zvedl pouze o 1
    ```
- řešením je vyznačení problematické části jako kritické sekce
- pro kritickou sekci se musí vynutit přístupová pravidla písařů a čtenářů:
    - pokud existuje písař, musí být jediný a nesmí existovat žádní čtenáři
    - pokud neexistuje písař, může existovat libovolný počet čtenářů
- striktnějším řešením je uzamčení kritické sekce, aby k ním měl přístup vždy jen 1 proces
- pokud máme vícero kritických sekcí a používáme zámky
- u zamykání je třeba dávat pozor na uváznutí (deadlock)

Některé chyby bývají specifické pro určité programovací jazyky (buffer overflow pro C/C++)

Některé útoky co je dobré znát:
- *DoS útok*
	- snažíme se pod náporem dotazů zahltit služby
	- ty jsou následně odstavené a nezvládají další dotazy
- *Code Injection*
	- podaří se útočníkovi v cílovém systému rozjet nějaký kus kódu
	- většinou k tomu dojde, když z uživatelského vstupu nějak neopatrně tvoříme kus kódu
	- dá se řešit přes nějaké prepared statements a podobně
- *SQL injection*
	- speciální případ Code Injection, kdy nějak modifikujeme databázi
	- většinou díky vstupu
- *Man-in-the-middle*
	- vstupuji mezi komunikaci dvou zařízení
	- může být buď pasivní, že pouze naslouchám
	- může být aktivní, kdy nějak modifikuji posílané zprávy
- *Cross-Site Scripting (XSS)*
	- dovolíme například přes komentář vložit nějaký skript tag
	- pokud se uloží a vidí ho ostatní v komentářích tak máme kontrolu na jiným uživatelem
- *Cross-Site Request Forgery (CSRF)*
	- většinou, přes automaticky odeslaný odeslaný formulář na stránce
	- provolávám akce na cílovém serveru
	- nefunguje CORS, protože je to formulář a cookie se přiloží sama

**Zero-day exploit** 
- využití bezpečnostní chyby, která ještě není obecně známá/neexistuje proti ní obrana

Zdrojový kód se může od výsledné binárky značně lišit (optimalizace, debug-only sekce kódu). Při vývoji se hodí mít dodatečné informace pro debugging (umožňující třeba detailní stack trace). V release verzi však tyto informace mohou pomoct útočníkovi.

Pro explicitní řízení přechodů mezi stavy programu lze použít **automata-based modelling**, kdy stavy a přechody programu modelujeme jako stavový automat; pomocí dat reprezentujeme stav a na základě něj můžeme explicitně definovat validní přechody (e.g. switch/match statement, případně transformace objektů (pokročilejší builder pattern)). Minimalizujeme tak místa, ve kterých se mění stav, díky čemuž je kód přehlednější a bezpečnější.

##### Ošetření vstupů
Pro **ošetřování vstupů** je vhodný použít fail-fast přístup. Jakmile zjistíme, že pracujeme s chybnými daty, měli bychom přerušit standardní průchod funkcí a zpracovat chybu. 

Koncovému uživateli sdělujeme jen nutné minimum nutné pro identifikaci důvodu chyby (nadbytečné informace, jako třeba názvy tříd, by mu mohly odhalit interní strukturu aplikace, což by mohlo být bezpečnostní riziko).

Obecné rady
- pro jednodušší ověřování je vhodné omezit počet validních vstupů (e.g. jen čísla)
- vstupní data mapujeme na interní data (e.g. používáme enumy)
- maximální délku vstupu je důležité brát v potaz zvlášť u zpracování souborů
- problém může dělat třeba UTF-8 řetězce, kde jeden znak může mít různou délku
- pro ošetření vstupů je navíc fajn používat validační knihovny (e.g. zod, clap) 
- **taint analysis** - průzkum co všechno v systému závisí na uživatelském vstupu je
- jednotky systému mohou používat [kontrakty](./dev_1_analyza_a_navrh.md#rozhraní-komponent-kontrakty-na-úrovni-rozhraní-ocl) (preconditions, postconditions, invariants) 
- pro kontrolu dostatečného ošetření vstupů je možné použít **fuzzing**
- důležité je samozřejmě nikdy nevěřit uživatelským vstupům

##### Chyby u souběžnost
- **race conditions**
	- máme více vstupujících vláken do kritické sekce
	- útočník buď může rozbít systém, případně obejít nějaké bezpečnostní kontroly
- **deadlocks, livelocks**
	- nekonečné čekání
	- většinou velmi zpomalíme systém, případně se rozbije a nechová se jak by měl
- **shared resource vulnerability**
	- většinou při paralelismu přistupujeme k databázím, souborů případně síti
	- pokud zde máme nějaké ne úplně dobré řízení přístupu, opět máme problémy
- **thread synchronization issue**
	- většinou můžeme odhalit nějaké chyby v zamykání, bariérách a podobně
	- vede to ke zničení dat, případně odepření služby když se nám podaří shodit systém


---

## Detekce bezpečnostních zranitelností, penetrační testování.

Pro detekci (nejen) bezpečnostních zranitelností je možné použít vícero přístupů. Typicky jich chceme co nejvíce, abychom měli co nejlepší bezpečnost našeho systému.
- statická analýza a dynamická analýza
- fuzzing
- penetrační testování a security review

Tady se dá rozdělit do skupin
-  Protection on the *source code level*
	- implicitní podpora v rámci jazyku
	- kontrolování vstupů, alternativy ke zranitelným funkcím, ošetření dat
- Protection by *extensive testing*
	- automatická detekce statickou nebo dynamickou analýzou
	- code reviews, testování bezpečnost
- Protection by *compiler*
	- máme flagy při kompilaci, které nás upozorní na chyby v implementaci
- Protection *by execution environment*
	- máme sandboxy, ve kterých se izolované spouští systémy
- Protection *by defence in depth*
	- vytvoříme z bodů výše nějaký systematický postup, případně životní cyklus
	- použijeme více věcí dohromady a kombinujeme

Například Microsoft má celý **Secure development lifecycle (SDL)**
- *trénují* lidí
- popisují si *požadavky* a *metriky* pro držení kvality
- modelují potenciální hrozby, používají *ověřené nástroje*, *statickou analýzu*
- verifikují program *dynamickou analýzou*, mají *fuzz testing*
- při release definují *Incident Response plan* (připravují se na chyby)

**Data Execution Prevention (DEP)** 
Prevencí code injection může být data execution prevention - paměť dělíme na datovou a spustitelnou, není možné spouštět kód z datové části. SQL injection (zprávy jsou obvykle interpretované) se řeší pomocí prepared statements, čímž efektivně dělíme části příkazu na datovou a příkazovou.

Prevencí změny návratové adresy funkce útočníkem (důsledek buffer overflow) je randomizace adres funkcí v kódu. Ta se provádí vždy když se načte proces do paměti.


**Statická analýza**
- analýza kódu programu, aniž by byl program spuštěn
- lze analyzovat zdrojový kód (jednodušší, je k tomu víc kontextu), ale i binárku
- lze aplikovat i na nedokončený kód
- lze využít i pro vynucení jednotného stylu kódu
- důležitou (ale špatně automatizovatelnou a škálovatelnou) variantou je code review
- lze využít automatizované nástroje, kterým stačí zdrojový kód 
	- e.g. cargo check, eslint, cargo clippy, pro vícero jazyků třeba sonarqube
	- většinou je potřeba dávat si na false positives a false negatives
- běžně bývá součástí CI - důraz na rychlost
- snadno odhalí i časté chyby jako ponechání hardcoded API klíče
- type checking - překladač, style checking - automatizované nástroje

**Dynamická analýza**
- program je spuštěn, poskytujeme různé vstupy
- je možné použít virtualizovaný procesor/interpret, můžeme sledovat paměť
- lze vynutit omezené prostředí (málo paměti, omezená práva)
- lze sledovat data a jejich změny v programu
- lze vložit logovací instrukce
- příkladem je třeba Valgrind
	- nahrazuje standardní alokátor a poskytuje vlastní
	- umožňuje mu sledovat dění v paměti
- můžeme v rámci Taint analýzy sledovat propagace vstupu uživatele

**Fuzzing** 
- dynamické testování
- program spouštíme s *náhodnými* generovanými vstupy a sledujeme výstupy
- vhodné pro blackbox
- většinou najdeme jen menší chyby
- vstupy mohou být zcela náhodné, v praxi chceme poskytnout několik vhodných vstupů (jako základ), které fuzzer modifikuje různými způsoby (zcela náhodně, nebo pomocí nějaké inteligentní strategie)
- klíčové je, aby vstupů bylo hodně a proces je možné snadno automatizovat a opakovat
- během fuzzingu sledujeme chování aplikace (zamrzla? běží bez chyby?)
- po skončení fuzzingu máme množinu problematických vstupů, které musíme vyřešit
- obvykle se takto najdou jen poměrně jednoduché chyby, nebo chyby validace

**Taint analýza** 
- data, které nějakým způsobem závisí na nedůvěrném vstupu, jsou označena
- pokud se označení dostane i ke kritickým částem kódu, vyskočí nám upozornění

**A stack canary**
Pro detekci buffer overflow lze pomocí překladače použít tzv. *canary* - data za každým polem. Pokud dojde k přetečení pole, bude canary přepsán, což je signál problému. Problém přetrvá, pokud útočník zná hodnotu canary. Alternativně (režijně náročnější) lze kontrolovat délku pole a zapisovaných dat.

**Management zranitelnost**
Jde o nějaký proces, kdy objevuji, analyzuji a zmírňuji dopady zranitelnosti. Často také sledování jejího stavu, prioritizace, opravy a ověřování.

**Detekce zranitelností**
Můžeme mít přímo aktivity, kdy je odhalujeme, tedy nějaký aktivní monitoring, hodnocení zranitelností a podobně. Můžeme také koukat na specifické známé exploity a nebo mít přímo nástroje, které skenují SW.

**Security review**
- provádí se top-down, bottom up (vhodnější při nejasné architektuře, ale náročnější na provedení) či hybridně
- začíná u architektury a dokumentace, snaha o detekci návrhových chyb, stanovují se možná rizika a zranitelnosti
- u kódu se sleduje, jak dobře implementuje architekturu (často existují rozdíly), hledají se možné zranitelnosti v high-level logice, pak i v samotném kódu
- hodnotí se dodržování bezpečnostních standardů
- prakticky se testuje zabezpečení (penetrační testování, DDoS útoky, statická analýza)
- sleduje se vliv nedůvěryhodných dat (taint analýza)
- lze analyzovat přímo kód (řádek po řádku, nebo podle pořadí volaných funkcí), případně si můžeme udělat seznam potenciálních slabin a na ty se zaměřit
- analyzuje se kontrola přístupu a správa oprávnění
- hodnotí se bezpečnostní opatření, monitoring
- hodnotí se ochrana dat, správa klíčů, šifrování
- výsledkem je zpráva popisující současný stav a doporučení do budoucna

**Analýza bezpečnostních útoků**
- *shromažďování informací o útoku* - logy, pakety, záznamy a podobně
- *identifikace a klasifikace* - technika, cíle útoku, vzory, charakteristiky
- *analýza příčiny* - hledání příčiny útoku, konfigurace, SW inženýrství
- *důsledková analýza* - dosah útoku, vyhodnocení ztráty a podobně
- *návrh opatření* - postup jak v budoucnu zamezit podobnému útoku

##### Penetrační testování
- je to metoda ujišťování se o bezpečnosti našeho systému
- cílem je najít bezpečností chyby s použitím stejných praktik a mechanismů jako útočník
- obecné penetrační testování je náročné obvykle je dobré si vytipovat slabá místa
- dá se také zaměřit útoky jen na některé části systému
- interně - týmem v rámci organizace
    - lze využít znalosti zdrojového kódu
    - vyžaduje udržování specializovaného odborného týmu
- externě - jinou, specializovanou společností 
    - nabízí pohled z venku, který může brát v potaz problémy, které sami nevidíme
    - může být součástí compliance
    - poskytovat kód externě může být problém
    - může být fajn použít víc společností, aby se vzájemně vychytala slabá místa
- lze provádět whitebox/blackbox (graybox pokud máme dokumentaci, ale ne kód)
- dobrou praxí je mít systém odměn za hlášení bezpečnostních chyb (bug bounty)

**Hlavní životní cyklus penetračního testování**
- Příprava
	- Dáme si cíle, definujeme rozsah, dohodneme se na testování, uděláme plány
	- většinou je dobré udělat i na to bokem prostředí
- Testování
	- zkoumáme systém, skenujeme cíle, modelujeme hrozby
	- využíváme slabá místa a vytváříme exploit (může uškodit systému)
	- testujeme hlouběji u slabých míst
	- používáme OWASP, případně jiné manuály a standardy
- Podání zprávy
	- sepíšeme jak pro vývojáře tak pro vedení zprávu
	- zahrnujeme vše z definice v prvním  kroku a přidáváme co se povedlo a co ne
	- kategorizujeme a prioritizujeme zranitelnosti

## Notes

**Brainstorm**
- používání neaktuálních/nepodporovaných verzí systémů
- odesílání uživateli zbytečně detailní informace, které mohou být zneužity
    - e.g. verze používaného dobře známého systému (třeba nginx), útočník může cílit na slabosti této konkrétní verze
    - e.g. *Cannot insert new record into table Users, unique constraint on column Email has been violated*
- xss

**Základní pojmy**
- [hašování](./5_databaze.md#hašování)
- **klíče** - rozsáhlé řetězce bitů, náhodná čísla, prvočísla...
- **šifrování** - zajišťuje důvěrnost (transformace zprávy za účelem skrytí jejího obsahu před nepovolanými aktéry)
- kódování není šifrování (e.g. zakódované heslo v base64 lze snadno převést do původního tvaru bez jakéhokoliv klíče)
- základním principem kryptografie je **veřejný algoritmus** (dobře otestovaný, vytvořený bezpečnostními experty) a zajištění bezpečnosti pomocí **tajného klíče**. Spoléhat na bezpečnost algoritmu jen jeho (algoritmu) utajením není dobrý nápad.
- **symetrická kryptografie** - komunikující strany sdílí identický klíč, kterým se šifruje i dešifruje. Je to rychlejší, než asymetrická kryptografie, ale hůře se využívají, když vyžadujeme autentizaci (e.g. server by si musel bezpečně uchovávat klíč u každého klienta, zároveň je potřeba se na klíči nějak dohodnout, což může být odposloucháváno)
    - e.g. **AES** (advanced encryption standard), **DES** (data encryption standard)
- **asymetrická kryptografie** - existují 2 druhy klíčů, veřejný (pro šifrování/ověření podpisu) a soukromý (pro dešifrování/tvorbu podpisu). Pokud chtějí 2 strany plně komunikovat (full duplex), pak každá potřebuje znát svůj soukromý klíč a veřejný klíč druhé strany. Pokud někomu prozradím svůj soukromý klíč, může se vydávat za mě.
    - e.g. **RSA, DSA**
    - pro šifrování a podepisování používáme rozdílné páry klíčů, abychom nemuseli čelit problémům, kdy zaměstnanec odejde z firmy (a stále zná soukromý klíč)
- **šifrování v praxi** - kombinace symetrické a asymetrické kryptografie
    - pro komunikaci proběhne ustanovení symetrického klíče náhodným vygenerováním, klíč se bezpečně předá pomocí asymetrické kryptografie. Následně probíhá komunikace šifrovaná symetricky.

**SHA**
- secure hashing algorithm
- SHA-0 a SHA-1 jsou zastaralé a nepovažují se za bezpečné
- rodina hašovacích funkcí SHA-2, zahrnuje SHA-224, SHA-256, SHA-384 a SHA-512 (jména podle jejich délky v bitech)

**RSA** - asymetricá kryptografie, funguje na principu faktorizace velkých čísel (a modulo) - faktorizace je lehká na výpočet, těžká na reverzní výpočet

**Bloková šifra** - symetrická, vstupní data jsou rozdělena na bloky fixní délky, které jsou šifrovány stejným způsobem. Pro větší bezpečnost se nešifrují všechny bloky stejně, ale může se použít e.g. Cipher Block Chaining (CBC), kdy je mezi bloky vytvořena závislost (každý další blok je xorován zašifrovaným předchozím blokem). Změna bitu zašifrovaných dat zmenožní dešifrování zprávy. E.g. AES, DES

**Proudová šifra** - symetrická, z klíče vygenerujeme posloupnost a na jejím základě šifrujeme jednotlivé bity dat (=> každý jinak). Díky tomu není nutné dešifrovat všechno (jako u blokových šifer v reřimu Cipher Block Chaining), ale můžeme jít *od prostředka*. Fungují rychle (třeba pomocí XOR dat s klíčem). Změna bitu zašifrované zprávy pozmění původní zprávu => je vhodné přidat nějakou formu hašování.

[https://www.youtube.com/watch?v=wlSG3pEiQdc&t=1s](https://www.youtube.com/watch?v=wlSG3pEiQdc&t=1s)

**Cyclic Redundancy Check (CRC)**
- kontrolní součet, umožňuje detekci neúmyslných chyb při přenosu/uložení
- je snadné vytvořit vstup odpovídající součtu, takže neposkytuje ochranu před úmyslnou změnou
- e.g. xor, modulo

Pro zajištění důvěrnosti dat bez šifrování lze použít **Chaffing and winnowing** - data rozdělíme na bity (lze i větší části). Pro každý bit budeme v náhodném pořadí posílat dvě zprávy, jednu s validním MAC a jednu (obsahující inverzi bitu) s nevalidním MAC.

**Čipové karty**
- součástí je paměť (RAM, ROM, EEPROM), procesor
- data se na kartě ukládají ve formě souborů, každému lze nastavit přístupová práva (volný přístup/přístup jen s pinem/zakázaný přístup)
- karta je schopná pracovat s kryptografickými algoritmy/protokoly
- lze provádět
    - fyzické útoky (preparace čipu, čtení paměti, využití záření/elektromagnetických polí), obvykle zanechávají viditelné známky útoku
    - logické útoky, vyžadují detailní znalosti o struktuře karty
        - časová analýza - sledujeme odezvu dle vstupu, 
            - jako prevenci se snažíme odstranit závislost délky zpracování na vstupu (e.g. vložíme fejkové instrukce)
        - výkonová analýza - odběrová, memory operace jsou levnější, než výpočty
        - indukce chyb - pomocí náhlých změn podmínek (napětí, teplota...) se snažíme změnit operační podmínky
        - útoky přes api - snažíme se využít možné chyby programátora
            - e.g. počítadlo pokusů by mělo nejdřív snížit počet pokusů, pak ověřit pin a v případě úspěchu resetovat počítadlo pokusů... jinak lze po zadání pinu a detekce neúspěchu rychle odpojit zdroj

**Honeypotting** - pro útočníka připravíme izolovaný subsystém, do kterého ho pustíme a sledujeme jeho chování, čímž se učíme o jeho způsobu práce
