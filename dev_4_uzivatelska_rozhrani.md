# Uživatelská rozhraní.

> Uživatelská rozhraní. Principy návrhu a vývoje uživatelského rozhraní v moderních softwarových systémech, vč. webových, mobilních. Proces vývoje uživatelského rozhraní a zásady kvality. User experience (UX), interaction design, prototypování, wireframování, uživatelský výzkum, testování použitelnosti. Technologie a nástroje. Příklady z praxe pro vše výše uvedené. (PV182 || PV247 || PV278)

## Principy návrhu a vývoje uživatelského rozhraní v moderních softwarových systémech, vč. webových, mobilních.

Klíčem k úspěchu UI je uživatelská přívětivost a snadné použití rozhraní. Našlapaný systém s tunou pokročilých funkcionalit bude k ničemu, pokud se nedá jednoduše používat koncovými uživateli. Běžní uživatelé obvykle dokáží systému s dobrým UI prominout i některé funkcionální nedostatky.

**Uživatelské rozhraní (UI)** by se dalo definovat, jako vizuální a interaktivní elementy, se kterými interaguje uživatel během práce se systémem. Můžeme zde zahrnout vytvoření layoutu, typografie, ikonografie a barevného schématu.

**Návrh rozhraní může ovlivňovat**
- jedná se i interní (uživatelé musí pracovat), nebo veřejný systém (chtějí pracovat)
- úroveň odbornosti uživatelů
- nutnost možnosti přizpůsobení
- nutnost vícejazyčnosti aplikace (problém mohou dělat třeba odlišné druhy písma)
- nutnost *přístupnosti* (accessibility) pro uživatele s nějakým omezením
- platforma

Klíčové vlastnosti při návrhu UI na které bychom měli cílit:
- *konzistence* - uživatel by si měl zvykat na to jak vypadají komponenty v aplikaci a neměl by na každé stránce vidět jiné barvy a jiný design
- *jednoduchost* - snažíme se jednoduše a přehledně předat informace, nedělat zbytečné věci okolo, trochu může překrývat i UX, kdy bych měl zjistit co je zbytečné v UI
- *feedback* - pokud se akce vykonává, ukažme tam loading, pokud selhala, dejme vědět co se stalo, je potřeba komunikovat s uživatelem a aktualizovat mu stav, co se děje
- *accessibility* - volíme barvy tak, aby byly kontrastní a snažíme se používat mechanismy, aby byla aplikace lépe přístupná pro čtení displeje a podobně
- *error recovery* - pokud se stala chyba, dejme uživateli informace a nástroje jak na toto reagovat
- *estetika a vizuálnost* - pokud máme hezkou aplikaci, některé chyby uživatel může snadno přejít a neřešit je

Je fajn brát ještě v potaz
- uživatelskou přívětivost 
	- složité formuláře je fajn dělit na vícero částí
	- mít pole od shora dolů a ne nějak komplikovaně
- bezpečnost 
	- pro aplikace, na které mohou cílit útočníci je fajn stránku uživateli přizpůsobit
	- pokud použijeme fotku uživatele, je těžké stránku napodobit
    - skrývání hesel
- používání vhodných input polí
- rozhraní by mělo být jednotné
- responsivity - fungování aplikace na různě velkých obrazovkách

##### Použitelnost a zpřístupnění

**Usability** - přizpůsobení systému, aby specifičtí uživatelé zvládli jednoduše a efektivně dosahovat cílů, kvůli kterým navštívili aplikaci, většinou se do toho neberou lidé s nějakým postižením

**Accessibility** - je to použitelnost aplikace pro lidi s nějakým omezením nebo postižením, tedy nemohou dobře číst málo kontrastní text, nevidí vůbec a podobně.

Většinou chci cílit prvně na usability a poté accessibility. Nejlépe řešit oboje, ale řešit accessibility fakt kvalitně je hodně náročné a chce to testování, abychom si byli fakt jistí, že to děláme správně.

Současná řešení
 - současnosti je nejuniverzálnějším způsobem tvorby UI HTML+CSS+JS
 - aktuálně jsou populární frontend JS frameworky (React, Vue, Solid, Svelte, Angular..)
 - pro desktopovou aplikaci můžeme použít buď Tauri, nebo Elektron
 - ještě je možnost použít pro SPA Progressive web app
 - pokud chceme plně využít výhody zařízení, můžeme použít (React Native, Svelte Native)
 - tyto technologie mají obvykle dobře řešené věci jako accessibility či lokalizace
 - díky tomu, že jsou hodně používané, existují pro ně solidní komponentové knihovny 
 
