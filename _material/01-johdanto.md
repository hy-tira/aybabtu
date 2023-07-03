---
title: 1. Johdanto
slug: johdanto
sections:
  - Mikä on algoritmi?
  - Algoritmin toteutus
  - Algoritmin tehokkuus
  - Aikavaativuus
---

# 1. Johdanto

## Mikä on algoritmi?

_Algoritmi_ (_algorithm_) on menetelmä, jonka avulla voidaan ratkaista jokin tehtävä tietokoneella.
Kun algoritmi toteutetaan jollakin ohjelmointikielellä, se voidaan suorittaa tietokoneella.

Algoritmin _syöte_ (_input_) tarkoittaa, mitä tietoja algoritmille annetaan.
Algoritmin _tuloste_ (_output_) puolestaan tarkoittaa, minkä vastauksen algoritmi antaa suorituksen jälkeen.
Python-kielessä algoritmi voidaan toteuttaa funktiona,
jolloin algoritmin syöte annetaan funktion parametreina ja
algoritmin tuloste on sen palautusarvo.

Tarkastellaan esimerkkinä tehtävää, jossa algoritmille annetaan lista lukuja ja algoritmin
pitää laskea, moniko luku on parillinen.
Esimerkiksi jos lista on `[5, 4, 1, 7, 9, 6]`, haluttu vastaus on `2`,
koska luvut `4` ja `6` ovat parillisia.

Tämä tehtävä voidaan ratkaista algoritmilla, joka käy läpi listan luvut ja pitää muuttujassa yllä tietoa,
moniko luku on parillinen. Algoritmi voidaan toteuttaa seuraavasti Pythonilla funktiona `count_even`:

```python
def count_even(numbers):
    result = 0
    for number in numbers:
        if number % 2 == 0:
            result += 1
    return result
```

Funktiota voidaan testata seuraavan pääohjelman avulla:

```python
print(count_even([1, 2, 3])) # 1
print(count_even([2, 2, 2, 2, 2])) # 5
print(count_even([5, 4, 1, 7, 9, 6])) # 2
```

Pääohjelmassa funktion toimintaa testataan kolmella eri listalla.
Jokaisen testin yhteydessä kommentissa lukee, mikä vastaus testistä pitäisi tulla.
Kun ohjelma suoritetaan, sen tulostus on seuraava:

```console
1
5
2
```

Tämän perusteella vaikuttaa siltä, että funktio toimii halutulla tavalla
eli olemme saaneet aikaan toimivan algoritmin tehtävään.

## Algoritmin toteutus

TODO

## Algoritmin tehokkuus

Samaan tehtävään on olemassa usein monia erilaisia algoritmeja,
joiden tehokkuudessa voi olla eroja.
Usein tavoitteena on löytää tehokas algoritmi tehtävään,
jolloin tehtävä voidaan ratkaista nopeasti algoritmin avulla.

Tarkastellaan esimerkkinä tehtävää, jossa annettuna on lista lukuja
ja tavoitteena on laskea, mikä on suurin ero kahden luvun välillä.
Esimerkiksi kun lista on `[3, 2, 6, 5, 8, 5]`, haluttu vastaus on `6`,
koska suurin ero on lukujen `2` ja `8` välillä.

Seuraavassa on kolme algoritmia tämän tehtävän ratkaisemiseen:

{: .code-title }
Algoritmi 1
```python
def max_diff(numbers):
    result = 0
    n = len(numbers)
    for i in range(0, n):
        for j in range(i + 1, n):
            result = max(result, abs(numbers[i] - numbers[j]))
    return result
```

Tämä algoritmi muodostuu kahdesta for-silmukasta,
jotka käyvät läpi kaikki tavat valita listalta kaksi lukua.
Algoritmi laskee lukujen eron `abs`-funktion (itseisarvo) avulla
ja pitää muistissa tietoa, mikä on suurin löytynyt ero.

{: .code-title }
Algoritmi 2
```python
def max_diff(numbers):
    numbers = sorted(numbers)
    return numbers[-1] - numbers[0]
```

