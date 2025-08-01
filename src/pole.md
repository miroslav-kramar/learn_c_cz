# Pole

## O co jde?

Představte si obyčejnou proměnnou jako krabičku. Krabička má nějaký tvar a můžeme do ní něco uložit.

Pole (anglicky *array*) je potom velká krabice, do které se dají tyto malé krabičky narovnat jedna vedle druhé.

Z hlediska paměti počítače jsou to stejně velké buňky paměti narovnané za sebe. Tyto buňky musí všechny mít stejnou velikost, jako je datový typ, jenž do pole ukládáme.

## K čemu je to dobré?

Když potřebujeme ukládat/zpracovávat více hodnot stejného datového typu, např. čísla k vypočítání průměru, souřadnice, ...

## Deklarace statického pole

Pole, stejně jako proměnná, se musí deklarovat. Součástí deklarace je, kromě datového typu, také délka pole. Délkou se rozumí počet buněk. Tato délka je **neměnná**.

Deklarace pole čtyř integerů bez inicializace:
```c
int arr[4];
```

Tentokrát s inicializací:
```c
int arr[4] = {1, 2, 3, 4};
```

Inicializace nulami:
```c
int arr[4] = {0};
```

Jiné datové typy:
```c
float arr_f[4] = {1.1, 1.2, 1.3, 1.4};
char  arr_c[4] = {'a', 'b', 'c', 'd'};
```

### Dedukce délky pole z literálu

Kompilátor je dokonce tak inteligentní, že je schopen určit délku pole pomocí toho, kolik hodnot uvedeme v literálu.

Toto je potom naprosto validní kód:
```c
int arr[] = {1,2,3,4,5};
```
Jaká bude délka pole?

## Indexace

Každá buňka v poli má svůj **index** (pozici). Pomocí tohoto indexu přistupujeme k hodnotě v konkrétní buňce.

**POZOR:** pole se číslují od **0**! Prvním indexem je tedy **0**. Proč, to se dozvíme, až se budeme zabývat ukazateli do paměti.

Pokud tedy máme pole o délce *10*, potom jsou přípustné indexy *0* až *9*.

### Zápis a čtení z konkrétního indexu

Pomocí operátoru `[]`:

```c
int arr[4] = {1,2,3,4};

arr[2] = 8;
arr[0] = 1;
arr[1] = arr[3];

printf("%d\n", arr[4]);
```
Která a v jakém pořadí uložená čísla budou v poli? A není v kódu náhodou chyba?

## Průchod polem

Procházet velká pole vypisováním jednotlivých indexů je nepraktické. Pokud chceme kód navíc udělat znovupoužitelný pomocí funkce, pole nemusí mít vždy ani stejnou délku. Pro takovéto případy se nám výborně hodí cyklus `for`:
```c
int arr[10];
for (int i = 0; i < 10; i++) {
	arr[i] = (i+1) * 2;
}

for (int i = 0; i < 10; i++) {
	printf("[%d]: %2d\n", i, arr[i]);
}
```
Která a v jakém pořadí uložená čísla budou v poli? A jak bude vypadat výstup?

## "Nepříjemnosti" kolem indexace

Jeden z důvodů, proč jsou programy napsané v C jedny z nejrychlejších vůbec, je ten, že nedělají téměř nic víc, než co jsme jim pomocí kódu řekli. Například samy nekontrolují, jestli přistupujeme na validní index.

Pokud tedy založíme pole o velikosti *10* a budeme chtít zapsat na index *1000*, tak můžeme. To je ale chyba, jelikož tato paměť již není součástí pole.

Dochází tak k poškození paměti programu. V lepším případě program spadne a my víme, že je někde chyba. V horším případě poběží dál, ale nebude se chovat podle očekávání. Takovéto chyby se hledají velmi špatně.

## Tip: ASan

Naštěstí již není rok 1989, a tak vznikla různá řešení. Jedním z nich je Address Sanitizer, zkráceně [ASan](https://github.com/google/sanitizers/wiki/addresssanitizer).

Jeho dovedností je, mimo jiné, že hlídá, zdali jsme nepřistoupili mimo paměť konkrétního pole. Pokud ano, tak ASan ukončí program a vypíše chybovou hlášku.

ASan aktivujeme nastavením flagu u kompilačního příkazu:
```bash
$ gcc main.c -o main -Wall -fsanitize=address -g
```
Flag `-g` je potom pro lepší chybové hlášky.

## Předávání pole funkcím

Jak víme, hodnoty se do funkcí předávají *by value*. Dochází tak k vytvoření jejich kopie. Jedinou výjimkou je pole.

Představme si, že bychom měli pole o 10K buňkách a chtěli ho předat nějaké funkci, třeba pro výpis. Zatěžovat paměť a CPU tím, že vytvoříme 10K duplicitních hodnot jen kvůli výpisu, je zcela zbytečné.

Místo toho se pole předávají funkcím *by reference*. Tak říkáme funkci, kde v paměti již existující pole najde. Nevzniká žádná kopie a pracuje se přímo na originálních datech.

*By reference* se v C předává pomocí *ukazatele do paměti*. V případě pole nám ukazatel říká, kde najdeme jeho začátek.

Příklad:
```c
#include <stdio.h>

// 1. argument funkce je typu 'ukazatel na const int'
void print_arr_int(const int * arr, const size_t length) {
	for (size_t length = 0; i < length; i++) {
		printf("%d\n", arr[i]);
	}
}

int main() {
	int arr[4] = {1,2,3,4};
	print_arr_int(arr, 4);
}
```

Pole se při předávání chová jako ukazatel, nemusíme se již o nic starat.

## Tip: makra

Při práci s polem budeme často potřebovat uvádět jeho délku (cykly, funkce). Místo uvádění délky všude "na tvrdo" je lepší zvolit si nejaký zástupný symbol. K tvorbě takovýchto symbolů slouží makra preprocesoru a zavádějí se pomocí direktivy `#define`.

```c
#define ARR_LEN 10

int arr[ARR_LEN];
for (int i = 0; i < ARR_LEN; i++) {
	arr[i] = i;
}
```

Pokud se nyní rozhodneme, že chceme délku pole změnit, nemusíme ji přepisovat všude, kde ji používáme. Stačí změnit hodnotu v makru.