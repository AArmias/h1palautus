h2 kotitehtävien palautus
Tehtävät tehty 12.4.2022 omalla henkilökohtaisella koneellani.

Pääkone:

*   Windows 10 Pro
*   32GB RAM
*   2TB levytilaa

Jolla ajettuna virtuaalikone.

Virtuaalikoneen kokoonpano:

*   Oracle VirtualBox 6.1.32
*   Ubuntu 21.10
*   8192MB RAM
*   25GB levytilaa

+ Lisäksi h1 läksyissä asentamani Salt master ja Minion nimeltä Teronapuri.




**a) Oletussivu. Vaihda Apachen oletussivu päällekirjoittamalla /var/ww/html/index.html . Voit käyttää pohjana tunnilla tekemääsi Apache-asennusta.**

Kuten tehtävän annossa vinkattiin, käytin apuna tehtävän ratkaisuun kurssimateriaalista löytyvää apache materiaalia. Aloitin lähestymisen luomalla myöhemmin tarvittavan oletussivun. sijainti on **/srv/salt/apache/**  ja tiedosto **default-index.html**  tiedosto tulee sisältämään tekstin ”Katohan, teretulemast!” jonka pitäisi korvata apachen oletussivu, mikäli tehtävä onnistuu. 

Seuraavaksi käytetään apuna kurssimateriaaleja ja tehdään Saltille ajettavaksi **init.sls** ja sijaintiin **/srv/salt/apache/**. 

Annetaan init.sls seuraavat tiedot:

_apache2:_
_pkg.installed_
_/var/www/html/index.html:_
_file.managed:_
  _- source: salt://apache/default-index.html
/etc/apache2/mods-enabled/userdir.conf:
file.symlink:_
  _- target: ../mods-available/userdir.conf
/etc/apache2/mods-enabled/userdir.load:
file.symlink:_
   _- target: ../mods-available/userdir.load
apache2service:
service.running:_
   _- name: apache2_
   _- watch:_
     _- file: /etc/apache2/mods-enabled/userdir.conf
     - file: /etc/apache2/mods-enabled/userdir.load_


Saltin eli Teronapurin tulisi korvata ajettaessa apachen alkuperäinen oletussivu, tuolla aiemmin tehdyllä **index.html** tiedostolla.

Käskytetään Teronapurille tuo nyt luotu init.sls.
”sudo salt ’*’ state.apply apache”

Vastauksesta voidaan löytää seuraavat tiedot:
”File /var/www/html/index.html updated”
sekä Diff: huomioiden alta, ”Katohan, teretulemast!” 

Tästä voidaan jo alustavasti päätellä tehtävän onnistuneen. 

Varmistus onnistuneesta tehtävästä saadaan käynnistämällä Firefox ja tuo oletussivu näkyviin käskyllä: ”**firefox "http://localhost"** ”

Nopealla tarkistuksella, muutettu teksti paistaa valkoiselta pohjalta kauniisti. Tehtävä apachen oletussivun muuttamisesta onnistui. 

**b) Tri Kaaaos. Aiheuta erilaisia vikatilanteita ja osoita, kuinka Apache-tilasi korjaa ne. Voit esimerksi sulkea demonin (sudo systemctl stop foobar), poistaa asetukset tai poistaa apachen paketit. Osoita yksinkertaisin testein, saat palvelun toimimattomaksi, ja salt-tilasi saa sen jälleen toimimaan.**

Tehtävä b on taas sellaisia tehtäviä, jotka ovat itselle todella hankalia lähestyä. Koska asioiden saaminen toimimaan ohjeilla on haasteellista, on melko mahdoton rikko niitä tarkoituksella. Pitäisi olla huomattavasti enemmän tietoa siitä, miten asia toimii, jotta sen osaisi tarkoituksellisesti rikkoa tai sabotoida. En kykene siis valitettavasti tehtävään kehittämään yhtään keinoa sabotoida hommaa.

**c) Shh! Asenna ja konfiguroi SSH-demoni. Laita se porttiin 7373.**

Tehtävä listan ainoa tehtävä, missä oli selkeä malli miten toimitaan. Olen huomannut, että koska käyttöjärjestelmä, kieli ja opeteltavat asiat ovat kaikki itselle vieraita. On todella vaikea tuntien jälkeen palata asioihin. Suurin osa kuitenkin opetuksen sisällöstä tapahtuu itse videokonferenssin aikana, jolloin ohjeistuksena on vain kuunnella ja olla tekemättä asioita. Jälkeenpäin tuota opetusta ei kuitenkaan voi enää katsoa uusintana ja tehdä samalla, mallien mukaan. Itselle mallien mukaan tekeminen on selvästi parasta tapa oppia, varsinkin jos vielä samalla asia selitetään miksi näin teemme. Tehtävässä c on selkeät mallit joiden mukaan toimia, joten itse tehtävän tekeminen ei sinällään tuottanut ongelmia. 

Kurssimateriaalista löytyy selkeät ohjeet askel askeleelta, jonka ohjeistuksella tälläinen ummikkokin onnistuu SSH-Demonin asentamisessa. 

Aluksi loin **/srv/salt/** kansioon tiedoston **sshd.sls** käskyllä ”**sudoedit /srvsalt/sshd.sls**” jonka sisälle kurssimateriaalin mukaan annoin seuraavat tiedot: 
_openssh-server:_
 _pkg.installed_
_/etc/ssh/sshd_config:
 file.managed:_
   _- source: salt://sshd_config
sshd:_
 _service.running:_
   _- watch:_
    _- file: /etc/ssh/sshd_config_

Seuraavaksi loin tiedoston sshd_config käskyllä “**sudoedit /srvsalt/sshd_config**”
ja määritin seuraavat tiedot tehtävän ja kurssimateriaalin mukaisesti: 
_Port 7373
Protocol 2
HostKey /etc/ssh/ssh_host_rsa_key
HostKey /etc/ssh/ssh_host_dsa_key
HostKey /etc/ssh/ssh_host_ecdsa_key
HostKey /etc/ssh/ssh_host_ed25519_key
UsePrivilegeSeparation yes
KeyRegenerationInterval 3600
ServerKeyBits 1024
SyslogFacility AUTH
LogLevel INFO
LoginGraceTime 120
PermitRootLogin prohibit-password
StrictModes yes
RSAAuthentication yes
PubkeyAuthentication yes
IgnoreRhosts yes
RhostsRSAAuthentication no
HostbasedAuthentication no
PermitEmptyPasswords no
ChallengeResponseAuthentication no
X11Forwarding yes
X11DisplayOffset 10
PrintMotd no
PrintLastLog yes
TCPKeepAlive yes
AcceptEnv LANG LC_*
Subsystem sftp /usr/lib/openssh/sftp-server
UsePAM yes_

Seuraavaksi oli ohjeessa tilan lisääminen salt orjalle eli Teronapurille 
Käskyllä ” **sudo salt '*' state.apply sshd**” alkoi heti tapahtua, ruudulle ilmestyi vino pino tekstiä, mutta tärkeinpänä vastaukset onnistunseesta muutoksesta. 

**_ID: sshd
Function: service.running
Result: True_**
 
**_Summery of Teronapuri_**

**_Succeeded 3 (changed=3)
Failed 0_**

**_Total states run: 3_**

      

**z) Lue ja tiivistä, muutama ranskalainen viiva riittää.**

**SaltStack Configuration Management: Get Started Tutorial – artikkelit.** 

- **Introduction:** Tiivistää keskeisimmän sisällön kyseessä olevasta Configuration Management tutoriaalista.
Lisäksi listaa aiemmassa tutoriaalissa opitut asiat, jotka tulisi tietä koskien Saltien käskyttämistä. 

- **Function:**  Käy läpi Saltin state functioita esimerkiksi. Paketin asentamisen, kansion luomisen, palvelun käynnistämisen,  palvelun käynnistämisen uudelleen käymistämisen jälkeen, Git repon lataamisen, jne… 

- **Files:** Käy läpi Saltin tiedoston hallintaa ja Saltin omaa tapaa käsitellä tiedostoja Salt:// urlin kautta. 

- **Karvinen 2008: Install Apache Web Server on Ubuntu:**
Käy läpi Apachen asentamisen tarpeellisimmat käskyt. Näillä käskyillä jopa ummikko onnistuu asentamisessa. Tärkeinpänä käskynä varmasti: ”sudo apt-get install apache2”

- **Apache User Homepages Automatically – Salt Package-File-Service Example:**
Opastaa miten saadaan Salt päivittämään apachen oletussivut automaattisesti. 

- **Pkg-File-Service – Control Daemons with Salt – Change SSH Server Port:**
Opastetaan asentamaan SSH-demoni ja määrittämään tälle portti, Saltin avulla. 

- **SaltStack contributors 2021: Salt system architecture:**
Artikkeli pyrkii avaamaan Saltin systeemi arkkitehtuuria. Esimerkiksi masterin eri toimintoja ja minionin taipuvuutta useilla eri alustoilla. Artikkeli myös avaa hieman sitä mikä Salt on ja mihink käyttötarkoituksiin sitä voidaan esimerkiksi käyttää.


**Lähteet**

Karvinen, Tero 2018: Apache User Homepages Automatically – Salt Package-File-Service Example. https://terokarvinen.com//2018/apache-user-homepages-automatically-salt-package-file-service-example/ Luettu 12.4.2022

Karvinen, Tero 2018: Pkg-File-Service – Control Daemons with Salt – Change SSH Server Port. https://terokarvinen.com//2018/pkg-file-service-control-daemons-with-salt-change-ssh-server-port/ Luettu 12.4.2022

Karvinen, Tero 2008: Karvinen 2008: Install Apache Web Server on Ubuntu. https://terokarvinen.com/2008/05/02/install-apache-web-server-on-ubuntu-4/ Luettu 12.4.2022

Karvinen, Tero 2021: Configuration management systems 2022. https://terokarvinen.com/2021/configuration-management-systems-2022-spring/ Luettu 3.4.2022
