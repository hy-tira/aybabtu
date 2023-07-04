---
title: 1. Johdanto algoritmeihin
slug: johdanto
#sections:
#  - Mikä on algoritmi?
---

# 1. Johdanto

Kurssin _Tietorakenteet ja algoritmit_ tavoitteena on syventää ohjelmointitaitoa
ja opettaa ajattelua ja tekniikoita, joiden avulla voi toteuttaa ohjelmia,
jotka toimivat oikein ja tehokkaasti kaikissa tilanteissa.

Tutustumme kurssin aiheisiin Python-kielen kautta, mutta suurin osa kurssin
asioista pätee myös muissa ohjelmointikielissä.
Kurssilla on tiedossa paljon ohjelmointia, minkä lisäksi käsittelemme myös
aiheeseen liittyvää teoriaa.

## Mikä on algoritmi?

_Algoritmi_ (_algorithm_) on menetelmä, jonka avulla voidaan ratkaista jokin tehtävä tietokoneella.
Kun algoritmi toteutetaan jollakin ohjelmointikielellä, se voidaan suorittaa tietokoneella.

Algoritmin _syöte_ (_input_) tarkoittaa, mitä lähtötietoja algoritmille annetaan.
Algoritmin _tuloste_ (_output_) puolestaan tarkoittaa, minkä vastauksen algoritmi antaa suorituksen jälkeen.
Python-kielessä algoritmi voidaan toteuttaa funktiona,
jolloin algoritmin syöte annetaan funktion parametreina ja
algoritmin tuloste on funktion palautusarvo.

Tarkastellaan esimerkkinä tehtävää, jossa algoritmille annetaan lista lukuja ja algoritmin
pitää laskea, moniko luku on parillinen.
Esimerkiksi jos lista on `[5, 4, 1, 7, 9, 6]`, haluttu vastaus on `2`,
koska luvut `4` ja `6` ovat parillisia.

Tämä tehtävä voidaan ratkaista algoritmilla, joka käy läpi listan luvut ja pitää muuttujassa yllä tietoa,
moniko luku on parillinen. Algoritmi voidaan toteuttaa seuraavasti Pythonilla funktiona `count_even`:

```python
def count_even(numbers):
    result = 0
    for x in numbers:
        if x % 2 == 0:
            result += 1
    return result
```

Funktiota voidaan testata seuraavan pääohjelman avulla:

```python
print(count_even([1, 2, 3])) # 1
print(count_even([2, 2, 2, 2, 2])) # 5
print(count_even([5, 4, 1, 7, 9, 6])) # 2
```

Tässä pääohjelmassa funktion toimintaa testataan kolmella eri listalla.
Jokaisen testin yhteydessä kommentissa lukee, mikä vastaus testistä pitäisi tulla.
Kun ohjelma suoritetaan, sen tulostus on seuraava:

```console
1
5
2
```

Tämän perusteella vaikuttaa siltä, että funktio toimii halutulla tavalla
eli olemme saaneet aikaan toimivan algoritmin tehtävään.

## Mikä on tietorakenne?

_Tietorakenne_ (_data structure_) on tapa pitää muistissa tietoa ohjelmassa.
Python-kielen tavallisimmat tietorakenteet ovat lista ja sanakirja.

Esimerkki listan käyttämisestä:

```python
numbers = [1, 2, 3, 4, 5]
print(numbers[2]) # 3
```

Esimerkki sanakirjan käyttämisestä:

```python
prices = {"omena": 2, "banaani": 5, "kaali": 1}
print(prices["omena"]) # 2
```

Tällä kurssilla perehdymme siihen, mihin yllä olevien tietorakenteiden
toiminta perustuu ja miten niitä kannattaa käyttää ohjelmoinnissa niin,
että koodista tulee tehokas.
Opimme toteuttamaan myös itse tietorakenteita, joita ei ole valmiina
Pythonissa eikä muissa kielissä.

## Algoritmin toteutus

Algoritmien toteuttamisessa on hyvä tietää, että minkä tahansa algoritmin
pystyy toteuttamaan ohjelmoinnin perusasioiden avulla.
Tällaisia perusasioita ovat:

* muuttujat
* ehdot (`if`)
* silmukat (`for`, `while`)
* listat
* funktiot
* luokat

Näiden lisäksi ohjelmointikielissä on usein paljon muita ominaisuuksia,
joiden avulla voi esimerkiksi tiivistää koodia mutta jotka eivät pohjimmiltaan
muuta koodin toimintalogiikkaa. Näitä ominaisuuksia voi käyttää
algoritmien toteuttamisessa, mutta niitä ilmankin pärjää mainiosti.

