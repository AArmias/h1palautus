# h4 Aikajana - Tehtävän palautus

**a) Captain obvious. Linuxissa on paketinhallinta, joten ohjelmien asentaminen on yksinkertaista. Tee tila, joka asentaa 10 suosikkiohjelmaasi paketinhallinnasta. Tässä a-kohdassa voit jättää ohjelmat oletusasetuksille**.

Tehtävän suorittemiseksi saltin avulla vaaditaan aiemmissa tehtävän palautuksissa tehty salt apurin ja masterin asentaminen. Mikäli salt apuri ja master on asennettu ja toimivat, voidaan tämä vaihe unohtaa. Lisäksi pitää keksiä 10 ohjelman lista ladattavia ohjelmia. Koska itse en käytä Linuxia tehtävien ulkopuolella juuri lainkaan, oma ohjelmien listani määräytyi melko sattumanvaraisesti. Listalta löytyy muutama Windospuolelta tuttu ohjelma kuten Audacity ja VLC player, muuten koitin pitää valittujen ohjelmien koon mahdollisimman pienenä, jotta asentaminen virtuaalikoneelle onnistuu. Omat asennettavat ohjelmani ovat. 1. Audacity, 2. Micro editor, 3. Kspaceduel, 4. M.A.R.S Shooter. 5. Mr. Rescue, 6. VLC, 7. FFmpeg, 8. Krop, 9. Remmina, 10.cpustat

Nyt kun ohjelmat ovat valittu, Salt apurit ja masterit kunnossa on seuraavaksi vuorossa ohjelmien käsin asentaminen ja kokeileminen. 
Kun tämä vaihe on tehty, voidaan siirtyä seuraavaan vaiheeseen, eli tilan luomiseen. 

ohjelmien asentaminen
```
sudo apt-get install "ohjelma" 
```
ohjelmien poistaminen 
```
sudo apt-get remove "ohjelma"
```

Nyt kun käsin asennus ja poistaminen on kokeiltu, sekä pakettejen nimet kaivettu aikajanan avulla esille. voidaan siirtyä tilan luomiseen. 
Asennetut paketit tarkistin  /etc hakemistosta komennolla:  `sudo find -printf '%T+ %p\\n'|sort|tail`

Aluksi luodaan tila.sls tiedosto kansioon /srv/salt. 

Sen jälkeen annetaan tilalle käskyjä alkaa asentamaan paketteja. Käskyjen antaminen onnistuu kirjoittamalla ne vaikkapa nano tai micro editorilla tila.sls tiedostoon.
```
install audacity:
  pkg.installed:
    - name: audacity
install micro:
  pkg.installed:
    - name: micro
install kspaceduel:
  pkg.installed:
    - name: kspaceduel
install marsshooter:
  pkg.installed:
    - name: marsshooter
install mrrescue:
  pkg.installed:
    - name: mrrescue
install vlc:
  pkg.installed:
    - name: vlc
install ffmpeg:
  pkg.installed:
    - name: ffmpeg
install krop:
  pkg.installed:
    - name: krop
install remmina:
  pkg.installed:
    - name: remmina
install cpustat:
  pkg.installed:
    - name: cpustat
```
Kun tiedosto on valmis annetaan salt apurin, tässä tapauksessa Teronapurin hoitaa tilan ajaminen käskyllä:
```
sudo salt Teronapuri state.apply tila
```
Koska asennettavia ohjelmia on 10 kappaletta, asennuksella kestää hetken, jos toisen. Lopulta salt ilmoittaa tapahtuneet muutokset ja perään onnistuneiden ja epännistuneiden käskyjen määrän. Koska olin tarkistanut käsin jokaisen asennuspaketin nimen, tällä kertaa kaikki paketit asentuivat ensimmäisellä yrityksellä. 

> Summery for Teronapuri
>Succeeded: 10 (changed=10)
> Failed:          0
> Total states run:                10

**b ) CSI Pasila. Tiedostoista saa aikajanan 'cd /etc/; sudo find -printf '%T+ %p\\n'|sort|tail'.**
*   **Anna esimerkki aikajanasta**
> tero@tero-VirtualBox:~$ sudo find -printf '%T+ %p\n'|sort|tail
> 2022-04-27+13:02:34.3687625580 ./snap/firefox/common/.mozilla/firefox/i02d7p3o.default/datareporting/session-state.json
> 2022-04-27+13:02:34.5007616280 ./snap/firefox/common/.mozilla/firefox/i02d7p3o.default/datareporting
> 2022-04-27+13:02:34.5007616280 ./snap/firefox/common/.mozilla/firefox/i02d7p3o.default/datareporting/aborted-session-ping
> 2022-04-27+13:02:52.9886881180 ./snap/firefox/common/.mozilla/firefox/i02d7p3o.default/xulstore.json
> 2022-04-27+13:02:55.9648415930 ./snap/firefox/common/.mozilla/firefox/i02d7p3o.default/broadcast-listeners.json
> 2022-04-27+13:03:06.4852954320 ./snap/firefox/common/.mozilla/firefox/i02d7p3o.default/storage/permanent/chrome/idb
> 2022-04-27+13:03:58.9744069050 ./snap/firefox/common/.cache/event-sound-cache.tdb.tero-VirtualBox.x86_64-pc-linux-gnu
> 2022-04-27+13:04:08.9505164870 ./snap/firefox/common/.mozilla/firefox/i02d7p3o.default/prefs.js
> 2022-04-27+13:04:08.9625166110 ./snap/firefox/common/.mozilla/firefox/i02d7p3o.default
> 2022-04-27+13:04:52.2188735530 ./snap/firefox/common/.mozilla/firefox/i02d7p3o.default/datareporting/glean/db/data.safe.bin

