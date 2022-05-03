# h5 Uusi komento 

Tehtävät tehty 3.5.2022 omalla henkilökohtaisella koneellani.

Pääkone:

*   Windows 10 Pro
*   32GB RAM
*   2TB SSD levytilaa

Jolla ajettuna virtuaalikone.

Virtuaalikoneen kokoonpano:

*   Oracle VirtualBox 6.1.32
*   Ubuntu 21.10
*   8192MB RAM
*   25GB levytilaa

*   Lisäksi asentamani Salt master ja Minion nimeltä Teronapuri.

### **a) Hei komento! Tee järjestelmään uusi "hei maailma" -komento ja asenna se orjille Saltilla. Liitä raporttiisi 'ls -l /usr/local/bin/' tulosteesta ainakin se rivi, jolla näkyy uuden komentotiedostosi oikeudet. Vinkkejä: tee shell script, joka tulostaa "hei maailma". Kokeile ensin käsin, sitten automatisoi. Luonteva paikka paketinhalllinnan ulkopuolelta asennetuille ohjelmille on /usr/local/bin/. Katso myös 'salt-call --local sys.state\_doc file.managed'. Muista (aina ja kaikessa mitä teet tietokoneella) testata lopputulos. Hyvä testi on mahdollisimman lähellä sitä, mitä käyttäjä tekisi.**

Ensimmäinen vaihe tehtävän tekemisessa on luoda uusi skripti "/usr/local/bin" kansioon.
Luodaan siis tiedosto.  `cd /usr/local/bin` ja `sudoedit heimaailma.sh` jonka sisälle rivi `echo "Hei Maailma"`.
Kokeillaan skriptin toimivuutta käskyllä: `bash heimaailma.sh` ja saadaan tuloste: **Hei maailma**.
Seuraavaksi pitäis muuttaa "heimaailma.sh" skriptin oikeuksia, niin että kaikki pystyvät sen suorittamaan. Käyttöoikeudet selviää tässä tapauksessa käskyllä: `ls -l /usr/local/bin/`  = **"-rw-r--r-- 1 root root 20 touko    3 13:17 heimaailma.sh"**.

Käskyllä `sudo chmod 755 /usr/local/bin/heimaailma.sh` saadaan oikeudet vaihdettua. Tarkistetaan uudet oikeudet tuolla jo ylenpänä esitellyllä käskyllä: `ls -l /usr/local/bin/` = **"-rwxr-xr--x 1 root root 20 touko    3 13:17 heimaailma.sh"** ja huomataan tulosteesta, että oikeudet ovat nyt muuttuneet. Nyt kaikilla pitäisi olla oikeus ajaa kyseinen skripti, mutta ei muokata sitä. 

Hei maailma on nyt testattu toimivaksi käsin ja käyttöoikeudet pitäisi olla kunnossa. Nyt voidaan luoda saltille tila. 
`cd /srv/salt` ja luodaan sinne kansio `sudo mkdir heimaailma2`  jonka sisälle luodaan saltille tila `sudoedit heimaailma2.sls`.


```
/usr/local/bin/heimaailma.sh:
  file.managed:
    - source: salt://heimaailma2/heimaailma.sh
    - mode: "0755"
```
heimaailman kopioimisen lisäksi, Teronapuri myös säätää käyttöoikeudet kuntoon, aivan kuten yllä tehtiin käsin.

Kopioidaan heimaailma.sh saltin kansioon `sudo cp /usr/local/bin/heimaailma.sh /srv/salt/heimaailma2`

Ajetaan tila: `sudo salt Teronapuri state.apply /heimaailma2/heimaailma2`

Vastaukseksi tuloste onnistuneesta tilasta.

--------

### **b) whatsup.sh. Tee järjestelmään uusi komento, joka kertoo ajankohtaisia tietoja; asenna se orjille. Vinkkejä: Voit näyttää valintasi mukaan esimerkiksi päivämäärää, säätä, tietoja koneesta, verkon tilanteesta...**

Luodaan orjille asennettavaaksi päivämäärän näyttävä komento. Komennolla `date` saadaan tulostettua päivämäärä, joten rakennetaan sen ympärille. 

Aloitetaan kuten äskeisessäkin tehtävässä, eli `cd /usr/local/bin`  ja luodaan sinne mikapaiva.sh `sudoedit mikapaiva.sh`.
mikapaiva.sh sisälle käsky `date` ja sille hieman tekstiä kaveriksi:
```
echo "Hei, kysyit mikä päivä tänään on. Tänään on:" 
  date
```
`bash mikapaiva.sh` voidaan kokeilla toimiiko komento. 
> Hei, kysyit mikä päivä tänään on. Tänään on:
> ti 3.5.2022 16.24.47 +0300

