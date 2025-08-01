# Proměnné

Pokud je smyslem programu převádět vstupní data na výstupní, pak proměnné jsou prostředky pro uchování těchto dat během chodu programu. Jedná se o datový objekt, který zadržuje určitou hodnotu.

## Co říkají proměnné?

Proměnné mají tyto informace:

- Datový typ
  - A všechny jeho související informace
- Název
- Adresu v paměti
  - Kde v operační paměti proměnnou najdeme
- Aktuální hodnotu

## Deklarace

Deklarace znamená "oznámení". Oznamujeme tak překladači, že zavádíme proměnnou.

Program za běhu vyčlení proměnné blok paměti o velikosti odpovídající jejímu datovému typu.

Proměnné najdeme prakticky ve všech vyšších programovacích jazycích. Deklarace v jazyce C má následující strukturu:

`[datový typ] [název] = [literál];`

## Pravidla pro pojmenovávání

Jméno se může skládat pouze z malých a velkých písmen, čísel a podtržítka. První znak jména navíc **nesmí** být číslice.

I přes fakt, že překladač rozumí českým znakům, se v seriózních projektech před národními jazyky upřednostňuje angličtina. I my ji budeme upřednostňovat, proto se vyvarujte diakritice.

Která jména jsou správně a která ne?

`abcd AhOj tohle.je.promenna Dnesni_den 4krat3 OsmdesatNaDruhou e-3-47 _internal_variable ABCD1234 1234ABCD kramar@spsmb`

## Inicializace

Pokud během deklarace proměnné nastavíme hodnotu, hovoříme o ní jako o inicializované. V opačném případě proměnná inicializovaná není.

```c
int a = 1; // inicializovana
int b;     // neinicializovana
```

**POZOR:** Neinicializované proměnné mohou mít jakoukoli hodnotu z rozsahu jejich datového typu. Navíc výpočty s nimi představují *nedefinované chování*, jeden ze skrytých prohřešků v jazyce C.

## Literál

Jedná se o jakoukoli hodnotu, která je zapsána ve zdrojovém kódu přímo pomocí znaků.

Literály se používají k inicializaci proměnných a ve výpočtech.

Příklady jednotlivých literálů:

```c
int i                  = 1;
unsigned ui            = 1U;
long l                 = 1L;
unsigned long ul       = 1UL
long long ll           = 1LL;
unsigned long long ull = 1ULL;

char c                 = 'A';

float f                = 1.2f;
double d               = 3.14;
long double ld         = 2.71L;

char str[]             = "Hello, World!";
```

Mimochodem, `char` literály skutečně zastupují odpovídající číselnou hodnotu v tabulce ASCII, lze tak s nimi i počítat:

```c
char c = 'A' + 1; // 'B'
```
## Automatická konverze

V příkladu výše jste si mohli všimnout, že různé číselné typy mají různé literály. Ovšem v podstatě u všech jsou tyto varianty díky automatické konverzi datového typu dobrovolné.

Validní kód tak potom je např.:

```c
unsigned long long int ull = 1;
float f                    = 3.14;
char c                     = 65;
```

Jakému znaku odpovídá ASCII kód 65?

Automatická konverze však nefunguje pouze u inicializace, ale u všech výpočtů.

```c
float f = 1.2 - 1; // cca 0.2f
int i   = 3.14;    // 3
```

## Přetypování

Automatická konverze se ale neděje vždy, kdy bychom ji čekali. Např. tento výpočet vyústí v hodnotu `1.0f`, protože oba literály figurující ve výpočtu jsou typu `int`:

```c
float f = 3 / 2; // 1.0f
```

K řešení tohoto problému máme dvě možnosti. Buď z jednoho literálu uděláme floating-point literál:

```c
float f = 3.0f / 2; // 1.5f
```

A nebo ho přetypujeme:

```c
float f = (float) 3 / 2; // 1.5f
```

V tomto případě by asi bylo lepší změnit literál. Přetypování má však tu výhodu, že funguje i na výpočty s proměnnými:

```c
int a = 3;
int b = 2;
float f = (float) a / b; // 1.5f
```

Ve všech případech pro získání očekávaného výsledku stačí, aby byl jen jeden z figurantů výpočtu typu `float`.

## Konstanty: neměnné proměnné

Nejen při matematických výpočtech se nám stane, že budeme muset pracovat s nějakou konstantou: číselnou nebo jinou hodnotou, která bude vždy stejná. Pro tyto případy existuje klíčové slovo `const`, které proměnnou "zamkne" a znemožní nám ji měnit:

```c
const float PI = 3.14159f;
PI = 2.71828f // NELZE!
```

Hlavní výhodou klíčového slova `const` je zpřehlednění a zkvalitnění kódu. Jednak dáváme jednoduše najevo, že se jedná o konstantu. A jednak tuto konstantu nemůžeme omylem přepsat, čímž se vyvarujeme případných chyb.
