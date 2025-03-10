# Harjoitus 7: Maalisuora
Kurssi: Linux palvelimet https://terokarvinen.com/linux-palvelimet/ \
Tehtävänanto: https://terokarvinen.com/linux-palvelimet/#h7-maalisuora

## Suoritusympäristö
Tietokone: Lenovo Legion Y540-15IRH kannettava kytkettynä langallisesti kotiverkkoon.\
-Intel Core i7-9750H\
-NVIDIA Geforce RTX 2060 6GB\
-16GB DDR4 2666MHz\
Käyttöjärjestelmä: Windows 11 23H2

Virtualisointiympäristö: VirtualBox Version 7.1.4. Käyttöjärjestelmänä toimii Debian 12 Bookworm käyttäen alla olevan kuvan mukaisia VirtualBox-asetuksia.

![virtualbox-asetukset](https://github.com/user-attachments/assets/ad4b8cd8-9cd2-4ebd-b4f7-86d0b8e23aa1)

## a) Kirjoita ja aja "Hei maailma" kolmella kielellä.

Aloitin avaamalla terminaalin ja luomalla uuden kansion koodeille kotihakemistoon

![image](https://github.com/user-attachments/assets/571d564a-e399-4f99-aa53-99c9543e1fc2)

Siirryin kansioon `cd koodit` \
Loin ensimmäiseksi bash-kielle hei_maailma.sh tiedoston, `micro hei_maailma.sh`.

![image](https://github.com/user-attachments/assets/56190a7d-c45c-45d4-8d96-1cec5b67e3fc)

Tiedoston ensimmäisellä rivillä voidaan määrittää millä tulkilla tiedosto ajetaan, kun tulkin hakemistopuun sijainti annetaan risuaidan ja huutomerkin (`#!`) jälkeen.
`echo Hei maailma` tulostaa merkkijonon "Hei maailma".

Tallensin tiedoston ja poistuin editorista. Yritin ajaa luomaani tiedostoa, mutta sain ilmoituksen puuttuvista oikeuksista.

![image](https://github.com/user-attachments/assets/b51b179d-e3d4-4ef8-a806-3fc3e5afb542)

Tarkastin hakemistossa olevien tiedostojen oikeudet.

![image](https://github.com/user-attachments/assets/eeda7f85-0d64-4757-a50e-bbcb9bc80db7)

Huomasin itseltäni, eli teidoston omistajalta (u) puuttuvan tiedoston ajo-oikeudet (x). Annoin tässä kohtaa itselleni ajo-oikeudet tiedostoon.

![image](https://github.com/user-attachments/assets/d93a9cca-d7eb-4ea4-b7f2-b0fe0d50848c)

Tarkastin, että ajo-oikeus tuli voimaan ja ajoin tiedoston.

![image](https://github.com/user-attachments/assets/e0a43e53-b62c-422e-a8e3-753afd94235c)

Tiedosto tulosti merkkijonon "Hei maailma", niin kuin oli tarkoitus.

#### SIIRRY SEURAAVAKSI LUKEMAAN OSIO C), JOSSA OLI TARKOITUS TEHDÄ KOMENTO, JOKA KIRJOITTAA JA AJAA KAKSI HEI_MAAILMA TIEDOSTOA.

#### Jatka sen jälkeen tästä.

Tein seuraavan tiedoston pythonilla. Micro-editoria käyttäessä virheilmoitus toistui edelleen.

![image](https://github.com/user-attachments/assets/37f2d7c9-7cfb-4adf-b603-f17405fc9c70)

![image](https://github.com/user-attachments/assets/6d72c4c2-2515-4285-b08b-6ed74e016e04)

Virheilmoituksesta huolimatta micro näytti toimivan oikein ja tallensi tällä kertaa tiedoston.

Muutin tiedoston oikeudet.

![image](https://github.com/user-attachments/assets/ad4e45df-e3d9-4570-a63e-e7bd9a0637b6)S

Ajoin tiedoston.

![image](https://github.com/user-attachments/assets/e70f6af5-89dd-4d89-8c6e-77b5e0254934)

Viimeiseksi käytin javaa. En ollut varma oliko java-ohjelma asentunut, niin ajoin komennon uudestaan.

![image](https://github.com/user-attachments/assets/33759b3b-f149-4edd-9e8c-589a761d9a60)

Loin ja avasin hei_maailma.java tiedoston. 

![image](https://github.com/user-attachments/assets/190f5750-4d68-4d5b-8d1e-8cb37d5214d1)

Tein https://terokarvinen.com/2018/hello-python3-bash-c-c-go-lua-ruby-java-programming-languages-on-ubuntu-18-04/ sivun ohjeiden mukaan koodin.

![image](https://github.com/user-attachments/assets/a996fab3-fd45-4abd-82dc-d9b48d497ceb)

Tallensin tiedoston ja poistuin editorista. Tein ajettavan .class tiedoston .java tiedostosta `javac` komennolla.

![image](https://github.com/user-attachments/assets/584fa341-5ec9-4217-9860-a21a305c64c1)

Koodissa oli virhe, joten kävin sen korjaamassa ja ajoin `javac` komennon uudestaan.

![image](https://github.com/user-attachments/assets/b2b96d5e-9380-4d48-aa0a-2d50e1be29a6)

Tuli uusi virhe, jonka korjasin nimeämällä tiedoston uudestaan. Ajoin taas `javac` komennon. Lopuksi ajoin tiedoston `java` komennolla.

![image](https://github.com/user-attachments/assets/b03b454f-1147-4f9a-8cd2-e6667aafe3d0)

## c) Laita Linuxiin uusi, itse tekemäsi komento niin, että kaikki käyttäjät voivat ajaa sitä.

Ajatus oli luoda komento `hei_maailmat`, joka lisäisi käyttäjän kotihakemistoon tiedostot `hei_maailma.py` ja `hei_maailma.java`, jotka tulostaisivat kumpikin "Hei maailma" merkkijonon kohdan a) automatisoimiseksi. Itse komennon loisin bash-kielellä.

Päivitin paketit komennolla `sudo apt-get update` ja asensin javan paketin komennolla `sudo apt-get install openjdk-17-jdk`. Python oli etukäteen asennettuna. \
Yritin luoda hakemistoon `/home/lassihi/koodit/` tiedostoa, mutta sain virheilmoituksen.

![image](https://github.com/user-attachments/assets/cbdcfc55-f95e-4dac-98a5-e3b3ceca2c07)

Hieman tutkittuani asiaa huomasin, että tiedosto ei tallenna sinne tehtyjä muutoksia. Löysin micron github sivuilta samasta viasta tehdyn tiketin (https://github.com/zyedidia/micro/issues/2386). Tiketin vastauksissa mainittiin, että virhe johtuu levytilan täyttymisestä. Yritin myös muokata tiedostoa nano-editorilla, joka ilmoitti levytilan olevan täynnä. 

![image](https://github.com/user-attachments/assets/97d40bd1-b12c-4047-96d4-923cbcef7544)

Tarkastin miltä tallennustila näyttää virtualboxissa.

![image](https://github.com/user-attachments/assets/f0fe9572-8456-48c6-89a5-1ffd65544ece)A

Tilaa näytti olevan vielä hyvin jäljellä, joten uudelleenkäynnistin virtuaalikoneen.

Syötin sisäänkirjautumiseen käyttäjätunnukseni ja salasanani, näyttö välähti muutaman kerran mustana ja pyysi uudelleen sisäänkirjautumista. Yritin noin viisi kertaa kirjautua takaisin sisään, joka kerta tarkastaen, että tiedot ovat varmasti oikein. Tämä ei toiminut, eli en pystynyt kirjautumaan sisään koneelleni. Tiesin, että salasana oli oikein, sillä väärän salasanan syöttäessä tuli ilmoitus väärästä salasanasta, jota oikeiden tunnusten jälkeen ei tullut.

![image](https://github.com/user-attachments/assets/139f0938-09ef-420d-b92c-3ad72305b7a2)

Yritin googlata ratkaisuja tähän, mutta en löytänyt kunnollista ratkaisua. Päätin yrittää lisätä tallennustilan määrää virtuaalikoneelle virtualboxissa, jos se ratkaisisi ongelmani. 

Tein tallennustilan lisäyksen https://www.howtogeek.com/124622/how-to-enlarge-a-virtual-machines-disk-in-virtualbox-or-vmware/ ohjeen mukaan. Sammutin virtuaalikoneen, virtualboxissa 
vasemmasta yläkulmasta klikkasin "Tools"->"Media".

![image](https://github.com/user-attachments/assets/94a0b72f-c2d4-4bc1-8c6f-bd9450f4760f)

Virtuaalikoneen levy valittuna klikkasin ylälaidasta "Properties", jonka jälkeen alalaidasta valitsin muistiksi 40,00 GB.

![image](https://github.com/user-attachments/assets/65f43c2e-0232-448c-9b7a-7ddadaaf0e1e)

Otin muutokset käyttöön "Apply" -napista. Avasin windowsin komentokehotteen ja annoin seuraavat komennot edellä mainittua artikkelia soveltaen. Tämä tehtiin virtualboxin virtuaalikoneen levyn osioimiseksi.

![image](https://github.com/user-attachments/assets/52575181-087a-46b9-b6d3-b946bc5d148c)

![image](https://github.com/user-attachments/assets/11ddbef3-17f4-47c7-95e3-fa5c29206b34)

Nyt virtualboxissa virtuaalikoneen levyn ja osion koko on tuplattu. Itse virtuaalikoneessa kuitenkin levyn koko on vielä ennallaan. Koneen levyn osioimiseksi asensin Gparted-osointityökalun gparted-live-1.7.0-1-amd64.iso tiedoston sivustolta https://gparted.org/download.php. 

Lisäsin tiedoston virtuaaliseen levyasemaan.

![image](https://github.com/user-attachments/assets/3c808d6f-2172-4467-877e-801488fc5aa7)

![image](https://github.com/user-attachments/assets/835de9ce-cee5-4f7e-a0e6-307ef9036e61)

Käynnistin koneen ja sen käynnistyessä painoin F12 ja valitsin käynnistyksen levyasemalta.

![image](https://github.com/user-attachments/assets/709347a7-4d73-4196-a770-d7219c3009e4)

![image](https://github.com/user-attachments/assets/2219a691-a712-496f-bc89-bd63dad71431)

Gparted käynnistyi ja aloituskonfiguraation ohitin oletusasetuksilla, enteriä näpyttelemällä.

![image](https://github.com/user-attachments/assets/8833f03d-4429-4d7b-84e6-3101682db04b)

Lopulta pääsin itse työkaluun. Manuaalisessa oisioinnissa riskinä on aina tietojen menettäminen. Itsellä tärkeimmät tiedot koneelta, kuten palvelimen ssh-avain on varmuuskopioituna, joten jatkoin eteenpäin.

![image](https://github.com/user-attachments/assets/8ce3de80-1112-4503-85f2-4370f7fe390e)

Virtuaalikovalevy on osoitu kahteen osioon (/dev/sda1 ja /dev/sda2), josta toisen olin täyttänyt. Täysi osio (/dev/sda1) on ilmeisesti pääosio, johon tiedot virtuaalikoneesta tallennetaan. Jotta pääosion voi suurentaa, niin täytyy toinen osio siirtä ns. "pois tieltä". En tiennyt tämän toisen osion merkitystä, joten en lähtenyt sitä poistamaan. Myöhemmin kävi ilmi, että kyseessä on todennäköisesti boot osio, jota käytetään koneen käynnistykseen.

Valitsin tyhjän osioin.

![image](https://github.com/user-attachments/assets/b1cb02ea-fe7b-42f0-81db-66cd244c7440)

Siirsin tyhjän osion levyn loppuun, jotta tyhjä tila voidaan määrittää pääosiolle.

![image](https://github.com/user-attachments/assets/3d8c3c38-1de5-4494-baee-3a9770a2e58c)

Tuli varoitus, jossa ilmoitettiin, että osion siirtäminen voi hajottaa koneen käynnistyksen. Käynnistys on jo rikki, joten jatketaan eteenpäin :). Muutin seuraavaksi pääosion kokoa.

![image](https://github.com/user-attachments/assets/7752398e-4cb5-41cc-9927-9d3bf9e39f45)

Lopuksi osiointi näytti seuraavalta. Tyhjän osion jälkeen on hieman vapaata muistia, sillä tyhjää osiota ei ollut mahdollista siirtää aivan levyn loppuun.

![image](https://github.com/user-attachments/assets/8307817d-c6df-4e25-b1ae-0dc196d6d24d)

Lopuksi otin osioinnit käyttöön yläreunasta vihreää pukkia klikkaamalla.

![image](https://github.com/user-attachments/assets/9ddad073-941c-4bf4-ac52-3182a680b5d0)

Sammutin koneen, poistin .iso päättyvän tiedoston virtuaalikoneesta ja käynnistin koneen sormet ristissä. Kone käynnistyi sisäänkirjautumisruutuun ja pääsin kirjautumaan sisään tunnuksillani.

![image](https://github.com/user-attachments/assets/32c58a0a-3802-4e1d-9456-8b368ed3edfe)

Tutkin hieman kansioita ja kaikki tiedostot näyttivät olevan tallellaan.

Tässä kohtaa tähän tehtävään oli jo lähes kolme tuntia, joten päätin ottaa lyhyimmän polun ja tehdä kohdassa a) luodusta tiedostosta `hei_maailma` komento jokaiselle käyttäjälle. Tarkastin tiedoston oikeudet ja annoin myös muille käyttäjille ja ryhmälle ajo-oikeudet.

![image](https://github.com/user-attachments/assets/42e528d0-9943-4d14-aaa8-5e79bcd2eadd)

Poistin tiedoston nimen perästä ".sh"-päätteen.

![image](https://github.com/user-attachments/assets/fcf715dd-40fd-46ed-a330-dfd478494b36)

Kopioin tiedoston sijaintiin `/usr/local/bin`, jolloin se tulee käytettäväksi jokaiselle käyttäjälle jokaiseen hakemistoon.

![image](https://github.com/user-attachments/assets/100145e8-6590-49e8-9bc0-fa19be0b5f6f)

Vaihdoin hakemistoa ja varmistin, että komento toimii.

![image](https://github.com/user-attachments/assets/ea5cd3a4-7d15-4a2f-8df9-ab7a2eca358c)

#### Siirry takaisin a) osaan.

## d) Ratkaise vanha arvioitava laboratorioharjoitus soveltuvin osin.
Tein 2024 kevään labraharjoituksen http://terokarvinen.com/2024/arvioitava-laboratorioharjoitus-2024-linux-palvelimet/ kohdat c, d, e ja g.

#### c) Ei kolmea sekoseiskaa
Loin uuden kansion, jonne loin tiedoston. Tiedosta poistin muilta kuin omistajalta automaattisesti annetut lukuoikeudet.

![image](https://github.com/user-attachments/assets/fd7b4b4a-3aef-4d13-ae53-92f030c3a1f5)

#### d) 'howdy'
Tein koodit hakemistoon howdy tiedoston, muutin jokaiselle käyttäjälle ajo-oikeudet ja kopioin tiedoston sijaintiin `/usr/local/bin/`.

![image](https://github.com/user-attachments/assets/1af2cfa0-da58-4a73-9404-fab0d53c1c2b)

Ajoin komennon testatakseni, että se toimii.

![image](https://github.com/user-attachments/assets/6aa9ed8d-d008-4ef0-96e1-8672e4bc5c93)

Howdy tiedosto:

![image](https://github.com/user-attachments/assets/05fcf056-c724-4980-8c20-5f2c9f28e868)

Ajan näyttämiseen bash-ohjelmassa käytin apuna artikkelia https://www.howtogeek.com/410442/how-to-display-the-date-and-time-in-the-linux-terminal-and-use-it-in-bash-scripts/.

#### e) Etusivu uusiksi
Apache on jo asennettu. Tein uudelle sivulle apachen asetustiedoston, otin asetustiedoston käyttöön, poistin edellisen käytöstä ja potkaisin apachea. Loin asetustiedostossa määritettyyn polkuun index.html tiedoston. Testasin, että index.html tiedosto näkyy selaimella loopback osoitteessa.

![image](https://github.com/user-attachments/assets/d707029b-b020-4363-8425-fceb4e85f4a4)

![image](https://github.com/user-attachments/assets/dc3e7bdf-4e34-4cb4-a501-0efc98d02925)

![image](https://github.com/user-attachments/assets/4b3ce810-ca52-4acf-8ab6-613080579689)

![image](https://github.com/user-attachments/assets/00e957f9-d318-4180-9cf5-66c5022b2ab1)

#### g) Salattua hallintaa.
Tein uuden käyttäjän.

![image](https://github.com/user-attachments/assets/586d4fef-f15f-46e5-90df-bd14e2f6936c)

Loin uudelle käyttäjälle .ssh hakemiston, jonka sisälle authorized_keys tiedostoon kopioin aiemmissa tehtävissä luomani julkisen avaimen. Pystyin kirjautumaan uudelle käyttäjälleni käyttäen yksityistä avainta.

![image](https://github.com/user-attachments/assets/e9d71950-fc65-43bc-9f98-a667e65a624a)

## Lähteet

Karvinen 2025: Linux palvelimet: https://terokarvinen.com/linux-palvelimet/

Micro tiketti: https://github.com/zyedidia/micro/issues/2386 (github lyhentää github-linkit, joten tässä alkuperäinen osoite: `https://github.com/zyedidia/micro/issues/2386`)

Hoffman & Lewis 2023: How to Enlarge a Virtual Machine's Disk in VirtualBox or VMware: https://www.howtogeek.com/124622/how-to-enlarge-a-virtual-machines-disk-in-virtualbox-or-vmware/

GNOME Partition Editor: Downloads: https://gparted.org/download.php

Karvinen 2018: Hello World Python3, Bash, C, C++, Go, Lua, Ruby, Java – Programming Languages on Ubuntu 18.04: https://terokarvinen.com/2018/hello-python3-bash-c-c-go-lua-ruby-java-programming-languages-on-ubuntu-18-04/

Karvinen 2024: Final Lab for Linux Palvelimet 2024 Spring: https://terokarvinen.com/2024/arvioitava-laboratorioharjoitus-2024-linux-palvelimet/

McKay 2023: How to Display the Date and Time in the Linux Terminal (and Use It In Bash Scripts): http://howtogeek.com/410442/how-to-display-the-date-and-time-in-the-linux-terminal-and-use-it-in-bash-scripts/
