# Technická dokumentace
!!!

Dokumentace je psána formou GitHub wiki [zde](https://github.com/elPytel/PDO-Psani_technicke_dokumentace/wiki/wiki_main).

!!!

# Psaní technické dokumentace
Dotazy psát na elerning na fórum.

## Zápočet
Zápočet za účast a práci v hodině.

## Zkouška
Prezentace mé dokumentace. Proč jsem se rozhodl pro danou strukturu a formu dokumentace. Není to o tom co jsem dělal k bakalářce, ale jak jsem to komentoval. 

10 minut vykládat o tom co jsem a jak udělal. 

- [ ] Finální verze práce den před zkouškou.

## Cvičení
1. Poznej svojí cílovou skupinu
-  [x] Git repositář pro dokumentaci. 
-  [x] Specifikace cílové skupiny. 
Napsat analýzu use case. Vybrat si pro koho dělám analýzu. Pro váš produkt vyberte, jaký typ dokumentace chcete vytvářet.
-  [x] Elerning přidat odkaz na repozitář. 

2. [[cv02|cvičení]]
3.  [x] Návrh struktury semestrální práce
4. [[cv04|cvičení]]
5. [[cv05|cvičení]]
6. [[cv06|cvičení]]
7. [[cv07|cvičení]]

## Semestrální projekt
Dokumentace k bakalářské práci.
[Dokumentace RISC-V](./README.md)

### Co dokumentuji?
Mou bakalářskou práci, která je dostupná na školním Git labu. Návrh procesoru RISC-V32I.

### Pro koho to dokumentuji?
Analýza cílové skupiny.
Pro koho to dělám?
Kdo, kde, co a jak bude dělat?

### Jaké jsou use case:
- Návod pro oponenta
Návod pro oponenta jak zprovoznit a otestovat práci. 
Jak oživit desku, nahrát program, načíst data....

- Programátor v ASEMBLY?
Musel bych se docela dost naučit programovat v ASEMBLY.

- Programátor překladače? 
Netuším jak kvalitně někoho navést ke psaní překladače.

- Návrh desky?
Žije to na FPGA, nemá vlastní pouzdro. 

### Návod pro oponenta
#### Specifikace cílové skupiny
Předpoklady na čtenáře:
- Uživatel je velmi technicky zdatný
- Má optimální pracovní podmínky
- Dokumentaci si čte na počítači
- Ovládá jazyk VHDL

#### Rozlišení textu:
- **BOLT** 
	- položky menu
- *Kurziva*
	- technické termíny
- `Kód`
	- Kusy kódu 
- "uvozovky"
	- čtení zkratek?

cesty k souborům
formát souborů

#### Struktura práce
Kroky potřebné k otestování praktické části:
- Jak nainstalovat IDE Vivado.
	- Jak používat Vivado?
	- Jak spustit testy?
- Překlad zdrojového kódu
	- Seznámení se s zdrojovým kódem (C/Assembler)
	- Stažení překladače (RISC-V32I)
	- kompilace
- Nahrání na desku
	- Komunikace s vývojovou deskou
	- Spuštění a ovládání demo programu

## Výpisky

PDF s textem není elektronická dokumentace. Vyhledávání, prolinkování.

Dokumentarista dostane use case a pro každý z nich vytvoří vlastní.

Čitatel má problém. Jinak by to vůbec neotevřel. 


Pro usnadnění hledání sekce s řešením psát klíčová slova tučně. 

Piš to jako by to měla číst opice co si zapomněla brýle na blízko. 

Základní typy dokumentace:
- Koncepty 
Vysvětlení základních pojmů a principů. Seznámení s názvoslovím. 

- Popis pracovních postupů
Tutoriál (učebnice).
How-To (Složitější, ale cílem je pouze dané řešení, není nutné dlouhodobé pochopení).
Kuchařka (v bodech, které se mají postupně udělat).

- Problémy a jejich řešení
Pomoc uživateli. FAQ - (často kladené otázky)
Identifikovat nastalý problém a nejkratší možnou cestou ho provést řešením. 

- Referenční příručka
Seznam úplně všeho.
Popis jednotlivých funkcí. Generování dokumentace z komentářů (Java doc).
Datasheet


Github action která hlídá commity, aby funkce měly dokumentaci.

RTFM - Read the fucking manual.

TL;DR - Too long; didn't read. 

Signle source publishing

XML - značkovací jazyk, je vhodné používat značkovací nástroje založené na XML.

### Fonty
Times New Roman - určen pro tisk na papír.
Helvetika - pro poznámky velikostí 8.5 bodů a menší.



