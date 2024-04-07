# h2 Soitto kotiin

Toisen viikon kotitehtävät.

Tehtävänannot kurssisivulla: https://terokarvinen.com/2024/configuration-management-2024-spring/.

## Kotitehtävissä käytetyn fyysisen tietokoneen tiedot

Malli: Lenovo ThinkPad X270

Suoritin: Intel(R) Core(TM) i5-6300U CPU @ 2.40GHz 2.50 GHz

Asennettu RAM-muisti: 8.00 GB (7.88 GB käytettävissä)

Järjestelmätyyppi: 64-bittinen käyttöjärjestelmä, x64-suoritin

Käyttöjärjestelmä: Windows 10 Pro

Käyttöjärjestelmän versio: 22H2

## x) Lue ja tiivistä

Tiivistelmät opettajan osoittamista artikkeleista.

### Usean virtuaalikoneen luonti Vagrantin avulla

- Vagrant-ohjelmistolla voidaan hallita samanaikaisesti useita virtuaalikoneita VirtualBox-virtualisointialustalla. 

- Ladataan Vagrant-ohjelmisto fyysiseen isäntäkoneeseen.

- Luodaan fyysiseen isäntäkoneeseen oma hakemisto virtuaalikoneille ja luodaan siihen Vagrant-konfiguraatiotiedosto. Konfiguraatiotiedosto sisältää määritykset luotavia virtuaalikoneita koskien.

- Käynnistetään haluttu virtuaalikone: fyysisen isäntäkoneen komentokehotteessa annetaan komento ```vagrant up``` + virtuaalikoneen ID.

- Otetaan SSH-yhteys haluttuun virtuaalikoneeseen: fyysisen isäntäkoneen komentokehotteessa annetaan komento ```vagrant ssh``` + virtuaalikoneen ID.

### Salt herra-orja -arkkitehtuuri

- Salt-ohjelmiston avulla voi hallita suuria määriä tietokoneita.

- Herra (master) on tietokone, joka hallitsee ohjaa ja hallitsee orjatietokonetta (slave) -> yksi herra hallitsee useita orjia.

- Herran tulee olla julkisesti saavutettavissa, mutta orjan sijainti voi olla tuntematon ja se voi sijaita esim. palomuurin takana.

- Tietokoneelle tulee ladata uusimmat päivitykset ennen herra- tai orjaroolin määrittämistä. Linux-pohjaisissa järjestelmissä tämä tapahtuu komennolla ```sudo apt-get update```.

- Herran rooli ladataan Linux-pohjaisissa järjestelmissä komennolla ```sudo apt-get -y install salt-master```.

- Orjan rooli ladataan Linux-pohjaisissa järjestelmissä komennolla ```sudo apt-get -y install salt-minion```.

- Orjan tulee tietää herran sijainti, eli orjan konfigurointitiedostoon tulee lisätä herran IP-osoite.

- Orjan konfigurointitiedostoon tehtyjen muutosten jälkeen orjarooli (slave minion) tulee käynnistää uudelleen komennolla ```sudo systemctl restart salt-minion.service```.

- Orjat saavat yhteyden herraan lähettämällä sille avaimen, jonka herra voi katsoa ja hyväksyä komennolla ```sudo salt-key -A```.

### Hello Salt Infra-as-Code

## a) Virtuaalikoneiden luonti ja niiden toimivuuden testaaminen

Asensin Vagrant-ohjelmiston fyysiseen tietokoneeseen edellisen kotitehtävän yhteydessä. Tarkistin asennetun Vagrant-ohjelmiston versio komennolla ```vagrant --version```.

