---
title: Listan koon muuttuminen
permalink: /lista-append
hide: true
---
    
# Listan koon muuttuminen

Kun listan loppuun lisätään alkio metodilla `append`, aikaa kuluu $$O(1)$$ tai $$O(n)$$ riippuen siitä, voidaanko uusi alkio sijoittaa suoraan varatun muistialueen loppuun vai tuleeko ensin varata uusi muistialue ja siirtää listan vanha sisältö sinne.

Vaikka alkion lisääminen vie välillä aikaa $$O(n)$$, voidaan osoittaa, että aikaa kuluu _keskimäärin_ vain $$O(1)$$, jos uuden muistialueen varaaminen toteutetaan sopivalla tavalla. Yksi mahdollinen tapa on _kaksinkertaistaa_ muistialueen koko aina, kun muistia varataan lisää.

Tarkastellaan tilannetta, jossa listalle on lisätty yhteensä $$n$$ alkiota ja listalle on juuri varattu uusi muistialue. Tässä tilanteessa $$n$$ alkiota on siirretty kerran, $$n/2$$ alkiota on siirretty kahdesti, $$n/4$$ alkiota on siirretty kolmesti jne., joten yhteensä siirrettyjen alkioiden määrä on

$$n+n/2+n/4+n/8+\dots = O(n).$$

Koska listalla on yhteensä $$n$$ alkiota ja kaikkien siirtojen määrä on $$O(n)$$, kunkin alkion lisääminen on vienyt _keskimäärin_ $$O(1)$$ aikaa.

Yleisemmin jos varatun alueen koko $$c$$-kertaistetaan, siirrettyjen alkioiden määrä on

$$n+n/c+n/c^2+n/c^3+\dots = O(n),$$

kun $$c$$ on mikä tahansa vakio, joka on suurempi kuin $$1$$.

Pythonin referenssitoteutuksessa (CPython) vakio $$c$$ on noin $$9/8$$, mikä tarkoittaa, että muistialueen koko kasvaa melko hitaasti. Mitä hitaammin muistialueen koko kasvaa, sitä vähemmän ylimääräistä muistia listat vievät, mutta toisaalta sitä useammin listoilla olevia alkioita täytyy kopioida muistissa.
