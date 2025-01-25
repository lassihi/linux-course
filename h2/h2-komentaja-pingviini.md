# Harjoitus 2: Komentaja pingviini
Kurssi: Linux palvelimet https://terokarvinen.com/linux-palvelimet/ \
Tehtävänanto: https://terokarvinen.com/linux-palvelimet/#h2-komentaja-pingviini

## Komentorivin perusteet
- Komentokehote on tehokas, kätevä ja nopea tapa hallita Linuxia.
- Komentokehotteessa toimitaan aina hakemistoissa. Hakemistopuuta navigoidessa hyödyllisimpiä komentoja ovat 'pwd', 'ls' ja 'cd'.
- Minimum privilege -periaate, eli tulisi aina käyttää pienimpiä mahdollisia oikeuksia komentojen suorittamiseen.

## Suoritusympäristö
Tietokone: Lenovo Legion Y540-15IRH kannettava kytkettynä langallisesti kotiverkkoon.\
-Intel Core i7-9750H\
-NVIDIA Geforce RTX 2060 6GB\
-16GB DDR4 2666MHz\
Käyttöjärjestelmä: Windows 11 23H2

Virtualisointiympäristö: VirtualBox Version 7.1.4. Käyttöjärjestelmänä toimii Debian 12 Bookworm käyttäen alla olevan kuvan mukaisia VirtualBox-asetuksia.