Tarkastellaan vielä äskeistä funktiota `count_even`,
joka on toteutettu käyttäen ohjelmoinnin perusasioita:

```python
def count_even(numbers):
    result = 0
    for x in numbers:
        if x % 2 == 0:
            result += 1
    return result
```

Tämän funktion voi toteuttaa selvästi tiiviimmin käyttämällä
Python-kielelle erityistä generaattorilauseketta:

```python
def count_even(numbers):
    return sum(x % 2 == 0 for x in numbers)
```

Tässä lausekkeen sisällä on for-silmukka, joka laskee jokaiselle listan
alkiolle lausekkeen `x % 2 == 0` arvon (`True` tai `False`).
Kun nämä arvot lasketaan yhteen `sum`-funktiolla, jokainen `True`-arvo
tulkitaan luvuksi `1` eli arvojen summa on yhtä suuri kuin parillisten
lukujen määrä.

Vaikka jälkimmäinen funktio on paljon lyhyempi, se kuitenkin tekee
pohjimmiltaan saman asian kuin ensimmäinen funktio.
Molemmat funktiot käyvät läpi listan luvut ja laskevat yhteen
parillisten lukujen määrän, eikä funktioissa ole eroa algoritmin
toimintalogiikan kannalta.

Ensimmäisen funktion etuna on, että se on helpompi ymmärtää henkilölle,
joka ei tunne Python-kielen erikoisominaisuuksia.
Funktion voisi toteuttaa samalla tavalla esimerkiksi JavaScriptilla:

```js
function countEven(numbers) {
    let result = 0;
    for (let x of numbers) {
        if (x % 2 == 0) result++;
    }
    return result;
}
```

Toisen funktion etuna on, että se on tiiviimpi ja sen voi ajatella olevan
enemmän Python-kielen tyylin mukainen.

## Algoritmin tehokkuus

Samaan tehtävän ratkaisemiseen on olemassa usein monia erilaisia algoritmeja,
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

_Aikavaativuus_ (_time complexity_) on matemaattinen tapa mitata
algoritmin tehokkuutta.
Aikavaativuus on hyödyllinen työkalu algoritmien suunnittelussa,
koska sen avulla pystyy arvioimaan nopeasti,
miten tehokkaasti algoritmi toimii.

Aikavaativuus ilmoitetaan yleensä $$O$$-merkinnän avulla niin,
että muuttuja $$n$$ kuvastaa syötteen kokoa.
Esimerkiksi jos syötteenä on lista, $$n$$ tarkoittaa listan kokoa,
ja jos syötteenä on merkkijono, $$n$$ tarkoittaa merkkijonon pituutta.

Tutustumme kurssin aikana pikkuhiljaa aikavaativuuden käsitteeseen.
Usein hyvä ajattelutapa on, että aikavaativuus ilmaisee,
montako sisäkkäistä syötteen läpi käyvää
silmukkaa algoritmissa on pahimmillaan.
Aikavaativuus $$O(n^k)$$ ilmaisee usein, että algoritmissa
on $$k$$ sisäkkäistä silmukkaa.

Esimerkiksi seuraavan funktion aikavaativuus on $$O(n)$$,
koska siinä on yksi silmukka, joka käy läpi listan sisällön.

```python
def count_even(numbers):
    result = 0
    for x in numbers:
        if x % 2 == 0:
            result += 1
    return result
```

Seuraavan funktion aikavaativuus on puolestaan $$O(n^2)$$,
koska koodissa on kaksi sisäkkäistä silmukkaa, jotka käyvät listaa läpi.

```python
def max_diff(numbers):
    result = 0
    n = len(numbers)
    for i in range(0, n):
        for j in range(i + 1, n):
            result = max(result, abs(numbers[i] - numbers[j]))
    return result
```

Jos algoritmissa ei ole yhtään silmukkaa vaan se suorittaa vain kiinteän
määrän komentoja, aikavaativuus on $$O(1)$$.
Esimerkiksi lukujen $$1 \dots n$$ summa voidaan laskea
tehokkaasti ajassa $$O(1)$$ seuraavasti:

```python
def sum_to_n(n):
    return n * (n + 1) // 2
```

Tämä algoritmi hyödyntää summakaavaa

$$1+2+\dots+n = \frac{n(n+1)}{2}.$$