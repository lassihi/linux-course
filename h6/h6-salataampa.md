# Harjoitus 6: Salataampa
Kurssi: Linux palvelimet https://terokarvinen.com/linux-palvelimet/ \
Tehtävänanto: https://terokarvinen.com/linux-palvelimet/#h6-salataampa

## x) Lue ja tiivistä. Tiivistelmäksi riittää muutama ranskalainen viiva per artikkeli.
Let's Encrypt 2024: [How It Works](https://letsencrypt.org/how-it-works/)
- Let's Encrypt on voittoa tavoittelematon varmenteen myöntäjä, joka mahdollistaa https-palvelinten sertifikaattien hallinnoinnin ACME (Automatic Certificate Management Environment) -protokollan ja palvelimelle asennettavan agenttiohjelmiston avulla.
- Domainin varmistamiseksi CA (varmenteen myöntäjä, tässä tapauksessa Let's Encrypt) ja palvelinagentti jakavat palvelinagentin luoman avainparin julkisen avaimen keskenään, jonka jälkeen CA pyytää agenttia todistamaan domainin hallinnan esimerkiksi luomalla tietyn tiedoston tiettyyn sijaintiin kyseisessä domainissa. Lopuksi palvelinagentti varmistaa CA:lle omistavansa julkista avainta vastaavan yksityisen avaimen, lähettämällä CA:n märittämän satunnaisluvun takaisin CA:lle, allekirjoitettuna yksityisellä avaimella. 
- Varmistuksen jälkeen palvelinagentti voi hallinnoida sertifikaattia allekirjoittamalla hallintaviestit yksityisellä avaimellaan.

Lange 2024: Lego: Obtain a Certificate: [Using an existing, running web server](https://go-acme.github.io/lego/usage/cli/obtain-a-certificate/index.html#using-an-existing-running-web-server)
- Jos palvelimen portti 80 on jo käytössä, tulee komennossa `--http`-valinnan lisäksi käyttää `--http.webroot`-valintaa. Tällöin http-01 haasteen tiedot tallennetaan annettuun hakemistoon kansion `.well-known/acme-challenge` sisälle, eikä palvelinta käynnistetä.
- Komennossa annetun hakemiston on oltava julkisesti saatavilla domainin juurihakemistossa.
- Esimerkki komennosta:

      lego --accept-tos --email you@example.com --http --http.webroot /path/to/webroot --domains example.com run

The Apache Software Foundation 2025: Apache HTTP Server Version 2.4 [Official] Documentation: SSL/TLS Strong Encryption: How-To: [Basic Configuration Example](https://httpd.apache.org/docs/2.4/ssl/ssl_howto.html#configexample)
- Toimiakseen SSL(Secure Sockets Layer)/TLS(Transport Layer Security)-yhteydellä, sivuston konfiguraatiotiedoston tulee sisältää vähintään seuraava:

      LoadModule ssl_module modules/mod_ssl.so
      Listen 443
      <VirtualHost *:443>
          ServerName www.example.com
          SSLEngine on
          SSLCertificateFile "/path/to/www.example.com.cert"
          SSLCertificateKeyFile "/path/to/www.example.com.key"
      </VirtualHost>


## Suoritusympäristö
Tietokone: Lenovo Legion Y540-15IRH kannettava kytkettynä langallisesti kotiverkkoon.\
-Intel Core i7-9750H\
-NVIDIA Geforce RTX 2060 6GB\
-16GB DDR4 2666MHz\
Käyttöjärjestelmä: Windows 11 23H2

Virtualisointiympäristö: VirtualBox Version 7.1.4. Käyttöjärjestelmänä toimii Debian 12 Bookworm käyttäen alla olevan kuvan mukaisia VirtualBox-asetuksia.

![virtualbox-asetukset](https://github.com/user-attachments/assets/ad4b8cd8-9cd2-4ebd-b4f7-86d0b8e23aa1)

## a) Let's. Hanki ja asenna palvelimellesi ilmainen TLS-sertifikaatti Let's Encryptilta. Osoita, että se toimii.
28.2.2024 17.55-19.00

Aloitin kirjautumalla palvelimelle ssh-yhteydellä, `ssh lassi@lassihirvonen.com`. \
Käynnistin apachen uudestaan, jotta pystyin aloittamaan puhtaalta pöydältä, `sudo systemctl apache2 restart`. \
Ja varmistin selaimella, että sivu vielä toimii. 

![image](https://github.com/user-attachments/assets/9b9d2c02-6814-4a7c-bc66-af70738dd200)

Päivitin seuraavaksi paketit, `sudo apt-get update` ja `sudo apt-get upgrade`.

Asensin lego-ohjelman palvelimen sertifikaattien hallintaa varten.

![image](https://github.com/user-attachments/assets/26285756-4503-4462-8aec-80b69dabd7a3)

Ennen oikean sertifikaatin hakemista, varmistin ensiksi että sertifikaatin hakeminen onnistuu testipalvelimelta. Testipalvelimen osoitteen hain Let's Encryptin sivuilta (https://letsencrypt.org/fi/docs/staging-environment/). Luennon muistiinpanoja hyödyntämällä annoin seuraavan komennon hakeakseni testisertifikaatin.

![image](https://github.com/user-attachments/assets/45301fb8-79e8-42e3-83dd-61ff1c2635dc)

Tulosten perusteella komento vaikutti toimivan, joten varmistin antamastani polusta sertifikaattien olemassaolon.

![image](https://github.com/user-attachments/assets/9f1d8fe2-c1a7-4059-92eb-88739f1a8f06)

Sertifikaatit löytyivät ja koska ne eivät ole toimivia, niin poistin ne aitojen sertifikaattien tieltä.

![image](https://github.com/user-attachments/assets/c1c41999-7b09-41fe-bf08-b8e4d2882eab)

Ajoin lego-komennon uudestaan hakeakseni tällä kertaa oikeat sertifikaatit. Muokkasin komentoa poistaen testipalvelimen asetuksen `--server=https://acme-staging-v02.api.letsencrypt.org/directory`.

![image](https://github.com/user-attachments/assets/98d9420d-d431-48c4-9ab9-3c03c2cdd5e1)

Avasin name based host sivun asetustiedoston ja loin sinne asetukset porttiin 443 tuleville https-yhteyksille.

![image](https://github.com/user-attachments/assets/042574fc-4f0b-4bd1-b2ee-1811fa7a45cb)

![image](https://github.com/user-attachments/assets/68cbee55-94f6-4150-a256-9d205e4cc1fc)

Yritin ottaa SSL-yhteyden käyttöön ajamalla komennon `sudo a2enmod ssl` ja käynnistämällä apachen uudestaan, `sudo systemctl restart apache2`, joka ei onnistunut.

![image](https://github.com/user-attachments/assets/0a8ee76c-ddb8-43bf-ba6c-2081e3bced14)

Kävin tarkastamalla apachen statuksen virheilmoituksessa annetulla ensimmäisellä komennolla.

![image](https://github.com/user-attachments/assets/e39e853e-4e5a-4356-9472-041547d660a8)

Tulosteessa puhuttiin puuttuvista moduuleista konfiguraatiossa ja muistin Apachen dokumentaatiossa mainitut asetukset `LoadModule ssl_module modules/mod_ssl.so`, `Listen 443`, jotka kävin lisäämässä tiedostoon.

![image](https://github.com/user-attachments/assets/c0e9b438-29f9-4065-b341-cffda888c885)

Yritin käynnistää apachea uudelleen ja sama virheilmoitus tulostui. 

![image](https://github.com/user-attachments/assets/5a9bd3de-eac9-432a-9ffb-ab7965a7862c)

Olin saanut saman virheilmoituksen [harjoituksessa 3](https://github.com/lassihi/linux-course/blob/main/h3/h3-hello-web-server.md), jolloin virhe johtui kirjoitusvirheestä asetustiedostossa. Tarkastin asetustiedoston vielä kerran verraten sitä luennolla käytyyn esimerkkiin ja huomasin kirjoittaneeni `SSLCertificateFileKey`, vaikka esimerkissä oli `SSLCertificateKeyFile`. Muokkasin asetustiedostoa ja poistin myös apachen suosittelemat juuri lisäämäni asetukset, jotta omani vastaisi mahdollisimman tarkasti esimerkkiä.

![image](https://github.com/user-attachments/assets/682c89f9-7654-4d80-b9cf-a94f672600af)

Nyt uudelleenkäynnistys onnistui ongelmitta. 

Tein https-yhteydelle reiän palomuuriin porttiin 443.

![image](https://github.com/user-attachments/assets/598dd8c7-584f-498c-bb19-ee241e4a147b)

Tässä kohtaa varmennetun sivuston tulisi toimia salatulla yhteydellä. Varmistin tietokoneen ja puhelimen selaimella, että https://lassihirvonen.com ja https://www.lassihirvonen.com toimivat.

![image](https://github.com/user-attachments/assets/c7bbfaa0-bb3b-4a21-84f9-c235cd7ebf1a)
![image](https://github.com/user-attachments/assets/0a0e70b5-9b22-4810-8617-15d2a86c20b3)

## b) A-rating. Testaa oma sivusi TLS jollain yleisellä laadunvarmistustyökalulla.
28.2.2024 23.41-23.46

Menin selaimella osoitteeseen https://www.ssllabs.com/ssltest/ ja syötin domainnimen lassihirvonen.com hostname-hakukenttään. Sivusto lataili tuloksia noin kaksi minuuttia, jonka jälkeen antoi arvosanaksi A.

![image](https://github.com/user-attachments/assets/3f7519f7-0af9-4127-9078-0d4ed7d94342)

## c) Vapaaehtoinen: Tee weppilomake, jossa on käyttäjätunnus ja salasana. Käytä salaamatonta http-yhteyttä. Sieppaa liikennettä (esim. Wireshark, ngrep). Mitä havaitset? Mitä vaikutuksia tällä on tietoturvaan?
28.2.2024 23.11-23.41

En tehnyt tässä tehtävässä weppilomaketta palvelimelle, vaan vertailin Wiresharkilla http- ja https-yhteyksiä.

Testasin TLS:n toiminnan manuaalisesti vertaamalla Wireshark-ohjelmalla paketteja, joita lähetettiin http- ja https-yhteydellä tietokoneen ja palvelimen välillä. Otin ensiksi selaimella yhteyttä osoitteeseen http://lassihirvonen.com, jonka jälkeen host-koneelle asennetulla Wiresharkilla suodatin näyttämään vain kyseisen keskustelun paketit.

![image](https://github.com/user-attachments/assets/e3304c85-6da4-46bf-a389-f4d647dd1790)

Avasin palvelimen (94.237.117.142) lähettämän paketin, joka sisälsi "HTTP 200 OK" vastauksen. Pakettia tutkimalla vastaus näkyi tekstinä.

![image](https://github.com/user-attachments/assets/f2a940fe-3d7a-47d3-83b1-8f96803c7190)

Jos liikennettä tarkkailtaisiin esimerkiksi langattoman verkon kautta, kun käyttäjätunnus ja salasana syötetään salaamatonta yhteyttä käyttävään palveluun, niin tiedot näkyisivät yhtä lailla selkotekstinä, todennäköisesti client laitteelta lähetetyssä get- tai post-pyynnössä.

Otin seuraavaksi yhteyttä osoitteeseen https://lassihirvonen.com, suodatin jälleen sovelluksen näyttämään vain kyseisen keskustelun paketit.

![image](https://github.com/user-attachments/assets/b598f9e5-05da-4dd0-b46d-f037ff081023)

Heti ensisilmäyksellä huomaa, että nyt protokollina on käytössä TCP ja TLS, eikä pakettien tulkinta ole yhtä helppoa kuin salaamattomassa liikenteessä. Hieman TLS-protokollaa tutkittuani uskoin, että ensimmäiset TCP- ja TLS-kättelyn jälkeiset paketit ovat paketit numero 56 ja 57. Kuten salaamatonta liikennettä tarkastellessa, niin avasin nytkin palvelimen lähettämän paketin (no. 57) tarkempaa tutkintaa varten. Kohdassa "Encrypted Application Data" näkyy paketissa lähetetty tieto salattuna.

![image](https://github.com/user-attachments/assets/fb432481-3a87-4078-a180-89be049573a7)

Toisin kuin salaamattomassa liikenteessä, niin mahdollisten käyttäjätunnusten ja salasanojen löytäminen salatusta liikenteestä on lähes mahdotonta, ellei tiedossa ole salauksessa käytetyn avainparin yksityinen avain.

## Lähteet
Karvinen 2025: Linux palvelimet: https://terokarvinen.com/linux-palvelimet/

Let's Encrypt 2024: How It Works: https://letsencrypt.org/how-it-works/

Lange 2024: Lego: Obtain a Certificate: Using an existing, running web server: https://go-acme.github.io/lego/usage/cli/obtain-a-certificate/index.html#using-an-existing-running-web-server

The Apache Software Foundation 2025: Apache HTTP Server Version 2.4 [Official] Documentation: SSL/TLS Strong Encryption: How-To: Basic Configuration Example: https://httpd.apache.org/docs/2.4/ssl/ssl_howto.html#configexample

Let's Encrypt 2024: Staging Environment: https://letsencrypt.org/fi/docs/staging-environment/

SSLLabs: SSL Server Test: https://www.ssllabs.com/ssltest/

Cloudflare: What is TLS (Transport Layer Security)?: https://www.cloudflare.com/learning/ssl/transport-layer-security-tls/
