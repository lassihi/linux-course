# Harjoitus 4: Maailma kuulee
Kurssi: Linux palvelimet https://terokarvinen.com/linux-palvelimet/ \
Tehtävänanto: https://terokarvinen.com/linux-palvelimet/#h4-maailma-kuulee

## x) Lue ja tiivistä
Susanna Lehto 2022: [Teoriasta käytäntöön pilvipalvelimen avulla (h4)](https://susannalehto.fi/2022/teoriasta-kaytantoon-pilvipalvelimen-avulla-h4/)
* a) Palvelimen vuokraus ja asennus
  - Palvelin hankittiin DigitalOceanilta ja domainnimi NameCheapilta.
  - Palvelimen tiedot: Intelin 1-ytiminen prosessori, 1 Gt muisti, 25 Gt SSD-levy. Pyörii Debian 11 käyttöjärjestelmällä. Sijainti Amsterdamissa. Salasanakirjautuminen.
  - Domainnimeksi valittiin susannalehto.me (nykyään susannalehto.fi). Nimi ja www alkuinen nimi määritettiin ohjaamaan palvelimen IP-osoitteeseen.
* d) Palvelin suojaan palomuurilla
  - Ennen asennuksia päivitettiin paketit `sudo apt-get update`.
  - Palomuuri määritettiin ufw ohjelmalla.
  - Ensiksi tehtiin etäyhteydelle reikä `sudo ufw allow 22/tcp`, jonka jälkeen kytkettiin palomuuri päälle `sudo ufw enable`
* e) Kotisivut palvelimelle
  - Ensiksi luotiin uusi käyttäjä, tehtiin tästä käyttäjästä pääkäyttäjä ja luktittiin root-tili.
  - Asennettiin Apache2 demoni, tehtiin palomuurin reikä http-yhteydelle ja kirjoitettiin testisivulle "Hello world!".
  - Otettiin userdir-moduuli käyttöön, luotiin käyttäjän kotihakemistoon public_html hakemisto ja lisättiin sinne index.html tiedosto, jotta sivun päivittäminen onnistuu ilman sudoa.
* f) Palvelimen ohjelmien päivitys
  - Haettiin tiedot saatavilla olevista päivityksistä: `sudo apt-get update`
  - Asennettiin päivitykset: `sudo apt-get upgrade`
  - Asennettiin tietoturvapäivitykset: `sudo apt-get dist-upgrade`
 