Tämän algoritmin ideana on, että suurin ero kahden luvun välillä
saadaan valitsemalla listan pienin ja suurin luku.

Algoritmi järjestää ensin listan sisällön `sorted`-funktion avulla.
Tämän jälkeen pienin luku on listan alussa ja suurin luku on listan lopussa,
joten algoritmin riittää palauttaa listan ensimmäisen luvun (indeksi `0`)
ja viimeisen luvun (indeksi `-1`) ero.

{: .code-title }
Algoritmi 3
```python
def max_diff(numbers):
    return max(numbers) - min(numbers)
```

Tässä on vielä toinen tapa toteuttaa äskeiseen ideaan perustuva algoritmi.
Listan järjestämisen sijasta algoritmi käyttää funktioita `min` ja `max`,
jotka palauttavat listan pienimmän ja suurimman alkion.

Algoritmin tehokkuutta voidaan tutkia testiohjelmalla,
joka antaa algoritmille tietyn syötteen ja mittaa sen suoritusajan.
Usein hyvä tapa on laatia testiohjelma niin, että se muodostaa
halutun kokoisen syötteen satunnaisesti.
Tämän avulla algoritmia voidaan testata helposti erikokoisilla syötteillä.

Seuraavassa on ohjelma, joka testaa funktion `max_diff` tehokkuutta:

```python
import random
import time

def max_diff(numbers):
    ...

n = 1000
print("n:", n)
random.seed(1337)
numbers = [random.randint(1, 10**6) for _ in range(n)]

start_time = time.time()
result = max_diff(numbers)
print("result:", result)
end_time = time.time()
print("time:", round(end_time - start_time, 2), "s")
```

Muuttujassa `n` annetaan testissä käytettävän listan pituus.
Funktio `random.seed` määrittää siemenluvun (tässä `1337`),
jonka ansiosta satunnaisluvut muodostetaan aina samalla tavalla.
Tästä on hyötyä, kun testi suoritetaan useita kertoja,
jolloin listan sisältö on aina sama.
Ohjelma luo funktiolla `random.randint` listan,
jossa on `n` satunnaista lukua väliltä `1` ja `10**6`.

Tämän jälkeen ohjelma mittaa funktion ajankäytön funktion `time.time` avulla.
Funktio antaa sekunteina kuluneen ajan vuoden 1970 alusta alkaen.
Kun tämä aika laitetaan talteen ennen funktion kutsua ja funktion
kutsun jälkeen, aikojen erotus kertoo, kauanko funktion suoritus vei aikaa.
Aika pyöristetään kahden desimaalin tarkkuudelle funktion `round` avulla.

Testiohjelman suoritus voi näyttää seuraavalta:

```console
n: 1000
result: 999266
time: 0.09 s
```

Tämä tarkoittaa, että algoritmin syötteenä oli `1000`-kokoinen lista,
algoritmi antoi tuloksen `999266` ja siihen meni aikaa `0.09` sekuntia.

Seuraava taulukko näyttää, paljonko äskeiset algoritmit vievät
aikaa erikokoisilla syötteillä testikoneella:

| Listan koko `n` | Algoritmi 1 | Algoritmi 2 | Algoritmi 3 |
| --- | --- | --- | --- |
| 1000 | 0.09 s | 0.00 s | 0.00 s |
| 10000 | 8.75 s | 0.00 s | 0.00 s |
| 100000 | -- | 0.01 s | 0.00 s |
| 1000000 | -- | 0.27 s | 0.02 s |

Taulukosta näkee, että algoritmien tehokkuudessa on suuria eroja.
Algoritmi 1 on hidas suurilla syötteillä, ja kaksi testiä keskeytettiin,
koska suoritus vei liikaa aikaa.
Algoritmit 2 ja 3 ovat sen sijaan tehokkaita myös suurilla syötteillä.

Tällä kurssilla tavoitteemme on oppia, mitkä tekijät vaikuttavat
algoritmin tehokkuuteen ja miten suunnitella tehokkaita algoritmeja.

## Aikavaativuus

TODO
