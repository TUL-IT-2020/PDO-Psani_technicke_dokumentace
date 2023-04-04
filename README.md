# Technická dokumentace
## Co dokumentuji?
Mou bakalářskou práci, která je dostupná na školním Git labu. Návrh procesoru RISC-V32I.

## Pro koho to dokumentuji?
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

## Návod pro oponenta
### Specifikace cílové skupiny
Předpoklady na čtenáře:
- Uživatel je velmi technicky zdatný
- Má optimální pracovní podmínky
- Dokumentaci si čte na počítači
- Ovládá jazyk VHDL

### Slovníček
| Anglicismus | Český ekvivalent |
| --- | --- |
| kompilace | překlad |
| kompilátor | překladač |

### Struktura práce
Kroky potřebné k otestování praktické části:
- Jak nainstalovat IDE Vivado.
	- Jak používat Vivado?
	- Jak spustit testy?
- Přklad zdrojového kódu
	- Seznámení se s zdrojovým kódem (C/Assembler)
	- Stažení překladače (RISC-V32I)
	- kompilace
- Nahrání na desku
	- Komunikace s vývojovou deskou
	- Spuštění a ovládání demo programu

### Struktura repositáře
```Bash
$ tree -d -L 4
├── assets
├── DOC
│   └── official
├── programs
└── RISC-V
    ├── RISC-V.gen
    │   └── sources_1
    │       └── ip
    ├── RISC-V.ip_user_files
    │   ├── ip
    │   ├── ipstatic
    │   ├── mem_init_files
    │   └── sim_scripts
    ├── RISC-V.runs
    │   └── synth_1
    ├── RISC-V.sim
    │   └── sim_1
    │       └── synth
    └── RISC-V.srcs
        ├── sim_1
        │   └── new
        └── sources_1
            ├── ip
            └── new
```
Obsahuje adresářů:
- `RISC-V/`  - projekt IDE Vivado
- `programs/` - programy pro otestování procesoru a přiložené scripty
- `RISC-V.srcs/sources_1/new` - *.VHD* zdrojové soubory 
- `RISC-V.srcs/sim_1/new` - testovací soubory pro simulace

# Obsahová část
## Testování
### Spuštění simulace

### Nahrání jiného programu
Pro změnu programu v simulaci *tb_run_program.vhd* je potřeba změnit .coe soubor a rekonfigurovat *instruction_memory*.

