# h4 Aikajana - Tehtävän palautus

**a) Captain obvious. Linuxissa on paketinhallinta, joten ohjelmien asentaminen on yksinkertaista. Tee tila, joka asentaa 10 suosikkiohjelmaasi paketinhallinnasta. Tässä a-kohdassa voit jättää ohjelmat oletusasetuksille**.

Tehtävän suorittemiseksi saltin avulla vaaditaan aiemmissa tehtävän palautuksissa tehty salt apurin ja masterin asentaminen. Mikäli salt apuri ja master on asennettu ja toimivat, voidaan tämä vaihe unohtaa. Lisäksi pitää keksiä 10 ohjelman lista ladattavia ohjelmia. Koska itse en käytä Linuxia tehtävien ulkopuolella juuri lainkaan, oma ohjelmien listani määräytyi melko sattumanvaraisesti. Listalta löytyy muutama Windospuolelta tuttu ohjelma kuten Audacity ja VLC player, muuten koitin pitää valittujen ohjelmien koon mahdollisimman pienenä, jotta asentaminen virtuaalikoneelle onnistuu. Omat asennettavat ohjelmani ovat. 1. Audacity, 2. M.A.R.S, 3. Micro editor, 4. Kspaceduel, 5. Mr. Rescue, 6. VLC, 7. FFmpeg, 8. Krop, 9. Remmina, 10.cpustat

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

Nyt kun käsin asennus ja poistaminen on kokeiltu, sekä pakettejen nimet kaivettu (tähän termi) avulla esille. voidaan siirtyä tilan luomiseen. 

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
