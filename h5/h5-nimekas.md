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

![image](https://github.com/user-attachments/assets/6a7b86e6-a707-4dbc-bbf6-a1f5d49ee695)

Kopioin index.html muiden tiedostojen pohjaksi.

![image](https://github.com/user-attachments/assets/b2d2613b-ddc5-477d-bd4d-e8467fe34975)

Muokkasin julkaisut sivua `micro index.html`.

![image](https://github.com/user-attachments/assets/ea8c6972-1a3c-416b-9676-509f4b6540e7)

Muokkasin projektit sivua `micro julkaisut.html`.

![image](https://github.com/user-attachments/assets/17c2fcc3-71c7-4883-8818-12442b38bf8d)

Kopioin seuraavaksi kansion lassihirvonen.com virtuaalikoneeltani palvelimelle public_sites kansioon scp-komennon avulla. 

![image](https://github.com/user-attachments/assets/f302bfc2-9123-4680-a7f9-2cb427ccb6cc)

Tarkastin selaimella, että muutokset toimivat.

![image](https://github.com/user-attachments/assets/e3147cb1-71f3-426a-9ad8-cca368cc9ea4)
![image](https://github.com/user-attachments/assets/deb02be1-1b6d-414e-b36d-e89df227bcfb)
![image](https://github.com/user-attachments/assets/bbe71bc8-5838-48d8-adee-881c03d85a57)

## d) A- ja CNAME-tietue alidomain
Siirryin luomaan alidomaineja namecheapin sivulle. Sivulla navigoin Account -> Dashboard -> Manage -> Advanced DNS -> Add a new record. Olin jo tehtävässä a määrittänyt www-alidomainin A-tietueella, joten tein uuden alidomainin CNAME-tietueella. A- ja CNAME-tietueen pääasiallinen ero on, että A-tietueella määritetään domainnimi osoittamaan IP-osoitteeseen, kun taas CNAME-tietueella määritetään domainnini osoittamaan toiseen nimeen.

Loin uuden CNAME tietueen it-alidomainille. Laitoin tässä kohtaa alidomainin osoittamaan vain päädomainiin.

![image](https://github.com/user-attachments/assets/0b29981b-0a6d-4350-b4b3-386aed8204af)

Testasin lopuksi selaimella, että alidomain toimii.

![image](https://github.com/user-attachments/assets/b3f3dd61-d616-462b-beac-b011ea03da30)

## e) Tutki jonkin nimen DNS-tietoja 'host' ja 'dig' -komennoilla
"Host" tai "dig" -komennot eivät ole asennettuna koneellani, joten asensin ne komennolla `sudo apt-get install dnsutils`. Host on DNS lookup työkalu, jota käytetään tavallisesti hakemaan nimeä vastaava IP-osoite ja toisinpäin. Dig on taas DNS palvelinten tutkimiseen ja vianselvitykseen käytetty työkalu, joka tarjoaa host komentoa monipuolisemmat ominaisuudet. 

Ajoin seuraavaksi komennot omalle domainnimelleni.
![image](https://github.com/user-attachments/assets/4661c726-916d-4741-b2a8-f22b3573d451)
![image](https://github.com/user-attachments/assets/925eab2b-1e4b-4a22-9c3a-0ce27571df97)

Host komennolla saatu vastaus on yksinkertainen ja näyttää mikä IP-osoite on yhdistetty nimeen. Tämän lisäksi näytetään sähköpostista vastaavat viestipalvelimet, joita Dig komento ei oletuksena näytä. Dig komento näyttää tarkemmat tiedot DNS kyselystä ja vastauksesta. Oleellista on katsoa ANSWER SECTION -kohdan tiedot, jossa näytetään DNS palvelimen vastaus kyselyyn. Kumpikin komento sai selville domainnimeeni yhdistetyn IP-osoitteen.
