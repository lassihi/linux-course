# Harjoitus 2: Komentaja pingviini
Kurssi: Linux palvelimet https://terokarvinen.com/linux-palvelimet/ \
Tehtävänanto: https://terokarvinen.com/linux-palvelimet/#h2-komentaja-pingviini

## Komentorivin perusteet

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
Tässä kohtaa törmäsin ensimmäisiin virheilmoituksiin (seuraavassa kuvassa). Aloitin virheilmoitusten tutkimisen avaamalla selaimen ja kopioimalla ne Googleen. Silmäilin muutaman ehdotetun artikkelin, joissa kaikissa lueteltiin pitkä lista keinoja virheen korjaamiseksi. Ennen vian syvempää tutkimista päätin vielä yrittää komentoa uudelleen, jolloin se toimi moitteettomasti. Ensimmäisen ja toisen yrityksen välillä oli aikaa ehtinyt kulua noin 4 minuuttia.

![image](https://github.com/user-attachments/assets/6129ed43-28e9-479b-93e1-5078c38f7b8e)

Päätin vielä kokeilla Micro-sovelluksen toiminnan. Siirryin kotihakemistosta "Documents"-hakemistoon ja loin Micro-editorilla uuden tekstitiedoston nimeltä "testi.txt" seuraavilla komennoilla.

    cd Documents/
    micro testi.txt
Tiedosto avautui Micro-editorissa, kirjoitin kolme riviä tekstiä ja poistuin Ctrl+Q-näppäinkomennolla, varmistaen teidoston muutoksen vielä "y"-näppäimellä ennen sovelluksen sulkeutumista. Käytin vielä seuraavia komentoja listaamaan nykyisen hakemiston sisältämät tiedostot ja hakemistot, sekä tiedoston uudelleen avaamiseen.

    ls
    micro testi.txt
Tiedosto oli tallentunut oikein, joten poistuin editorista edellä mainitulla tavalla. Näin sain varmistettua ainakin tiedostojen luonnin, avaamisen ja sisällön muokkaamisen ja tallentamisen toiminnan sovelluksessa.
