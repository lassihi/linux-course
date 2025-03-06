# Harjoitus 7: Maalisuora
Kurssi: Linux palvelimet https://terokarvinen.com/linux-palvelimet/ \
Tehtävänanto: https://terokarvinen.com/linux-palvelimet/#h6-salataampa

## Suoritusympäristö
Tietokone: Lenovo Legion Y540-15IRH kannettava kytkettynä langallisesti kotiverkkoon.\
-Intel Core i7-9750H\
-NVIDIA Geforce RTX 2060 6GB\
-16GB DDR4 2666MHz\
Käyttöjärjestelmä: Windows 11 23H2

Virtualisointiympäristö: VirtualBox Version 7.1.4. Käyttöjärjestelmänä toimii Debian 12 Bookworm käyttäen alla olevan kuvan mukaisia VirtualBox-asetuksia.

![virtualbox-asetukset](https://github.com/user-attachments/assets/ad4b8cd8-9cd2-4ebd-b4f7-86d0b8e23aa1)

## a) Kirjoita ja aja "Hei maailma" kolmella kielellä.
16.47-17.10

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

#### [Siirry lukemaan osio c)](https://github.com/lassihi/linux-course/edit/main/h7/h7-maalisuora.md#c-laita-linuxiin-uusi-itse-tekem%C3%A4si-komento-niin-ett%C3%A4-kaikki-k%C3%A4ytt%C3%A4j%C3%A4t-voivat-ajaa-sit%C3%A4).

## b)

## c) Laita Linuxiin uusi, itse tekemäsi komento niin, että kaikki käyttäjät voivat ajaa sitä.
Ajatus oli luoda komento `hei_maailmat`, joka lisäisi käyttäjän kotihakemistoon tiedostot `hei_maailma.py` ja `hei_maailma.java`, jotka tulostaisivat kumpikin "Hei maailma" merkkijonon. Itse komennon loisin bash-kielellä.

Päivitin paketit komennolla `sudo apt-get update` ja asensin javan paketin komennolla `sudo apt-get install openjdk-17-jdk`. Python oli etukäteen asennettu. \
Yritin luoda hakemistoon `/home/lassihi/koodit/` tiedostoa, mutta sain virheilmoituksen.

![image](https://github.com/user-attachments/assets/cbdcfc55-f95e-4dac-98a5-e3b3ceca2c07)

Hieman tutkittuani asiaa huomasin, että tiedosto ei tallenna sinne tehtyjä muutoksia. Löysin micron github sivuilta samasta viasta tehdyn bugiraportin (https://github.com/zyedidia/micro/issues/2386). Raportin vastauksissa mainittiin, että virhe johtuu levytilan täyttymisestä. Yritin myös muokata tiedostoa nano-editorilla, joka ilmoitti levytilan olevan täynnä. 

![image](https://github.com/user-attachments/assets/97d40bd1-b12c-4047-96d4-923cbcef7544)

Tarkastin miltä tallennustila näyttää virtualboxissa.

![image](https://github.com/user-attachments/assets/f0fe9572-8456-48c6-89a5-1ffd65544ece)

Tilaa näytti olevan vielä hyvin jäljellä, joten käynnistin uudelleenkäynnistin virtuaalikoneen.

Syötin sisäänkirjautumiseen käyttäjätunnukseni ja salasanani, näyttö välähti muutaman kerran mustana ja pyysi uudelleen sisäänkirjautumista. Yritin noin viisi kertaa kirjautua takaisin sisään, joka kerta tarkastaen, että tiedot ovat varmasti oikein. Tämä ei toiminut. Alla esimerkit.

