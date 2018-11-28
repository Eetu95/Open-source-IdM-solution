# Avoimen lähdekoodin IdM ratkaisu 
Loppuraportti

Tekijät: Jan Parttimaa, Eetu Pihamäki & Markus Nissinen

Kurssi: Monialaprojekti
 
Päivämäärä: 28.11.2018
 
## Sisällysluettelo
<ol>
  <li><a href="#johdanto">Johdanto</a></li>
  <li><a href="#yleista">Yleistä IdM-järjestelmistä (Identity Management System)</a></li>
  <li><a href="#idm-jarjestelmien-vertailu">IdM-järjestelmien vertailu</a></li>
  <li><a href="#midpoint">Midpoint</a></li>
  <ol>
      <li><a href="esivalmistelut">Esivalmistelut</a></li>
      <ol>
          <li><a href="ubuntu-server-asennus-ja-konfigurointi">Ubuntu Server asennus ja konfigurointi</a></li>
          <li><a href="windows-server-asennus-ja-konfigurointi">Windows Server asennus ja konfigurointi</a></li>
          <li><a href="testityoasemien-seka-testipalvelimen-asennus-ja-konfigurointi">Testityöasemien sekä testipalvelimen asennus ja konfigurointi</a></li>
      </ol>
      <li><a href="asennus">Asennus</a></li>
      <li><a href="konfigurointi">Konfigurointi</a></li>
      <ol>
          <li><a href="tietokannan-maarittaminen">Tietokannan määrittäminen</a></li>
          <li><a href="connectoreiden-maarittaminen">Connectoreiden määrittäminen</a></li>
          <li><a href="suojatun-yhteyden-konfigurointi">Suojatun yhteyden konfigurointi</a></li>
      </ol>
      </ol>
 <li><a href="testaus">Testaus</a></li>
 <li><a href="#yhteenveto">Yhteenveto</a></li>
 <li><a href="#lahteet">Lähteet</a></li>
</ol>

## Johdanto<div id='johdanto'></div>
Tässä raportissa kerromme alussa lyhyesti mikä on Identiteetinhallintajärjestelmä (IdM), mitä sillä tehdään ja mitä hyötyjä kyseinen järjestelmä tuo yrityksen tietojärjestelmien käyttäjähallintaan. Tämän jälkeen kerromme kuinka vertailimme avoimen lähdekoodin IdM-järjestelmiä ja kuinka juuri valitsimme testattavaksi järjestelmäksi midPointin. Kerromme myös kuinka midPointin asennus ja konfigurointi onnistuu vaiheittain. Raportin loppuvaiheessa kerromme lisäksi kuinka lisäsimme Linux-palvelimen, OpenLDAP-palvelimen sekä Windows -palvelimen midPointtiin ja kuinka teimme testauksen.

Käynnistimme projektin aiheesta, koska muutamat projektiryhmän jäsenet ovat työssään joutuneet tekemään
töitä Iddentiteetinhallintajärjestelmien parissa. Yleensä kyseiset järjestelmät, jotka ovat yrityksissä
käytössä ovat suljetun lähdekoodin järjestelmiä, jonka vuoksi yritykset
joutuvat maksamaan järjestelmän käytöstä lisenssimaksua. Tämän lisäksi
järjestelmän ylläpidosta, tuesta sekä päivityksistä joudutaan yleensä
maksamaan useita tuhansia euroja. Projektityön ideana oli lähteä vertailemaan
markkinoilla saatavilla olevia avoimen lähdekoodin Identiteetinhallintajärjestelmiä,
vertailla niiden ominaisuuksia sekä laatua. Laatua päästiin kokeilemaan esimerkiksi verkossa saatavilla olevilla demoversioilla.

Projektimme tehtävänä oli vertaa avoimen lähdekoodin Identiteetinhallintajärjestelmiä, joista valitsemme parhaan ja testaamme sen toimivuutta testiympäristössä.

