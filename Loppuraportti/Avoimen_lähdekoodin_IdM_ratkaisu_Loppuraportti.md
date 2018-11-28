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


Maksuttomia, avoimen lähdekoodin IdM-järjestelmiä tarjoaa muun muassa seuraavat valmistajat:

| Valmistaja | Tuote | Linkki |
| --- | --- | --- |
| Apache Foundation | Apache Syncope | https://syncope.apache.org/ |
| Evolveum | midPoint | https://evolveum.com/midpoint/ |
| ForgeRock | OpenIDM | https://www.forgerock.com/platform/identity-management |
<br>
Lisää avoimen lähdekoodin IdM-järjestelmistä sekä niiden vertailusta löytyy Kappaleesta 3: _"IdM-järjestelmien vertailu"_.

Monissa avoimen lähdekoodin järjestelmistä on myös tarjolla myös maksullisia vaihtoehtoja, joiden tarkoitus on yleensä tuoda kyseiseen IdM-järjestelmään enemmän ominaisuuksia sekä reaaliaikaisen teknisen tuen.

Tässä projektissa keskitymme ainoastaan niihin IdM-järjestelmiin, jotka eivät maksa mitään ja joiden lähdekoodi on vapasti saatavilla.


## IdM-järjestelmien vertailu<div id='idm-jarjestelmien-vertailu'></div>

### Avoimen lähdekoodin IdM-järjestelmien vertailun aloitus

Etsimme ensin Googlettamalla avoimen lähdekoodin IdM-järjestelmiä. Otimme vertailuun:
<li><a href="Apache Syncope">https://syncope.apache.org/</a></li>
<li><a href="MidPoint">https://evolveum.com/midpoint/</a></li>
<li><a href="OpenIDM">https://backstage.forgerock.com/docs/idm</a></li>
<li><a href="Soffid">http://www.soffid.com/</a></li>
<li><a href="Keycloak">https://www.keycloak.org/</a></li>
<li><a href="Unity">http://www.unity-idm.eu/</a></li>
<li><a href="OpenIAM">https://www.openiam.com/</a></li>
<li><a href="Shibboleth">https://www.shibboleth.net/</a></li>
<li><a href="WSO2 Identity Server">https://wso2.com/identity-and-access-management/</a></li>
<li><a href="Gluu">https://www.gluu.org/</a></li>
<li><a href="Josso">http://www.josso.org/install.html</a></li>
<li><a href="FreeIPA">https://www.freeipa.org/page/Main_Page</a></li>
<li><a href="Aerobase">http://aerobase.org/</a></li>

 
IdM-järjestelmien dokumentaatiot:
<li>Apache Syncope:<a href="https://syncope.apache.org/docs/">https://syncope.apache.org/docs/</a></li>
<li>MidPoint:<a href="https://wiki.evolveum.com/display/midPoint/Documentation">https://wiki.evolveum.com/display/midPoint/Documentation</a></li>
<li>OpenIDM:<a href="https://backstage.forgerock.com/docs/idm">https://backstage.forgerock.com/docs/idm</a></li>
<li>Soffid:<a href="http://www.soffid.com/products-and-services/open-source-sso-and-identity-and-access-management/">http://www.soffid.com/products-and-services/open-source-sso-and-identity-and-access-management/</a></li>
<li>Keycloak:<a href="https://www.keycloak.org/documentation.html">https://www.keycloak.org/documentation.html</a></li>
<li>Unity:<a href="http://www.unity-idm.eu/documentation/unity-2.6.2/manual.html">http://www.unity-idm.eu/documentation/unity-2.6.2/manual.html</a></li>
<li>OpenIAM:<a href="http://docs41.openiam.com/">http://docs41.openiam.com/</a></li>
<li>Shibboleth:<a href="https://wiki.shibboleth.net/confluence/#all-updates">https://wiki.shibboleth.net/confluence/#all-updates</a></li>
<li>WSO2 Identity Server:<a href="https://github.com/wso2/product-is/">https://github.com/wso2/product-is/</a></li>
<li>Gluu:<a href="https://gluu.org/docs/">https://gluu.org/docs/</a></li>
<li>Josso:<a href="http://docs.atricore.com/josso2/2.4.0/josso-reference-guide/html/en-US/JOSSO_Reference.html">http://docs.atricore.com/josso2/2.4.0/josso-reference-guide/html/en-US/JOSSO_Reference.html</a></li>
<li>FreeIPA:<a href="https://www.freeipa.org/page/Documentation">https://www.freeipa.org/page/Documentation</a></li>
<li>Aerobase:<a href="http://aerobase.org/documentation">http://aerobase.org/documentation</a></li>