Aktuálním trendem se zajímavým potenciálem je WebAssembly, které umožňuje použití kompilovaného jazyka. Výsledná aplikace je spustitelná v prohlížeči a z pravidla rychlejší, než JS. WASM podporuje 2 mody - práci s DOM, nebo přímé vykreslování na canvas (používá třeba Firma).

Alternativou může být použití multiplafrormního frameworku Flutter (používá jazyk Dart, podporuje Android, IOS, web), který umožňuje vývoj pro vícero platform z jednoho zařízení.

Nativními jazyky pro mobilní aplikace jsou *Swift* (IOS) a *Java/Kotlin* (Android). Pro desktopové aplikace je možné použít i technologie jako GTK (existují bindingy na různé jazyky) nebo Qt (C++), JavaFx...


**Specifika pro web**
- můžeme rozlišovat různé přístupy, jako je SSR, SPA, SSG
- podpora pro více zařízení
- můžeme řešit v rámci UI i nějaké SEO optimalizace
- je zde nějaká konektivita na internet, takže bychom měli více řešit nějaké načítání
- navigace pomocí URL, kterou bychom měli využívat

**Specifikace pro telefon**
- limitovaní velikost displeje
- většinou děláme vývoj mobile-first
- je zde touch-based interakce, tedy trochu hůře se řeší třeba tooltipy
- více dbát na potvrzovací dialogy, protože můžeme kliknout někam omylem
- interakce se zařízením ve formě vibrací, kamery, GPS apod.

**Specifikace pro desktop**
- mohou být offline
- hůře se řeší aktualizace
- máme window management
- interakce hlavně přes myš a klávesnici


---

## Proces vývoje uživatelského rozhraní a zásady kvality.

Začneme uživatelským výzkumem, abychom pochopili skutečné požadavky na UI. Následuje návrh pomocí wireframů a prototypů, které můžeme použít pro zpětnou vazbu a jako předlohu pro vývojovou práci. Na konec je důležité provést uživatelské testování s různými typy uživatelů, abychom předešli problémům při nasazení aplikace.

Postup při vývoji UI
1. *User research* - základní pochopení kdo jsou uživatelé
2. *Information Architecture and Wireframing* - struktura a hrubé náčrtky
3. *Visual design* - dodáváme typografii, barvy, detaily
4. *Interaction design* - děláme interaktivní a klikatelné prototypy
5. *Usability testing* - zkoušíme a dostáváme feedback na návrhy
6. *Development and implementation* - programování aplikace
7. *Iteration and Refirement* - ladíme naprogramované UI
8. *Maintenance and updates* - monitorujeme a děláme aktualizace

#### Interaction design
Snažíme se pochopit, jakým způsobem uživatelé se systémem pracují či interagují a uzpůsobit tomu uživatelské rozhraní. Cílíme na interaktivitu uživatele s aplikací ve formě například použití gest, animací, mikrointerakce jako je třeba tooltip, indikátory a podobně.

#### Uživatelský výzkum, analýza
- je důležité určit, kdo jsou naši uživatelé, jak dosud pracují se stávajícími systémy
- co jim vyhovuje a co ne, na co jsou zvyklí
- je důležité určit, co jsou požadavky na systém, jak se používá
	- můžeme se snažit o minimalizaci kliknutí pro dosažení operace a podobně
- na základě uživatelského výzkumu chceme navnímat uživatele
- na základě toho můžeme potom vytvářet *personu*
- s uživateli lze řešit i náš produkt ve *focus groups*
- lze použít A/B testování 
	- každé skupině uživatelů prezentujeme určitou variantu produktu a sledujeme vliv
	- lepší variantu použijeme

Uživatelské výzkumy můžeme dělit na

|                | **Quantitative**   | **Qualitative**        |
| -------------- | ------------------ | ---------------------- |
| **Generative** | dotazníky          | pozorování, rozhovory  |
| **Evaluative** | analytické metriky | testování použitelnost |
Typicky u generativního tak přicházíme s novými nápady. Tedy dáváme dotazníky a rozhovory, abychom zjistili, co lidi chtějí a případně jim něco navrhneme řešíme jestli by jim to přišlo dobré. U evaluativního můžeme třeba testovat, zda nám úpravy na webovce zvýšili konverzní poměr uživatelů.

Pokud si vybíráme respondenty, měli bychom si dávat pozor na to, že bereme naše potenciální zákazníky nebo uživatele a ne každého. Měli bychom dbát na to, že není nějak ovlivněný a měli bychom dbát na nějakou rozmanitost (věk, lokace, úroveň práce s počítačem).