Asetimme projektille tavoitteet, jotka olivat seuraavat: 
- IdM-järjestelmä on toimiva ja luotettava. Testaamme järjestelmää testiympäristössä.
Lopputuloksena on asennettu IdM-järjestelmän Master-kone
sekä muutamat testikoneet.
- Järjestelmä on monipuolinen, ilmainen ja avoimeen lähdekoodiin perustuva.
- IdM-järjestelmiä on vertailtu monipuolisesti sekä vertailussa otetaan
huomioon vaatimukset. Lopputuloksena vertailusta Excel-taulukko
sekä lista ennalta määritellyistä vaatimuksista.

Asetimme myös oppimistavoitteita, jotka olivat seuraavat:
- Oppia IdM-järjestelmistä sekä niiden yhteyksistä muihin järjestelmiin
ja rajapintoihin.
- Kuinka asennetaan IdM-järjestelmä ja kuinka se saadaan käyttövalmiiksi.
- Kuinka liitetään IdM-järjestelmän piiriin muita järjestelmiä.
- Tulokset, lokit ja raportit ovat valmiiksi näytettävissä.
- Opitaan pitämään projektin aikataulusta huolta ja pitämään kiinni työaikakirjauksesta.
<br>



## Yleistä IdM-järjestelmistä (Identity Management System)<div id='yleista'></div>
IdM-järjestelmä (Englanniksi: Identity Management System, Suomeksi:
Identiteetinhallintajärjestelmä) on järjestelmä,
jonka avulla voidaan keskitetysti hallita yrityksen eri tietojärjestelmiä,
palveluita, tietokantoja, ohjelmistoja sekä ohjelmien käyttöoikeuksia että
pääsynhallintaa. IdM:n ansiosta yritys pystyy helposti pitämään huolen siitä ketkä työntekijät pääsevät käyttämään mitäkin tietojärjestelmiä sekä palveluita ja ketkä taas eivät. IdM-järjestelmiä on hyvin erilaisia ja hyvin erilaisina kokonaisuuksina.

IdM-järjestelmiä löytyy markkinoilta sekä maksullisia että maksuttomia. Makullisia, suljetun lähdekoodin IdM-järjestelmiä on tarjolla muun muassa seuraavia:

| Valmistaja | Tuote | Linkki |
| --- | --- | --- |
| Efecte | Efecte Identity Management | https://www.efecte.com/edge-for-identity-and-access-management |
| Microsoft | Microsoft Identity Manager | https://www.microsoft.com/en-us/cloud-platform/microsoft-identity-manager |
| SAP | SAP Identity Management | https://www.sap.com/products/identity-management.html |
| Oracle | Oracle Identity Management (IdM) and Access Management | https://www.oracle.com/technetwork/middleware/id-mgmt/overview/index.html |
<br>
Havaintojemme perusteella monissa yrityksissä on käytössä maksullisia IdM -järjestelmiä, koska niiden laatu on erittäin hyvä sekä yritykset saavat käyttöönsä reaaliaikaisen teknisen tuen halutessan, jos tulee jotain ongelmia tai kysymyksiä käytössä olevaan IdM-järjestelmään liittyen. 
<br><br>
Maksuttomia, avoimen lähdekoodin IdM-järjestelmiä tarjoaa muun muassa seuraavat valmistajat:

| Valmistaja | Tuote | Linkki |
| --- | --- | --- |
| Apache Foundation | Apache Syncope | https://syncope.apache.org/ |
| Evolveum | midPoint | https://evolveum.com/midpoint/ |
| ForgeRock | OpenIDM | https://www.forgerock.com/platform/identity-management |
<br>
Lisää avoimen lähdekoodin IdM-järjestelmistä sekä niiden vertailusta löytyy Kappaleesta 3: "IdM-järjestelmien vertailu" .

Monissa avoimen lähdekoodin järjestelmistä on myös tarjolla myös maksullisia vaihtoehtoja, joiden tarkoitus on yleensä tuoda kyseiseen IdM-järjestelmään enemmän ominaisuuksia sekä reaaliaikaisen teknisen tuen.

Tässä projektissa keskitymme ainoastaan niihin IdM-järjestelmiin, jotka eivät maksa mitään ja joiden lähdekoodi on vapasti saatavilla.
