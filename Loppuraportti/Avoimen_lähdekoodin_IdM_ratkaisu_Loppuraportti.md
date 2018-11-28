# Avoimen lähdekoodin IdM ratkaisu 
Loppuraportti

Tekijät: Jan Parttimaa, Eetu Pihamäki & Markus Nissinen

Kurssi: Monialaprojekti
 
Päivämäärä: 28.11.2018
 
## Sisällysluettelo
<ol>
  <li><a href="#johdanto">Johdanto</a></li>
  <li><a href="#yleista">Yleistä IdM-järjestelmistä (identity management)</a></li>
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
Tässä raportissa kerromme alussa lyhyesti mikä on Identiteetinhallintajärjestelmä (IdM), mitä sillä tehdään ja mitä hyötyjä kyseinen järjestelmä tuo yrityksen tietojärjestelmien käyttäjähallintaan. Tämän jälkeen kerromme kuinka vertailimme avoimen lähdekoodin IdM-järjestelmiä ja kuinka juuri valitsimme testattavaksi järjestelmäksi MidPointin. Kerromme myös kuinka MidPointin asennus ja konfigurointi onnistuu vaiheittain. Raportin loppuvaiheessa kerromme lisäksi kuinka testasimme kyseistä järjestelmää.

Projektia tehdessämme tarvitsimme seuraavan laitteistokokoonpanon:
<li>Kolme (3) keskusyksikköä</li>
<li>Neljä (4) virtuaalista tietokonetta</li>

Käytössä olevamme keskusyksiköt olivat seuraavat:
| Merkki |Malli|Prosessori|Keskusmuisti|Kiintolevyjen lukumäärä|Kiintolevyjen koko|Tietokoneen nimi|
|---|---|---|---|---|---|---|
|HP|<a href="http://h20195.www2.hp.com/v2/GetDocument.aspx?docname=4AA6-9033EEAP&doctype=data%20sheet&doclang=EN_GB&searchquery=&cc=nz&lc=en">Prodesk 600 G3 MT</a>|Intel(R) Core(TM) i5-7500 CPU @ 3.40GHz (4 ydintä)|32 Gt|2 kpl|149 Gt (SSD) ja 500 Gt (HDD) |MIDPOINTIDM|
|HP|   |   |   |   |   |   |
|HP|   |   |   |   |   |   |

## IdM-järjestelmien vertailu<div id='idm-jarjestelmien-vertailu'></div>