#### 1. hex dump
Vzorové programy jsou připraveny v souborech *.txt* v adresáři: `RISC-V/programs/`. Pro překlad vlastního kódu lze například použít [[6. semestr/PDO-Psani_technicke_dokumentace/README#Překlad online|online překladač]].

#### 2. Aktualizace .coe souboru
Python script `RISC-V/programs/coe_generator.py` slouží pro přepis hex-dump souboru do formátu .coe:
```Bash
$ python3 .\coe_generator.py   
usage: coe_generator.py [-h] -i INPUT
                        [-o OUTPUT]
                        [-r RADIX]
coe_generator.py: error: the following arguments are required: -i/--input
```
Pro vygenerování nové konfigurace *test1.coe* ze souboru *sum.txt* zadejte příkaz:
```Bash
python3 coe_generator.py -i sum.txt -o test1.coe
Generating COE file from: sum_func.txt to: test1.coe
```

#### 3. Rekonfigurace paměti IP jádra
TODO:

Nyní již můžete spustit simulaci s novým programem. 

## Otestování vlastního programu
Před nahráním vlastního programu je vhodné otestovat jeho funkčnost, k tomu lze využít některého ze simulátorů RISC-V.
[riscfive: seznam simulátorů](https://www.riscfive.com/risc-v-simulators/)
[Online: venus.kvakil](https://venus.kvakil.me)
[Online: ascslab](https://ascslab.org/research/briscv/simulator/simulator.html)
[VS Code rozšíření: venus](https://marketplace.visualstudio.com/items?itemName=hm.riscv-venus)

### Překlad zdrojových kódů online
Pro jednodušší programy je vhodné použít překlad online, pro který není potřeba na vlastní počítač nic instalovat. 

#### C -> asm
Překlad z C na asm RISC-V [compiler explorer](https://godbolt.org). Umožnuje překlad překlad z mnohých jazyků do asm pro různé platformy. Nás zajímá jazyk **C** na **RISC-V rv32gc clang (trunk)**. Instrukční sada rv32i je podmnožinou rv32gc a je tedy nutné mít na mysli, že ne všechny instrukce (například: násobení, FP operace) půjde po překladu spustit. 
V nastavení výstupu je vhodné zaškrtnout položky *Demangle identifiers* a odfiltrovat vše kromě *Comments*. 

#### asm -> hexa
Překladač z asm na hexa RISC-V překladač: [riscvasm.lucasteske](https://riscvasm.lucasteske.dev/#)
Na ovládání velmi jednoduchý překladač. Po vložení asm kódu stačí zmáčknout "BUILD" a kód se přeloží do hexa souboru. Poskytuje i disasembly výstup pro zpětný přepis, který obsahuje již i čísla adres v paměti vizualizující jednotlivé skoky na návěští.

### Překlad zdrojových kódů na vašem stroji
Lze použít různých překladačů, například: Clang/LLVM nebo GCC.
- 64 bitů

Kompilace zdrojových pro 64bitvůou architekturu mohou zajistit již sestavené nástroje od [sifive](https://github.com/sifive/freedom-tools/releases)

- 32 bitů

Naše architektura je však 32bitová a proto si musíme sestavit vlastní překladač. Podrobný postup je popsán na stránkách [repositáře](https://github.com/riscv-collab/riscv-gnu-toolchain). Překlad gcc pro křížový překlad.

Zkrácený postup pro operační systémy Linux:

1. Naklonování repositáře s nástroji:
```bash
git clone https://github.com/riscv/riscv-gnu-toolchain
```

2. Instalace potřebných balíčků:
```bash
sudo apt-get install autoconf automake autotools-dev curl python3 libmpc-dev libmpfr-dev libgmp-dev gawk build-essential bison flex texinfo gperf libtool patchutils bc zlib1g-dev libexpat-dev ninja-build
```

3. Konfigurace před sestavením:
```bash
cd riscv-gnu-toolchain/
./configure --prefix=/opt/riscv --with-arch=rv32i --with-abi=ilp32
```
- `/opt/riscv` je cesta k adresáři kam se nástroj pro překlad sestaví
- `rv32i` je naše architektura
- `ilp32` je konfigurace pro architekturu bez jednotky s plavoucí řádovou čárkou

4. Sestavení nástroje:
```bash
make linux
```

5. Přidání nástroje do cesty spustitelných nástrojů:
```bash
export PATH="/opt/riscv/bin:$PATH"
```

### Disassembly
Překlad programu do binárního souboru:
```bash
riscv32-unknown-elf-gcc -c -o code.o sum.c
```
- *sum.c* vzorový program k překladu.
- `-o` nastavuje název výstupního souboru na *code.o*.
- `-c` kód pouze přeloží

Přepis binárního kódu do assembly:
```bash
riscv32-unknown-elf-objdump -d code.o
```


6. Kompilace zdrojového kódu programu:
- Překlad v jednom kroku:
```bash
riscv32-unknown-elf-gcc fibonaci_rekurze.c -o fib.bin
```
- Překlad a slinkování postupně:
```bash
riscv32-unknown-elf-gcc -c -o fib.o fibonaci_rekurze.c
riscv32-unknown-elf-gcc -g -o fib.bin fib.o
```

### HexDump
Pro otevření *.bin* souborů lze použít programů typu hexdump.

- Windows [free hex editor](https://www.hhdsoftware.com/free-hex-editor)
- Linux [hexdump](https://manpages.ubuntu.com/manpages/bionic/en/man1/hexdump.1.html)

#### Disassembly
Překlad programu do binárního souboru:
```bash
riscv32-unknown-elf-gcc -c -o code.o sum.c
```
- *sum.c* vzorový program k překladu.
- `-o` nastavuje název výstupního souboru na *code.o*.
- `-c` kód pouze přeloží

Přepis binárního kódu do assembly:
```bash
riscv32-unknown-elf-objdump -d code.o
```


### asm -> hexa
#### Překlad online
Překladač z asm na hexa RISC-V překladač: [riscvasm.lucasteske](https://riscvasm.lucasteske.dev/#)
Na ovládání velmi jednoduchý překladač. Po vložení asm kódu stačí zmáčknout "BUILD" a kód se přeloží do hexa souboru. Poskytuje i disasembly výstup pro zpětný přepis, který obsahuje již i čísla adres v paměti vizualizující jednotlivé skoky na návěští.

6. Kompilace zdrojového kódu programu:
- Překlad v jednom kroku:
```bash
riscv32-unknown-elf-gcc fibonaci_rekurze.c -o fib.bin
```
- Překlad a slinkování postupně:
```bash
riscv32-unknown-elf-gcc -c -o fib.o fibonaci_rekurze.c
riscv32-unknown-elf-gcc -g -o fib.bin fib.o
```

### HexDump
Pro otevření *.bin* souborů lze použít programů typu hexdump.

- Windows [free hex editor](https://www.hhdsoftware.com/free-hex-editor)
- Linux [hexdump](https://manpages.ubuntu.com/manpages/bionic/en/man1/hexdump.1.html)

## Zdroje:
https://stackoverflow.com/questions/74231514/how-to-install-riscv32-unknown-elf-gcc-on-debian-based-linuxes
https://stackoverflow.com/questions/31390127/how-can-i-compile-c-code-to-get-a-bare-metal-skeleton-of-a-minimal-risc-v-assemb
https://web.eecs.utk.edu/~smarz1/courses/ece356/notes/assembly/




