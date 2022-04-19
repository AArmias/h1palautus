# h3 Versionhallinta - kotitehtävän palautus

a) Tämä tehtävä on tehty MarkDownina virtuaalikoneelta omalle Github-tililleni. 
Ainoastaan Github kansio ja h3Versionhallinta tiedosto, on luotu etukäteen githubin puolelle, kaikki muut muutokset tapahtuvat MarkDownina, esimerkiksi tämä tekstin lisäys. 

Jotta pääsiin alkuun piti ensiksi luoda tili Githubiin ja kytkeä virtuaalikone ja github toimimaan yhdessä julkista SSH avainta hyödyntäen. 
Tämä mahdollistaa jatkossa muutoksien tapahtumisen myös Github varastossani. Tämän lisäksi tuli git versionhallinnan käyttäjänimi ja sähköpostiosoite asettaa kuntoon. 

git config toimii seuraavasti: 
	git config --global user.name "käyttäjänimi"
	git congig --global user.email "sähköpostitunnus@sähköposti.fi"


Lisäksi Githubiin luotu git kansio pitää kloonata koneelle:
	git clone git@github.com:AArmias/palautukset.git


Näin ollen perusasetukset on kunnossa ja voin jatkossa päivittää git varastoani molempiin suuntiin. 

Tehdessäni muutoksia git kansiooni, pitää muistaa aina järjestys. Ensiksi pitää vetää eli git pull ja kun tiedot ovat virtuaalikoneella ajantasalla, voidaan tehdä tarvittavat muutokset, committaa ne ja sen jälkeen työntää tiedosto takaisin githubin varastoon git push komennolla.

b) Lisäsin nano editorilla tähän palautukseen otsikon, tekstiä ja tämän kuvauksen tulevasta commitista. Tehtävän ohjeena on tehdä yksi selkeä  commit, koskemaan useampaa muutosta.
Commitin tekeminen onnistuu käskyllä:
	git add -A
	git commit
Jonka jälkeen aukeaa editori johon tuon commitin voi kirjoittaa.
commit jonka annan on "Add Header, text and code"

c) 
git log käsky:
	tero@tero-VirtualBox:~/palautukset/h3$ git log
commit 66a82cb4ddbf385c9f77c5339c168b4e1f654167 (HEAD -> main, origin/main, origin/HEAD)
Merge: f4c8f2c a9faef7
Author: Tero S <tero.höpöhöpö@gposti.fi>
Date:   Tue Apr 19 20:21:58 2022 +0300

    Add Header, text and code

commit a9faef728fdb30ef0567dd6e08a46b09b330aba2
Author: AArmias <102689055+AArmias@users.noreply.github.com>
Date:   Tue Apr 19 20:15:23 2022 +0300

    Delete h3 Versionhallinta

commit aa2fc71b6d454d2e771b9369459cde3de3ad03fa
Author: AArmias (NotesHub App) <contact@noteshub.app>
Date:   Tue Apr 19 20:12:53 2022 +0300

Antamalla "git log" käskyn, saan koko versiohistorian kaikkineen muutoksineen koskien palautukset kansion gitejä. Pystyn näkemään niin editoidut, luodut kuin poistetutkin tiedot. Myös sen kuka tämän on tehnyt ja onko asiasta jätetty commit.

git diff käsky:

	tero@tero-VirtualBox:~/palautukset/h3$ git diff
diff --git a/h3/h3_Versionhallinta.md b/h3/h3_Versionhallinta.md
index 0686240..09e5471 100644
index 0686240..09e5471 100644
--- a/h3/h3_Versionhallinta.md
+++ b/h3/h3_Versionhallinta.md
@@ -1,6 +1,6 @@
 # h3 Versionhallinta - kotitehtävän palautus
 
-Tämä tehtävä on tehty MarkDownina virtuaalikoneelta omalle Github-tililleni. 
+a) Tämä tehtävä on tehty MarkDownina virtuaalikoneelta omalle Github-tililleni. 
 Ainoastaan Github kansio ja h3Versionhallinta tiedosto, on luotu etukäteen githubin puolelle, kaikki muut muutokset tapahtuvat MarkDownina, esimerkiksi tämä tekstin lisäys. 
 
 Jotta pääsiin alkuun piti ensiksi luoda tili Githubiin ja kytkeä virtuaalikone ja github toimimaan yhdessä julkista SSH avainta hyödyntäen. 
@@ -19,9 +19,34 @@ Näin ollen perusasetukset on kunnossa ja voin jatkossa päivittää git varastani molempiin suuntiin...


Käskyllä git diff siis saan esille h3_Versionhallinta.md tiedoston josta pystyn katsomaan eroavaisuudet jotka tiedostoon on tehty. Diff käsky vertailee kahta versiota toisiinsa ja kertoo onko niissä eroja. 