**Persona** - fiktivní reprezentace cílového uživatele. Jeho cíle, motivace a chování. Díky němu mohou nejen UI vývojáři, ale i tým programátorů navnímat pro koho produkt dělají.

**Scénáře** - nějaké příběhy a postupy proč, jak a s jakým cílem chce uživatel komunikovat s naší aplikací. Může jít klidně o nějaké komiksy, kde se na pár obrázcích ukáže nějaká situace, kdy mu aplikace pomůže.

**Úkoly** - asi by se dalo přirovnat k nějakému Use Case diagramu. Tedy sada úkolů, které bude chtít v aplikaci uživatel dělat.

Při vývoji UI se můžeme odkazovat na C. R. A. P. 
- *Contrast* - barvy, elementy by měly být dobře odlišitelné
- *Repetition* - konzistentní UI prvky
- *Alignment* - v době návrhu už správně řadit a layoutovat jednotlivé prvky
- *Proximity* - dávat společné akce a prvky blízko k sobě

#### Wireframování

Vhodné pro návrh rozložení jednotlivých komponentů rozhraní, neřešíme barvy/styly, ale jen layout a hrubé rozložení obsahu. Jde nám o to vystihnou nějaký koncept. Dalo by se to podle mě zařadit, že wireframing je podtyp low-fidelity prototypů.

#### Mockupy

Vyšší verze wireframu, většinou jde o nějakou statickou verzi, kde už přidáváme barvy a nějaké grafické prvky.

### Prototypování 

Pomocí návrhových nástrojů jako AdobeXD nebo Figma, lze vytvořit (z části i interaktnvní) prototyp, který lze použít pro prvotní uživatelské testování. Rozlišujeme na:
- **Low-Fidelity Prototypes**
	- na začátku procesu
	- většinou jen náčrtky a schémata stránek
	- základní layout co kam dát
	- zabýváme se strukturou a aby nás to nestálo moc peněz
- **High-Fidelity Prototypes**
	- mohou být už typografii, barvy, finální verze komponent
	- používáme i nástroje, které nám dodají interaktivitu
	- testujeme jak se budou komponenty chovat a jak bude vypadat flow
- **Horizontal Prototypes**
	- zabýváme se obrazovkami a nechodíme do moc detailu
	- většinou jen jednoduchá ukázka jak bude vypadat
	- jako kdybychom jen proklikávali aplikaci na té nejvyšší navigační úrovni
- **Vertical Prototypes**
	- vezmeme jednu stránku nebo funkcionalitu a jdeme do hloubky
	- koukáme se na všechny případy flow, které mohou nastat
	- zkoušíme interakci uživatele při nějakém procesu a podobně

## User experience (UX)

Jedná se o záležitost týkající se nejen vizuální stránky, ale hlavně toho jak se uživatel v aplikaci cítí. Tedy například se snažím zodpovídat otázky uživatele dříve než si je položí. Chci mu ukazovat nějaké data, které v tu chvíli hledá a snažím se, aby zážitek z používání aplikace měl co nejlepší.

Může to být například ve formě, že vysvětlím některé akce, které nemusí být jasné, snížím počet rozhodování uživatele, odstraňuji překážky, které mohou nastat a podobně.

## Testování použitelnosti

Většinou chci nějak zjistit, jestli to co se navrhlo dává uživatelům smysl, případně pokud mi nefungují konverze na stránkách tak mohu dělat testování, zda není chyba ve špatném designu.

Měl bych tedy v tom nejlepším případě si pozvat nějaké uživatele a nechat je řešit problémy na místě. Můžeme je díky tomu pozorovat a řešit s nimi problémy hned. Pokud není možnost, dá se použít například software na trackování kurzoru a dívat se na reálné uživatele. Dá se také nasadit sledování očí uživatele při používání produktu, zjistíme tak, jaké části rozhraní nejvíce upoutají pozornost uživatelů, je k tomu potřeba souhlas uživatele. Poté se k tomu dají vykreslovat heat mapy.

Můžeme se jich pak ptát
- co byste udělali zde?
- proč jste váhal před kliknutím na tlačítko?
- co se právě snažíte najít?

Na základě těchto testování poté navrhneme další postupy jak vyřešit problémy.

Pokud potřebujeme nějaké testování například zpřístupnění, můžeme třeba použít také automatizované nástroje jako Lighthouse.

## Technologie a nástroje

Hlavně jde asi o
- Figma - návrhy UI a interaktivních prototypů
- FigJam - na kooperaci a brainstorming s ostatními kolegy
- AdobeXD - to samé jako Figma, ale od Adobe