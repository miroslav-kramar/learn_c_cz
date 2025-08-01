# Funkce

## O co jde?

Veškerý kód, co napíšeme ve funkci `main`, můžeme bez problému vyjmout a vložit do našich vlastních funkcí. Funkce je ve své podstatě pojmenovaný blok funkčního kódu.

## Jak funkce vypadá?

Mějme třeba funkci `max`, která vrátí větší ze dvou celých čísel:

```c
int max(const int a, const int b) {
    if (a > b) {
        return a;
    }
    if (b > a) {
        return b;
    }
    return a;
}
```

Jak si můžeme všimnout, funkce se skládá ze dvou hlavních částí: hlavičky a těla.

V hlavičce najdeme:

- **návratový typ**

    Datový typ hodnoty, kterou funkce vrací.

- **jméno**

    Jméno funkce, pomocí kterého se na ni budeme odkazovat.

- **seznam parametrů**

    V našem případě máme dva parametry, oba celá čísla `a` a `b`. Funkce mohou mít tolik parametrů, kolik potřebujeme, klidně i žádný. Jejich datové typy jsou taktéž libovolné.

V těle najdeme:

- **kód funkce**

    Jednoduše popis toho, co funkce dělá. V našem případě porovnává parametry a jeden z nich vrací.

## Jak funkci použít?

Abychom funkci použili, musíme ji tzv. *zavolat*. Na funkce se volá stejně, jako na lidi: jménem. Součástí volání funkce je i předání parametrů.

```c
int main() {
    int a = 22;
    int b = 11;
    int m = max(a, b);
    printf("%d\n", m);
}
```

## Kíčové slovo `return`

Jak jste si mohli všimnout, naše funkce `max` ve svém těle několikrát využívá klíčového slova `return`. Jak název napovídá, slouží k vrácení hodnoty z funkce. Vrácenou hodnotou může být jak hodnota proměnné, tak i konstanta:

```c
float return_pi() {
    return 3.14159f;
}
```

Klíčové slovo `return` zároveň způsobí ukončení funkce. V každé funkci musí být vždy aspoň jednou, nejčastěji na konci. Jakýkoli kód uvedený po něm se nikdy neprovede:

```c
double multiply(double a, double d) {
    return a * b; // vrati soucin 'a' a 'b'
    return a + b; // nikdy se neprovede
}
```

## K čemu je to všechno dobré?

Hlavní výhodou funkcí je zpřehlednění zdrojového kódu, a pokud je funkce dostatečně obecná, tak i znovupoužitelnost. Než abychom kód zbytečně kopírovali, můžeme ho jednoduše vložit do funkce a odkazovat se na něj.

Dobrým příkladem znovupoužitelných funkcí je standardní knihovna funkcí jazyka C.

## Funkce VS Procedura

Existuje jeden speciální datový typ, o kterém jsme dosud nemluvili: `void`. Nemá žádnou velikost a nelze z něho vytvořit proměnnou, protože by do ní nešlo nic uložit.

Používá se ale jako návratový typ tzv. *procedur*, funkcí, co nic nevracejí:

```c
void pretty_print(const float f) {
    printf("%7.5f\n", f); // jak bude vypadat vystup?
}
```

Jak vidíte, klíčové slovo `return` by v tomto případě bylo poněkud zbytečné. Naštěstí si ho v tomto případě můžeme dovolit vynechat. Ale nic nám nebrání v tom ho použít:

```c
void pretty_print(const float f) {
    printf("%7.5f\n", f);
    return;
    printf("Hello!\n"); // nikdy neprobehne
}
```