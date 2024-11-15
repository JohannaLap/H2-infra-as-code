## x) Tiivistelmä
tämä vielä kesken

## a) Vagrantin asennus
Tarkistin, että vagrant on asennettuna koneelle. 

![kuvateksti](https://github.com/JohannaLap/H2-infra-as-code/blob/main/vagrant%20--version2.png)


## b) Vagrantilla tehty linux-virtuaalikone
Tässä kohtaa minulla oli jotakin ongelmia hyvin pitkään. Sain useaan kertaan saman error viestin. 

![ongelmia](https://github.com/JohannaLap/H2-infra-as-code/blob/main/ongelmia...png)

Yritin ladata ja asentaa vagrantin uudelleen ja tämä ratkaisikin ongelmani. 

Olin siis luonut uuden hakemiston.

![hakemisto vagrantille](https://github.com/JohannaLap/H2-infra-as-code/blob/main/hakemisto%20vagrantille.png)

Loin vagrantfilen.

![vagrantinit](https://github.com/JohannaLap/H2-infra-as-code/blob/main/vagrant%20init.png)

Jonka jälkeen tosiaan käynnistin vagrantin uudelleen. 

![vagrant up](https://github.com/JohannaLap/H2-infra-as-code/blob/main/vagrant%20up.png)

Tarkistin vielä, että versio on päivitetty nyt. Tässä näkyy, että nyt on käytössä uudempi versio.

![uusiversio](https://github.com/JohannaLap/H2-infra-as-code/blob/main/uusiversio.png)

Ja tässä vielä näkymä virtualboxissa. Uusi vagrant kone on ilmestynyt. 

![vagrant virtualboxissa](https://github.com/JohannaLap/H2-infra-as-code/blob/main/vagrant%20virtualboxissa.png)

Avasin yhteyden ssh:lla virtuaalikoneeseen, jolla pääsin koneen sisälle. Testasin vielä komennolla ls -la että näen koneen sisältöä. 

![ssh ja ls](https://github.com/JohannaLap/H2-infra-as-code/blob/main/ssh%20ja%20ls%20vagrantkoneella%20.png)

## c) Kaksin kaunihimpi
Muokkasin edellisessä kohdassa jo valmiiksi löytyvää vagrantfileä ohjeiden mukaiseen muotoon. 
Näin sain luotua kaksi virtuaali konetta. 
Ajoin vagrant up komennon uudestaan ja tarkistin, että molemmat koneet ovat näkyvillä virtualboxissa. 

![t_001 ja t_002](https://github.com/JohannaLap/H2-infra-as-code/blob/main/vagrantt%20up%20ja%20notepadkomento.png)

![notepad](https://github.com/JohannaLap/H2-infra-as-code/blob/main/notepad.png)

![testvagrant_0012](https://github.com/JohannaLap/H2-infra-as-code/blob/main/testvagrant_0012.png)

Testatin, että koneet saavat yhteyden nettiin ja toisiinsa

![t_001 googleping](https://github.com/JohannaLap/H2-infra-as-code/blob/main/t_001%20googleping.png)

![ping 001 to 002](https://github.com/JohannaLap/H2-infra-as-code/blob/main/pint001%20to%20t002.png)

![ping 002 to 001](https://github.com/JohannaLap/H2-infra-as-code/blob/main/ping%20002%20to%20001.png)


## d) Herra-orja verkossa
Asensin salt-masterin t001 koneelle. Ja minionin t002 koneelle. 

![salt001](https://github.com/JohannaLap/H2-infra-as-code/blob/main/salt001.png)

![salt002](https://github.com/JohannaLap/H2-infra-as-code/blob/main/salt002.png)

Tarkistin että sekä minion, että masteri ovat aktiivisina. 

![master active](https://github.com/JohannaLap/H2-infra-as-code/blob/main/master%20active.png)

![minionactive](https://github.com/JohannaLap/H2-infra-as-code/blob/main/minion%20active.png)

Muokkasin minionin tiedostoon masterin ip osoitteen. Tämän jälkeen käynnistin minionin vielä uudestaan. Masterin ip:n sai helposti esimerkiksi aiemmin muokatusta tiedostosta, jossa oli molempien koneiden ip:t.

![masteripnotepad](https://github.com/JohannaLap/H2-infra-as-code/blob/main/minionille%20master.png)

![restart minion](https://github.com/JohannaLap/H2-infra-as-code/blob/main/restart%20minion.png)

Hyväksyin avaimen.

![kuvateksti](https://github.com/JohannaLap/H2-infra-as-code/blob/main/unaccepted.png)

![kuvateksti](https://github.com/JohannaLap/H2-infra-as-code/blob/main/avaimen%20hyv%C3%A4ksyminen.png)

Testasin, että t001 kone voi pingata t002

![testping](https://github.com/JohannaLap/H2-infra-as-code/blob/main/t002%20test..ping%20from%20t001.png)

Testasin myös masterkoneen kautta asentaa vimin t002 koneelle. 

![vim asennus](https://github.com/JohannaLap/H2-infra-as-code/blob/main/vim%20asennus%20t002%20t001.lt%C3%A4.png)

## e) Infrakoodi
Ensiksi loin hakemiston komennolla sudo mkrid -p /srv/salt/hello.
Tämän jälkeen siirryin hakemistoon ja loin tiedoston init.sls.

![luominen ja testaus](https://github.com/JohannaLap/H2-infra-as-code/blob/main/luominen%20ja%20testaus.png)

Lisäsin sisältöä.

![sisöltö](https://github.com/JohannaLap/H2-infra-as-code/blob/main/sis%C3%A4lt%C3%B6.png)

Testasin. Testauksessa näkyy tietoja (kuten tehdyistä muutoksista, jos niitä on)ajetusta sudo salt-call --local state.apply komennosta.

![salt-call --local](https://github.com/JohannaLap/H2-infra-as-code/blob/main/salt-call%20--local.png)

## f) Tiedoston ajo verkon yli orjalla 

Kun olin ensiksi testannut toiminnan t001 koneella jolla loin tiedoston, kokeilin toimiiko se myös orjalla. Toimihan se!

![stateapplyt002](https://github.com/JohannaLap/H2-infra-as-code/blob/main/stateapply%20t002.png)

## g) sls tiedosto joka käyttää usempaa funktiota

Ensiksi loin salt hakemistoon testi1.sls tiedoston. Lisäsin tiedostoon sisällön, joka varmistaa että apache2 on asennettuna ja tarvittaessa asentaa sen. Sen jälkeen testasin toimiiko tämä minion koneella ja näytti toimivan

![apache hakemisto luominenja testaus](https://github.com/JohannaLap/H2-infra-as-code/blob/main/apache%20hakemiston%20luominen%20ja%20state%20aplly.png)

![apache2](https://github.com/JohannaLap/H2-infra-as-code/blob/main/apache%202.png)

![apache asennuksen onnistuminen](https://github.com/JohannaLap/H2-infra-as-code/blob/main/apachen%20asennuksen%20onnistumisen%20varmistaminen.png)

Testasin että sls-tiedosto on idempotentti. Nähdään, ettei näkymä muutu, vaikka komento ajetaan uudestaan.

![apache testaus ja idempotentti](https://github.com/JohannaLap/H2-infra-as-code/blob/main/apasche%20testaus%20%2B%20idempotentti.png)

Halusin ensiksi testä apachen toimivuuden, enne kuin lisäsin sisältöä sls tiedostoon. 
Lisäsin testuser käyttäjän, jonka kotihakemisto on /home/testuser

![apache + test user nano](https://github.com/JohannaLap/H2-infra-as-code/blob/main/apache%20%2B%20testuser%20nano.png)

![testi apche ja testuser](https://github.com/JohannaLap/H2-infra-as-code/blob/main/testi%20apache%20ja%20testuser.png)


## Lähteet:

https://terokarvinen.com/palvelinten-hallinta/

https://terokarvinen.com/2024/hello-salt-infra-as-code/

https://terokarvinen.com/2018/salt-quickstart-salt-stack-master-and-slave-on-ubuntu-linux/?fromSearch=salt%20quickstart%20salt%20stack%20master%20and%20slave%20on%20ubuntu%20linux

https://terokarvinen.com/2021/two-machine-virtual-network-with-debian-11-bullseye-and-vagrant/

https://terokarvinen.com/2023/salt-vagrant/#infra-as-code---your-wishes-as-a-text-file

https://oispadotka.wordpress.com/2020/05/12/h6/

https://docs.saltproject.io/en/latest/topics/cloud/vagrant.html

https://tuomasvalkamo.com/CMS-course/week-6/