![virtualbox-asetukset](https://github.com/user-attachments/assets/ad4b8cd8-9cd2-4ebd-b4f7-86d0b8e23aa1)

## Micro-editorin poisto ja asennus
Käynnistin virtuaalikoneen, kirjauduin sisään sudo-oikeuksilla varustetulle käyttäjätilille ja aloitin Micro-editorin asennuksen virtuaalikoneelle käynnistämällä komentokehotteen tuplaklikkaamalla "Terminal Emulator" kuvaketta työpöydän alareunasta. Komentokehotteessa päivitin ensiksi paketinhallintaohjelman käyttämän listan saatavilla olevista sovelluksista seuraavalla komennolla.

    sudo apt-get update
Komentokehote pyysi tämän jälkeen käyttäjän salasanaa sudo-oikeuksien käyttöä varten ja annoin salasanan.

![sudo-apt-get-update](https://github.com/user-attachments/assets/26d136af-b762-4627-9959-6a0e68d1210e)

Tiesin, että virtuaalikoneellani oli viime luennolta ladattuna Micro-editori, joten poistin sen esimerkin vuoksi järjestelmästä seuraavalla komennolla.

    sudo apt-get purge micro
Jonka jälkeen komenotkehote pyysi varmistusta sovelluksen poistoon. Varmistin poiston klikkaamalla Enter-näppäintä.

![image](https://github.com/user-attachments/assets/89fa9c42-c855-4838-a1ea-829254e291e3)

Nyt kun vanha asennus sovelluksesta oli poistettu, voitiin Micro-editorin asentaminen aloittaa uudelleen nollasta. Sovelluksen asentamiseksi paketinhallintaohjelmalla syötin alla olevan komennon, jonka jälkeen sudo-oikeuksiin vaaditun käyttäjätilin salasana.

    sudo apt-get install micro
Tässä kohtaa törmäsin ensimmäisiin virheilmoituksiin (seuraavassa kuvassa). Aloitin virheilmoitusten tutkimisen avaamalla virtuaalikoneen selaimen ja kopioimalla ne Googleen. Silmäilin muutaman ehdotetun artikkelin, joissa kaikissa lueteltiin pitkä lista keinoja virheen korjaamiseksi. Ennen vian syvempää tutkimista päätin vielä yrittää komentoa uudelleen, jolloin se toimi moitteettomasti. Ensimmäisen ja toisen yrityksen välillä oli aikaa ehtinyt kulua noin 4 minuuttia.

![image](https://github.com/user-attachments/assets/6129ed43-28e9-479b-93e1-5078c38f7b8e)

Päätin vielä kokeilla Micro-sovelluksen toiminnan. Siirryin kotihakemistosta "Documents"-hakemistoon ja loin Micro-editorilla uuden tekstitiedoston nimeltä "testi.txt" seuraavilla komennoilla.

    cd Documents/
    micro testi.txt
Tiedosto avautui Micro-editorissa, kirjoitin kolme riviä tekstiä ja poistuin Ctrl+Q-näppäinkomennolla, varmistaen teidoston muutoksen vielä "y"-näppäimellä ennen sovelluksen sulkeutumista. Käytin vielä seuraavia komentoja listaamaan nykyisen hakemiston sisältämät tiedostot ja hakemistot, sekä tiedoston uudelleen avaamiseen.

    ls
    micro testi.txt
Tiedosto oli tallentunut oikein, joten poistuin editorista edellä mainitulla tavalla. Näin sain varmistettua ainakin tiedostojen luonnin, avaamisen ja sisällön muokkaamisen ja tallentamisen toiminnan sovelluksessa.

## Apt
Asensin htop, 2048 ja figlet ohjelmat samanaikaisesti käyttäen alla olevaa komentoa ja hyväksymällä lataukset.

        sudo apt-get install htop 2048 figlet
Htop toimii kuin komentokehoitteen sisäänrakennettu top komento, mutta on hieman selkeämpi. Kaikessa yksinkertaisuudessaan se näyttää käynnissä olevat prosessit ja käytetyt resurssit. 

![image](https://github.com/user-attachments/assets/59926caf-542b-4881-b107-2d63c8f291b2)

Sovelluksesta poistutaan Ctrl+C.

2048 peli on tuotu myös komentokehoitteelle. Pelin tarkoitus on yhdistellä saman numeroisia neliöitä 4x4 aluella, samalla kasvatten laatikoiden sisällä olevia numeroita. 

![image](https://github.com/user-attachments/assets/c30225cb-933c-4d0b-97d7-39724db0e2a4)

Neliöiden liikutus toimii nuolinäppäimillä. Pelin voittaa kun saa muodostettua laatikon 2048 numerolla ja häviää kun alue täyttyy niin, että laatikoita ei pysty enää yhdistelemään.

![image](https://github.com/user-attachments/assets/80ea953f-e475-4c9e-a6d7-3f55a4c784de)

Figlet on sovellus, joka muuttaa sille annetun tekstin suureksi ASCII tekstiksi.

![image](https://github.com/user-attachments/assets/cdd70182-1dc8-493e-bfb5-fc7ea0743c20)

## FHS

Juurihakemisto sisältää kaikki muut järjestelmässä olevat kansiot ja tiedostot. Siirrytään kansioon ja listataan sen sisältö komennoilla

    cd /
    ls
![image](https://github.com/user-attachments/assets/7e3c3bcd-94ac-4ca3-9e4b-88fd680c0b8b)

Juurihakemistossa sijaitsee kansio home, jossa sijaitsee koneen kaikkien käyttäjien kotihakemistot. Siirrytään juurihakemistosta home-kansioon ja tulostetaan sen sisältö.

    cd home/
    ls
![image](https://github.com/user-attachments/assets/4b2f0da3-4976-47ee-b97a-9d7fb0f8a919)

Home-kansiossa sijaitsee kansio lassihi, joka on käyttäjän lassihi kotihakemisto. Jos koneella olisi muita käyttäjiä, niin käyttäjät olisivat näkyneet tässä. Käyttäjän kotihakemisto on ainoa paikka mihin käyttäjä voi säiyttää dataa. Siirrytään käyttäjän lassihi kotihakemistoon ja listataan sen sisältö. Avataan myös hakemistossa oleva kansio ja kurkataan sen sisälle.

    cd lassihi/
    ls
    cd Documents/
    ls
![image](https://github.com/user-attachments/assets/1f186b64-bfa5-4d38-b8b6-ef6573d51afb)

Muita tärkeitä kansioita ovat:
- /etc/, joka sisältää asetukset. Esim firefox-esr asetukset:
    ![image](https://github.com/user-attachments/assets/0a46e27b-9479-453a-989f-14527e0911fb)
    ![image](https://github.com/user-attachments/assets/6dd4e4ee-acb2-43e0-85d9-23ac551d9e67)
 
- /media/, joka sisältää järjestelmään yhdistetyt ulkoiset mediat, kuten cd-aseman tai muistikortin.
- /var/log/, joka sisältää lokit. Esim apt-loki:
    ![image](https://github.com/user-attachments/assets/ac307c1c-ce06-48ee-88ee-5db6af6325a4)
    ![image](https://github.com/user-attachments/assets/174315ce-8f96-482c-ba89-598fa85629fa)

## Grep
Grep-komento mahdollistaa rivien hakemisen ja suodattamisen hakusanan tai lausekkeen avulla. Yleinen käyttötarkoitus merkkijonon sisältävän rivin hakeminen tiedostosta. Alla olevassa kuvassa haetaan Documents hakemistossa olevasta tiedostosta "testi.txt" rivit, jotka sisältävät merkkijonon "rivi". 

![image](https://github.com/user-attachments/assets/9b20d8d0-03a3-479c-904f-9a10ed5df3c7)

Kuten useisiin muihin komentoihin, niin grep-komentoihin voidaan lisätä optioita, jotka ovat lisäohjeita. Esimerkiksi optio -w hakee vain rivit, joissa on merkkijonoa vastaava sana. Usein optio -n on hyödyllinen, sillä se lisää tulosteeseen rivinumerot. Tein edellisen kuvan mukaisen komennon uudelleen tällä kertaa hyödyntäen edellä näytettyjä optioita.

![image](https://github.com/user-attachments/assets/fefc2565-b037-42a5-8032-f4baf7603a44)

## Pipe
Putket "|" mahdollistavat komentojen ketjuttamiseen komentorivillä niin, että ennen putkea olevan komennon tulosteesta tulee putken jälkeen olevan komennon syöte. Esimerkkinä listasin koti-hakemistoni kansiot, jonka jälkeen käytin putkea ja grep-komentoa listaamaan kansiot, jotka päättyvät kirjaimeen s.

![image](https://github.com/user-attachments/assets/d6d0cc90-3827-4110-a627-ff40e1592ed3)

## Rauta
Asensins lshw-sovelluksen komennolla

    sudo apt-get install lshw

Jonka jälkeen listasin raudan

![image](https://github.com/user-attachments/assets/07c5e414-b07a-4d30-9866-4db854a5de27)

Komennossa optio -short listaa raudan h/w path -osoitteen mukaan ja -sanitize poistaa yksilöivät tiedot kuten sarjanumerot. Komennon tuloste on järjestetty neljään sarakkeeseen, joiden otsikot ovat H/W path, Device, Class ja Description. Sarake H/W kuvaa komponenttien loogista sijaintia, jota voisi verrata Linuxin hakemistopuuhun. Devices sarake kuvaa komponenttia (esim. scsi2 = small computer system interface 2). Class sarake kuvaa komponentin tyyppiä yleisesti. Description saraakkeessa on kuvaus komponentista, joka on usein sen malli tai nimi.

## Lähteet
Komentorivin perusteet, komennot, pipe: https://terokarvinen.com/2020/command-line-basics-revisited/?fromSearch=command%20line%20basics%20revisited \
Grep: https://www.linux.fi/wiki/Grep \
lshw: https://ezix.org/project/wiki/HardwareLiSter 