Tero Karvinen 2012: [First Steps on a New Virtual Private Server – an Example on DigitalOcean and Ubuntu 16.04 LTS](https://terokarvinen.com/2017/first-steps-on-a-new-virtual-private-server-an-example-on-digitalocean/)
* Luo uusi Linux-palvelin, lisää SSH-avaimet tai käytä vahvaa salasanaa, määritä palomuuri ja lisää tavallinen käyttäjä. Lukitse root-käyttäjä ja estä sen SSH-kirjautuminen.
* Päivitä ohjelmistojt aktiivisesti komennoilla `sudo apt-get update`, `sudo apt-get upgrade`.
* DNS-nimen ostamiseen suositellaan NameCheap tai Gandi palveluita. Täytä palvelussa tarvittavat tiedot ja testaa toimivuus.

## Suoritusympäristö
Tietokone: Lenovo Legion Y540-15IRH kannettava kytkettynä langallisesti kotiverkkoon.\
-Intel Core i7-9750H\
-NVIDIA Geforce RTX 2060 6GB\
-16GB DDR4 2666MHz\
Käyttöjärjestelmä: Windows 11 23H2

Virtualisointiympäristö: VirtualBox Version 7.1.4. Käyttöjärjestelmänä toimii Debian 12 Bookworm käyttäen alla olevan kuvan mukaisia VirtualBox-asetuksia.

![virtualbox-asetukset](https://github.com/user-attachments/assets/ad4b8cd8-9cd2-4ebd-b4f7-86d0b8e23aa1)

## a) Palvelimen vuokraus
Päätin vuokrata palvelimen käyttäen upcloud.com sivuston palveluita. Suuntasin sivulle ja loin ensiksi käyttäjätunnuksen, jonka jälkeen kirjauduin sisään. Aloitin ilmaisen kokeilujakson lisäämällä maksukortin tiedot palveluun. 
Aloitin palvelimen vuokrauksen klikkaamalla Deploy now ja valitsemalla Server. 

![image](https://github.com/user-attachments/assets/3b639c63-6f24-42b1-8a1d-04f37bc71cf1)

Palvelimen sijainniksi halusin valita mahdollisimman lähellä olevan. Vaihtoehdot olivat FI-HEL1 ja FI-HEL2, jatkoin ykkösvaihtoehdolla. Palvelimeksi valitsin halvimman vaihtoehdon (prosessori: 1 ydin, muisti: 1 Gt, tallennustila: 10Gt, hinta: 3.00€/kk).

Jätin tallennustila-osion asetukset oletuksiksi.

![image](https://github.com/user-attachments/assets/c8c114b4-481d-4aee-bd03-8b024dc07da9)

En ottanut käyttöön automaattisia palvelimen varmuuskopiointeja, sillä tämä olisi luonut lisäkustannuksia.

![image](https://github.com/user-attachments/assets/1ec6f4f1-51a0-45ad-8377-5e012035d1dd)

Käyttöjärjestelmäksi valitsin Debian GNU/Linux 12 (Bookworm). Käyttöjärjestelmä on kurssin aikana tullut tutuksi, joten miksi vaihtaa nyt.

![image](https://github.com/user-attachments/assets/4b39e695-4ceb-4cf5-9f4f-a3afc1d939f1)

Verkkoasetukset jätin oletuksiksi. 

![image](https://github.com/user-attachments/assets/1d26738a-9c98-4850-8ab6-5a14389496e7)

En muokannut vaihtehtoisia valintoja.

![image](https://github.com/user-attachments/assets/915200ff-af04-4712-92f8-ae7aae8c5f50)

Kirjautumisvaihtoehdoksi valitsin SSH avaimen. Ilmeisesti SSH avain on valitsemassani käyttöjärjestelmässä ainoa kirjautumisvaihtoehdo. 

![image](https://github.com/user-attachments/assets/568c8dc8-bce4-4f29-8327-4dc23c1fc5eb)

Tässä vaiheessa avasin terminaalin SSH avainten generoimista varten. Generoin avaimet komennolla `ssh-keygen`

![image](https://github.com/user-attachments/assets/2f114c46-7bae-44b1-8ed8-69a0ece92e56)

Avasin tiedoston, johon julkinen avain tallennettiin ja kopioin sieltä julkisen avaimen, jonka jälkeen liitin avaimen upcloud-sivustolle. Loput  palvelimen määritykset jätin oletuksiksi ja otin palvelimen käyttöön klikkaamalla Deploy. Käyttöönotto oli minuutin latailun jälkeen valmis.

## b) Alkutoimet virtuaalipalvelimella
Yhdistin palvelimen root-käyttäjään ssh-yhteyden avulla. Konsoli varoitti tuntemattomasta osoitteesta, mutta jatkoin eteenpäin naputtelemalla "yes".

![image](https://github.com/user-attachments/assets/a66f4473-2b35-4966-84bf-b47fd2ad34b7)

Ensitöikseni päivitin asennetut paketit ja listan paketeista komennoilla `sudo apt-get update`, `sudo apt-get upgrade`. 

Seuraavaksi otin palomuurin käyttöön ufw-ohjelmalla. En ollut varma oliko ohjelma esiasennettuna palvelimelle, joten yritin suorittaa komennon `sudo ufw allow 22/tcp`, tehdäkseni ssh-yhteydelle reiän.
Komento ei toiminut, joten asensin tämän yhdessä bash-completion ohjelman kanssa, `sudo apt-get install ufw bash-completion`. Tein asennuksen jälkeen reiän ssh-yhteydelle edellä mainitulla komennolla ja otin palomuurin käyttöön komennolla `sudo ufw enable`. 

Loin seuraavaksi käyttäjän itselleni ja lisäsin tämän käyttäjän ryhmiin sudo ja adm.

    sudo adduser lassi
    sudo adduser lassi sudo
    sudo adduser lassi adm

Kopioin tämän jälkeen kirjautumiseen käytetyn ssh-avaimen uudelle käyttäjälle.

![image](https://github.com/user-attachments/assets/422b5d62-9b60-4ea3-ac0e-b2396c725e59)

Yrityn kirjautua uudelle käyttäjälle uudesta terminaaliyhteydestä.

![image](https://github.com/user-attachments/assets/b0afe0aa-4241-4546-ae15-4043395b2ccf)

En muistanut luennolta kuinka tästä edettiin, mutta uskoin virheen johtuvan kopioidun kansion ja tiedoston käyttöoikeuksista. Löysin artikkelin uuden käyttäjän luonnista (https://humanwhocodes.com/snippets/2021/03/create-user-linux-ssh-key/) ja seurasin sen ohjeita. Tarkastin ensiksi kuka omistaa kansion .ssh, vaihdoin omistajaksi käyttäjän, vaihdoin käyttöoikeudet ja tarkastin lopuksi, että muutokset toteutuivat.

![image](https://github.com/user-attachments/assets/f38c4b67-d380-467a-90a5-91ac5ae43fdd)

Yritin kirjautumista uudestaan, joka tällä kertaa onnistui. Varmistin samalla, että sudo toimii käyttäjällä. Lukitsin root-käyttäjän komennolla `sudo usermod --lock root` ja poistin ssh kirjautumisen käyttäen komentoa `sudoedit /etc/ssh/sshd_config` ja vaihtamalla kohdan "PermitRootLogin" arvoksi "no".

![image](https://github.com/user-attachments/assets/bd05337e-1f07-4b14-ad61-cffed6cbdfa1)

Varmistin lopuksi, että root-käyttäjälle ei voinut enää kirjautua. 

![image](https://github.com/user-attachments/assets/f6c0304d-28f7-4a8a-ad99-f49d79cbbd99)

## c) Apache virtuaalipalvelimelle
Tein palomuuriin reiän porttin 80 ja asensin apachen.

![image](https://github.com/user-attachments/assets/c302823e-fa6f-4a49-bfa7-8064ecb06560)

![image](https://github.com/user-attachments/assets/7e1fb0f7-e433-45e8-a607-735e0d033a21)

Muokkasin testisivun index tiedostoa komennolla `sudoedit /var/www/html/index.html`.

![image](https://github.com/user-attachments/assets/3ec3cdf4-ec7c-4d07-8193-dfc2b6abae0d)

Tallensin muokkaukset ja avasin sivun selaimella.

![image](https://github.com/user-attachments/assets/1ced663d-2473-49d8-805a-5072c7decf4f)

## d) Name based virtual host virtuaalipalvelimella
Seurasin [viime raporttiani](https://github.com/lassihi/linux-course/blob/main/h3/h3-hello-web-server.md) name based virtual hostin määrittämiseksi. \
Askeleet lyhyesti:
* Loin ja määritin sivun asetustiedoston `sudoedit /etc/apache2/sites-available/toimiiko.sivusto.com.conf` ![image](https://github.com/user-attachments/assets/ed1462b9-3fa7-4897-8867-eb50c808536b)
* Otin asetukset käyttöön ja poistin ylimääräiset `sudo a2ensite toimiiko.sivusto.com.conf`, `sudo a2dissite 000-default.conf default-ssl.conf`
* Apache uudelleenkäynnistys `sudo systemctl restart apache2`
* Loin käyttäjän kotihakemistoon index.html tiedoston, asetustiedostossa määritettyyn sijaintiin. Asensin micro-ohjelman tiedoston muokkaamista varten komennolla `sudo apt-get install micro`. ![image](https://github.com/user-attachments/assets/c1b2ea1b-6f52-41ce-a611-130123e0e2b6)

Tein askeleet, eikä sivusto toiminut selaimella. Virhe "403 Forbidden". Tarkastin lokin `tail /var/log/apache2/error.log`, josta löytyi seuraava virheilmoitus.

![image](https://github.com/user-attachments/assets/8131d873-6524-4e8d-a35f-66f7e520d665)

Virheilmoituksen perusteella uskoin, että virhe johtui aiemmin määrittelemistäni `/home/lassi` hakemiston tiukista oikeuksista. Löysin netistä vastaukset ongelmaani (https://stackoverflow.com/questions/1225594/apache-13-permission-denied-in-users-home-directory). Annoin hakemistoon ja sen alihakemistoihin luku- ja ajo-oikeudet komennolla `sudo chmod 755 -R /home/lassi`. Latasin sivun selaimella uudestaan ja onnekseni se toimi.

![image](https://github.com/user-attachments/assets/98d47498-ead3-4c6b-88c3-34b932d6b509)

## Lähteet:
Susanna Lehto 2022: Teoriasta käytäntöön pilvipalvelimen avulla (h4): https://susannalehto.fi/2022/teoriasta-kaytantoon-pilvipalvelimen-avulla-h4/ \
Tero Karvinen 2012: First Steps on a New Virtual Private Server – an Example on DigitalOcean and Ubuntu 16.04 LTS: https://terokarvinen.com/2017/first-steps-on-a-new-virtual-private-server-an-example-on-digitalocean/ \
Palvelin vuokrattu: https://upcloud.com/ \
SSH public key uudelle käyttäjälle: https://humanwhocodes.com/snippets/2021/03/create-user-linux-ssh-key/ \
Apache virhekoodin 13 ratkaisu: https://stackoverflow.com/questions/1225594/apache-13-permission-denied-in-users-home-directory
