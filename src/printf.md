# Funkce `printf` pro začátečníky

Grafickým aplikacím se zatím věnovat nebudeme. Naší jedinou možností, jak interagovat s uživatelem, potom je textové rozhraní konzole. Jednou z funkcí, která dokáže vypsat text do konzole, je právě funkce `printf` ze standardní knihovny pro textový vstup a výstup *stdio.h*.

## Jak funkce funguje?

Funkce `printf` vypisuje *formátovaný* text do konzole. Jejím prvním argumentem je tzv. *formátovací string*:

```c
printf("Hello, World!\n");
```

Toto volání funkce `printf` vyústí ve vypsání zadané zprávy "Hello, World!" do konzole.

## Formát?

Na předchozím textu zadaného do funkce k vytisknutí není nic zvláštního. Funkce `printf` však neumí přijímat pouze text k výpisu, ale i libovolný počet dalších parametrů. Tyto parametry navíc mohou mít jakýkoli základní datový typ:

```c
printf("I am %d years old.\n", 23);
```

Zde již můžeme vidět formátovací string v akci. *Specifikátor* `%d` znamená, že si přejeme vytisknout nějaké celé číslo v desítkové soustavě (*d* jako *decimal*). Skutečné číslo k vytisknutí se uvede jako další argument. Výstup do konzole, dle očekávání, poté vypadá nějak takto:

`I am 23 years old.`

To ale není nic zajímavého. Věk jsme mohli stejně tak dobře napsat přímo do formátovacího řetězce. Skutečná síla funkce `printf` se projeví při použití proměnných:

```c
int age = 23;
printf("I am %d years old.\n", age);
```

Zde může hodnota proměnné `age` nabývat jakékoli hodnoty, dokonce se i měnit. Funkce `printf` při zavolání její aktuální hodnotu dostane a jelikož znovu uvádíme, že ji chceme vytisknout jako celé číslo, tak se tak i stane:

`I am 23 years old.`

## A co další datové typy?

Jak již bylo řečeno, funkce `printf` umí vypsat všechny základní datové typy a i typy z nich odvozené. Pár příkladů:

```c
printf("%d\n", 1);
printf("%f\n", 1.2f);
printf("%c\n", 'A');
printf("%c\n", 65);  // stejne, jako 'A'
printf("%s\n", "Hello, World!");
```

Vylistovat všechny podporované specifikátory je nad mé síly. Místo toho doporučuji nahlédnout např. do některé z [online dokumentací](https://cplusplus.com/reference/cstdio/printf/) nebo, pokud jste na POSIXu, do lokálních manuálových stránek:

```bash
$ man printf.3
```

### Specifikátor délky a znaménkovosti

Nejen různé varianty datového typu `int` mají také své specifikátory:

```c
printf("%u\n",   1U);   // unsigned
printf("%ld\n",  1L);   // long
printf("%lu\n",  1UL);  // unsigned long
printf("%lld\n", 1LL);  // long long
printf("%llu\n", 1ULL); // unsigned long long

printf("%lf\n", 1.2L);  // double
```

Jeden z odvozených základních datových typů, se kterým často přijdeme do styku, je `size_t`, schopen pojmout informaci o velikosti jakéhokoli objektu. Jeho formátový specifikátor je trochu kryptický, proto si ho dovoluji uvést extra:

```c
printf("%zu\n", sizeof(int));
```

## Další možnosti formátování

Funkce `printf`, co se formátování textu týče, je skutečné kladivo. Vylistovat všechny možnosti je opět nad mé síly, proto si dovolím ukázat jen ty nejpraktičtější:

```c
printf("%3d\n",   1);       // "  1"
printf("%03d\n",  1);       // "001"
printf("%.2f\n",  3.14159); // "3.14"
printf("%6.2f\n", 3.14159); // "  3.14"
```