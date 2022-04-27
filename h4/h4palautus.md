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
*   Anna esimerkki aikajanasta
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


*   Selitä jokainen kohta komennosta, jolla aikajana tehdään. Vinkki: '%T+' löytyy 'man find' kohdasta printf.
*   Aja jokin komento, joka muuttaa järjestelmän yhteisiä asetustiedostoja
*   Ota uusi aikajana ja etsi muutos sieltä
*   Onko samalla hetkellä muutettu yhtä vai useampaa tiedostoa?


c)