Tämän lisäksi luodaan srv/salt/mikapaiva kansioon tila paiva.sls

```
/usr/local/bin/mikapaiva.sh:
  file.managed:
     - mode "0755"
```
Kopioidaan mikapaiva.sh /usr/local/bin/ kansiosta saltille kansioon /srv/salt/mikapaiva.

ajetaan tila `sudo salt Teronapuri state.apply paiva` ja saadaan vastaukseksi onnistunut tilan ajo. 

Kokeillaan komentoa orjalla:  /srv/salt/mikapaiva$ `sudo salt Teronapuri cmd.run mikapaiva.sh `
> Teronapuri: 
> 	Hei, kysyit mikä päivä tänään on. Tänään on:
> 	Tue May  3 16:40:22 EEST 2022

Hieman erityylinen vastaus siis, mitä tuli ilman Teronapurilla suorittamista. Komento toimii kuitenkin.

-------

### **c) hello.py. Tee järjestelmään uusi komento Pythonilla ja asenna se orjille. Vinkkejä: Hei maailma riittää, mutta propellihatut saavat toki koodaillakin. Shebang on "#!/usr/bin/python3". Helpoin Python-komento on: print("Hei Tero!")**

Aloitetaan siitä missä aiemmissakin tehtävissä, luodaan tiedosto hei.py kansioon /user/local/bin.
Kirjoitetaan hei.py sisällöksi tehtävän annon mukaisesti seuraavat asiat:
```
#!/usr/bin/python3
print("Hei, hyvää päivää!")
```
Kokeillaan toimivuutta käskyllä: `pyhthon3 hei.py` ja saadaan vastaukseksi:
> Hei, hyvää päivää!

Siirretään kuten aiemmissakin tehtävissä hei.py saltin kansioon . `sudo cp /usr/local/bin/hei.py /srv/salt/hei/`

luodaan tila saltille:  `sudoedit hei.sls`:
```
python3: 
  pkg.installed
  
/user/local/bin/hei:
  file.managed:
    - source: salt://hei/hei.py
    - mode: "0755"
```
Tarkistetaan, että apurilla on pyhton asennettuna pkg.installed käskyllä. Mikäli ei ole, se asentuu. 
Asetetaan myös käyttöoikeudet kuntoon. 

Ajetaan tila: `sudo salt Teronapuri state.apply hei/hei`

Tuloste kertoi python3 olevan asennettuna ja tilan toimivan. 

Kokeillaan toimivuutta: `sudo salt Teronapuri cmd.run hei` ja saadaan vastaukseksi:
> Teronapuri: 
> 	Hei, hyvää päivää! 

Mikäli käyttöoikeudet eivät olisi kunnossa, olisi vastaus sisältänyt ilmoituksen "Permission denied" hyvänpäivän toivotuksen sijaan.

------------------------

### **d) Laiskaa skriptailua. Tee kansio, josta jokainen skripti kopioituu orjille. Vinkki: 'salt-call --local sys.state\_doc file.recurse'. Kun tämä on valmis, on todella helppoa laittaa orjille mikä tahansa yhden tiedoston shell script, Python-ohjelma, Perl-ohjelma, Go-binääri tai muu yhden binäärin ohjelma.**

Tehtävässä voidaan höydyntää aiempia kolmea tehtävää. Luodaan /salt/srv/ kansioon uusi kansio /kokoelma: `sudo mkdir /srv/salt/kokoelma` ja kopioidaan edellisten tehtävien tehtävät tuohon kansioon. 

Eli kopidaan yksitellen "projektit" heimaailma.sh, mikapaiva.sh ja hei tuohon /kokoelma kansioon. 

```
sudo cp /user/local/bin/ "projekti" /srv/salt/kokoelma
```
nyt tiedostot löytyvät kaikki /kokoelma kansion sisältä. 

Tehdään tilatiedosto `sudoedit kokoelma.sls`: 
```
/usr/local/bin/:
  file.recurse:
    - source: salt://kokoelma/
    - file_mode: "0755"
```
Kokeillaan ajaa tila: sudo salt Teronapuri state.apply kokoelma/kokoelma ja saadaan vastaukseksi onnistunut tilanajo. joka kertoo kokoelma.sls tidoston lisäyksestä /usr/local/bin hakemistoon ja käyttöoikeuksista mode: 0755. Koko kokoelma kansion tiedostojen siirtäminen siis onnistuu nyt. Mikäli jatkossa päivitän kokoelma kansioon lisää tavaraa, onnistuu myös näiden tiedostojen siirto jatkossa samalla tilalla. 

-----------




