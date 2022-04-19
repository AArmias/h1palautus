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

b) 
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

git blame käsky:
	tero@tero-VirtualBox:~/palautukset/h3$ git blame
	usage: git blame [<options>] [<rev-opts>] [<rev>] [--] <file>

    <rev-opts> are documented in git-rev-list(1)

    --incremental         show blame entries as we find them, incrementally
    -b                    do not show object names of boundary commits (Default: off)
    --root                do not treat root commits as boundaries (Default: off)
    --show-stats          show work cost statistics
    --progress            force progress reporting
    --score-debug         show output score for blame entries
    -f, --show-name       show original filename (Default: auto)
    -n, --show-number     show original linenumber (Default: off)
    -p, --porcelain       show in a format designed for machine consumption
    --line-porcelain      show porcelain format with per-line commit information
    -c                    use the same output mode as git-annotate (Default: off)
    -t                    show raw timestamp (Default: off)
    -l                    show long commit SHA1 (Default: off)
    -s                    suppress author name and timestamp (Default: off)
    -e, --show-email      show author email instead of name (Default: off)
    -w                    ignore whitespace differences
    --ignore-rev <rev>    ignore <rev> when blaming
    --ignore-revs-file <file>
                          ignore revisions from <file>
    --color-lines         color redundant metadata from previous line differently
    --color-by-age        color lines by age
    --minimal             spend extra cycles to find better match
    -S <file>             use revisions from <file> instead of calling git-rev-list
    --contents <file>     use <file>'s contents as the final image
    -C[<score>]           find line copies within and across files
    -M[<score>]           find line movements within and across files
    -L <range>            process only line range <start>,<end> or function :<funcname>
    --abbrev[=<n>]        use <n> digits to display object names

git blame käskyt antaa seuraavan listan lisäparametreista käskylle. Käytännössä git blame käskynä kertoo kuka on vastuussa viimeisistä muutoksista tiedostossa. Myös jokaisen rivin hyväksyjä tai commitin tehnyt  voidaan selvittää.

c) HUPS! Poistin vahingossa kaiken tekstin tästä kyseisestä tiedostosta. En kuitenkaan tehnyt katastrooffistani  committia ja sain palautettua kaiken poistamani tekstin käskyllä:
	git reset --hard
Mikäli siis käy vahinko, kyseisellä käskyllä voit perua tallentamattomat muutokset ja palauttaa viimeksi tallennetun version.

z) Artikkeli Commonmark contributors: Markdown Reference pitää sisällään perus käskyt tekstin asetteluun Markdownia tehdessä. Esimerkiksi otsikko1 (#), otsikkos2 (##), tekstin boldaus jne.. Tämän lisäksi artikkelissa on nopea noin 10 minuutin tutoriaali Markdownien tekemiseen. 


    
 
 