![kuva](https://github.com/NooraOlkkonen/Palvelinten-hallinta/assets/165004946/6d25cb46-6ab8-4f37-b3d1-5042bbd0aee5)

Loin h2-nimisen hakemiston fyysiselle tietokoneelle tämän tehtävän virtuaalikoneita varten. Käytin hakemiston luontiin komentoa ```mkdir h2```.

  ![kuva](https://github.com/NooraOlkkonen/Palvelinten-hallinta/assets/165004946/a9a77544-e169-44fe-9dcf-0461263a4942)

Loin virtuaalikoneille t001 ja t002 konfiguraatiotiedoston NotePad-tekstieditorilla. Käytin konfiguraatiotiedoston pohjana opettajan jakamaa konfiguraatiotiedostomallia. Tallensin konfiguraatiotiedoston h2-hakemistoon.

![kuva](https://github.com/NooraOlkkonen/Palvelinten-hallinta/assets/165004946/a50ae087-867b-4b4e-ab57-754b36bb7822)

Konfiguraatiotiedoston nimessä näkyi tiedostopääte (.txt). Opin tiistain 2.4.2024 opetuskerralla, ettei konfugiraatiotiedosto toimi, jos nimessä näkyy tiedostopääte. 

![kuva](https://github.com/NooraOlkkonen/Palvelinten-hallinta/assets/165004946/ebaf8551-c9cc-4016-9b70-96044b4a9beb)

Nimesin uudelleen konfiguraatiotiedoston ilman tiedostopäätettä .txt käyttämällä komentokehotteessa komentoa ```mv Vagrantfile.txt Vagrantfile``` (vanha tiedoston nimi -> uusi tiedoston nimi). Tämän jälkeen konfiguraatiotiedosto oli sellainen kuin pitää. 

![kuva](https://github.com/NooraOlkkonen/Palvelinten-hallinta/assets/165004946/c52b9ccc-e5ec-4b2b-80c3-ccdf6eecffdb)

Käynnistin t001-virtuaalikoneen komennolla ```vagrant up t001```.

![kuva](https://github.com/NooraOlkkonen/Palvelinten-hallinta/assets/165004946/02617b97-b28c-4b60-8a56-0ef0821fb795)

Otin SSH-yhteyden t001-virtuaalikoneeseen komennolla ```vagrant ssh t001```.

![kuva](https://github.com/NooraOlkkonen/Palvelinten-hallinta/assets/165004946/af477418-1b1c-4984-91ed-e11b9898b9d0)

Käynnistin myös t002-virtuaalikoneen ja otin siihenkin SSH-yhteyden.

![kuva](https://github.com/NooraOlkkonen/Palvelinten-hallinta/assets/165004946/29e649c2-3ac5-4d4c-a409-3ed0ca363c1e)

![kuva](https://github.com/NooraOlkkonen/Palvelinten-hallinta/assets/165004946/32775013-9115-4728-9519-846ac42d17a3)

Molemmat virtuaalitietokoneet näkyivät käynnistyneinä VirtualBoxissa.

![kuva](https://github.com/NooraOlkkonen/Palvelinten-hallinta/assets/165004946/1afa27df-c32b-49cc-8c9c-5419716be28c)

Seuraavaksi tarkistin t001- ja t002-virtuaalikoneiden IPv4-osoitteet komennolla ```hostname -I```. Kyseisellä komennolla saadaan selville isäntänimen kaikkien verkkoliitäntöjen IPv4-osoitteet.

![kuva](https://github.com/NooraOlkkonen/Palvelinten-hallinta/assets/165004946/e5e546ef-7c89-4333-9b4e-5e21a9628af2)

![kuva](https://github.com/NooraOlkkonen/Palvelinten-hallinta/assets/165004946/25201bb4-7e64-47b4-8c66-611ce7c8389f)

Testasin toimiiko yhteys t001- ja t002-virtuaalikoneiden välillä. Käytin tähän komentoa ```ping``` + virtuaalikoneen IPv4-osoite. Yhteys toimi kumpaankin suuntaan.

![kuva](https://github.com/NooraOlkkonen/Palvelinten-hallinta/assets/165004946/e662252c-1ae1-410d-a198-b6fd2377e74b)

![kuva](https://github.com/NooraOlkkonen/Palvelinten-hallinta/assets/165004946/25d192fb-9495-4537-a776-ddd2b7419f2a)


## b) Salt herra-orja-arkkitehtuuri verkon yli

1. Määritin **t001**-virtuaalikoneen herraksi (master)

- Latasin uusimmat päivitykset komennolla ```sudo apt-get update```. Tämän jälkeen latasin herran roolin komennolla ```sudo apt-get -y install salt-master```.

  ![kuva](https://github.com/NooraOlkkonen/Palvelinten-hallinta/assets/165004946/205e11b2-d4fb-4ddd-bda4-6a69ae9b5268)

- Tarkistin herran roolin statuksen (salt-master status) komennolla ```sudo systemctl status salt-master```. Rooli asentui ja käynnistyi, koska tilana active (running).

  ![kuva](https://github.com/NooraOlkkonen/Palvelinten-hallinta/assets/165004946/875bd45f-9e3b-495c-b7c8-8842933646f4)


2. Määritin **t002**-virtuaalikoneen orjaksi (slave)

- Latasin uusimmat päivitykset komennolla ```sudo apt-get update```. Tämän jälkeen latasin orjan roolin komennolla ```sudo apt-get -y install salt-minion```.

  ![kuva](https://github.com/NooraOlkkonen/Palvelinten-hallinta/assets/165004946/6b624ec3-4494-48f1-bd56-47f41b89313c)

  ![kuva](https://github.com/NooraOlkkonen/Palvelinten-hallinta/assets/165004946/6beb15ad-4180-423c-b5e7-336fb477aed2)

- Tarkistin orjan roolin statuksen (salt-minion status) komennolla ```sudo systemctl status salt-minion```. Rooli asentui ja käynnistyi, koska tilana active (running).

  ![kuva](https://github.com/NooraOlkkonen/Palvelinten-hallinta/assets/165004946/a70a95f5-e222-4e4f-a832-88054523ad38)

- Määritin herran IP-osoitteen orjan konfiguraatiotiedostoon. Herran IPv4-osoite on 192.168.88.101, kuten kohdassa a) todettu. Pääsin muokkaamaan konfiguraatiotiedostoa komennolla ```sudoedit /etc/salt/minion```.
   
  ![kuva](https://github.com/NooraOlkkonen/Palvelinten-hallinta/assets/165004946/541bee06-e66a-46bc-9ecb-bfdeb89044cd)

- Käynnistin uudelleen orjaroolin (slave minion) komennolla ```sudo systemctl restart salt-minion.service```.

  ![kuva](https://github.com/NooraOlkkonen/Palvelinten-hallinta/assets/165004946/f5fa9eb3-3e5a-4b91-84f2-267ebfebd09a)

3. Hyväksyin herratietokoneella (t001) orjatietokoneen (t002) lähettämän avaimen

- Tarkistin ja hyväksyin orjan (t002) herralle (t001) lähettämän avaimen komennolla ```sudo salt-key -A```.
  
  ![kuva](https://github.com/NooraOlkkonen/Palvelinten-hallinta/assets/165004946/476911d2-f99b-4758-be70-8248c33262da)

## c) Shell-komento herra-orja-yhteyden yli

Selvitin orjatietokoneen nykyisen kirjautuneen käyttäjän nimen ajamalla herratietokoneessa komennon ```sudo salt '*' cmd.run 'whoami'```.

![kuva](https://github.com/NooraOlkkonen/Palvelinten-hallinta/assets/165004946/3cd35930-cdd3-43dc-b27e-e8659914e515)

## d) Idempodentit komennot herra-orja-yhteyden yli

### 1. user

- Suoritin herratietokoneella komennon ```sudo salt '*' state.single user.present 'käyttäjä'```, joka luo käyttäjä-nimisen käyttäjän, jos sellaista ei entuudestaan ole olemassa. Tässä tapauksessa kyseinen käyttäjä todella luotiin, koska sitä ei ollut olemassa (ID: käyttäjä, Result: True, Comment: New user käyttäjä created).

  ![kuva](https://github.com/NooraOlkkonen/Palvelinten-hallinta/assets/165004946/15d14b8e-61dd-4500-9d93-6e6a7921f5d5)

- /etc/passwd-tiedostosta löytyy listattuna kaikki tietokoneen käyttäjät. Tarkistin vielä komennolla ```sudo salt '*' cmd.run 'cat /etc/passwd'```, että uusi käyttäjä-niminen käyttäjä todella luotiin orjatietokoneelle.

  ![kuva](https://github.com/NooraOlkkonen/Palvelinten-hallinta/assets/165004946/eefe926d-eee5-4f21-bc10-ce08ee5c02c3)

- Suoritin uudelleen saman komennon ```sudo salt '*' state.single user.present 'käyttäjä'``` herratietokoneella. Toista samannimistä käyttäjää ei luotu orjatietokoneeseen. Järjestelmä ilmoitti, että kyseinen käyttäjä on jo olemassa (ID: käyttäjä, Result: True, Comment: User käyttäjä is present and up to date).

  ![kuva](https://github.com/NooraOlkkonen/Palvelinten-hallinta/assets/165004946/47ba44fb-1acc-4dea-96ae-299895a59e00)


## e) Tietojen kerääminen orjasta

Tutustuin orjatietokoneen (t002) tietoihin käyttäen herratietokoneella (t001) komentoa ```sudo salt '*' grains.items```. Poimin kolme mielenkiintoista tietoa, jotka sain eriteltyä komennolla ```sudo salt '*' grains.item master ip4_interfaces oscodename```.

![kuva](https://github.com/NooraOlkkonen/Palvelinten-hallinta/assets/165004946/ca21187d-891a-4aba-ba2a-634413899f65)

- ip4_interfaces = orjatietokoneen liitäntöjen IPv4-osoitteet 

- master = orjatietokoneeseen määritetyn herran IPv4-osoite

- oscodename = orjatietokoneen käyttöjärjestelmän koodinimi
 

## f) Hello IaC

# Lähteet

Gite 2024: Linux List All Users In The System Command. Luettavissa: https://www.cyberciti.biz/faq/linux-list-users-command/. Luettu 7.4.2024.

Karvinen 2023: Two Machine Virtual Network With Debian 11 Bullseye and Vagrant. Luettavissa: https://terokarvinen.com/2021/two-machine-virtual-network-with-debian-11-bullseye-and-vagrant/. Luettu: 6.4.2024.

Karvinen 2018: Salt Quickstart – Salt Stack Master and Slave on Ubuntu Linux. Luettavissa: https://terokarvinen.com/2018/salt-quickstart-salt-stack-master-and-slave-on-ubuntu-linux/?fromSearch=salt%20quickstart%20salt%20stack%20master%20and%20slave%20on%20ubuntu%20linux. Luettu: 6.4.2024.

Karvinen 2023: Hello Salt Infra-as-Code. Luettavissa: https://terokarvinen.com/2024/hello-salt-infra-as-code/. Luettu: 7.4.2024.
 
Linux 2009: Hostname-komennon manuaalisivu. Luettu 6.4.2024.