Esimerkki aikajanasta, jossa näkyvissä käynnissä olevan firefoxin jatkuvasti käynnissä/käytössä ollessaan tekemiä muutoksia, aika järjestyksessä. 


*   **Selitä jokainen kohta komennosta, jolla aikajana tehdään. Vinkki: '%T+' löytyy 'man find' kohdasta printf.**

**sudo** = suoritetaan komento järjestelmänvalvojana / pääkäyttäjänä. Mikäli find haku tehdään /etc kansiossa ilman sudo komentoa mitä todennäköisimmin tulee ilmoitus, että osan alikansion kahdalla lupa haulle on evätty. Osassa kansiossa find haku onnistuu ilman sudo komentoakin. 

 **find** = Todella tehokas haku käsky, kolla on olemassa todella suuri määrä lisä parametreja joilla määrittää mitä tietoa haluaa hakea. 
 käskyllä `man find` saa luettavaksi täydelliset ohjeet eri parametreista joita on käytettävänä. Tiedostoja voi hakea mm. koon mukaan jolloin voi määritellä esimerkiksi haetaanko kaikki alle 5mb tiedostot vai kaikki yli 5mb tiedostot. Voit hakea kaikki .php tiedostot, mikäli et muista tiedoston tarkkaa nimeä, mutta kuitenkin minkä tyyppisestä tiedostosta on kyse. Haku mahdollisuuksia on siis todella laajasti. 

**-printf **= Määrittää miten haku tulostetaan ruudulle. -printf käskyn lisäksi voidaan antaa -printf käskylle lisäparametreja, joilla muotoilla tapaa jolla haku tulostetaan näytölle. 

**'%T+** =  %t = hakee viimeisimmät muokatut tiedostot, tulkitseminen kuitenkin on hankalempaan.  %T+ parametrilla tuodaan tuohon hakuun lisää selkeyttä, ja määritellään tulostuksen alkamaan vuosi-kuukausi-päivä+kello ja vasta sitten polku ja tiedostonimi. Näin hakua on helpompi tulkita ja lukea. 

**%p** = tiedoston nimi ja polku.

**\n**  = uusi rivi. jaa haun riveille, muuten haku tulisi yhtenä isona pötkönä. 

**sort **= määrittää missä järjestyksessä tiedostot tulostetaan näkyville.

**tail** =  Mikäli tiedostopolku on pitkä, saadaan tail komennolla siitä tulostettua vain viimeiset 10 riviä. Tämä tekee haun tulosteen lukemisesta huomattavasti helpompaa. 


*   Aja jokin komento, joka muuttaa järjestelmän yhteisiä asetustiedostoja
Muutin Micro editorin väriteemaa editorissa käskyllä:
ctrl + e ja `set colorscheme gotham`

*   Ota uusi aikajana ja etsi muutos sieltä
> tero@tero-VirtualBox:~$ sudo find -printf '%T+ %p\n'|sort|tail
> 2022-04-27+14:01:57.0469816820 ./snap/firefox/common/.cache/mozilla/firefox/i02d7p3o.default
> 2022-04-27+14:02:08.4590187510 ./snap/firefox/common/.cache/mozilla/firefox/i02d7p3o.default/thumbnails
> 2022-04-27+14:02:08.9550203600 ./snap/firefox/common/.mozilla/firefox/i02d7p3o.default/prefs.js
> 2022-04-27+14:02:08.9710204100 ./snap/firefox/common/.mozilla/firefox/i02d7p3o.default
> 2022-04-27+14:02:34.5511036390 ./snap/firefox/common/.mozilla/firefox/i02d7p3o.default/datareporting/archived/2022-04
> 2022-04-27+14:02:34.5511036390 ./snap/firefox/common/.mozilla/firefox/i02d7p3o.default/datareporting/archived/2022-04/1651057354532.9ddc5a73-3840-494b- 9e03-417a5b00c6b5.event.jsonlz4
> 2022-04-27+14:03:18.0912462220 ./snap/firefox/common/.mozilla/firefox/i02d7p3o.default/cookies.sqlite-wal
>**2022-04-27+14:05:06.6956063670 ./.config/micro/settings.json**  <- TÄÄLLÄ
> 2022-04-27+14:05:21.9556574500 ./.config/micro/buffers/history
> 2022-04-27+14:06:02.9517951630 ./snap/firefox/common/.mozilla/firefox/i02d7p3o.default/datareporting/glean/db/data.safe.bin

**2022-04-27+14:05:06.6956063670 ./.config/micro/settings.json** riviltä löytyy micron asetukset, jonne kyseinen väriteeman muutos tallennettiin. 


*   Onko samalla hetkellä muutettu yhtä vai useampaa tiedostoa?
Kuten find tuloste kertoo, samalla hetkellä muokattiin vain tuota yhtä tiedostoa. 


c)  **Tiedän mitä teit viime kesän^H^H^H komennolla. Säädä jotain ohjelmaa ja etsi sen muuttamat tiedostot aikajanasta. Tee sitten tästä oma Saltin tila**



