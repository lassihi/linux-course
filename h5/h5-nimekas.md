# Harjoitus 5: Nimekäs
Kurssi: Linux palvelimet https://terokarvinen.com/linux-palvelimet/ \
Tehtävänanto: https://terokarvinen.com/linux-palvelimet/#h5-nimekas

## Suoritusympäristö
Tietokone: Lenovo Legion Y540-15IRH kannettava kytkettynä langallisesti kotiverkkoon.\
-Intel Core i7-9750H\
-NVIDIA Geforce RTX 2060 6GB\
-16GB DDR4 2666MHz\
Käyttöjärjestelmä: Windows 11 23H2

Virtualisointiympäristö: VirtualBox Version 7.1.4. Käyttöjärjestelmänä toimii Debian 12 Bookworm käyttäen alla olevan kuvan mukaisia VirtualBox-asetuksia.

![virtualbox-asetukset](https://github.com/user-attachments/assets/ad4b8cd8-9cd2-4ebd-b4f7-86d0b8e23aa1)

## a) Laita julkinen nimi osoittamaan omaan koneeseesi
Kirjauduin sisään.

Tarkistin nimen.

![image](https://github.com/user-attachments/assets/b9cac9f9-51d8-4798-85e8-256afdfd7e60)

Vein nimen ostoskoriin, otin auto-renew valinnan päälle, lisäsäin alennuskoodin ja vahvistin tilauksen.

![image](https://github.com/user-attachments/assets/e3db233c-8bcc-454b-bc79-4764dc250c16)

Syötin nimen, osoitteen, puhelinnumeron.

Registrant Contact, Administrative Contact, Technical Contact, Billing Contact oletuksena.

Lisäsin pankkikortin palveluun ja ostin nimen.

Seuraavaksi menin päivittämään A-tietueen nimelle Account -> Dashboard -> Domain list

![image](https://github.com/user-attachments/assets/abaf1ec4-7df7-489a-9cc9-d6832312d7fd)

Nimen oikealta puolelta klikkasin Manage ja siirryin Advanced DNS osioon.

![image](https://github.com/user-attachments/assets/66e74929-e9d1-48aa-a5e7-1dc1228c2a0c)

Klikkasin ADD NEW RECORD ja täytin tiedot, jotta domainnimi alkaisi ohjaamaan palvelimeeni. Lopuksi klikkasin SAVE ALL CHANGES.

![image](https://github.com/user-attachments/assets/3b962076-1c0c-40ce-86dc-e2faa831819d)

Odotin noin 5 minuttia ennen domainnimen kokeilemista selaimessa, että asetukset ehtisivät astua voimaan, jottei vahnat tiedot tallennu tietokoneeni tai DNS-palvelinten välimuistiin. Kokeilin selaimella nimiä ja lassihirvonen.com, kuin www.lassihirvonen.com yhdistivät palvelimeen.

![image](https://github.com/user-attachments/assets/cefd9d79-9ba1-4080-a880-b3f3ae54cef9)

## b) Name based host uudessa nimessä
Kirjauduin ssh-yhteydellä palvelimelle ja loin uuden asetustiedoston Apachen sites-available kansioon Name based hostille.

    sudoedit /etc/apache2/sites-available/lassihirvonen.com.conf
![image](https://github.com/user-attachments/assets/beb052cf-984d-4bd5-aa3d-4994503d37d0)

Otin seuraavaksi asetustiedoston käyttöön komennolla `sudo a2ensite lassihirvonen.com.conf`. \
Poistin edellisen name based hostin asetustiedoston käytöstä komenoolla `sudo a2dissite toimiiko.sivusto.com.conf` \
Käynnistin apachen uudestaan, jotta muutokset astuisivat voimaan komennolla `sudo systemctl restart apache2`

Tarkastin muutokset päivittämällä sivun selaimella.

![image](https://github.com/user-attachments/assets/0cdde749-c6f9-44aa-bc0e-e40a95be80d6)

Siirryin kotihakemistossa sijaitsevaan hakemistoon public_sites ja loin sinne uuden hakemiston lassihirvonen.com ja lisäsin uuden hakemiston sisälle index.html tiedoston

![image](https://github.com/user-attachments/assets/e7076464-472f-41e2-a7f7-9c0dcb8932e7)

![image](https://github.com/user-attachments/assets/184dcdbc-e60e-42b6-8567-1d524ecdb441)

Tallensin tiedoston ja päivitin sivun selaimella.

![image](https://github.com/user-attachments/assets/6b58a30c-551f-4a27-98f1-57150b9343a5)

## c) Kolmen erillisen alasivun kotisivu
Katkaisin ssh-yhteyden, jotta voin luodata ja muokata sivuja omalta koneeltani ilman, että ne näkyvät julkisesti netissä. 

Siirryin public_sites kansioon ja loin uuden alikansion lassihirvonen.com, jonne tein index.html tiedoston.

![image](https://github.com/user-attachments/assets/2d25e884-bb34-452c-b902-c9720509acb2)
![image](https://github.com/user-attachments/assets/6efa4fde-6db6-4292-ad62-1b8f612d1df8)

![image](https://github.com/user-attachments/assets/76f3372b-fcce-4361-b593-2d1a90e6530e)

Kopioin index.html muiden tiedostojen pohjaksi.

![image](https://github.com/user-attachments/assets/7872a57e-3b4d-4bc7-9ba3-93a8609e73be)



