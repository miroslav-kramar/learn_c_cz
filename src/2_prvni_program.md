# První program

## Zrození programu

Máme nějaký algoritmus. Tento algoritmus popíšeme v **programovacím jazyce**. V našem případě v C.

Kódu v jazyce C rozumíme my, lidé. Pro počítač je to ale obyčejný textový soubor, bezvýznamná halda bajtů.

Aby počítač byl schopen program spustit, musí být v podobě sady instrukcí pro procesor.

Přechod od textového C kódu ke spustitelnému binárnímu souboru zajišťuje **kompilátor**.

## Co budeme potřebovat?

- **PC**
  
  Srdcem každého počítače je procesor. Procesor rozumí pouze instrukcím zapsaným ve strojovém kódu, číselným kódům uložených v paměti. Jazyk C se do strojového kódu překládá. Jaké další jazyky to mají stejně?

- **Monitor**
  
  Dnes je standardem, že monitor má v sobě vestavěný operační systém. Skrze jeho grafické rozhraní lze pohodlně měnit nastavení displeje. Takovýto firmware (FW) je obvykle napsán v C kvůli velikosti a přímé interakci s HW.

- **Klávesnici**
  
	I jiná příslušenství mají svůj FW. Klávesnice posílá do PC kódy stisklých kláves, běžně přes rozhraní USB. Tyto kódy se musí pro přenos zakódovat pomocí mikročipu běžně vykonávajícího C kód.

- **Operační systém**
  
  	Operační systém je ve své podstatě balík programů. Nejdůležitějším z nich je bezesporu jádro. Jádra všech relevantních operačních systémů jsou napsána v jazycích C a C++, nově i Rust.

- **Textový editor**
  
  Protože zmagnetizovanou jehlou přímo na plotně disku se programuje špatně :) Například populární lehký textový editor v prostředí GNU/Linux je Nano, celý napsaný v C.

- **Kompilátor**
  
  Kódu programovacího jazyka rozumí lidé, ne stroje. Abychom dostali funkční program, musíme ho přeložit do strojového kódu pomocí kompilátoru. V jakém jazyce je asi napsán kompilátor jazyka C?

## Hello, World!

Možná jste slyšeli o programech typu "Hello World". Věděli jste, že ten první napsal v roce 1978 profesor Brian Kernighan právě v C? Vypadal nějak takto:
```c
#include <stdio.h>

int main() {
	printf("Hello, World!\n");
	return 0;
}
```

## Anatomie C programu

Základním stavebním kamenem každého programu v jazyce C je *funkce* `main`. Toto jméno kompilátor očekává. Označuje místo, kde program začíná. Minimální C program vypadá takto:

```c
int main() {
	return 0;
}
```

Takový program ale vůbec nic nedělá. Jen co funkce začne, tak dojde ke *klíčovému slovu* `return`, které způsobí její konec. A v okamžiku, kdy skončí funkce `main`, skončí i celý program. *0* je potom stavový kód označující úspěch. A nesmíme zapomenout na středník!

Pojďme vypsat něco do konzole. Třeba pomocí funkce `printf`. Text, který chceme vypsat, se udává mezi uvozovky. `\n` označuje nový řádek.

```c
int main() {
	printf("Hello, World!\n");
	return 0;
}
```

Pokud zkusíme tento program přeložit, tak bohužel neuspějeme. Kompilátor nás informuje, že nenalezl funkci `printf`. To je v pořádku, její definici (popis toho, co dělá) totiž nikde neuvádíme. Definice funkce `printf` je součástí standardní knihovny *stdio*. Musíme ji proto vložit do našeho kódu.

```c
#include <stdio.h>

int main() {
	printf("Hello, World!\n");
	return 0;
}
```

Nyní je program kompletní a přeloží se bez chyb. Ale jak?

## Kompilátor (překladač)

Kompilátor je program, který převádí (překládá) kód zapsaný v programovacím jazyce na sadu instrukcí pro procesor.

Často je součástí větší sady nástrojů. Jelikož se ale přesvědčivě jedná o nejdůležitější část, běžně se celá tato sada nazývá jako kompilátor.

V našem případě budeme chtít pomocí kompilátoru převádět soubory s C kódem na spustitelné soubory (.exe, .elf, ...).

## Kompilace

Proces přechodu od C kódu ke spustitelnému souboru má několik kroků. Každý obstarává samostatný podprogram:

1. **Preprocessor**
   
	Řídí se direktivami. Obstárává např. vkládání hlavičkových souborů.

2. **Kompilátor**
   
	Jediný, kdo "rozumí" kódu jazyka C. Ten převede do *assembly*, lidsky čitelnou sadu instrukcí pro procesor.

3. **Assembler**
   
	Instrukce zapsané v assembly převede na *strojový kód*, "jedničky a nuly", kterým rozumí procesor.

4. **Linker**

	"Sešije" náš program s ostatními přeloženými soubory, například kódem standardních knihoven. Jeho výstupem je spustitelný soubor.

## Konkrétní kompilátory

**GNU/Linux, macOS**

- [GCC](https://gcc.gnu.org/)

	Doporučuji

- [Clang](https://clang.llvm.org/)

**MS Windows**

- [mingw-w64](https://www.mingw-w64.org/) (GCC)

	Doporučuji, konkrétně implementaci [WinLibs](https://winlibs.com/)

- Clang
- [MSVC](https://visualstudio.microsoft.com/vs/features/cplusplus/)

	Nedoporučuji, primárně C++ kompilátor

Kompilátory lze používat samostatně, nebo jako součást vývojového prostředí (IDE).

## Kompilace pomocí překladače GCC

Pomocí příkazu `gcc`

Příklad použití (prostředí BASH):
```bash
$ gcc hello.c -o hello -Wall
$ ./hello
Hello, World!
```

Použité flagy:

- `-o` specifikuje název cílového spustitelného souboru
- `-Wall` aktivuje všechna základní varování