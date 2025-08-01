# Datové typy

## Bity a byty...

... musí každý znát.

### Bit

Základní, dále nedělitelnou jednotkou informace je v počítači *bit*. Ten nabývá hodnoty 0 nebo 1. Fyzicky se jedná o paměťovou buňku, která kóduje hodnotu pomocí elektrického napětí.

### Byte

*Byte* je určitá N-tice bitů. V dávné minulosti se mohlo jednat o šestice nebo i dvanáctice. Dnes je však standardem, že 1 byte se skládá z 8 bitů. Prakticky se pracuje s bytem jako s celkem, přístup na individuální bity není obvyklý.

Vzhledem k tomu, že se jedná o osmici bitů, tak může nabývat 2^8^ (256) hodnot, 0 až 255.

## Proč datové typy?

Všechna data v paměti počítače mají stejnou podobu. Vše je nějaká sekvence jedniček a nul. Abychom takto zapsaným datům dali nějaký význam a byli schopni s nimi pracovat, potřebujeme datové typy.

## Co říkají datové typy?

Datové typy udávají mnoho informací o datech:

- **Kódování**

  Způsob, jakým se data zakódují jako sekvence 1 a 0. Stejná kombinace jedniček a nul pro jeden datový typ představuje jinou hodnotu, než pro jiný.

- **Velikost v paměti**

  Udávají, kolik bytů je potřeba, aby se daly zakódovat všechny hodnoty, které datový typ podporuje. Běžně se pohybuje od 1 do 8 bytů.

- **Přípustné hodnoty**

  Vycházejí z velikosti, jakou datový typ zabírá v paměti.

## Dělení datových typů

Datové typy se v C dělí na 3 hlavní kategorie:

- celočíselné datové typy (celá čísla)
- datové typy s plovoucí desetinnou čárkou (reálná čísla)
- ukazatele do paměti

## Celočíselné datové typy

Určené ke kódování celých čísel.

### Datový typ `int`

Z anglického *integer* (celé číslo).

Asi nejběžnější datový typ, s jakým přijdeme do styku.

V paměti 64bitových systémů zabírá z pravidla 32 bitů. Kolik je to bytů?

Rozsah hodnot se pohybuje od -2&nbsp;147&nbsp;483&nbsp;648 do 2&nbsp;147&nbsp;483&nbsp;647. Proč zrovna tato čísla?

Nejvýznamější bit ("ten nejvíc vlevo") se používá pro zakódování znaménka.

#### Varianty

- **`unsigned int`**

  Nejvýznamější bit se místo kódování znaménka používá pro kódování čísla. Výsledný rozsah hodnot je od 0 do 4&nbsp;294&nbsp;967&nbsp;295.

- **`short int`**
  
  Na 64bitovém systému zabírá zpravidla 16 bitů.

- **`long int`**
  
  V celém POSIXu (Linux, macOS, BSD,...) má na 64bitovém systému, dle očekávání, 64 bitů. Ovšem na jediném 64bitovém MS Windows má 32 bitů.

- **`long long int`**

  V 64bitovém POSIXu stejný, jako `long int`. Na 64bitovém MS Windows má 64 bitů.

"Znaménkovost" a modifikátor velikosti lze kombinovat, např. jako `unsigned long int`. K velkému zklamání `long short int` bohužel není validní kombinace.

### Datový typ `char`

Nejmenší datový typ, na všech systémech zabírá 1 byte.

Slouží k zápisu znaků (písmen, číslic, speciálních znaků, netisknutelných znaků).

Všechny znaky mají své odpovídající číselné kódy. Ty nejzákladnější specifikuje tabulka [ASCII](https://www.ascii-code.com/).

Ve výchozím stavu je znaménkový, tedy dovoluje hodnoty od -128 do 127. Pomocí modifikátoru `unsigned` získáme rozsah od 0 do 255.

### Datový typ `bool`

Reprezentuje jediný bit, logickou jedničku nebo nulu (`true`/`false`). V praxi ale zabírá celý byte, jelikož proměnným není možné vyčlenit jednotlivé bity v paměti.

V C je pro tento datový typ rezervováno klíčové slovo `_Bool`. Abychom mohli používat `bool`, musíme vložit knihovnu *stdbool.h*.

## Datové typy s plovoucí desetinnou čárkou

Pro kódování reálných čísel.

### Datový typ `float`

Standardně zabírá 32 bitů.

Obyčejný převod mezi binární a dekadickou soustavou není postačující. Často se stává, že i "krátké" desetinné dekadické číslo vyústí v binární soustavě v číslo s nekonečný rozvojem. Paměť počítače ale nekonečná není.

Kódování je proto složitější. Řídí se standardem [IEEE 754](https://en.wikipedia.org/wiki/IEEE_754).

Vzhledem k omezené paměti není možné reprezentovat všechna čísla zcela přesně.

### Datový typ `double`

Standardně zabírá 64 bitů.

Stejný, jako `float`, pouze s dvounásobnou přesností.

Existuje i varianta `long double`, která je definována na 80ti bitech. Na MS Windows má ovšem stejnou velikost, jako `double`.

## Ukazatele do paměti

Technicky vzato se jedná o celočíselný datový typ, nicméně jejich užití je natolik specifické, že je vhodné k nim přistupovat jako k extra kategorii.

Běžně mají stejnou velikost, jako je velikost registrů daného procesoru. Na 64bitové architektruře tedy budou zabírat všech 64 bitů.

Slouží k ukládání adresy v paměti. Datový typ v tomto případě přímo neovlivňuje ukazatel samotný, ale je podstatný při přístupu na adresu, na kterou ukazuje.