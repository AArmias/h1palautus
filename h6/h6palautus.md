# h6 Akkuna
--------------
### a) Suolaikkuna. Asenna Salt Windowsiin. Jos ehdit jo asentaa, voit kirjoittaa muistinvaraisesti, mutta muista silloin merkitä, että tämä on muistista kirjoitettu. Näytä testillä (test.ping, file.managed tms), että Salt toimii.

Ensimmäinen vaihe on ladata Saltin asennuspaketti osoitteesta https://repo.saltproject.io/#windows

(huom. Tuntitehtävien aikaan kävi ilmi, että mikäli linuxilla oleva salt master vanhempi salta versio kuin minkä asennat windowsille, mahdollisia yhteensopivuus ongelmia esiintyä. )

Aloitetaan avustettu saltin asentaminen ja edetään ohjeiden mukaisesti. Valitaan asennuksen sijainti ja tämän jälkeen annetaan Masteri IP tai Hostname. Tämän lisäksi nimetään Minion. Tämän jälkeen jatketaan asennusta, kunnes asennus sovellus kertoo asennuksen onnistuneen ja asennuksen olevan valmis. 

Kokeillaan toimivuutta komennolla: `salt-call --version` ja saadaan vastaus:
```
salt-call 3004.1

```
Tehdään vielä toinen testi: `salt-call --local test.ping` ja saadaan vastaus: 
```
local:
    True

```
-----------------
### b) Single. Näytä komentorivillä Saltilla (state.single) esimerkit funktioista file ja cmd.

esimerkki cmd. Annetaan käsky `salt-call --local cmd.run 'echo moi maailma'`
saadaan vastaukseksi:
```
local:
    moi maailma
```
------------
### e) Goal. Tee projektisi palautussivu. Voit tehdä sen GitHubiin, kotisivullesi tai mihin vain haluat. Mistä teet miniprojektin? Kuvaile miniprojektin tarkoitus lauseella tai parilla. Asenna käsin (jokin alustava osa) projektistasi ja ota ruutukaappaus siitä, miten lopputulosta käytetään. Tietysti pääset tekemään paremman ruutukaappauksen, kun projektisi on valmis. Valitse projektille lisenssi (suosittelen GPL 2, voit valita lisenssin vapaasti). Laita sivulle nimesi (tai jos haluat, nimimerkki, mutta suosittelen nimeä). Ja lähdekoodiksi vaikkapa vain Saltin hei maailma. Kirjoita ohje, miten projektisi otetaan käyttöön. Kirjoita projektin kypsyys näkyviin, tässä vaiheessa se on varmaankin alpha, eli vasta aloitettu eikä vielä voi varsinaisesti edes kunnolla testata. Yritä tehdä sivu, jossa tärkeimmät asiat näkyvät taitoksen yllä (skrollaamatta): tarkoitus, ruutukaapaus, lisenssi, nimesi, latauslinkki, kypsyysaste (alpha). Tässä vaiheessa projektin ei vielä tarvitse toimia, vaan kaikkiin osiin tehdään vielä parannuksia. Voit kirjoittaa englanniksi tai suomeksi, suosittelen englantia.

Tulevan projektin palautussivu löytyy tästä: https://github.com/AArmias/projektinimitulossa

-----------
### v) **Lue ja tiivistä** artikkeli muutamalla ranskalaisella viivalla. Tässä z-alakohdassa ei tarvitse siis tehdä testejä tietokoneella.

*   Karvinen 2018: [Control Windows with Salt](https://terokarvinen.com/2018/04/18/control-windows-with-salt/)

Artikkelissa avustetaan saltin asennus ja käyttöönotto windowsille. Artikkelista löytyvät tarvittavat linkit ja käskyt siihen, että käyttäjä pääsee alkuun asennuksen kanssa ja etenee aina siihen pisteeseen, että salt ja salt minion ovat käytettävissä windossilla. Käsykistä löytyy myös käskyjä asennuksen onnistumisen tarkistamiseksi, jotta voi varmistua siitä että kaikki toimii. Artikkelista löytää tämän lisäksi opastuksen windows puolella ohjelmien asennukseen saltin avulla, sekä ohjeen mionin asentamiseen windows serverille. 

----------------


Lähteet: 

Karvinen, Tero 2018: Control Windows with Salt. https://terokarvinen.com/2018/04/18/control-windows-with-salt Luettu: 4.5.2022

