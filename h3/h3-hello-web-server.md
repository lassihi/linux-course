# Harjoitus 3: Hello Web Server
Kurssi: Linux palvelimet https://terokarvinen.com/linux-palvelimet/ \
Tehtävänanto: https://terokarvinen.com/linux-palvelimet/#h3-hello-web-server

## Lue ja tiivistä
Apache documentation:

Name based virtual hosts:

## Suoritusympäristö
Tietokone: Lenovo Legion Y540-15IRH kannettava kytkettynä langallisesti kotiverkkoon.\
-Intel Core i7-9750H\
-NVIDIA Geforce RTX 2060 6GB\
-16GB DDR4 2666MHz\
Käyttöjärjestelmä: Windows 11 23H2

Virtualisointiympäristö: VirtualBox Version 7.1.4. Käyttöjärjestelmänä toimii Debian 12 Bookworm käyttäen alla olevan kuvan mukaisia VirtualBox-asetuksia.

![virtualbox-asetukset](https://github.com/user-attachments/assets/ad4b8cd8-9cd2-4ebd-b4f7-86d0b8e23aa1)

## Localhost-testi
Apache oli jo asennettuna virtuaalikoneelle luennolta, joten varmistin localhost-osoitteen toimivuuden
weppiselainta käyttämällä

![image](https://github.com/user-attachments/assets/74093462-d1ed-433e-81e6-8e5c9a1f2420)

komentorivissä `curl` komentoa käyttämällä

![image](https://github.com/user-attachments/assets/979ed5f4-10bb-4931-9be2-e69d03a13b34)


Toimi kummassakin

## Apache-loki
Avasin lokin viimeiset 10 riviä komennollo `sudo tail /var/log/apache2/access.log`.

![image](https://github.com/user-attachments/assets/a46f710b-9e68-4b5e-aa4c-b9fbfe7a0ec0)

## Etusivu uusiksi
Aloitun uuden etusivun hattu.example.com luomisen kertaamalla teorian (https://terokarvinen.com/2018/04/10/name-based-virtual-hosts-on-apache-multiple-websites-to-single-ip-address/). Loin uuden asetustiedoston Apachen sites-available -kansioon

    sudoedit /etc/apache2/sites-available/hattu.example.com.conf

Lisäsin samalla asetukset tiedostoon

![image](https://github.com/user-attachments/assets/eec4828a-2086-47e1-a42e-d87febfb78d2)

Lisäsin seuraavaksi uudesta asetustiedostosta linkin Apachen sites-enabled -kansioon komennolla

    sudo a2ensite hattu.example.com

Jonka jälkeen poistin samasta kansiosta linkityksen vanhalta kotisivulta testi.example.com

    sudo a2dissite testi.example.com

Muutosten jälkeen boottasin Apachen komennolla `sudo systemctl restart apache2`, josta seurasi vikailmoitus.

![image](https://github.com/user-attachments/assets/57a244f1-6a44-4c91-898c-9411c608a727)

Avasin selaimen ja latasin localhost-sivun uudestaan, sivulle tuli "Unable to connect" -ilmoitus. Ilmoituksen perusteella voi päätellä, että Apache ei ole käytössä tai se ei kuuntele http-porttiin 80 tulevaa liikennettä.

En ollut varma mistä edellisen komennon virhe johtui, joten tarkastin apache-lokit access.log ja error.log, mutta niissä ei ollut mitään uutta. 
Kävin varmuuden vuoksi luomassa kansion `/home/lassihi/public_sites/hattu.example.com/`, johon asetustiedostosta viitattiin. Sama virhe toistui edelleen.
Päätin vielä tarkistaa asetustiedoston mahdollisten kirjoitusvirheiden varalta, jolloin huomasin että en ollut sulkenut VirtualHost-elementtiä. Suljin sen ja boottasin Apachen uudelleen ilman virheilmoitusta.

Avasin selaimen ja tällä kertaa localhost-sivulla näkyi toivottu ilmoitus 403 "Forbidden", josta voi päätellä, että portti 80 on ylhäällä, mutta ei salli siihen tulevaa liikennettä. 

![image](https://github.com/user-attachments/assets/90b68163-f899-4055-bcc6-8d840452317a)

Loin seuraavaksi index.html-tiedoston kansioon `/home/lassihi/public_sites/hattu.example.com/` micro-editorilla. Tiedostoon irjoitin mitä halusin hattu.example.com sivulla näkyvän.

![image](https://github.com/user-attachments/assets/9da45f00-2852-4489-9888-fa95d9b069cc)

Latasin localhost-sivun uudelleen ja kirjoittamani teksti näkyi sivulla.

![image](https://github.com/user-attachments/assets/b4004a91-7b33-49af-aaf0-d2b43c841b34)

## HTML5 sivu
Tehdään hattu.example.com sivusta HTML5 sivu Karvisen ohjeiden mukaan (https://terokarvinen.com/2017/starting-with-javascript-arrays-for-of-f12-console/2012/short-html5-page).

Muokkasin sivun index.html tiedostoa

        micro /home/lassihi/public_sites/hattu.example.com/intex.html

![image](https://github.com/user-attachments/assets/5c3b21d4-425f-488e-afc3-b54b49606c98)

Lisäsin vielä kuvan piristämään sivua. Jotta kuva näkyisi sivulla, niin vein kuvatiedoston samaan kansioon, kuin index.html.

![image](https://github.com/user-attachments/assets/26c74339-f499-4637-97ab-54149d27641c)

Avasin sivun selaimella.

![image](https://github.com/user-attachments/assets/7736949f-43ed-45ac-b6a1-4b125279f5c3)

## Curl
curl mahdollistaa datan hakemisen URLin avulla palvelimilta. 
