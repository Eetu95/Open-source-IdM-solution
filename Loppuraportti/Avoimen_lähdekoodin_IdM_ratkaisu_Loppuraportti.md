<h1>Avoimen lähdekoodin IdM ratkaisu</h1>
 
Loppuraportti

Tekijät: Jan Parttimaa, Eetu Pihamäki & Markus Nissinen

Kurssi: Monialaprojekti 
 
Päivämäärä: 28.11.2018
 
<h2>Sisällysluettelo</h2>
<ol>
  <li><a href="#johdanto">Johdanto</a></li>
  <li><a href="#yleista-idm-jarjestelmista-identity-management-system">Yleistä IdM-järjestelmistä (Identity Management System)</a></li>
  <li><a href="#idm-jarjestelmien-vertailu">IdM-järjestelmien vertailu</a></li>
  <ol>
        <span>3.1.</span> <a href="#idm-jarjestelmien-dokumentaatiot">IdM-järjestelmien dokumentaatiot</a><br>
        <span>3.2. </span><a href="#avoimen-lahdekoodin-idm-jarjestelmien-valintakriteerit">Avoimen lähdekoodin IdM-järjestelmien valintakriteerit</a><br>
        <span>3.3. </span><a href="#alustavat-vaatimukset">Alustavat vaatimukset</a><br>
        <span>3.4. </span><a href="#vertailu-ja-aputaulukko">Vertailu- ja aputaulukko</a><br>
  </ol>
  <li><a href="#midpoint">Midpoint</a></li>
  <ol>
      <span>4.1. </span><a href="#esivalmistelut">Esivalmistelut</a><br>
      <ol>
          <span>4.1.1. </span><a href="#ubuntu-server-asennus-ja-konfigurointi-midpointidm-keskusyksikkoon">Ubuntu Server asennus ja konfigurointi "MIDPOINTIDM" -keskusyksikköön</a><br>
          <ol>
                <span>4.1.1.1. </span><a href="#palvelimen-perusmaaritykset">Palvelimen perusmääritykset</a><br>
          </ol>
          <span>4.1.2. </span><a href="#windows-server-2016-asennus-ja-konfigurointi-windowsserver-keskusyksikkoon">Windows Server 2016 asennus ja konfigurointi "WINDOWSSERVER" -keskusyksikköön</a><br>
          <ol>
                <span>4.1.2.1. </span><a href="#windows-palvelimen-perusmaaritykset">Windows -palvelimen perusmääritykset</a><br>
                <span>4.1.2.2. </span><a href="#hyper-vn-seka-uuden-virtuaalipalvelimen-asennus">Hyper-V:n sekä uuden virtuaalipalvelimen asennus</a><br>
                <span>4.1.2.3. </span><a href="#openldap-serverin-asennus-ja-konfigurointi-hyper-vn-virtuaalipalvelimeen">OpenLDAP serverin asennus ja konfigurointi Hyper-V:n virtuaalipalvelimeen</a><br>
                <span>4.1.2.4. </span><a href="#phpLDAPadmin-web-kayttoliittyman-asennus-ja-konfigurointi">phpLDAPadmin -web-käyttöliittymän asennus ja konfigurointi</a><br>
                <span>4.1.2.5. </span><a href="#ryhmien-luonti-openldap-palvelimeen">Ryhmien luonti OpenLDAP-palvelimeen</a><br>
                <span>4.1.2.6. </span><a href="#openldap-palvelimen-maaritys-midpointtia-varten">OpenLDAP -palvelimen määritys midPointtia varten</a><br>
                <span>4.1.2.7. </span><a href="#suojatun-web-yhteyden-maaritys-https1">Suojatun web-yhteyden määritys (https)
                </a><br>
          </ol>
          <span>4.1.3. </span><a href="#virtualbox-palvelimen-asennus-ja-konfigurointi-vmserver-keskusyksikkoon">VirtualBox -palvelimen asennus ja konfigurointi "VMSERVER" -keskusyksikköön</a><br>
          <ol>
                <span>4.1.3.1. </span><a href="#phpVirtualbox-web-kayttöliittyman-asennus-ja-konfigurointi">phpVirtualbox -web-käyttöliittymän asennus ja konfigurointi</a><br>
                <span>4.1.3.2. </span><a href="#suojatun-web-yhteyden-maaritys-https2">Suojatun web-yhteyden määritys (https)</a><br>
          </ol>
          <span>4.1.4. </span><a href="#testityoasemien-seka-testipalvelimen-asennus-ja-konfigurointi">Testityöasemien sekä testipalvelimen asennus ja konfigurointi</a><br>
          <ol>
                <span>4.1.4.1. </span><a href="#windows-10-testipc1">Windows 10 (TESTIPC1)</a><br>
                <span>4.1.4.2. </span><a href="#ubuntu-desktop-18041-lts-testipc2">Ubuntu Desktop 18.04.1 LTS (TESTIPC2)</a><br>
                <span>4.1.4.3. </span><a href="#ubuntu-server-16045-lts-testipalvelin">Ubuntu Server 16.04.5 LTS (TESTIPALVELIN)</a><br>
          </ol>
      </ol>
      <span>4.2. </span><a href="#asennus">Asennus</a><br>
      <span>4.3. </span><a href="#konfigurointi">Konfigurointi</a><br>
      <ol>
          <span>4.3.1. </span><a href="#tietokannan-maarittaminen">Tietokannan määrittäminen</a><br>
          <span>4.3.2. </span><a href="#connectoreiden-maarittaminen">Connectoreiden määrittäminen</a><br>
            <ol>
                <span>4.3.2.1. </span><a href="#active-directory-connector">Active Directory connector</a><br>
                <span>4.3.2.2. </span><a href="#ldap-connector">LDAP-connector</a><br>
                <span>4.3.2.3. </span><a href="#unix-connector">Unix-connector</a><br>
		<span>4.3.2.4. </span><a href="#csv-connector">CSV-connector</a><br>
          </ol>
          <span>4.3.3. </span><a href="#suojatun-web-yhteyden-maaritys-https3">Suojatun yhteyden määritys (https)</a><br>
          <span>4.3.4. </span><a href="#roolien-seka-muiden-objektien-lisaaminen">Roolien sekä muiden objektien lisääminen</a><br>
          <ol>
                <span>4.3.4.1 </span><a href="#openldap">OpenLDAP</a><br>
                <span>4.3.4.2 </span><a href="#unix">Unix (Unix-connector)</a><br>
          </ol>
      </ol>
 <span>5. </span><a href="#testaus">Testaus</a><br>
 <ol>
        <span>5.1. </span><a href="#kayttajien-luonti-midpointtiin">Käyttäjien luonti midPointtiin</a><br>
        <span>5.2. </span><a href="#kayttajan-liittaminen-active-directoryn-kayttajaksi">Käyttäjän liittäminen Active Directoryn käyttäjäksi</a><br>
        <span>5.3. </span><a href="#kayttajan-liittaminen-testipalvelin-palvelimeen-unix-connector">Käyttäjän liittäminen TESTIPALVELIN -palvelimeen (Unix Connector)</a><br>
        <span>5.4. </span><a href="#kayttajan-liittaminen-openldapn-kayttajaksi">Käyttäjän liittäminen OpenLDAP:n käyttäjäksi</a><br>
        <span>5.5. </span><a href="#kayttajan-kayttooikeudet-midpointin-kayttoliittymaan">Käyttäjän käyttöoikeudet midPointin kayttöliittymään</a><br>
        <span>5.6. </span><a href="#havaintoja-testauksesta">Havaintoja testauksesta</a><br>
 </ol>
 <span>6. </span><a href="#lokitus">Lokitus</a><br>
 <ol>
		<span>6.1 <a href="#eclipse-midPoint-log-viewer">Log Viewer</a><br>
		<span>6.2 <a href="#audit-log-viewer">Audit Log Viewer</a><br>
</ol>
 <span>7. </span><a href="#yhteenveto">Yhteenveto</a><br>
 <span>8. </span><a href="#lahteet">Lähteet</a><br>
</ol>

<h2 id="johdanto">1. Johdanto</h2>
 
Tässä raportissa kerromme kuinka avoimen lähdekoodiin perustuvan Identiteetinhallintajärjestelmän saa käyttöön (asennus ja määritys) sekä kuinka sillä voidaan hallita Unix/Linux -palvelimien, OpenLDAP-palvelimen sekä Windows -domainin käyttäjiä. Käytämme projektissa Evolveumin <a href="https://evolveum.com/midpoint/">"midPoint"</a> nimistä avoimen lähdekoodin identiteetinhallintajärjestelmää.

Käynnistimme projektin kyseisestä aiheesta, koska muutamat projektiryhmän jäsenet ovat työssään joutuneet tekemään
töitä Identiteetinhallintajärjestelmien parissa. Yleensä kyseiset järjestelmät, jotka ovat yrityksissä
käytössä ovat suljetun lähdekoodin järjestelmiä, jonka vuoksi yritykset
joutuvat maksamaan järjestelmän käytöstä lisenssimaksua. Tämän lisäksi
järjestelmän ylläpidosta, tuesta sekä päivityksistä joudutaan yleensä
maksamaan useita tuhansia euroja. Projektityön ideana oli lähteä vertailemaan
markkinoilla saatavilla olevia avoimen lähdekoodin Identiteetinhallintajärjestelmiä,
vertailla niiden ominaisuuksia sekä laatua. Laatua päästiin kokeilemaan esimerkiksi verkossa saatavilla olevilla demoversioilla.

Projektimme tehtävänä oli vertaa avoimen lähdekoodin Identiteetinhallintajärjestelmiä, joista valitsemme parhaan ja testata sen toimivuutta testiympäristössä.

Asetimme projektille seuraavat tavoitteet: 
- IdM-järjestelmä on toimiva ja luotettava. Testaamme järjestelmää testiympäristössä.
Lopputuloksena on asennettu IdM-järjestelmän Master-kone
sekä muutamat testikoneet.
- Järjestelmä on monipuolinen, ilmainen ja avoimeen lähdekoodiin perustuva.
- IdM-järjestelmiä on vertailtu monipuolisesti sekä vertailussa otetaan
huomioon vaatimukset. Lopputuloksena vertailusta Excel-taulukko
sekä lista ennalta määritellyistä vaatimuksista.
<br>
 
Asetimme myös seuraavia oppimistavoitteita:  
- Oppia IdM-järjestelmistä sekä niiden yhteyksistä muihin järjestelmiin
ja rajapintoihin.
- Kuinka asennetaan IdM-järjestelmä ja kuinka se saadaan käyttövalmiiksi.
- Kuinka liitetään IdM-järjestelmän piiriin muita järjestelmiä.
- Tulokset, lokit ja raportit ovat valmiiksi näytettävissä.
- Opitaan pitämään projektin aikataulusta huolta ja pitämään kiinni työaikakirjauksesta.


<h2 id="yleista-idm-jarjestelmista-identity-management-system">2. Yleistä IdM-järjestelmistä (Identity Management System)</h2>
 
IdM-järjestelmä (Englanniksi: Identity Management System, Suomeksi: Identiteetinhallintajärjestelmä) on järjestelmä, jonka avulla voidaan keskitetysti hallita yrityksen eri tietojärjestelmiä, palveluita, tietokantoja, ohjelmistoja sekä ohjelmien käyttöoikeuksia että pääsynhallintaa. IdM:n ansiosta yritys pystyy helposti pitämään huolen siitä ketkä työntekijät pääsevät käyttämään mitäkin tietojärjestelmiä sekä palveluita ja ketkä taas eivät. IdM-järjestelmiä on olemassa hyvin erilaisia ja hyvin erilaisina kokonaisuuksina.

![](https://raw.githubusercontent.com/Eetu95/Open-source-IdM-solution/master/Kuvat/IdM_esimerkki.jpg)
 
Kuva 1: Havainnollistava esimerkki Indentiteetinhallintajärjestelmästä (IdM).
 
<br>
 
IdM-järjestelmiä löytyy markkinoilta sekä maksullisia että maksuttomia. Makullisia, suljetun lähdekoodin IdM-järjestelmiä on tarjolla muun muassa seuraavia:

| Valmistaja | Tuote | Linkki |
| --- | --- | --- |
| Efecte | Efecte Identity Management | https://www.efecte.com/edge-for-identity-and-access-management |
| Microsoft | Microsoft Identity Manager | https://www.microsoft.com/en-us/cloud-platform/microsoft-identity-manager |
| SAP | SAP Identity Management | https://www.sap.com/products/identity-management.html |
| Oracle | Oracle Identity Management (IdM) and Access Management | https://www.oracle.com/technetwork/middleware/id-mgmt/overview/index.html |
<br>
 
Havaintojemme perusteella monissa yrityksissä on käytössä maksullisia IdM -järjestelmiä, koska niiden laatu on erittäin hyvä sekä yritykset saavat käyttöönsä reaaliaikaisen teknisen tuen halutessan, jos tulee jotain ongelmia tai kysymyksiä käytössä olevaan IdM-järjestelmään liittyen. 

<br>

Maksuttomia, avoimen lähdekoodin IdM-järjestelmiä tarjoaa muun muassa seuraavat valmistajat:

| Valmistaja | Tuote | Linkki |
| --- | --- | --- |
| Apache Foundation | Apache Syncope | https://syncope.apache.org/ |
| Evolveum | midPoint | https://evolveum.com/midpoint/ |
| ForgeRock | OpenIDM | https://www.forgerock.com/platform/identity-management |
<br>
Lisää avoimen lähdekoodin IdM-järjestelmistä sekä niiden vertailusta löytyy Kappaleesta 3: <a href="#idm-jarjestelmien-vertailu">"IdM-järjestelmien vertailu"</a> .
 
<br>
 
Monissa avoimen lähdekoodin järjestelmistä on myös tarjolla myös maksullisia vaihtoehtoja, joiden tarkoitus on yleensä tuoda kyseiseen IdM-järjestelmään enemmän ominaisuuksia sekä reaaliaikaisen teknisen tuen.
 
<br>
 
Tässä projektissa keskitymme ainoastaan niihin IdM-järjestelmiin, jotka eivät maksa mitään ja joiden lähdekoodi on vapasti saatavilla.


<h2 id="idm-jarjestelmien-vertailu">3. IdM-järjestelmien vertailu</h2>

Etsimme ensin Googlettamalla avoimen lähdekoodin IdM-järjestelmiä. Otimme vertailuun seuraavat, joita löysimme:
- <a href="https://syncope.apache.org/">Apache Syncope</a>
- <a href="https://evolveum.com/midpoint/">MidPoint</a>
- <a href="https://backstage.forgerock.com/docs/idm">OpenIDM</a>
- <a href="http://www.soffid.com/">Soffid</a>
- <a href="https://www.keycloak.org/">Keycloak</a>
- <a href="http://www.unity-idm.eu/">Unity</a>
- <a href="https://www.openiam.com/">OpenIAM</a>
- <a href="https://www.shibboleth.net/">Shibboleth</a>
- <a href="https://wso2.com/identity-and-access-management/">WSO2 Identity Server</a>
- <a href="https://www.gluu.org/">Gluu</a>
- <a href="http://www.josso.org/install.html">Josso</a>
- <a href="https://www.freeipa.org/page/Main_Page">FreeIPA</a>
- <a href="http://aerobase.org/">Aerobase</a>


<br>


<h3 id="idm-jarjestelmien-dokumentaatiot">3.1. IdM-järjestelmien dokumentaatiot</h3>
 
- Apache Syncope:<a href="https://syncope.apache.org/docs/">https://syncope.apache.org/docs/</a>
- MidPoint:<a href="https://wiki.evolveum.com/display/midPoint/Documentation">https://wiki.evolveum.com/display/midPoint/Documentation</a>
- OpenIDM:<a href="https://backstage.forgerock.com/docs/idm">https://backstage.forgerock.com/docs/idm</a>
- Soffid:<a href="http://www.soffid.com/products-and-services/open-source-sso-and-identity-and-access-management/">http://www.soffid.com/products-and-services/open-source-sso-and-identity-and-access-management/</a>
- Keycloak:<a href="https://www.keycloak.org/documentation.html">https://www.keycloak.org/documentation.html</a>
- Unity:<a href="http://www.unity-idm.eu/documentation/unity-2.6.2/manual.html">http://www.unity-idm.eu/documentation/unity-2.6.2/manual.html</a>
- OpenIAM:<a href="http://docs41.openiam.com/">http://docs41.openiam.com/</a>
- Shibboleth:<a href="https://wiki.shibboleth.net/confluence/#all-updates">https://wiki.shibboleth.net/confluence/#all-updates</a>
- WSO2 Identity Server:<a href="https://github.com/wso2/product-is/">https://github.com/wso2/product-is/</a>
- Gluu:<a href="https://gluu.org/docs/">https://gluu.org/docs/</a>
- Josso:<a href="http://docs.atricore.com/josso2/2.4.0/josso-reference-guide/html/en-US/JOSSO_Reference.html">http://docs.atricore.com/josso2/2.4.0/josso-reference-guide/html/en-US/JOSSO_Reference.html</a>
- FreeIPA:<a href="https://www.freeipa.org/page/Documentation">https://www.freeipa.org/page/Documentation</a>
- Aerobase:<a href="http://aerobase.org/documentation">http://aerobase.org/documentation</a>


<h3 id="avoimen-lahdekoodin-idm-jarjestelmien-valintakriteerit">3.2. Avoimen lähdekoodin IdM-järjestelmien valintakriteerit</h3>

Katsoimme kyseisten avoimen lähdekoodin IdM-järjestelmien lisenssit läpi. Laitoimme ne ylös vertailudokumenttiin ja selitimme ne. Lisäsimme lähteet, joista ilmenee lisenssit ja mitä ne pitävät sisällään.

![Apache 2.0 -lisenssi](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Vertailu/Apache%202.0%20-lisenssi.PNG?raw=true)

Yksi projektiryhmämme jäsenistä konsultoi työpaikallaan IdM-järjestelmän vaatimuksista, mm. mitä mieltä kollegat olivat vaatimuksista ja mitä voisi vielä lisätä. Otimme ne huomioon vertailussamme.

Otimme huomioon vertailussa IdM-järjestelmien GitHub -suosion, kuinka paljon seuraajia (Watch), tähtiä (Star), haarukoita (Fork). Tutkimme myös muut versionhallintapalvelut - ei löytynyt muualta kuin GitHubista. Esim. Apache Syncopella, midPointilla ja Keycloakilla oli projektit GitHubissa.

Käytimme myös Google Scholarista ja Google Trendsistä löytyvää tietoa IdM-järjestelmistä hyväksemme vertailussa. Google Scholarissa etsimme järjestelmistä tietoa mm. siitä kuinka monta hakutulosta löytyy koko maailmasta viimeisen kahden vuoden ajalta sekä koko ajalta. Apache Syncopesta löytyi mm. 101 hakutulosta viimeisen kahden vuoden ajalta ja koko ajalta yhteensä 1270 tulosta. MidPointilla, Shibboleth ja WSO2 Identity Server saivat myös lähes yhtä paljon hakutuloksia kuin Apache Syncope. Otimme myös ylös hyödyllisiä artikkeleita, joita löytyi Google Scholarista.

Google Trendsissä kriteerit olivat samat kuin Google Scholarissa. Google Trendsissä pystyi helposti vertailemaan hakusanoja, joista saatiin selkokielinen kaavio. Google Trendsissä pystyi vertailemaan viittä hakusanaa kerrallaan, joten vertailtiin IdM-järjestelmiä kolmessa eri ryhmässä, joista suosituimmat vertaillaan vielä kerran keskenään.

<ol>
 <li>Ryhmä: Apache Syncope, midPoint (Evolveum), OpenIDM, Soffid ja Keycloak.
 <br/>
 <br/>
 Kaksi viimeisintä vuotta: <a href="https://trends.google.fi/trends/explore?date=2016-09-01%202018-09-01&q=apache%20syncope,evolveum,openidm,soffid,keycloak">https://trends.google.fi/trends/explore?date=2016-09-01%202018-09-01&q=apache%20syncope,evolveum,openidm,soffid,keycloak</a>
 <br/>
 <br/>
 Kokoaika: <a href="https://trends.google.fi/trends/explore?date=all&q=apache%20syncope,evolveum,openidm,soffid,keycloak"> https://trends.google.fi/trends/explore?date=all&q=apache%20syncope,evolveum,openidm,soffid,keycloak</a></li>
 </br>
 <li>Ryhmä: OpenIAM, Unity, Shibboleth, WSO2 Identity Server ja Gluu Server.
 <br/>
 <br/>
 Kaksi viimeistä vuotta: <a href="https://trends.google.fi/trends/explore?date=2016-09-01%202018-09-01&q=openiam,unity%20idm,shibboleth%20identity,wso2%20identity%20server,gluu%20server">https://trends.google.fi/trends/explore?date=2016-09-01%202018-09-01&q=openiam,unity%20idm,shibboleth%20identity,wso2%20identity%20server,gluu%20server</a></li>
 </br>
 Kokoaika: <a href="https://trends.google.fi/trends/explore?date=all&q=openiam,unity%20idm,shibboleth%20identity,wso2%20identity%20server,gluu%20server">https://trends.google.fi/trends/explore?date=all&q=openiam,unity%20idm,shibboleth%20identity,wso2%20identity%20server,gluu%20server</a>
 </br>
 </br>
 <li>Ryhmä: Josso, FreeIPA, Aerobase ja Grouper.</li>
 </br>
 Kaksi viimeistä vuotta: <a href="https://trends.google.fi/trends/explore?date=2016-09-01%202018-09-01&q=josso,freeipa,aerobase%20-%20group,grouper%20idm">https://trends.google.fi/trends/explore?date=2016-09-01%202018-09-01&q=josso,freeipa,aerobase%20-%20group,grouper%20idm</a>

 Kokoaika: <a href="https://trends.google.fi/trends/explore?date=all&q=josso,freeipa,aerobase%20-%20group,grouper%20idm">https://trends.google.fi/trends/explore?date=all&q=josso,freeipa,aerobase%20-%20group,grouper%20idm</a>
</ol>

Suosituimpia IdM-järjestelmiä Google Trendsissä olivat: Keycloak, Josso, WSO2 Identity Server, Gluu Server ja FreeIPA. Kaikista suosituin viimeisen kahden vuoden aikana oli Keycloak. Koko ajalta suosituin oli keskiarvon perusteella Josso.

Kaavio 1: <a href="https://trends.google.fi/trends/explore?date=2016-09-01%202018-09-01&q=keycloak,josso,wso2%20identity%20server,gluu%20server,freeipa">Kaavio kahden vuoden ajalta</a>

![trends_2v_vertailu_SUOSITUIMMAT_keycloak_josso_wso2identityserver_gluuserver_freeipa](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Trends/trends_2v_vertailu_SUOSITUIMMAT_keycloak_josso_wso2identityserver_gluuserver_freeipa.PNG?raw=true)

Kaavio 2: <a href="https://trends.google.fi/trends/explore?date=all&q=keycloak,josso,wso2%20identity%20server,gluu%20server,freeipa">Kaavio koko ajalta</a>

![trends_kokoaika_vertailu_SUOSITUIMMAT_keycloak_josso_wso2identityserver_gluuserver_freeipa](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Trends/trends_kokoaika_vertailu_SUOSITUIMMAT_keycloak_josso_wso2identityserver_gluuserver_freeipa.PNG?raw=true)

Etsimme myös tietoa Amazonista ja Safari Books Onlinesta mm. kuinka monta kirjaa kustakin järjestelmästä on kirjoitettu. Suurimmasta osasta IdM-järjestelmistä ei löytynyt julkaistuja kirjoja. IdM-järjestelmät, joista löytyi julkaistuja kirjoja olivat: OpenIDM (Amazon), Keycloak (Safari), Shibboleth (Safari), WSO2 Identity Server (Safari) ja Josso (Safari).

Lisäsimme vertailuumme löytämämme uuden avoimen lähdekoodin IdM-järjestelmän nimeltä Grouper: <a href="https://www.internet2.edu/products-services/trust-identity/grouper/#service-overview">https://www.internet2.edu/products-services/trust-identity/grouper/#service-overview</a>

- Dokumentaatio löytyy osoitteesta: <a href="https://spaces.at.internet2.edu/display/TI/TI.25.1">https://spaces.at.internet2.edu/display/TI/TI.25.1</a>

- Muutamat ulkomaiset yliopistot käyttävät Grouper IdM-järjestelmää: <a href="https://idm.unl.edu/grouper">https://idm.unl.edu/grouper</a>

Etsimme muita referenssejä vertailun kohteena oleville avoimen lähdekoodin IdM-järjestelmille. Löydettiin myös suomalaisia yrityksiä ja järjestöjä, jotka käyttävät joitakin vertailussamme olevista IdM-järjestelmistä. Löydettiin mm. että <a href="http://www.tirasa.net/customer/university-of-helsinki.html">Helsingin Yliopisto käyttää Apache Syncopea</a>

<h3 id="alustavat-vaatimukset">3.3. Alustavat vaatimukset</h3>

| Vaatimus  |  Lisätietoja   |
|---|---|
|IdM-järjestelmä pyörii Linux-palvelimella   |Säästytään näin ollen lisenssikustannuksissa, kun ei tarvitse käyttää maksullista käyttöjärjestelmää.    |
|IdM oltava avoimeen lähdekoodiin perustuva ja kaikille ilmainen   | Säästytään muun muassa lisenssikustannuksilta, kun IdM-järjestelmän hankinnasta ei tarvitse maksaa. Lisenssi täytyy myös olla [Free Sofware Foundationin](https://www.fsf.org/) sekä [Open Source Initiativen](https://opensource.org/licenses) hyväksymiä.   |
|Lisenssi sallii kaupallisen toiminnan ja järjestelmämuutokset  | Voidaan käyttää IdM-järjestelmää näin ollen yritysympäristössä ja voidaan sitä halutessaan myös kehittää.  |
|Ainakin tuki tunnettuihin järjestelmiin ja palveluihin (muun muassa Microsoft Active Directory, Linux,  Tietokannat, LDAP). Valmiita connectoreita eli välikappaleita Idm-järjestelmän ja kohdejärjestelmän/palvelun yhdistämiseen on tarjolla. IdM on yleisellä tasolla kattava (On mahdollisuus tehdä esimerkiksi custom connectoreita eli omia välikappaleita IdM-järjestelmän ja kohdejärjestelmän/-palvelun yhdistämiseksi.) |Jotta käyttöoikeuksien hallinta keskitetysti mahdollisimman moneen järjestelmään/palveluun on mahdollista.   |
|Tapahtumien kirjaus lokeihin, jäljitettävyys on mahdollista | Jotta nähdään kuka on käyttö-oikeuden tilannut, mitä on tilattu, kenelle on tilattu sekä koska on tilattu ja onko tapahtuma käyttäjätunnus vai käyttäjäryhmätasoisesti.|
|Eri salasana eri tasoisiin palveluihin eli IdM-järjestelmä tukee muiden järjestelmien omia käytäntöjä   | Jos ei haluta käyttää samoja tunnuksia eri järjestelmiin.   |
|IdM-järjestelmästä löytyy valmistajalta/kehittäjältä dokumentaatiota   | Jotta järjestelmän asennus, käyttö ja ylläpito on vaivattomampaa.   |
|IdM-järjestelmää kehitetään aktiivisesti   |Jotta järjestelmää voidaan käyttää huoletta kauan, siihen saadaan tietoturvapäivityksiä sekä muita parannuksia ja ei tarvitse heti vaihtaa toiseen järjestelmään. Jos järjestelmä on viimeksi päivitetty kaksi vuotta sitten tai enemmän, voidaan todeta kehityksen olevan ei-aktiivista.   |
|Governance   |Voidaan valvoa ja tarkistaa, että halutut yrityksen asettamat vaatimukset toteutuvat esimerkiksi salasanavaatimukset ja että vain tietyt henkilöt pääsevät kirjautumaan tiettyihin järjestelmiin ja palveluihin.   |
|Toimeksiantojen hyväksyntämahdollisuus   |Jotta joku toinen henkilö voi hyväksyä jonkun toisen henkilön pyynnön saada oikeudet tiettyyn järjestelmään/palveluun. Esimerkiksi esimies hyväksyy alaisensa pyynnön saada oikeudet kirjautua tietokantaan.   |
|Salasanojen hallinta   | Voidaan halutessaan esimerkiksi resetoida tietyn henkilön salasanan, jos se häneltä vaikkapa unohtui.   |
|Tunnusten jäädytys ja poisto   | Jotta voidaan välttyä irtisanottujen henkilöiden pääsy järjestelmiin ja palveluihin.  |
|Henkilö- ja käyttäjätunnusprofiilien muokkausmahdollisuus   | Jos esimerkiksi työtekijän titteli ja työnkuva muuttuu, voidaan nämä tiedot kätevästi päivittää ajan tasalle.  |
|Hakumahdollisuus   |Voidaan helposti etsiä esimerkiksi halutun henkilön henkilötili ja käyttäjäprofiili tiettyyn järjestelmään ja palveluun.   |
|Raporttien luontimahdollisuus   | Voidaan tehdä tulosteet, joissa esimerkiksi nähdään tietyn henkilön oikeudet tiettyihin järjestelmiin ja palveluihin.  |
|Vaarallisten työyhdistelmien tunnistus tehtävätasoisesti   | Esimerkiksi sama henkilö ei saa luoda oikeuksia ja hyväksyä niitä itselleen johonkin kohdejärjestelmään tai palvelu.  |
|Mahdollisuus manuaaliprovisiointiin   |Tukeeko valittavat mahdollisuudet esimerkiksi radiobuttoneita, checkboxeja jne.   |
|Soveltuu myös suureen yritykseen   |  Käyttöoikeuksia voi olla esimerkiksi yli 7000  |

<h3 id="vertailu-ja-aputaulukko">3.4. Vertailu- ja aputaulukko</h3>

![vertailutaulukko](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Vertailu/vertailutaulukko.jpg?raw=true)

Kuva 2: Vertailutaulukko.
 
Tässä vertailutaulukossa näkyy vertaulumme varsinainen tulos ja se miten päädyimme valintaan. Huom! Jotkin vaatimukset ovat kriittisempiä kuin toiset, joka johtaa kriittisemmän vaatimuksen täyttävän järjestelmän suosimiseen. Lataa PDF <a href="https://opensourceidm.files.wordpress.com/2018/10/vertailutaulukko.pdf">tästä</a>.
<br>
<br>
![aputaulukko](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Vertailu/aputaulukko.jpg?raw=true)
 
Kuva 3: Aputaulukko.
 
Aputaulukko selventää vertailutaulukon lukua. Lataa PDF <a href="https://opensourceidm.files.wordpress.com/2018/10/aputaulukko.pdf">tästä</a>.

<h2 id="midpoint"4. >Midpoint</h2>

Vertailtuamme IdM-järjestelmiä ja kriteereidemme perusteella eniten ominaisuuksia ja pisteitä omisti midPoint IdM-järjestelmä, mistä syystä päädyimme juuri tähän järjestelmään. Vahvaksi toiseksi ehdokkaaksi valiutui Apache Syncope, joka muuten midPointin kanssa sisälsi melkein identtiset ominaisuudet kuin midPoint, mutta midPoint IdM-järjestelmä tuki enemmän muita järjestelmiä ja rajapintoja. Järjestelmät ja rajapinnat, joita midPoint tukee ovat:
- Active Directory
- Unix/Linux
- Office365
- Google Apps
- SAP
- Box
- Drupal
- Atlassian ohjelmat (JIRA, Nitbucket, Confluence)
- Lotus Notes
- Tietokannat
- LDAP
- CSV

Tosin kaikissa connectoreissa ja rajapinnoissa käyttäjätietojen synkronointi ei valmistajan mukaan toimi esimerkiksi Atlassian tuotteiden ja Oraclen kanssa. Omien connectoreiden teko on myös mahdollista midPontissa. Tämän projektin aikana kokeilimme Active Directory, Unix/Linux ja LDAP connectoreita.
 
<h3 id="esivalmistelut">4.1. Esivalmistelut</h3>

Valittuamme midPoint IdM-järjestelmän, ryhdyimme tekemään esivalmisteluja IdM-järjestelmää varten. Tarkoituksena oli, että kokeilemme mahdollisimman montaa connectoria. Tätä varten tarvitsimme sekä Linux että Windows käyttöjärjestelmillä varustetut työasemat ja palvelimet. Aluksi kokeilimme midPointin käyttöä sekä työasemien asennusta ja konfigurointia virtuaaliympäristössä. Käytössämme oli Oracle VM VirtualBox, jonne loimme virtuaalikoneita testauksia varten. Myöhemmin kuitenkin teimme samat muutokset fyysisellä työasemalla, johon midPoint IdM-järjestelmä asennettiin, kun virtuaaliympäristössä saatiin haluttu lopputulos toimimaan. 

Projektia tehdessämme tarvitsimme seuraavan laitteistokokoonpanon:
- Kolme (3) keskusyksikköä 
- Neljä (4) virtuaalista tietokonetta
 
<br>
 
Käytössä olevat keskusyksiköt olivat meillä seuraavat:

| Merkki | Malli | Prosessori | Keskusmuisti | Kiintolevyjen lukumäärä | Kiintolevyjen koko | Tietokoneen nimi |
| --- | --- | --- | --- | --- | --- | --- |
| HP | <a href="http://h20195.www2.hp.com/v2/GetDocument.aspx?docname=4AA6-9033EEAP&doctype=data%20sheet&doclang=EN_GB&searchquery=&cc=nz&lc=en">Prodesk 600 G3 MT</a> | Intel(R) Core(TM) i5-7500 CPU @ 3.40GHz (4 ydintä) | 32 Gt | 2 kpl | 500 Gt (HDD) ja 500 Gt (HDD) | MIDPOINTIDM |
| HP | <a href="https://support.hp.com/us-en/product/hp-compaq-8200-elite-microtower-pc/5037940/document/c02779504">HP Compaq 8200 Elite Microtower</a>   | Intel(R) Core(TM) i5-2400 CPU @ 3.10GHz (4 ydintä) | 8 Gt  |  1 kpl | 500 Gt (HDD)  | VMSERVER  |
| HP | <a href="https://support.hp.com/us-en/product/hp-compaq-8200-elite-microtower-pc/5037940/document/c02779504">HP Compaq 8200 Elite Microtower</a>   | Intel(R) Core(TM) i5-2400 CPU @ 3.10GHz (4 ydintä) | 8 Gt  |  1 kpl | 500 Gt (HDD)  | WINDOWSSERVER  |

Asennamme Identiteetinhallintajärjestelmän keskusyksikköön "MIDPOINT", VirtualBox-palvelimen testityöasemia sekä testipalvelinta varten keskusyksikköön "VMSERVER" sekä Windows -palvelimen keskusyksikköön "WINDOWSSERVER". Toisin sanoen nämä edellä mainitut keskusyksiköt toimivat palvelinkäytössä.

VMSERVERiin asennamme myöhemmin seuraavat virtuaaliset testikoneet ja -palvelimen:
 
| Virtuaalikoneen nimi | Käyttöjärjestelmä | Prosessorin ytimien lukumäärä | Keskusmuisti | Kiintolevyjen koko | Näytönohjaimen muisti
| --- | --- | --- | --- | --- | --- |
| TESTIPC2 | Ubuntu Desktop 18.04.1 LTS (64-bit) | 2 | 2048 Mt | 50 Gt | 128 Mt |
| TESTIPC1 | Windows 10 Pro (Version: 1803) (64-bit) | 1 | 2048 Mt | 50 Gt | 128 Mt |
|TESTIPALVELIN | Ubuntu Server 16.04.5 LTS (64-bit) | 1 | 1024 Mt | 10 Gt | 16 Mt |  
 
Tämän lisäksi asenamme WINDOWSSERVER -palvelimeen OpenLDAP -virtuaalipalvelimen Hyper-V:n kautta. Käyttöjärjestelmältään se on myös Ubuntu Server 16.04.5 LTS (64-bit). Spekseiltään palvelin on sama mitä esimerkiksi TESTIPALVELIN -palvelimen kanssa.
 
<br> 
 
<h4 id="ubuntu-server-asennus-ja-konfigurointi-midpointidm-keskusyksikkoon">4.1.1. Ubuntu Server asennus ja konfigurointi "MIDPOINTIDM" -keskusyksikköön</h4>

Ensimmäisenä esivalmisteluvaiheena oli Linux palvelimen käyttöjärjestelmän asennus ja konfigurointi. MidPoint järjestelmä asennetaan tähän käyttöjärjestelmään. Valitsimme palvelimeksi Ubuntu Server 16.04.5 LTS 64-bittisen version. Asensimme käyttöjärjestelmän fyysiselle tietokoneelle USB-livetikun avulla. Valitsimme tietokoneesta käynnistystavaksi USB boottauksen, jolloin pääsimme asentamaan käyttöjärjestelmää.

![käyttöjärjestelmän kielen valinta](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Ubuntu%20Server%2016.04.5%20LTS%20asennuksen%20ruutukaappaukset/Vaihe%20(01).png?raw=true) 
<br>
Kuva 4: Käyttöjärjestelmän kielen valinta.
<br>
<br>
Heti ensimmäiseksi ”USB-boottauksen” jälkeen ja kun tuli asennusruutu näkyviin, painoimme F2:sta (1.) ja valitsimme käyttöjärjestelmän kieleksi englannin (2.). Hyväksyimme valinnan painamalla Enter.

![näppäimistön kieli](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Ubuntu%20Server%2016.04.5%20LTS%20asennuksen%20ruutukaappaukset/Vaihe%20(02).png?raw=true)
<br>
Kuva 5: Näppäimistön kieli.
<br>
<br>
Tämän jälkeen painoimme F3:sta (1.) ja valitsimme näppäimistön kieleksi suomen (2.). Hyväksyimme valinnan painamalla Enter.

![ubuntu server asennus](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Ubuntu%20Server%2016.04.5%20LTS%20asennuksen%20ruutukaappaukset/Vaihe%20(03).png?raw=true)
<br>
Kuva 6: Ubuntu Server asennus.
<br>
<br>
Aloitimme tänän jälkeen asennuksen valitsemalla ”Install Ubuntu Server” nuolinäppäimillä ja hyväksymällä valinnan painamalla Enter.

![palvelimen kieli](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Ubuntu%20Server%2016.04.5%20LTS%20asennuksen%20ruutukaappaukset/Vaihe%20(04).png?raw=true)
<br>
Kuva 7: Palvelimen kieli.
<br>
<br>
Avautui ohjattu asennus. Valitsimme nuolinäppäimillä palvelimen kieleksi englannin eli ”English”. Hyväksyimme valinnan painamalla Enter.

![sijainti](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Ubuntu%20Server%2016.04.5%20LTS%20asennuksen%20ruutukaappaukset/Vaihe%20(05).png?raw=true)
<br>
Kuva 8: Sijainti.
<br>
<br>
Seuraavassa kohdassa piti valita sijainti. Koska sijaintimme on Suomi, valitsimme ”other”. Jatkoimme eteenpäin painamalla Enter.

![sijainti_europe](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Ubuntu%20Server%2016.04.5%20LTS%20asennuksen%20ruutukaappaukset/Vaihe%20(06).png?raw=true)
<br>
Kuva 9: Sijainti "Europe".
<br>
<br>
Sitten valitsimme ”Europe”. Hyväksyimme sen painamalla Enter.

![sijainti_finland](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Ubuntu%20Server%2016.04.5%20LTS%20asennuksen%20ruutukaappaukset/Vaihe%20(07).png?raw=true)
<br>
Kuva 10: Sijainti "Finland".
<br>
<br>
Lopulta valitsimme "Finland". Hyväksyimme tämänkin painamalla Enter.

![näppäimistön kieli_UTF-8](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Ubuntu%20Server%2016.04.5%20LTS%20asennuksen%20ruutukaappaukset/Vaihe%20(08).png?raw=true)
<br>
Kuva 11: Näppäimistön kieli "UTF-8".
<br>
<br>
Koska valitsemamme maa ja kieli eivät muka sopineet yhteen, jouduimme valitsemaan ”United States – en_US.UTF-8”. Hyväksyimme valinnan painamalla Enter.

![hostname](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Ubuntu%20Server%2016.04.5%20LTS%20asennuksen%20ruutukaappaukset/Vaihe%20(09).png?raw=true)
<br>
Kuva 12: Hostname.
<br>
<br>
Annoimme järjestelmän hostnameksi ”MIDPOINTIDM” (1.). Jatkoimme tämän jälkeen eteenpäin valitsemalla tabilla ”Continue” (2.) ja hyväksymällä valinta painamalla Enter.

![pääkäyttäjän nimi](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Ubuntu%20Server%2016.04.5%20LTS%20asennuksen%20ruutukaappaukset/Vaihe%20(10).png?raw=true)
<br>
Kuva 13: Pääkäyttäjän nimi.
<br>
<br>
Seuraavaksi piti kertoa luotavan pääkäyttäjän koko nimi. Laitoimme nimeksi projektiryhmämme nimen eli ”Pisnismiehet” (1.). Kun olimme tämän kirjoittanut, valitsimme tabilla ”Continue” (2.) ja hyväksyimme valinnan painamalla Enter.

![käyttäjätunnus](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Ubuntu%20Server%2016.04.5%20LTS%20asennuksen%20ruutukaappaukset/Vaihe%20(11).png?raw=true)
<br>
Kuva 14: Käyttäjätunnus.
<br>
<br>
Käyttäjätunnukseksi ehdotettiin kuvan mukaisesti projektiryhmämme nimeä ilman isoa alkukirjainta (1.). Jatkoimme eteenpäin valitsemalla tabilla ”Continue” (2.) ja hyväksyimme valinnan painamalla Enter.

![salasana](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Ubuntu%20Server%2016.04.5%20LTS%20asennuksen%20ruutukaappaukset/Vaihe%20(12).png?raw=true)
<br>
Kuva 15: Salasana.
<br>
<br>
Seuraavaksi loimme hyvän salasanan käyttäjälle ”pisnismiehet” (1.). Jatkoimme eteenpäin valitsemalla tabilla ”Continue” (2.) ja hyväksyimme valinnan painamalla Enter.

![salasanan toisto](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Ubuntu%20Server%2016.04.5%20LTS%20asennuksen%20ruutukaappaukset/Vaihe%20(13).png?raw=true)
<br>
Kuva 16: Salasanan vaihto.
<br>
<br>
Toistimme seuraavaksi salasanan (1.). Jatkoimme eteenpäin valitsemalla tabilla ”Continue” (2.) ja hyväksyimme valinnan painamalla Enter.

![kotihakemiston kryptaus](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Ubuntu%20Server%2016.04.5%20LTS%20asennuksen%20ruutukaappaukset/Vaihe%20(14).png?raw=true)
<br>
Kuva 17: Kotihakemiston kryptaus.
<br>
<br>
Seuraavaksi kysyttiin, halutaanko kotihakemisto kryptata. Koska halusimme näin tehdä tietoturvallisuuden parentamiseksi valitsimme nuolinäppäimillä valinnan ”Yes” ja hyväksyimme valinnan painamalla Enter.

![aikavyöhyke](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Ubuntu%20Server%2016.04.5%20LTS%20asennuksen%20ruutukaappaukset/Vaihe%20(15).png?raw=true)
<br>
Kuva 18: Aikavyöhyke.
<br>
<br>
Asennusohjelma ehdotti aikavyöhykkeeksi ”Europe/Helsinki”. Se oli oikein ja valitsimme nuolinäppäimillä ”Yes” ja hyväksyimme sen painamalla Enter.

![kiintolevyn osiointi](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Ubuntu%20Server%2016.04.5%20LTS%20asennuksen%20ruutukaappaukset/Vaihe%20(16).png?raw=true)
<br>
Kuva 19: Kiintolevyn osiointi.
<br>
<br>
Seuraavaksi kysyttiin palvelimen kiintolevyn osioinnista, mitä sille tehdään. Meillä ei ollut tarvetta alkaa kryptaamaan levyä, joten valitsimme nuolinäppäimillä  ”Guided – use entire disk and set up LVM” ja painoimme Enter.Toinen syy sille miksi emme lähteneet kryptaamaan levyä oli se, että tällöin SSH-yhteydenotto palvelimen uudelleenkäynnistyksen yhteydessä ei olisi onnistunut ilman fyysistä käyntiä palvelimella. Tällöin olisimme joutuneet antamaan fyysisesti palvelimelle kryptauksen salasanan.

![osioitava kiintolevy](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Ubuntu%20Server%2016.04.5%20LTS%20asennuksen%20ruutukaappaukset/Vaihe%20(17).png?raw=true)
<br>
Kuva 20: Osioitava kiintolevy.
<br>
<br>
Seuraavaksi kysyttiin osioitavaa kiintolevyä.  Valitsimme haluamamme ja jatkoimme eteenpäin painamalla Enter. (Kuvassa näkyvä levy ei ole aivan oikea, sillä imitoimme asennusta Oracle VM VirtualBoxissa kuvankaappausten takia.)

![hyväksytään muutokset](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Ubuntu%20Server%2016.04.5%20LTS%20asennuksen%20ruutukaappaukset/Vaihe%20(18).png?raw=true)
<br>
Kuva 21: Hyväksytään muutokset.
<br>
<br>
Hyväksyimme kirjoitettavat muutokset liittyen osiointiin valitsemalla nuolinäppäimillä ”Yes” ja kuittaamalla valinta painamalla Enter.

![kiintolevyn osioinnin koko](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Ubuntu%20Server%2016.04.5%20LTS%20asennuksen%20ruutukaappaukset/Vaihe%20(19).png?raw=true)
<br>
Kuva 22: Kiintolevyn osioinnin koko.
<br>
<br>
Seuraavaksi jouduimme kertomaan kuinka suuren osan kiintolevystä halusimme osioida. Valitsimme koko levyn koon eli kirjoitimme ”max” (1.). Tämän jälkeen valitsimme tabilla ”Continue” (2.) ja hyväksyimme sen painamalla Enter.

![yhteenveto](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Ubuntu%20Server%2016.04.5%20LTS%20asennuksen%20ruutukaappaukset/Vaihe%20(20).png?raw=true)
<br>
Kuva 23: Yhteenveto.
<br>
<br>
Hyväksyimme yhteenvedon tehtävistä muutoksista liittyen kiintolevyyn osiointiin valitsemalla nuolinäppäimillä ”Yes” ja hyväksymällä valinta painamalla Enter.

![asennus käynnistyy](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Ubuntu%20Server%2016.04.5%20LTS%20asennuksen%20ruutukaappaukset/Vaihe%20(21).png?raw=true)
<br>
Kuva 24: Asennus käynnistyy.
<br>
<br>
Dataa aletaan kopioimaan levylle.

![proxy](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Ubuntu%20Server%2016.04.5%20LTS%20asennuksen%20ruutukaappaukset/Vaihe%20(22).png?raw=true)
<br>
Kuva 25: Proxy.
<br>
<br>
Seuraavaksi kysyttiin välityspalvelimen (proxy) osoitetta. Emme tarvitse valityspalvelinta, joten jätimme kohdan tyhjäksi ja valitsimme tabilla ”Continue” ja hyväksyimme valinnan painamalla Enter.

![päivitykset](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Ubuntu%20Server%2016.04.5%20LTS%20asennuksen%20ruutukaappaukset/Vaihe%20(23).png?raw=true)
<br>
Kuva 26: Päivitykset.
<br>
<br>
Seuraavaksi kysyttiin kuinka halumme hallita palvelimelle tulevia päivityksiä. Halusimme, että tietoturvapäivitykset asentuu automaattisesti, joten valitsimme nuolinäppäimillä ”Install security updates automatically” ja painoimme sitten Enter.

![ohjelmat](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Ubuntu%20Server%2016.04.5%20LTS%20asennuksen%20ruutukaappaukset/Vaihe%20(24).png?raw=true)
<br>
Kuva 27: Ohjelmat.
<br>
<br>
Tuli listaus mitä ohjelmia halutaan meidän asentavan palvelimelle. Valitsimme, että palvelimelle asennetaan standardeja järjestelmän hyötyohjelmia (esimerkiksi palomuuri) ja OpenSSH server, jotta voimme ottaa palvelimeen SSH-yhteyden (1.). Valinnan jälkeen jatkoimme eteenpäin valitsemalla ”Continue” (2.) ja hyväksymällä se painamalla Enter.

![ohjelmien asennus](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Ubuntu%20Server%2016.04.5%20LTS%20asennuksen%20ruutukaappaukset/Vaihe%20(25).png?raw=true)
<br>
Kuva 28: Ohjelmien asennus.
<br>
<br>
Haluttuja ohjelmia alettiin asentamaan. Tässä ei kestänyt kauan.

![grub lataaja](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Ubuntu%20Server%2016.04.5%20LTS%20asennuksen%20ruutukaappaukset/Vaihe%20(26).png?raw=true)
<br>
Kuva 29: "Grub" -lataaja.
<br>
<br>
Kun halutut ohjelmat oli asennettu, alettiin asentamaan GRUB -käynnistyksen lataajaa, jonka ansioista voidaan palvelin käynnistää asennettuun käyttöjärjestelmäämme.

![grub käynnistyksenlataaja](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Ubuntu%20Server%2016.04.5%20LTS%20asennuksen%20ruutukaappaukset/Vaihe%20(27).png?raw=true)
<br>
Kuva 30: "Grub" -käynnistyksenlataaja.
<br>
<br>
Tuli ilmoitus, jossa kysyttiin, että halutaanko GRUB asentaa pääasialliseksi käynnistyksenlataajaksi. Valitsimme ”Yes” eli kyllä ja hyväksyimme valinnan painamalla ”Enter”.

![asennuksen viimeistely](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Ubuntu%20Server%2016.04.5%20LTS%20asennuksen%20ruutukaappaukset/Vaihe%20(28).png?raw=true)
<br>
Kuva 31: Asennuksen viimeistely.
<br>
<br>
Asennusta viimeisteltiin.

![valmis asennus](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Ubuntu%20Server%2016.04.5%20LTS%20asennuksen%20ruutukaappaukset/Vaihe%20(29).png?raw=true)
<br>
Kuva 32: Valmis asennus.
<br>
<br>
Asennus oli valmis! Käynnistimme palvelimen uudelleen valitsemalla nuolinäppäimillä ”Continue” ja hyväksymällä se painamalla Enter. Palvelin käynnistyi uudelleen ja irroitimme USB-asennustikun palvelinlaitteesta.

<br>
 
<h5 id="palvelimen-perusmaaritykset">Palvelimen perusmääritykset</h5>

Kirjauduimme palvelimelle sisään pääkäyttäjänä, jonka jälkeen teimme heti seuraavat toimenpiteet:

- Laitoimme palomuurin päälle .
- Teimme palomuurin säännön, joka sallii SSH-yhteyden. 
- Latasimme ja asensimme kaikki päivitykset, jonka jälkeen käynnistimme palvelimen uudelleen.
<br>
<br>

Teimme nämä seuraavalla komentoskriptillä:

```
sudo ufw enable && sudo ufw allow ssh && sudo apt update && sudo apt upgrade -y && sudo apt autoremove -y && reboot
```
<br>
Kun palvelin oli käynnistynyt uudelleen, asetimme siihen staattisen IP-osoitteen. Avasimme tiedoston, johon IP-osoitemääritykset tehdään komennolla:

```
sudoedit /etc/network/interfaces
```
<br>
Avautui ”interfaces” -tiedosto, johon laitoimme seuraavat määritykset:

![interfaces määritykset](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/etc_network_interfaces.png?raw=true)
<br>
Kuva 33: "Interfaces" -määritykset.
 
<br>
 
<h4 id="windows-server-2016-asennus-ja-konfigurointi-windowsserver-keskusyksikkoon">4.1.2. Windows Server 2016 asennus ja konfigurointi "WINDOWSERVER" -keskusyksikköön</h4>

Seuraavaksi asensimme Windows Server 2016 Datacenter, 64-bittisen version fyysiselle tietokoneelle, jota tarvisimme, jotta saamme tähän koneeseen tehtyä Active Directoryn ja yhdistettyä sen midPointiin. Kokeilimme aluksi Windows Serverin asennusta Oraclen VM VirtuaBoxiin, jotta voisimme testata sitä Windows Serveriä sitä kautta. Ilmeni kuitenkin ongelmia Windowsin aktivoinnin kanssa myöhemmin. Kun veimme (export) valmiin VirtualBoxin Windows Serverin imagen talteen, johon oli liitetty tuoteavain huomattiin, että kun tuotiin (import) levykuva takaisin VirtualBoxiin niin Windowsia ei oltu enää aktivoitu ja piti hankkia uusi tuoteavain. Tästä syystä on aihetta välttää Windowsin käyttöä virtuaaliympäristössä ainakin niiltä osin, jos tuodaan ja viedään VirtualBoxin levykuvia. Virtuaalikoneita voidaan käyttää kuitenkin esimerkiksi VirtualBox -palvelimella, jolloin vältytään levykuvien tuomisesta ja viemisestä. 
 
<br>
 
Aloitimme Windows Server 2016 Datacenter 64-bittisen version asennuksen fyysiselle tietokoneelle USB-livetikun avulla.

![kielen ja ajan valinta](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Windows%20Server/Screenshot%20(1).png?raw=true)
<br>
Kuva 34: Kielen ja ajan valinta.
<br>
<br>
Valitsimme asennusnäkymästä käyttöjärjestelmän kieleksi englannin [English (United States)]. Ajan ja valuutan määritykseksi valittiin suomenkieliset määritteet [Finnish (Finland)]. Näppäimistön kieleksi valittiin Suomi (Finnish).
Seuraavaksi klikattiin Next.

![lisenssin ehdot](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Windows%20Server/Screenshot%20(2).png?raw=true)
<br>
Kuva 35: Lisenssin ehdot.
<br>
<br>
Hyväksyimme lisenssin ehdot laittomalla täpän kohtaan "I accept the license terms" ja klikkasimme Next.

![käyttöjärjestelmän valinta](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Windows%20Server/Screenshot%20(3).png?raw=true)  
<br>
Kuva 36: Käyttöjärjestelmän valinta.
<br>
<br>
Seuraavaksi piti valita haluttu käyttöjärjestelmä. Vaihtoehtoina oli Windows Server 2016 Datacenter versio käyttöliittymällä tai ilman. Valitsimme käyttöjärjestelmän käyttöliittymällä [Windows Server 2016 Datacenter (Desktop Experience)] ja klikkasimme Next.

![asennustyypin valinta](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Windows%20Server/Screenshot%20(4).png?raw=true)
<br>
Kuva 37: Asennustyypin valinta.
<br>
<br>
Seuraavaksi asennusvaiheessa piti valita asennustyypin valinta. Valitsimme ensimmäisen vaihtoehdon: "Upgrade: Install Windows and keep files, settings, and applications". Vaikka meillä ei ollut ennestään asennettuna Windows käyttöjärjestelmää tietokoneella, niin tämä valinta ei haittaa, koska kyseisessä valinnassa on maininta, että nämä tiedostot, asetukset ja sovellukset säilyvät vain jos Windows käyttöjärjestelmä on valmiiksi asennettuna. 

![kiintolevylle asennus](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Windows%20Server/Screenshot%20(5).png?raw=true)
<br>
Kuva 38: Kiintolevyn asennus.
<br>
<br>
Seuraavaksi piti valita levy, jolle käyttöjärjestelmä asennetaan (tässä ei näy oikeaa levyä, koska imitoimme asennusta VirtualBoxissa). Valitsimme levyn ja klikkasimme Next.
 
<br>
 
<h5 id="windows-palvelimen-perusmaaritykset">4.1.2.1. Windows -palvelimen perusmääritykset</h5>

Asennettuamme Windows Server 2016 Datacenter 64-bittisen version fyysiselle koneelle, aktivoimme aluksi Windowsin. Windowsin voi aktivoida seuraavasti antamalla tuoteavaimen:
```
Settings - Update & Security - Activation
```
 
<br> 
 
Tämän jälkeen asetimme palvelimelle staattisen IP-osoiteen:
 
```
Network and Sharing Center - Connections: - Properties - Internet Protocol Version 4 - Properties 
```

<br>
 
Lisättyämme IP-osoitteen, verkkomaskin ja oletusyhdyskäytävän osoitteen staattiseksi asetimme DNS-osoitteiksi Haaga-Helian omat DNS-osoitteet, koska teimme projektia Haaga-Helian tiloissa. Otimme myös IPv6 kokonaan pois käytöstä kohdasta Internet Protocol Version 6 ottamalla täpän siitä pois.

Seuraavaksi laitoimme Network Discoveryn päälle, jotta testityöasemat löytävät palvelimen:
 
```
File Explorer - Network - Network discovery is turned off. - Turn On Network Discovery
```
 
<br>
 
Tämän jälkeen vaihdoimme tietokoneen nimeksi WINDOWSSERVER ja laitoimme Remote Desktop yhteyden päälle: 
```
System - Change settings - Change 
```
 
<br>
 
```
System - Remote settings - Allow remote connections to this computer
```
 
<br>
 
Käynnistimme koneen tässä vaiheessa uudestaan. Näiden perusmääritysten jälkeen ryhdyimme asentamaan Active Directorya. Avasimme Server Managerin, josta klikkasimme Manage - Add roles and Features.

![add roles and features](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Windows%20Server/Capture1.PNG?raw=true)
<br>
Kuva 39: Add Roles and Features.
<br>
<br>
Aukesi asennusohjelma. Klikattiin Next. 

![role-based or feature-based installation](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Windows%20Server/Capture2.PNG?raw=true)
<br>
Kuva 40: Role-based or feature-based installation
<br>
<br>
Seuraavaksi valitsimme kohdan Role-based or feature-based installation ja klikkasimme Next. 

![palvelimen valinta](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Windows%20Server/Capture3.PNG?raw=true)
<br>
Kuva 41: Palvelimen valinta.
<br>
<br>
Seuraavaksi piti valita tietokone, johon rooli aiotaan asentaan. Meille ei ollut muita kuin yksi vaihtoehto. Klikattiin Next.

![server roles](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Windows%20Server/Capture4.PNG?raw=true)
<br>
Kuva 42: Server Roles.
<br>
<br>
Seuraavaksi piti valita haluttu rooli, joka halutaan asentaa. Valitsimme Active Directory Domain Services, jonka jälkeen tuli pop-up, josta piti valita Add Features. 

![ad domain services](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Windows%20Server/Capture5.PNG?raw=true)
<br>
Kuva 43: Active Directory Domain Services.
<br>
<br>
Klikattiin seuraavaksi Next kun Active Directory Domain Services oli valittu.

![group policy management](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Windows%20Server/Capture6.PNG?raw=true)
<br>
Kuva 44: Group Policy Management.
<br>
<br>
Seuraavassa vaiheessa varmistettiin, että Group Policy Management ominaisuus oli valittuna. Tämän jälkeen klikattiiin Next.

![AD DS](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Windows%20Server/Capture7.PNG?raw=true) 
<br>
Kuva 45: AD DS.
<br>
<br>
Seuraavaksi tuli tietoa kyseisestä roolista. Klikattiin Next.

![confirmation](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Windows%20Server/Capture8.PNG?raw=true)
<br>
Kuva 46: Confirmation.
<br>
<br>
Varmistettiin seuraavaksi, että halutut ominaisuudet ja roolit tuli valittua. Näin olikin ja varmistettiin, että ei käynnistetä tietokonetta uudelleen vielä. Llikattiin Install.

![asennus valmis](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Windows%20Server/Capture9.PNG?raw=true)
<br>
Kuva 47: Asennus valmis.
<br>
<br>
Asennuksen jälkeen tuli vahvistus asennuksen onnistumisesta. Haluttiin konfiguroida domain controller heti, joten valittiin kohta "Promote this server to a domain controller"

![domain controller määritys](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Windows%20Server/Capture10.PNG?raw=true)
<br>
Kuva 48: Domain Controller -määritys.
<br>
<br>
Aukesi uusi määritysikkuna. Valitsimme uuden domain nimen: Add a new forest - pisnismiehet.local. Tämän jälkeen klikattiin Next.

![DSRM](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Windows%20Server/Capture11.PNG?raw=true)
<br>
Kuva 49: DSRM.
<br>
<br>
Seuraavaksi piti antaa salasana domainille, jos halutaan palauttaa Domain Controller. Annettiin salasana ja klikattiiin Next. 

![DNS delegation](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Windows%20Server/Capture12.PNG?raw=true)
<br>
Kuva 50: DNS Delegation
<br>
<br>
Seuraavaksi kysyttiin, että halutaanko luoda DNS delegation. Emme halunneet, joten klikkasimme Next.

![NetBIOS nimi](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Windows%20Server/Capture13.PNG?raw=true)
<br>
Kuva 51: NetBIOS -nimi.
<br>
<br>
Seuraavaksi määritysikkuna ehdotti NetBIOS nimeä. Hyväksyimme tämän ja klikkasimme Next.

![AD DS tietokanta](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Windows%20Server/Capture14.PNG?raw=true) 
<br>
Kuva 52: AD DS -tietokanta.
<br>
<br>
Seuraavaksi ehdotettiin kansioita, johon tiedostot tallennetaan. Meille sopivat nämä ja klikkasimme Next.

![tarkastelu](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Windows%20Server/Capture15.PNG?raw=true)
<br>
Kuva 53: Tarkastelu.
<br>
<br>
Seuraavaksi tuli määriteltyjen asetusten tarkasteluruutu. Kaikki oli OK eli klikkasimme Next. 

![edellytykset AD DS](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Windows%20Server/Capture16.PNG?raw=true)
<br>
Kuva 54: Edellytykset (AD DS).
<br>
<br>
Seuraavaksi määritysohjelma tarkisti edellytykset AD DS:n määritykseen. Edellytykset olivat OK. Klikkasimme Install. Asennuksen jälkeen tietokone käynnistyi uudelleen ja käynnistyksen yhteydessä huomattiin, että tietokone on nyt liitetty Domainiin.
 
<h5 id="hyper-vn-seka-uuden-virtuaalipalvelimen-asennus">4.1.2.2. Hyper-V:n sekä uuden virtuaalipalvelimen asennus</h5>
 
Halusimme laittaa Windows Serveriin OpenLDAP -palvelimen, joka asennetaan siihen virtuaalipalvelimena. Jotta virtuaalipalvelimen käyttö on mahdollista, lisäsimme Windows Serveriin Hyper-V:n. Sitä ennen latasimme <a href"http://releases.ubuntu.com/16.04/ubuntu-16.04.5-server-amd64.iso">64-bittisen Ubuntu Server 16.04.5 LTS:n levykuvan</a> talteen Windows -palvelimelle.
 
Lisäsimme sen Windows Server 2016:sta seuraavanlaisesti:

1. Avattiin Server Manager (Start -> Server Manager).
2. Valitiin Manage -> Add Roles and Features.
3. Ruutuun tuli "Before you begin" sivu. Painettiin eteenpäin painamalla "Next"
4. "Select installation type" -sivulta valittiin "Role-based or feature-based installation" ja klikattiin eteenpäin valisemalla "Next".
5. "Select destination server" -sivulta valittiin meidän palvelin eli WINDOWSSERVER.pisnismiehet.local. Seuraavaksi mentiin eteenpäin valitsemalla Next.
6. "Select server roles" -sivulta valittiin "Hyper-V".
7. Painettiin avautuvasta ikkunasta "Add Features". Ohitettiin "Features" -kohta painamalla "Next".
8. Mentiin "Create Virtual Switches", "Virtual Machine Migration" ja "Default Stores" -sivut oletusasetuksilla. Näissä vain painettiin "Next".
9. "Confirm installation selections" sivulla valittiin "Restart the destination server automatically if required" ja painettiin "Install".
 
Hyper-V saatiin asennettua.
 
Asennuksen jälkeen avattiin "Hyper-V Manager" (Tools -> Hyper-V Manager).
 
Kun Hyper-V Manager avautui, loimme uuden virtuaalisen kytkimen painamalla Actions- valikosta New -> Virtual Switch Manager.

Avautui uusi ikkuna. Vasemmasta paneelista valitsimme "New virtual network switch" ja valitsimme External. Lopuksi painoimme "Create Virtual Switch" -painiketta. Uudeksi nimeksi laitettiin "OPENLDAP Server" ja alimmaisesta "Connection type" kohdasta varmistettiin, että "External network" oli valittu. Lopuksi painoimme OK.

Tämän jälkeen alkoi varsinainen virtuaalipalvelimen luominen Hyper-V:ssä. Valittiin valikosta Actions -> New -> Virtual Machine.

Avautui virtuaalipalvelimen ohjattu asennus. Virtuaalipalvelimen nimeksi laitoimme "OPENLDAP Server". Käytämme virtuaalipalvelimessa oletussijaintia tallennuspaikaksi. Menimme eteenpäin painamalla "Next >". 

Seuraavasta ikkunasta valitsimme, että virtuaalipalvelin on 2. sukupolvea. Valitsimme siis "Generation 2" ja siirryimme eteenpäin painamalla "Next >".

Seuraavasta kohdassa määritimme virtuaalipalvelimelle keskusmuistin määrä (RAM). Meille riittää 2048 Megatavua, joten kirjoitamme arvoksi 2048 ja siirryimme eteenpäin painamalla "Next >".

"Configure Networking" -kohdassa valitsimme aiemmin tehdyn virtuaalisen kytkimen ja painoimme "Next >".

"Connect Virtual Hard Disk" -kohdassa märitämme, että teemme uuden virtuaalisen kiintolevyn ("Create a virtual hard disk") ja sen koko määriteltiin 80 Gigatavuun. Jatkoimme eteenpäin painamalla "Next >".

"Installation Options" -kohdassa valitsimme, että asennus tapahtuu levykyvan kautta "Install an operating system from a bootable CD/DVD-ROM -> Image file (.iso))". Haimme aiemmin ladatun levynkuvan sijainnin.

Lopuksi painoimme "Finish".

Käynnistimme luodun virtuaalipalvelimen ja teimme ohjatun Ubuntu Serverin asennusvaiheen samalla tavalla kuten muissakin aiemmin. Annoimme asennusvaiheessa palvelimen nimeksi "openldapserver".

Kirjauduimme asennuksen jälkeen sisälle tunnuksilla, jotka asennusvaiheessa teimme tämän jälkeen teimme seuraavat peruskonfiguraatiot:

1. Lataamaan ja asentamaan uusimmat päivitykset:
    ```
    sudo apt update && sudo apt upgrade -y && sudo apt autoremove -y
    ```
2. Laittamalla palomuurin päälle:
    ```
    sudo ufw enable
    ```
3. Sallimalla palomuurista SSH-yhteydet:
    ```
    sudo ufw allow ssh
    ```
4. Asettamalla palvelimelle staattiset IP-osoitteet:
    ```
    sudoedit /etc/network/interfaces
    ```
    "interfaces" -tiedosto avautui Nano-ohjelmaan, johon korvasimme kyseisen otsakkeen alla (otsakeessa risuaita edessä) olevat määritykset seuraavilla:
    <pre>
    # The primary network interface
    auto eth0
    iface eth0 inet static
    address 172.28.171.15
    netmask 255.255.0.0
    gateway 172.28.1.254
    network 172.28.0.0
    dns-nameservers 172.28.170.201 172.28.170.202
    </pre>
    Tallensimme muutokset näppäinkomennoilla ```Ctrl+X```, ```Y``` ja ```Enter```.
5. Konfiguroimalla DNS-asetukset:
    ```
    sudoedit /etc/hosts
    ```
    "hosts" -tiedosto avautui Nano-ohjelmaan, johon teimme seuraavat määritykset riville numero 2:
    ```
    127.0.1.1       ldap.pisnismiehet.local ldap openldapserver LDAP.PISNISMIEHET.LOCAL OPENLDAPSERVER LDAP
    ```
    Tallensimme muutokset näppäinkomennoilla ```Ctrl+X```, ```Y``` ja ```Enter```.

6. Asettamalla palvelimelle MOTD (Message Of The Day) -viestin, jos yrittää kirjautua SSH:n kautta:
    ```
    sudoedit /etc/motd
    ```
    "motd" -tiedosto avautui Nano -ohjelmalla, johon lisäsimme haluamamme viestin:
    ```
    OPENLDAPSERVER
    --------

    HUOMIO!
    -------
    Tämä työasema on varattu palvelinkäyttöön 13.1.2019 asti.
    Lisätietoja antaa tarvittaessa Jan Parttimaa (jan.parttimaa@myy.haaga-helia.fi)
    Kurssi: Monialaprojekti (ICT-Infrastruktuuri) PRO4TN004-3001
    Varaajat: Jan Parttimaa, Eetu Pihamäki ja Markus Nissinen
    Kurssiopettajat: Tero Karvinen ja Harto Holmström                                           

    ÄLÄ SAMMUTA TYÖASEMAA!


    TERVETULOA / WELCOME
    --------------------
    ```
    Tallensimme muutokset näppäinkomennoilla ```Ctrl+X```, ```Y``` ja ```Enter```. Kyseinen viesti näkyy, kun kirjautuu onnistuneesti SSH-yhteyden kautta sisään palvelimelle.

7. Asettamalla palvelimelle MOTD (Message Of The Day) -viestin, joka näkyy heti ruudulla, jos yrittää kirjautua suoraan palvelimelle:
    ```
    sudoedit /etc/issue
    ```
    "issue" -tiedosto avautui Nano -ohjelmalla, josta poistimme kaikki tiedot ja lisäsimme tämän jälkeen haluamamme viestin:
    ```
                                          OPENLDAPSERVER
    --------------------------------------------------------------------------------------------

    ----------------------------------------- HUOMIO! ------------------------------------------
    | Tämä työasema on varattu palvelinkäyttöön 13.1.2019 asti.                                |
    | Lisätietoja antaa tarvittaessa Jan Parttimaa (jan.parttimaa@myy.haaga-helia.fi)          |
    | Kurssi: Monialaprojekti (ICT-Infrastruktuuri) PRO4TN004-3001                             |
    | Varaajat: Jan Parttimaa, Eetu Pihamäki ja Markus Nissinen                                |
    | Kurssiopettajat: Tero Karvinen ja Harto Holmström                                        |
    |                                                                                          |
    --------------------------------------------------------------------------------------------
                                            NÄPIT IRTI!
                                       ÄLÄ SAMMUTA TYÖASEMAA!
    



    TERVETULOA / WELCOME
    --------------------
    ```
    Tallensimme muutokset näppäinkomennoilla ```Ctrl+X```, ```Y``` ja ```Enter```.


8. Käynnistämällä palvelimen uudelleen:
    ```
    sudo reboot
    ```
 
<br>
 
<h5 id="openldap-serverin-asennus-ja-konfigurointi-hyper-vn-virtuaalipalvelimeen">4.1.2.3. OpenLDAP serverin asennus ja konfigurointi Hyper-V:n virtuaalipalvelimeen</h5>

Asensimme OpenLDAP:n tyhjälle virtuaalipalvelimelle seuraavanlaisesti:

1. Avasimme palomuurista porttinumerot 389, 1389, 636 ja 1636 komennolla:
    ```
    sudo ufw allow 389/tcp && sudo ufw allow 389 && sudo ufw allow 1389/tcp && sudo ufw allow 1389 && sudo ufw allow 636/tcp && sudo ufw allow 636 && sudo ufw allow 1636/tcp && sudo ufw allow 1636
    ```
    Komennon jälkeen painoimme Enter.
 
2. Aloitimme OpenLDAP:n asennuksen komennoilla:
    ```
    sudo apt-get update
    sudo apt-get install slapd ldap-utils -y
    ```
    Jokaisen komennon jälkeen painoimme Enter. Lataus ja asennus alkoi. Ohjatun asennuksen aikana kysyttiin luomaan järjestelmänvalvojan salasanan LDAP-hakemistolle. Loimme sen ruudussa olevien ohjeiden mukaan. Asennuksessa ei kestänyt kauan.
 
3. Muokkasimme tiedostoa "ldap.conf" -tiedostoa komennolla:
    ```
    sudoedit /etc/ldap/ldap.conf
    ```
    Komennon jälkeen painoimme Enter. Tiedosto avautui Nano -ohjelmaan.
    
    Poistimme olemassa olevat pois ja laitoimme tiedostoon tämän tilalle:
    ```
    #
    # LDAP Defaults
    #

    # See ldap.conf(5) for details
    # This file should be world readable but not world writable.

    BASE    dc=ldap,dc=pisnismiehet,dc=local
    URI     ldap://localhost

    #SIZELIMIT      12
    #TIMELIMIT      15
    #DEREF          never

    # TLS certificates (needed for GnuTLS)
    TLS_CACERT      /etc/ldap/ca_certs.pem
    # TLS_CACERT    /etc/ssl/certs/ca-certificates.crt

    SSL start_tls
    TLS_REQCERT never
    ```
    Suljimme ja tallensimme tiedoston lopuksi.
     
4. Seuraavaksi aloitimme LDAP:n konfiguroinnin komennolla:
    ```
    sudo dpkg-reconfigure slapd
    ```
    Komennon annon jälkeen painoimme Enter. Alkoi ohjattu LDAP:n konfigurointi. Laitoimme seuraavat määritykset:
    - Omit OpenLDAP server configuration? No
    - DNS domain name: ldap.pisnismiehet.local
    - Organization name: pisnismiehet
    - Administrator password: <aikaisemmin luotu LDAP:n pääkäyttäjän salasana>
    - Confirm password: <aikaisemmin luotu LDAP:n pääkäyttäjän salasana>
    - Database backend to use: MDB
    - Do you want the database to be removed when slapd is purged? No
    - Move old database? Yes
    - Allow LDAPv2 protocol? No
     
    Konfigurointi oli valmis.
     
5. Asensimme seuraavaksi SSL-komponentit komennolla:
    ```
    sudo apt-get install gnutls-bin ssl-cert -y
    ```
    Komennon antamisen jälkeen painoimme Enter. Latauksessa ja asennuksessa kesti tovin.
     
6. Teimme kansion SSL-mallitiedostoille komennolla:
    ```
    sudo mkdir /etc/ssl/templates
    ```
    Komennon antamisen jälkeen painoimme Enter. Kansio luotiin haluttuun sijaintiin.
 
7. Loimme "ca_server.conf" -tiedoston komennolla:
    ```
    sudo nano /etc/ssl/templates/ca_server.conf
    ```
    Kyseinen tiedosto avautui Nano -ohjelmassa.

    Laitoimme tiedostoon seuraavat tiedot:
    ```
    cn = Pisnismiehet CA
    ca
    cert_signing_key
    ```
    Suljimme ja tallensimme lopuksi tiedoston.
     
8. Loimme "ldap_server.conf" -tiedoston komennolla:
    ```
    sudo nano /etc/ssl/templates/ldap_server.conf
    ```
    Kyseinen tiedosto avautui Nano -ohjelmassa.
     
    Laitoimme tiedostoon seuraavat tiedot:
    ```
    organization = "Pisnismiehet"
    cn = ldap.pisnismiehet.local
    tls_www_server
    encryption_key
    signing_key
    expiration_days = 3652
    ```
    Suljimme ja tallensimme lopuksi tiedoston.
 
9. Aloitimme yksityisen SSL-avaimen luonnin ```certtool``` työkalulla komennolla:
    ```
    sudo certtool -p --outfile /etc/ssl/private/ca_server.key
    ```
    Komennon antamisen jälkeen painoimme Enter. Avain luotiin.
 
10. Kirjoitimme äsken tehdyn avaimen sijaintiin ```/etc/ssl/certs``` komennolla:
    ```
    sudo certtool -s --load-privkey /etc/ssl/private/ca_server.key --template /etc/ssl/templates/ca_server.conf --outfile /etc/ssl/certs/ca_server.pem
    ```
    Komennon antamisen jälkeen painoimme Enter. Tämä onnistui moitteetta.
 
11. Loimme seuraavaksi yksityisen avaimen LDAP-palvelimelle komennolla:
    ```
    sudo certtool -p --sec-param high --outfile /etc/ssl/private/ldap_server.key
    ```
    Komennon antamisen jälkeen painoimme Enter. Tämäkin onnistui moitteetta.
 
12. Kirjoitimme myös tämän avaimen ```/etc/ssl/certs``` sijaintiin komennolla:
    ```
    sudo certtool -c --load-privkey /etc/ssl/private/ldap_server.key --load-ca-certificate /etc/ssl/certs/ca_server.pem --load-ca-privkey /etc/ssl/private/ca_server.key --template /etc/ssl/templates/ldap_server.conf --outfile /etc/ssl/certs/ldap_server.pem
    ```
    Komennon antamisen jälkeen painoimme Enter. Tämäkin myös onnistui moitteetta.
     
13. Lisäsimme OpenLDAP:lle pääsyn LDAP palvelinavaimiin. Ensiksi sallimme ```openldap``` ryhmälle oikeaan ryhmään komennolla:
    ```
    sudo usermod -aG ssl-cert openldap
    ```
    Komennon annon jälkeen painoimme Enter.
     
14. Seuraavaksi määrittelimme ```openldap``` ryhmälle käyttöikeudet ```ldap_server.key``` -tiedostolle komennolla:
    ```
    sudo chown :ssl-cert /etc/ssl/private/ldap_server.key
    ```
    Komennon jälkeen painoimme Enter.
     
15. Annoimme seuraavaksi ```ssl-cert``` -ryhmälle lukuoikeudet samaiseen tiedostoon komennolla:
    ```
    sudo chmod 640 /etc/ssl/private/ldap_server.key
    ```
    Komennon jälkeen painoimme Enter.
     
16. Siiryimme seuraavaksi kotihakemistoon ja loimme tiedoston ```addcerts.ldif``` komennoilla:
    ```
    cd
    nano addcerts.ldif
    ```
    Tiedosto avautui Nano -ohjelmaan. Lisäsimme seuraavat tiedostoon:
    ```
    dn: cn=config
    changetype: modify
    add: olcTLSCACertificateFile
    olcTLSCACertificateFile: /etc/ssl/certs/ca_server.pem
    -
    add: olcTLSCertificateFile
    olcTLSCertificateFile: /etc/ssl/certs/ldap_server.pem
    -
    add: olcTLSCertificateKeyFile
    olcTLSCertificateKeyFile: /etc/ssl/private/ldap_server.key
    ```
    Tallensimme ja suljimme lopuksi tiedoston.
 
17. Laitoimme tehdyt muutokset OpenLDAP-järjestelmään komennolla:
    ```
    sudo ldapmodify -H ldapi:// -Y EXTERNAL -f addcerts.ldif
    ```
    Komennon jälkeen painoimme Enter.
 
18. Käynnistimme OpenLDAP:n uudelleen komennolla:
    ```
    sudo service slapd force-reload
    ```
    Komennon jälkeen painoimme Enter.
 
19. Kopioitiin seuraavaksi ```ca_certs.pem``` toisesta sijainnista toiseen komennolla:
    ```
    sudo cp /etc/ssl/certs/ca_server.pem /etc/ldap/ca_certs.pem
    ```
    Komennon jälkeen painoimme Enter.
 
20. Kokeiltiin seuraavaksi toimiiko OpenLDAP:n yhteys komennolla:
    ```
    ldapwhoami -H ldap:// -x -ZZ
    ```
    Komennon jälkeen painoimme Enter. Tulokseksi tuli ```anonymous``` eli toisin sanoen yhteys toimi! Nyt on OpenLDAP asennettu, konfiguroitu ja suojattu LDAP-yhteys määritelty.

Koska emme halua käyttää suojaamatonta LDAP-yhteyttä, pakotamme käyttämään suojattua yhteyttä:

1. Kirjoitamme seuraavan komennon:
    ```
    sudo ldapsearch -H ldapi:// -Y EXTERNAL -b "cn=config" -LLL -Q "(olcSuffix=*)" dn olcSuffix
    ```
    Komennon jälkeen painoimme Enter. Tulokseksi tuli:
    ```
    dn: olcDatabase={1}mdb,cn=config
    olcSuffix: dc=ldap,dc=pisnismiehet,dc=local
    ```
    Pidämme tämän muistissa myöhempää varten.
 
2. Teimme kotihakemistoon ```forcetls.ldif``` -tiedoston komennolla:
    ```
    nano forcetls.ldif
    ```
    Komennon jälkeen painoimme Enter. Tiedosto avautui Nano -ohjelmaan.
    Laitoimme tiedostoon seuraavaa:
    ```
    dn: olcDatabase={1}mdb,cn=config
    changetype: modify
    add: olcSecurity
    olcSecurity: tls=1
    ```
    Tallensimme ja suljimme lopuksi tiedoston.
 
3. Ajoimme edellä mainitun tiedoston OpenLDAP-järjestelmään komennolla:
    ```
    sudo ldapmodify -H ldapi:// -Y EXTERNAL -f forcetls.ldif
    ```
 
4. Käynnistimme OpenLDAP -palvelimen uudelleen komennolla:
    ```
    sudo service slapd force-reload
    ```
5. Kokeilimme yhteyttä komennolla: 
    ```
    ldapsearch -H ldap:// -x -b "dc=ldap,dc=pisnismiehet,dc=local" -LLL -Z dn
    ```
    Yhteys toimi!
 
6. Kokeilimme lisäksi yhteyttä komennolla:
    ```
    ldapsearch -H ldap:// -x -b "dc=ldap,dc=pisnismiehet,dc=local" -LLL dn
    ```
     
    Tuli seuraava ilmoitus merkkinä siitä, ettei yhteys toiminut:
    ```
    Confidentiality required (13)
    Additional information: TLS confidentiality required
    ```
     
    Tämän piti siis tulla, koska pakotimme äskön käyttämään suojattua LDAP-yhteyttä. Eli kaikki toimii niin kuin piti!
 
<br>
 
<h5 id="phpLDAPadmin-web-kayttoliittyman-asennus-ja-konfigurointi">4.1.2.4. phpLDAPadmin -web-käyttöliittymän asennus ja konfigurointi</h5>
 
Asensimme phpLDAPadmin -web-käyttöliittymän OpenLDAP-palvelimelle, jotta siihen pääsee näppärästi käsiksi graaffisen käyttöliittymän kautta.

Teimme asennuksen ja konfiguroinnin seuraavanlaisesti:
 
1. Asensimme phpLDAPadminin komennolla:
    ```
    sudo apt-get install phpldapadmin -y
    ```
    Komennon jälkeen painoimme Enter. Latauksessa ja asennuksessa kesti tovin.
 
2. Seuraavaksi avasimme ```config.php``` -tiedoston komennolla:
    ```
    sudoedit /etc/phpldapadmin/config.php
    ```
    Komennon jälkeen painoimme Enter. Tiedosto avautui Nano-ohjelmaan. Muutimme tiedostosta seuraavat rivit:
    ```
    /* Hide the warnings for invalid objectClasses/attributes in templates. */
    $config->custom->appearance['hide_template_warning'] = true;
     
    /* Array of base DNs of your LDAP server. Leave this blank to have phpLDAPadmin
    auto-detect it for you. */
    $servers->setValue('server','base',array('dc=ldap,dc=pisnismiehet,dc=local'));

    /* A convenient name that will appear in the tree viewer and throughout
    phpLDAPadmin to identify this LDAP server to users. */
    $servers->setValue('server','name','OpenLDAP Server');

    /* Examples:
   'ldap.example.com',
   'ldaps://ldap.example.com/',
   'ldapi://%2fusr%local%2fvar%2frun%2fldapi'
    (Unix socket at /usr/local/var/run/ldap) */
    $servers->setValue('server','host','ldap://172.28.171.15');

    /* The port your LDAP server listens on (no quotes). 389 is standard. */
    $servers->setValue('server','port',389);

    /* Array of base DNs of your LDAP server. Leave this blank to have phpLDAPadmin
    auto-detect it for you. */
    $servers->setValue('server','base',array('dc=ldap,dc=pisnismiehet,dc=local'));

    /* Use TLS (Transport Layer Security) to connect to the LDAP server. */
    $servers->setValue('server','tls',true);
    ```
    Tallensimme ja suljimme lopuksi tiedoston.
3. Asetimme OpenLDAP:n kuuntelemaan kumpaakin porttia, jotta yhteys phpLDAPadmin web-käyttöliittymän ja OpenLDAP-hakemiston välillä toimisi komennolla:
    ```
    sudo slapd -H 'ldap://:389/ ldap://:1389/'
    ```

Nyt kun menemme sivulle http://<ip-osoite>/phpldapadmin, pääsemme web-käyttöliittymään, joihin kirjaudutaan OpenLDAP:n asennusvaiheessa tehdyillä tunnuksilla.
 
<br>
 
<h5 id="ryhmien-luonti-openldap-palvelimeen">4.1.2.5. Ryhmien luonti OpenLDAP-palvelimeen</h5>

 
Jotta OpenLDAP -palvelimen määritys sekä sen liittäminen midPointtiin olisi mahdollisimman helppoa, lisäsimme valmiiksi tarvittavat ryhmät OpenLDAP -palvelimeen graaffisen web-käyttöliittymän kautta. Meidän täytyi luoda seuraavat ryhmät:
 
- people
- services
- groups
- unixgroups
 
Teimme tarvittavat toimenpiteet seuraavasti:
 
1. Kirjauduimme selaimella OpenLDAP -palvelimen web-käyttöliittymään:
    ```
    http:://<ip-osoite>/phpldapadmin
    ```
    Kirjautumisikkunassa annoimme samat tunnukset, mitkä teimme OpenLDAP-palvelimen asennusvaiheessa (1.). Kirjauduimme sisään painamalla "Authenticate".
     
    ![](https://raw.githubusercontent.com/Eetu95/Open-source-IdM-solution/master/Kuvat/phpldapadmin/Screenshot1.JPG)
    <br>
    Kuva 55: Kirjautumisikkuna (phpLDAPadmin)
    <br>
    <br>
     
2. Vasemmasta valikosta avattiin puuhakemisto ja valittiin "Create new entry here".
 
    ![](https://raw.githubusercontent.com/Eetu95/Open-source-IdM-solution/master/Kuvat/phpldapadmin/Screenshot2.JPG)
    <br>
    Kuva 56: "Create new entry here".
    <br>
    <br>
 
3. Valitsimme avautuvasta valikosta luotava objekti. Koska haluttiin luoda ryhmä, valittiin "Generic: Posix Group"
 
    ![](https://raw.githubusercontent.com/Eetu95/Open-source-IdM-solution/master/Kuvat/phpldapadmin/Screenshot3.JPG)
    <br>
    Kuva 57: "Templates" -valikko.
    <br>
    <br>
 
4. Seuraavaksi avautui sivu, jossa meidän piti määrittää ryhmälle nimi. Laitoimme siihen halutun ryhmän nimen. Lopuksi valitsimme "Create Object".
 
5. Hyväksyimme muutokset painamalla "Commit".
 
6. Ryhmä luotiin onnistuneesti. Muut ryhmät tehtiin samalla tavalla kuten ensimmäinenkin luotu ryhmä.
 
<br>
 
<h5 id="openldap-palvelimen-maaritys-midpointtia-varten">4.1.2.6. OpenLDAP -palvelimen määritys midPointtia varten</h5>

 
MidPointin yhteyttä varten jouduimme tekemään vielä lisäkonfiguraatiota OpenLDAP-palvelimeen (OPENLDAPSERVER):

1. Siirryimme terminaaliin root-käyttäjäksi komennolla:
    ```
    sudo su
    ```

2. Latasimme ensiksi seuraavat kirjastot komennolla:
    ```
    sudo apt-get install libnet-ldap-perl libauthen-sasl-perl libuuid-perl perl-doc -y
    ```
    Komennon jälkeen painoimme Enter. Latauksessa ja asennuksessa kesti tovin.
 
3. Latasimme GitHubista slapdconf -työkalun komennolla:
    ```
    sudo wget https://raw.githubusercontent.com/Evolveum/slapdconf/master/slapdconf
    ```
    Komennon jälkeen painoimme Enter. 
 
4. Siirsimme kyseisen työkalun haluttuun sijaintiin (```/usr/local/bin```) komennolla:
    ```
    sudo mv slapdconf /usr/local/bin
    ```
    Komennon jälkeen painoimme Enter.
 
5. Käynnistimme palvelimen uudelleen komennolla:
    ```
    sudo reboot
    ```
 
6. Uudelleenkäynnistyksen jälkeen kirjauduimme takaisin sisälle. Avasimme ```40-slapd.conf``` -tiedoston komennolla:
    ```
    sudoedit /etc/rsyslog.d/40-slapd.conf
    ```
    Komennon jälkeen painoimme Enter. Tiedosto avautui Nano -ohjelmaan. Lisäsimme tiedostoon seuraavaa:
    ```
    local4.*        -/var/log/slapd.log
    & ~
    ```
    Tallensimme ja suljimme lopuksi tiedoston.
 
7. Asetettiin login taso haluttuun komennolla:
    ```
    slapdconf set-log-level stats
    ```
 
 
9. Avasimme tiedoston ```slapd``` komennolla:
    ``` 
    sudoedit /etc/default/slapd
    ```
    Komennon jälkeen painoimme Enter. Tiedosto avautui Nano -ohjelmaan. Etsimme tiedostosta riviä ```SLAPD_SERVICES=``` ja laitoimme arvoksi seuraavaa:
    ```
    SLAPD_SERVICES="ldap:/// ldapi:///"
    ```
    Suljimme ja tallensimme lopuksi tiedoston.
     
10. Teimme seuraavaksi teknisen käyttäjän midPointtia varten. Teimme kotihakemistoon tiedoston ```admin.ldif``` komennolla:
    ```
    sudoedit admin.ldif
    ```
    Komennon jälkeen painoimme Enter. Tiedosto avautui Nano-ohjelmassa.
    ```
    dn: ou=Administrators,dc=example,dc=com
    objectclass: top
    objectclass: organizationalunit
    ou: Administrators
    
    dn: cn=idm,ou=Administrators,dc=example,dc=com
    objectclass: top
    objectclass: person
    cn: idm
    sn: IDM Administrator
    description: Special LDAP acccount used by the IDM
    to access the LDAP data.
    userPassword: {SSHA}R5KF3K4X2FX5gkWKuDxm4M6gZyO0QgNF
    ```
    Suljimme ja tallensimme lopuksi tiedoston.
     
11. Lisäsimme edellä mainitun tiedoston OpenLDAP-järjestelmään komennolla:
    ```
    ldapadd -Y EXTERNAL -H ldapi:/// -f admin.ldif
    ```
    Komennon jälkeen painoimme Enter.
 
12. Teimme seuraavaksi kotihakemistoon pääsynvalvontaa varten ```aci.ldif``` -tiedoston komennolla:
    ```
    sudoedit aci.ldif
    ```
    Komennon jälkeen painoimme Enter. Tiedosto avautui Nano -ohjelmaan.
    Laitoimme siihen seuraavaa:
    ```
    dn: olcDatabase={1}mdb,cn=config
    changetype: modify
    replace: olcAccess
    olcAccess: to attrs=userPassword dn.subtree="ou=people,dc=ldap,dc=pisnismiehet,dc=local" filter="(midPointAccountStatus=disabled)" by dn.subtree="ou=unixgroups,dc=ldap,dc=pisnismiehet,dc=l$
    olcAccess: to attrs=userPassword,shadowLastChange by dn="cn=idm,ou=Administrators,dc=ldap,dc=pisnismiehet,dc=local" write by dn.exact=gidNumber=0+uidNumber=0,cn=peercred,cn=external,cn=aut$
    olcAccess: to dn.base="" by * read
    olcAccess: to dn.subtree="ou=people,dc=ldap,dc=pisnismiehet,dc=local" by dn="cn=idm,ou=Administrators,dc=ldap,dc=pisnismiehet,dc=local" write
    olcAccess: to dn.subtree="ou=groups,dc=ldap,dc=pisnismiehet,dc=local" by dn="cn=idm,ou=Administrators,dc=ldap,dc=pisnismiehet,dc=local" write
    olcAccess: to dn.subtree="ou=unixgroups,dc=ldap,dc=pisnismiehet,dc=local" by dn="cn=idm,ou=Administrators,dc=ldap,dc=pisnismiehet,dc=local" write
    olcAccess: to * by dn.exact=gidNumber=0+uidNumber=0,cn=peercred,cn=external,cn=auth write by dn="cn=idm,ou=Administrators,dc=ldap,dc=pisnismiehet,dc=local" read by self read by * none
    ```
    Tallensimme ja suljimme lopuksi tiedoston. 
 
13. Annoimme seuraavaksi seuraavan komennon:
    ```
    slapdconf set-suffix-prop dc=ldap,dc=pisnismiehet,dc=local 'olcLimits:dn.exact="cn=idm,ou=Administrators,dc=ldap,dc=pisnismiehet,dc=local" size.prtotal=unlimited'
    ```
    Komennon jällkeen painoimme Enter. Nyt oli rajat määritelty midPointtia varten.
 
14. Määritimme salasanavaatimukset komennolla:
    ```
    slapdconf set-overlay-prop dc=ldap,dc=pisnismiehet,dc=local ppolicy olcPPolicyDefault:cn=pwpolicy,dc=ldap,dc=pisnismiehet,dc=local
    ```
    Komennon jälkeen painoimme Enter.

OpenLDAP -palvelimelle suositeltiin kanssa lisätä uusi skeematiedosto ```midpoint.schema```. Tämän teimme seuraavanlaisesti root-käyttäjänä:
 
1. Latasimme kyseisen skeematiedoston GitHubista komennolla:
    ```
    wget wget https://raw.githubusercontent.com/Evolveum/midpoint/master/samples/resources/ldap/midpoint.schema
    ```
    Komennon jälkeen painoimme Enter. Skeema latautui kotihakemistoon.
 
2. Kopioitiin tiedosto uuteen sijaintiin komennolla:
    ``` 
    sudo cp midpoint.schema /etc/ldap/schema/
    ```
 
3. Luotiin kansio ```openldapldif``` eri sijaintiin komennolla:
    ```
    mkdir /tmp/openldapldif
    ```
 
4. Luotiin seuraavaksi kyseiseen kansioon ```slapd.conf```:
    ```
    nano /tmp/openldapldif/slapd.conf
    ```
    Tiedosto avautui Nano -ohjelmaan. Lisättiin seuraavaksi kyseiseen tiedostoon seuraavaa:
    ```
    include /etc/ldap/schema/midpoint.schema
    ```
    Tallensimme ja suljimme lopuksi tiedoston. 
 
5. Ajettiin seuraavaksi seuraava komento:
    ```
    cd /tmp/openldapldif && slaptest -f slapd.conf -F .
    ```
    Tämä loi kansion ```cn=config``` ja tiedoston ```cn=config.ldif```
 
6. Muokattiin seuraavaksi ```{5}midpoint.ldif``` -tiedostoa ja poistettiin turhia rivejä:
    ```
    cd /etc/ldap/slapd.d/cn=config/cn=schema
    sudoedit sudoedit cn\=\{5\}midpoint.ldif
    ```
 
7. Seurattiin <a href="https://www.youtube.com/watch?v=qAedVMMunk8">ohjevideosta</a> mitä pitää poistaa (7:07 ->). Tallensimme tehdyt muutokset ja suljimme tiedoston.
 
8. Ajoimme lopuksi tiedoston OpenLDAP-järjestelmään komennolla:
    ```
    ldapadd -Y EXTERNAL -H ldapi:/// -f cn\=\{0\}midpoint.ldif
    ```
 
9. Verifoitiin, että tiedosto varmasti meni järjestelmään läpi komennolla:
    ```
    ldapsearch -Q -LLL -Y EXTERNAL -H ldapi:/// -b cn=config cn=*midpoint*
    ```
    Katsottiin ohjevideosta uudelleen mitä piti tulla tulokseksi ja saatiin sama eli onnistui skeeman laitto!
 
<br>
 
<h5 id="suojatun-web-yhteyden-maaritys-https1">4.1.2.7. Suojatun web-yhteyden määritys (https)</h5>
 
Suojattua yhteyttä tarvitaan, jotta  tietojen eheys ja luottamuksellisuus pysyy turvassa käyttäjän ja sivuston välillä. Otimme HTTPS suojauksen käyttöön midPoint palvelimella, jotta web-käyttöliittymä on suojattu. Suojauksen huomaa selaimella siitä, että selain käyttää https:// yhteyttä osoitepalkissa.

Koska meillä ei ole rahallista budjettia meidän projektissa, emme voineet hankkia kunnollista sertifikaattia, koska se olisi maksanut jonkin verran. Näin ollen käytimme itseallekirjoitettua sertifikaattia.
 
Suojatun yhtyeden määritys onnistui seuraavanlaisesti:

1. Suojattua yhteyttä varten tarvitsi asentaa Apache2 komennoilla:

```
sudo apt-get update
sudo apt-get install apache2 -y
```
Latauksessa ja asennuksessa kesti tovin.
 
2. Laitettiin seuraavaksi Apache2:sta ssl-moduuli päälle komennolla:
```
sudo a2enmod ssl
```
Komennon antamisen jälkeen painoimme Enter. Moduuli meni päälle.
 
3. Käynnistettiin Apache2 uudelleen komennolla:
```
sudo service apache2 restart
```
 
4. Luodaan uusi sijainti itseallekitjoitetulle sertifikaatille:
```
sudo mkdir /etc/apache2/ssl
```
Komennon antamisen jälkeen painoimme Enter. Uusi sijainti luotiin.
 
5. Itseallekirjoitetun sertifikaatin loimme komennolla:
```
sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /etc/apache2/ssl/apache.key -out /etc/apache2/ssl/apache.crt
```
Mitä komento tekee:

- openssl = CLI työkalu, jolla luodaan ja hallitaan OpenSSL sertifikaatteja, avaimia ja muita tiedostoja.
- req = alikomento, jolla kerrotaan että halutaan käyttää X.509 CSR:ää. X.509 on julkisenavaimen infrastruktuuri standardi, jota
SSL ja TLS noudattavat. Teimme siis uuden X.509 sertin.
- "-x509" = modifioi aikaisempaa alikomentoa kertomalla apuohjelmalle, että halutaan tehdä itsekirjoitettu sertifikaatti sen sijaan että tehtäisiin
sertifikaatin allekirjoitus pyyntö.
- "-nodes" = Kertoo OpenSSL:lle että se voi ohittaa sertifikaatin suojauksen tunnuslauseen. Apachen pitää pystyä
lukemaan tiedosto ilman, että käyttäjä puuttuu siihen silloin kun palvelin käynnistyy. Tunnuslause (passphrase)
estäisi tämän toteutumisen, koska meidän pitäisi aina syöttää se jokaisen uudelleenkäynnistyksen yhteydessä.
- "-days 365" = Tämä asettaa sertifikaatin voimassaolo ajan 365 päiväksi.
- "-newkey rsa:2048" =Tällä määritellään uuden sertifikaatin ja avaimen luonti samaan aikaan. Rsa:2048 kertoo että pitää
tehdä RSA avain, joka on 2048 bittiä pitkä.
- "-keyout" = Kertoo OpenSSL:lle minne luotu yksityinen avaintiedosto pistetään.
- "-out" = Kertoo OpenSSL:lle minne sertifikaatti pistetään.

Komentoon piti luoda tiedot meistä:
```
Country Name (2 letter code) [AU]:FI
State or Province Name (full name) [Some-State]:Uusimaa
Locality Name (eg, city) []:Helsinki
Organization Name (eg, company) [Internet Widgits Pty Ltd]:Pisnismiehet
Organizational Unit Name (eg, section) []:Projectgroup
Common Name (e.g. server FQDN or YOUR name) []:*palvelimen IP-osoite*
Email Address []:jan.parttimaa@myy.haaga-helia.fi
```
 
6. Siirryimme root -käyttäjäksi komennolla:
```
sudo su
```
 
7. Käänteistä välityspalvelinta varten joudumme sallimaan neljän eri moduulin käytön. Nämä sallimme komennoilla:
```
sudo a2enmod proxy
sudo a2enmod proxy_http
sudo a2enmod proxy_balancer
sudo a2enmod lbmethod_byrequests
```
 
8. Käynnistimme taas Apache2:sen uudelleen:
```
sudo systemctl restart apache2
```
9. Avasimme seuraavan tiedoston komennolla:
```
sudo nano /etc/apache2/sites-available/default-ssl.conf
```
Tiedosto avautui Nano- ohjelmassa.
 
10. Muutimme "default-ssl.conf" -tiedostosta seuraavat kohdat:
```
ServerAdmin jan.parttimaa@myy.haaga-helia.fi
# ServerName 172.28.171.15
DocumentRoot /var/www/html

#   SSL Engine Switch:
#   Enable/Disable SSL for this virtual host.
SSLEngine on

#   A self-signed (snakeoil) certificate can be created by installing
#   the ssl-cert package. See
#   /usr/share/doc/apache2/README.Debian.gz for more info.
#   If both key and certificate are stored in the same file, only the
#   SSLCertificateFile directive is needed.
SSLCertificateFile      /etc/apache2/ssl/apache.crt
SSLCertificateKeyFile /etc/apache2/ssl/apache.key

```
Tallensimme ja suljimme lopuksi tiedoston.
 
11. Avasimme tämän jälkeen seuraavan tiedoston:
```
sudoedit /etc/apache2/sites-available/000-default.conf
```
Tiedosto avautui myös Nano -ohjelmaan.
 
12. Muutimme "000-default.conf" -tiedostosta seuraavat kohdat:
```
ServerName http://172.28.171.15
Redirect /secure https://172.28.171.15/phpldapadmin
Redirect permanent / https://172.28.171.15/phpldapadmin

# ServerAdmin webmaster@localhost
# DocumentRoot /var/www/html
```
Tallensimme ja suljimme lopuksi tiedoston.
 
13. Aktivoimme Apachen SSL Virtuaalihostin komennolla:
```
sudo a2ensite default-ssl.conf
```
 
14. Käynnistimme lopuksi Apachen uudelleen komennolla:
```
sudo service apache2 restart
```

Käynnistyksen jälkeen testattiin Apachen toimivuutta. Kirjoitettiin selaimeen:
```
https://*palvelimen IP-osoite*
```
Tällöin tuli herja siitä, että sertifikaatti ei ole luotettava. Tämä johtuu siitä, koska sertifikaatti on itse allekirjoitettu eikä hankittu valtuutetulta taholta. Ohitin herjan Chromessa vain klikkaamalla Advanced ja ``` Proceed to https://*palvelimen IP-osoite*```
 
![https Chrome](https://raw.githubusercontent.com/Eetu95/Open-source-IdM-solution/master/Kuvat/chrome_https.PNG)
<br>
Kuva 58: Sertifikaattivaroitus (Chrome).
<br>
<br>
 
<br>
 
<h4 id="virtualbox-palvelimen-asennus-ja-konfigurointi-vmserver-keskusyksikkoon">4.1.3. VirtualBox -palvelimen asennus ja konfigurointi "VMSERVER" -keskusyksikköön</h4>

Asensimme "VMSERVER" -keskusyksikköön Linux -käyttöjärjestelmään pohjautuvan 64-bittisen Ubuntu Server 16.04.5 LTS -käyttöjärjestelmän samalla tavalla kuten se asennettiin "MIDPOINTIDM" -keskusyksikköön <a href="#ubuntu-server-asennus-ja-konfigurointi-midpointidm-keskusyksikkoon">aiemmassa kappaleessa</a>. Muuten tehdään siis samalla tavalla mutta asennusvaiheessa annetaan palvelimen nimeksi "VMSERVER" eikä "MIDPOINTIDM". Loimme myös samat käyttäjätunnukset asennusvaiheessa. Suositeltavaa tosin olisi tehdä erit käyttäjätunnukset.

Kun olimme asentaneet Ubuntun palvelimena toimivalle keskusyksikölle, kirjauduimme sisään käyttämällä asennusvaiheessa luotuja käyttäjätunnuksia. Kun olimme päässeet sisälle, aloimme tedä seuraavat peruskonfiguraatiot järjestyksessä (jokaisen komennon jälkeen painoimme Enter):

1. Lataamaan ja asentamaan uusimmat päivitykset:
    ```
    sudo apt update && sudo apt upgrade -y && sudo apt autoremove -y
    ```
2. Laittamalla palomuurin päälle:
    ```
    sudo ufw enable
    ```
3. Sallimalla palomuurista SSH-yhteydet:
    ```
    sudo ufw allow ssh
    ```
4. Asettamalla palvelimelle staattiset IP-osoitteet:
    ```
    sudoedit /etc/network/interfaces
    ```
    "interfaces" -tiedosto avautui Nano-ohjelmaan, johon korvasimme kyseisen otsakkeen alla (otsakeessa risuaita edessä) olevat määritykset seuraavilla:
    <pre>
    
    # The primary network interface
    auto eno1
    iface eno1 inet static
    address 172.28.175.26
    netmask 255.255.0.0
    gateway 172.28.1.254
    network 172.28.0.0
    dns-nameservers 172.28.170.201 172.28.170.202
    </pre>
    Tallensimme muutokset näppäinkomennoilla ```Ctrl+X```, ```Y``` ja ```Enter```.

5. Konfiguroimalla DNS-asetukset:
    ```
    sudoedit /etc/hosts
    ```
    "hosts" -tiedosto avautui Nano-ohjelmaan, johon teimme seuraavat määritykset riveille numero 2 ja 3:
    ```
    127.0.1.1       VMSERVER vmserver
    172.28.175.26   vmserver.pisnismiehet.local
    ```
    Tallensimme muutokset näppäinkomennoilla ```Ctrl+X```, ```Y``` ja ```Enter```.

6. Asettamalla palvelimelle MOTD (Message Of The Day) -viestin, jos yrittää kirjautua SSH:n kautta:
    ```
    sudoedit /etc/motd
    ```
    "motd" -tiedosto avautui Nano -ohjelmalla, johon lisäsimme haluamamme viestin:
    ```
    VMSERVER
    --------

    HUOMIO!
    -------
    Tämä työasema on varattu palvelinkäyttöön 13.1.2019 asti.
    Lisätietoja antaa tarvittaessa Jan Parttimaa (jan.parttimaa@myy.haaga-helia.fi)
    Kurssi: Monialaprojekti (ICT-Infrastruktuuri) PRO4TN004-3001
    Varaajat: Jan Parttimaa, Eetu Pihamäki ja Markus Nissinen
    Kurssiopettajat: Tero Karvinen ja Harto Holmström                                           

    ÄLÄ SAMMUTA TYÖASEMAA!
    JOS TARVITSEE SAMMUTTAA TAI KÄYNNISTÄÄ UUDELLEEN,
    SULJE ENSIN KAIKKI AVOINNA OLEVAT VIRTUAALIKONEET!


    TERVETULOA / WELCOME
    --------------------
    ```
    Tallensimme muutokset näppäinkomennoilla ```Ctrl+X```, ```Y``` ja ```Enter```. Kyseinen viesti näkyy, kun kirjautuu onnistuneesti SSH-yhteyden kautta sisään palvelimelle.

7. Asettamalla palvelimelle MOTD (Message Of The Day) -viestin, joka näkyy heti ruudulla, jos yrittää kirjautua suoraan palvelimelle:
    ```
    sudoedit /etc/issue
    ```
    "issue" -tiedosto avautui Nano -ohjelmalla, josta poistimme kaikki tiedot ja lisäsimme tämän jälkeen haluamamme viestin:
    ```
                                             VMSERVER
    --------------------------------------------------------------------------------------------

    ----------------------------------------- HUOMIO! ------------------------------------------
    | Tämä työasema on varattu palvelinkäyttöön 13.1.2019 asti.                                |
    | Lisätietoja antaa tarvittaessa Jan Parttimaa (jan.parttimaa@myy.haaga-helia.fi)          |
    | Kurssi: Monialaprojekti (ICT-Infrastruktuuri) PRO4TN004-3001                             |
    | Varaajat: Jan Parttimaa, Eetu Pihamäki ja Markus Nissinen                                |
    | Kurssiopettajat: Tero Karvinen ja Harto Holmström                                        |
    |                                                                                          |
    --------------------------------------------------------------------------------------------
                                            NÄPIT IRTI!
                                       ÄLÄ SAMMUTA TYÖASEMAA!
                        JOS TARVITSEE SAMMUTTAA TAI KÄYNNISTÄÄ UUDELLEEN,
                        SULJE ENSIN KAIKKI AVOINNA OLEVAT VIRTUAALIKONEET!



    TERVETULOA / WELCOME
    --------------------
    ```
    Tallensimme muutokset näppäinkomennoilla ```Ctrl+X```, ```Y``` ja ```Enter```.


8. Käynnistämällä palvelimen uudelleen:
    ```
    sudo reboot
    ```
 
Kun palvelin oli käynnistynyt uudelleen, kirjauduimme siihen uudelleen sisälle. Tämän jälkeen aloitimme VirtualBoxin asentamisen palvelimelle.
 
Teimme VirtualBoxin asennuksen seuraavanlaisesti:
 
1. Asensimme tarvittavat Linux Headers:it komennolla:
    ```
    sudo apt-get -y install gcc make linux-headers-$(uname -r) dkms
    ```
    Komennon antamisen jälkeen painoimme Enter. Lataus ja asennus alkoi. Tähän ei mennyt kauan.
 
2. Ladattiin ja lisättiin VirtualBoxin repositoryn avain sekä itse repository (jokaisen komennon annon jälkeen painettiin Enter):
    ```
    wget -q https://www.virtualbox.org/download/oracle_vbox_2016.asc -O- | sudo apt-key add -
    sudo sh -c 'echo "deb http://download.virtualbox.org/virtualbox/debian $(lsb_release -sc) contrib" >> /etc/apt/sources.list'
    ```
 
3. Asennettiin VirtualBox (jokaisen komennon annon jälkeen painettiin Enter):
    ```
    sudo apt-get update
    sudo apt-get install virtualbox-5.2 -y
    ```
 
4. Testasimme, että VirtualBox on asennettu komennolla:
    ```
    VBoxManage -v
    ```
    Oli asennettu onnistuneesti.
 
5. Ladattiin ja asennettiin VirtualBox Extension Pack (jokaisen komennon annon jälkeen painettiin Enter):
    ```
    curl -O https://download.virtualbox.org/virtualbox/5.2.20/Oracle_VM_VirtualBox_Extension_Pack-5.2.20.vbox-extpack
    sudo VBoxManage extpack install Oracle_VM_VirtualBox_Extension_Pack-5.2.20.vbox-extpack
    ```
    Latauksessa ja asennuksessa kesti jonkin aikaa.
 
6. Testasimme, että VirtualBox Extension Pack oli asennettu:
    ```
    VBoxManage list extpacks
    ```
     
    Tuloksena tuli seuraavaa:
    ```
    Extension Packs: 1
    Pack no. 0:   Oracle VM VirtualBox Extension Pack
    Version:      5.2.20
    Revision:     125813
    Edition:
    Description:  USB 2.0 and USB 3.0 Host Controller, Host Webcam, VirtualBox RDP, PXE ROM, Disk Encryption, NVMe.
    VRDE Module:  VBoxVRDP
    Usable:       true
    Why unusable:
    ```
    Onnistuneesti oli asennettu.

<br> 
 
<h4 id="phpvirtualbox-web-kayttöliittyman-asennus-ja-konfigurointi">4.1.3.1. phpVirtualBox -web-käyttöliittymän asennus ja konfigurointi</h4>

Jotta pystymme hallitsemaan VirtualBoxia graaffisesti, jouduimme asentamaan ja määrittämään palvelimelle phpVirtualBoxin. Tämän ansiosta voimme hallita palvelimelle asennettua VirtualBoxia graaffisesti suoraan verkkoselaimelta käsin mistä vain. Jotta phpVirtualBox toimisi, jouduimme myös asentamaan palvelimelle Apachen2:sen sekä PHP:n.

Hoidimme phpVirtualBoxin sekä muiden komponenttien asennuksen sekä konfiguroinnin seuraavanlaisesti:

1. Sallimme ensiksi palomuurista http, https:n, www:n sekä portit 9000, 9001 sekä 9002:
    ```
    sudo ufw allow http && sudo ufw allow https && sudo ufw allow www && sudo ufw allow 9000/tcp && sudo ufw allow 9000 && sudo ufw allow 9001/tcp && sudo ufw allow 9001 && sudo ufw allow 9002/tcp && sudo ufw allow 9002
    ```
    Komennon annon jälkeen painoimme Enter. Uudet palomuurisäännöt tulivat voimaan. Sallimme portit http, https ja www:lle, jotta asiakaskone voi ottaa yhteyden verkkoselaimella palvelimelle ja pääsee ohjaamaan VirtualBoxia graaffisesti verkkoselaimella. Sallimme porttinumerot 9000 - 9002, jotta asiakas voi tarpeen tullen ottaa konsoliyhteyden sekä etäyhteyden VirtualBoxissa oleviin kolmeen virtuaalikoneeseen.
2. Siirryttiin komentokehotteessa root käyttäjäksi:
    ```
    sudo su
    ```
    Komennon jälkeen painoimme Enter ja annoimme myös salasanan. Oltiin nyt root käyttäjiä.
3. Lisättiin uusi käyttäjä "vbox" ja se uuteen ryhmään "vboxusers"
    ```
    useradd -m vbox -G vboxusers
    ```
    Komennon jälkeen painoimme Enter. Uusi käyttäjä luotiin.
4. Määriteltiin tämän jälkeen "vbox" -käyttäjälle salasana komennolla:
    ```
    passwd vbox
    ```
    Komennon jälkeen painoimme Enter. Tämän jälkeen määritimme käyttäjälle uuden salasanan ruudussa olevien ohjeiden mukaisesti.
5. Lisäsimme uuden tiedoston:
    ```
    sudoedit /etc/default/virtualbox
    ```
    "virtualbox" -tiedosto avautui "Nano" -ohjelmassa. Lisäsimme siihen seuraavan määrityksen, jossa kiinnitämme käyttäjän "vbox" VirtualBoxin web-käyttöliittymän käyttäjäksi: ```VBOXWEB_USER=vbox```. Lopuksi tallensimme ja suljimme tiedoston.
6. Sallimme "vboxweb-servicen" käynnistyvän automaattisesti, kun palvelin käynnistyy (jokaisen komennon jälkeen painoimme Enter):
    ```
    systemctl enable vboxweb-service
    systemctl start vboxweb-service
    ```
7. Asensimme Apache2:n, PHP:n sekä muut tarvittavat:
    ```
    apt-get -y install apache2 libapache2-mod-php7.0 libapr1 libaprutil1 libaprutil1-dbd-sqlite3 libaprutil1-ldap libapr1 php7.0-common php7.0-mysql php7.0-soap php-pear wget -y
    ```
    Komennon annon jälkeen painoimme Enter. Latauksessa ja asennuksessa kesti tovin.
8. Käynnistettiin Apache2 uudelleen:
    ```
    systemctl restart apache2.service
    ```
    Komennon jälkeen painoimme Enter. Apache2 käynnistyi uudelleen.
9. Vaihdettiin sijaintia ja ladattiin phpVirtualBox (jokaisen komennon jälkeen painoimme Enter):
    ```
    cd /var/www/html
    wget https://github.com/phpvirtualbox/phpvirtualbox/archive/master.zip
    ```
10. Asennettiin "unzip", jotta voidaan purkaa ladattu zip -kansio:
    ```
    sudo apt-get install unzip -y
    ```
    Komennon jälkeen painoimme Enter. Lataus ja asenns alkoi, jossa ei kestänyt kauan.
11. Purkasimme ladatun zip-kansion:
    ```
    unzip phpvirtualbox-master.zip
    ```
    Komennon jälkeen painoimme Enter. Kansio purettiin haluttuun sijaintiin, mihin menimme kohdassa 8.
12. Uudelleennimettiin purettu kansio:
    ```
    mv phpvirtualbox-master phpvirtualbox
    ```
13. siirryttiin "phpvirtualbox" -kansioon:
    ```
    cd phpvirtualbox
    ```
14. Luotiin config tiedosto kopioimalla esimerkkitiedosto:
    ```
    cp config.php-example config.php
    ```
    Avattiin "config.php" tiedosto komennolla:
    ```
    sudoedit config.php
    ```
    Tiedosto avautui Nano -ohjelmassa. Etsimme tiedostosta kyseisen rivin:
    ```
    var $password = 'secret';
    ```
    Sanan "secret" tilalle asetimme saman salasanan mikä "vbox" käyttäjällä on. Tallensimme lopuksi tiedoston ja suljimme sen myös.
15. Käynnistimme "vboxweb-service" palvelun uudelleen komennolla:
    ```
    systemctl restart vboxweb-service
    ```
16. Kirjauduimme root-käyttäjästä pois komennolla:
    ```
    exit
    ```
 
Nyt on phpvirtualbox asennettu. Menimme verkkoselaimella osoitteeseen ```http://<VMSERVERIN ip-osoite>/phpvirtualbox``` eli meidän tapauksessa ```http://172.28.175.26/phpvirtualbox```. Siirrymme sivulle painamalla Enter.

Avautui kirjautumisikkuna. Oletuskäyttäjätunnus (Username) on ```admin``` ja salasana (Password) on ```admin```. Kirjauduimme näillä painamalla "Log in".

![](https://raw.githubusercontent.com/Eetu95/Open-source-IdM-solution/master/Kuvat/phpvirtualboxlogin.JPG)
<br>
Kuva 59: Kirjautumisruutu (phpVirtualBox).
<br>
<br>

Pääsimme sisään. Seuraavaksi vaihdamme oletussalasanan omaan, parempaan salasanaan. Se onnistuu valitsemalla käyttliittymän valikosta ```File -> Change Password```. Avautuu ikkuna, johon pitää kertoa sekä vanha salasana, että uusi salasana kahdesti. Lopuksi hyväksytään muutokset painamalla OK.

![](https://raw.githubusercontent.com/Eetu95/Open-source-IdM-solution/master/Kuvat/phpvirtualboxpassword.JPG)
<br>
Kuva 60: Salasanan vaihto (phpVirtualbox).
<br>
<br>
 
<br>
 
<h5 id="suojatun-yhteyden-maaritys-https2">4.1.3.2. Suojatun web-yhteyden määritys (https)</h5>
 
Suojattua yhteyttä tarvitaan, jotta  tietojen eheys ja luottamuksellisuus pysyy turvassa käyttäjän ja sivuston välillä. Otimme HTTPS suojauksen käyttöön midPoint palvelimella, jotta web-käyttöliittymä on suojattu. Suojauksen huomaa selaimella siitä, että selain käyttää https:// yhteyttä osoitepalkissa.

Koska meillä ei ole rahallista budjettia meidän projektissa, emme voineet hankkia kunnollista sertifikaattia, koska se olisi maksanut jonkin verran. Näin ollen käytimme itseallekirjoitettua sertifikaattia.
 
Suojatun yhtyeden määritys onnistui seuraavanlaisesti:

1. Suojattua yhteyttä varten tarvitsi asentaa Apache2 komennoilla:

```
sudo apt-get update
sudo apt-get install apache2 -y
```
Latauksessa ja asennuksessa kesti tovin.
 
2. Laitettiin seuraavaksi Apache2:sta ssl-moduuli päälle komennolla:
```
sudo a2enmod ssl
```
Komennon antamisen jälkeen painoimme Enter. Moduuli meni päälle.
 
3. Käynnistettiin Apache2 uudelleen komennolla:
```
sudo service apache2 restart
```
 
4. Luodaan uusi sijainti itseallekitjoitetulle sertifikaatille:
```
sudo mkdir /etc/apache2/ssl
```
Komennon antamisen jälkeen painoimme Enter. Uusi sijainti luotiin.
 
5. Itseallekirjoitetun sertifikaatin loimme komennolla:
```
sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /etc/apache2/ssl/apache.key -out /etc/apache2/ssl/apache.crt
```
Mitä komento tekee:

- openssl = CLI työkalu, jolla luodaan ja hallitaan OpenSSL sertifikaatteja, avaimia ja muita tiedostoja.
- req = alikomento, jolla kerrotaan että halutaan käyttää X.509 CSR:ää. X.509 on julkisenavaimen infrastruktuuri standardi, jota
SSL ja TLS noudattavat. Teimme siis uuden X.509 sertin.
- "-x509" = modifioi aikaisempaa alikomentoa kertomalla apuohjelmalle, että halutaan tehdä itsekirjoitettu sertifikaatti sen sijaan että tehtäisiin
sertifikaatin allekirjoitus pyyntö.
- "-nodes" = Kertoo OpenSSL:lle että se voi ohittaa sertifikaatin suojauksen tunnuslauseen. Apachen pitää pystyä
lukemaan tiedosto ilman, että käyttäjä puuttuu siihen silloin kun palvelin käynnistyy. Tunnuslause (passphrase)
estäisi tämän toteutumisen, koska meidän pitäisi aina syöttää se jokaisen uudelleenkäynnistyksen yhteydessä.
- "-days 365" = Tämä asettaa sertifikaatin voimassaolo ajan 365 päiväksi.
- "-newkey rsa:2048" =Tällä määritellään uuden sertifikaatin ja avaimen luonti samaan aikaan. Rsa:2048 kertoo että pitää
tehdä RSA avain, joka on 2048 bittiä pitkä.
- "-keyout" = Kertoo OpenSSL:lle minne luotu yksityinen avaintiedosto pistetään.
- "-out" = Kertoo OpenSSL:lle minne sertifikaatti pistetään.

Komentoon piti luoda tiedot meistä:
```
Country Name (2 letter code) [AU]:FI
State or Province Name (full name) [Some-State]:Uusimaa
Locality Name (eg, city) []:Helsinki
Organization Name (eg, company) [Internet Widgits Pty Ltd]:Pisnismiehet
Organizational Unit Name (eg, section) []:Projectgroup
Common Name (e.g. server FQDN or YOUR name) []:*palvelimen IP-osoite*
Email Address []:jan.parttimaa@myy.haaga-helia.fi
```
 
6. Siirryimme root -käyttäjäksi komennolla:
```
sudo su
```
 
7. Käänteistä välityspalvelinta varten joudumme sallimaan neljän eri moduulin käytön. Nämä sallimme komennoilla:
```
sudo a2enmod proxy
sudo a2enmod proxy_http
sudo a2enmod proxy_balancer
sudo a2enmod lbmethod_byrequests
```
 
8. Käynnistimme taas Apache2:sen uudelleen:
```
sudo systemctl restart apache2
```
9. Avasimme seuraavan tiedoston komennolla:
```
sudo nano /etc/apache2/sites-available/default-ssl.conf
```
Tiedosto avautui Nano- ohjelmassa.
 
10. Muutimme "default-ssl.conf" -tiedostosta seuraavat kohdat:
```
ServerAdmin jan.parttimaa@myy.haaga-helia.fi
# ServerName 172.28.175.26
DocumentRoot /var/www/html

#   SSL Engine Switch:
#   Enable/Disable SSL for this virtual host.
SSLEngine on

#   A self-signed (snakeoil) certificate can be created by installing
#   the ssl-cert package. See
#   /usr/share/doc/apache2/README.Debian.gz for more info.
#   If both key and certificate are stored in the same file, only the
#   SSLCertificateFile directive is needed.
SSLCertificateFile      /etc/apache2/ssl/apache.crt
SSLCertificateKeyFile /etc/apache2/ssl/apache.key

```
Tallensimme ja suljimme lopuksi tiedoston.
 
11. Avasimme tämän jälkeen seuraavan tiedoston:
```
sudoedit /etc/apache2/sites-available/000-default.conf
```
Tiedosto avautui myös Nano -ohjelmaan.
 
12. Muutimme "000-default.conf" -tiedostosta seuraavat kohdat:
```
ServerName http://172.28.175.26
Redirect /secure https://172.28.175.26/phpvirtualbox
Redirect permanent / https://172.28.175.26/phpvirtualbox

# ServerAdmin webmaster@localhost
# DocumentRoot /var/www/html
```
Tallensimme ja suljimme lopuksi tiedoston.
 
13. Aktivoimme Apachen SSL Virtuaalihostin komennolla:
```
sudo a2ensite default-ssl.conf
```
 
14. Käynnistimme lopuksi Apachen uudelleen komennolla:
```
sudo service apache2 restart
```

Tällöin tuli herja siitä, että sertifikaatti ei ole luotettava. Tämä johtuu siitä, koska sertifikaatti on itse allekirjoitettu eikä hankittu valtuutetulta taholta. Ohitin herjan Chromessa vain klikkaamalla Advanced ja ``` Proceed to https://*palvelimen IP-osoite*```
 
![https Chrome](https://raw.githubusercontent.com/Eetu95/Open-source-IdM-solution/master/Kuvat/chrome_https.PNG)
<br>
Kuva 61: Sertifikaattivaroitus (Chrome)
<br>
<br>
 
<br>
 
<h4 id="testityoasemien-seka-testipalvelimen-asennus-ja-konfigurointi">4.1.4. Testityöasemien sekä testipalvelimen asennus ja konfigurointi</h4>
 
Seuraavaksi aloimme asentelemaan ja konfiguroimaan testityöasemia ja palvelimia VirtualBox-palvelimelle.

<h5 id="windows-10-testipc1">4.1.4.1. Windows 10 (TESTIPC1)</h5>
 
Testityöasemia käytimme meidän omassa VirtualBox-palvelimessa. Latasimme Windows 10 virtuaalikoneen <a href="modern.ie"> modern.ie sivustolta</a>, joka toimii 90 päivän lisenssillä. Kyseinen virtuaalikone toimii testityöasemana ja on nimeltään "TESTIPC1".

Kirjauduimme SSH-yhteydellä VirtualBox_palvelimeen (VMSERVER) ja kirjaudumme sisään tunnuksilla, jotka teimme VMSERVERI:n asennuksen yhteydessä
2. Latasimme TESTIPC1:sen modern.ie -sivulta komennolla:
 
    wget https://az792536.vo.msecnd.net/vms/VMBuild_20180425/VirtualBox/MSEdge/MSEdge.Win10.VirtualBox.zip

Komennon jälkeen painoimme Enter. Virtuaalikonetta alettiin lataamaan ja siinä kesti tovin.

3. Purkasimme kansion kotihakemistoon komennolla:
    ```
    unzip MSEdge.Win10.VirtualBox.zip
    ```
4. Siirryimme seuraavaksi root- käyttäjäksi komennolla:
    ```
    sudo su
    ```
5. Siirsimme virtuaalikoneen imagen ```vbox``` käyttäjän kotihakemistoon komennolla:
    ```
    mv 'MSEdge - Win10.ova' /home/vbox/
    ```
    Komennon jälkeen panoimme Enter. Virtuaalikoneen image siirtyi haluttuun sijaintiin. Kirjauduimme lopuksi pois root-käyttäjästä komennolla ```exit```.

6. Kirjauduimme sisään VirtualBoxin web-käyttöliittymään ja valitsimme valikosta ```File -> Import Appliance... ``` Klikkattiin  avautuvasta ikkunasta kansion kuvaa
 
![](https://raw.githubusercontent.com/Eetu95/Open-source-IdM-solution/master/Kuvat/phpvirtualboximport.JPG)
<br>
Kuva 62: Virtuaalikoneen ohjattu tuonti.
<br>
<br>

 
ja haimme virtuaalikoneen imagen ````vbox```` käyttäjän kotihakemistosta. Lopuksi painoimme ```OK```. 

![](https://raw.githubusercontent.com/Eetu95/Open-source-IdM-solution/master/Kuvat/phpvirtualboxselect.JPG)
<br>
Kuva 63: Virtuaalikoneen valinta.
<br>
<br>
     
Valtsimme se jälkeen ```Next >>``` ja katsoimme onko avautuvasta ikkunasta onko virtuaalikoneen asetukset ok. Muutimme nimeksi "TESTIPC1" ja laitoimme täpän kohtaan "Reinitialize the MAC address of all network cards". Lopuksi painoimme ```Import```. Testikone oli tuotu VirtualBox-palvelimelle onnistuneesti. Tämän jälkeen muutimme virtuaalikoneesta verkkokortin siltaavaksi, jotta se näkyy lähiverkossa muiden laitteiden joukossa. Teimme sen klikkaamalla hiiren oikealla virtuaalikonetta ja valitsemalla ```Settings -> Network -> Adapter 1```  ja drop-down valikosta valitsemalla "Bridged Adapter". 
 Tämän jälkeen sallimme etäyhteyden virtuaalikoneeseen. Valitsimme auki olevista asetuksista ```Display -> Remote Display``` Porttinumeroksi laitoimme 9000. Hyväksyimme muutoksen painamalla OK. Käynnistimme virtuaalikoneen klikkaamalla hiiren oikealla virtuaalikonetta ja valitsemalla ```Start```.
 TESTIPC1 oli päällä. Seuraavaksi teimme siihen seuraavat määritykset:
<ul>
    <li>IPv6 pois päältä</li>
    <li>IPv4 verkkokorttiin DNS osoitteeksi Windows palvelimen IP-osoite</li>
    <li>Network Discovery päälle</li>
    <li>Etäyhteyden salliminen</li>
    <li>Tietokoneen nimen muuttaminen (TESTIPC1)</li>
</ul>

Tämän jälkeen liitettiin Windows testityöasema domainiin: 
```
Control Panel -> System and Security -> System -> Change settings -> Change
```
Valittiin täppä, että liitetään domainiin ja kirjoitettiin domain nimi. Seuraavaksi kysyttiin domainin Admin käyttäjän tunnuksia. Kirjoitettiin ne ja domainin liitos onnistui. Virtuaalikone kirjautui ulos ja takaisin. Virtuaalikoneesta nyt näki, että kone on liitoksissa domainiin esimerkiksi System asetuksista.

Testattiin seuraavaksi, että Active Directory toimii. Windows palvelimella loimme uuden käyttäjän Active Directoryyn:
```
Start - Windows Administrative Tools - Active Directory Users and Computers - pisnismiehet.local - Users - New - User
```
Käyttäjän luonti-ikkunaan kirjoitimme käyttäjätunnuksen ja tietoja käyttäjästä sekä luotiin käyttäjälle salasana. Tämän jälkeen kun käyttäjä oli luotu niin testattiin kirjautua käyttäjälle testityöasemaa käyttäen. Kirjautuminen onnistui ja varmistuttiin siitä, että testityöasema on liitoksissa domainiin.
 
<br>
 
<h5 id="ubuntu-desktop-18041-lts-testipc2">4.1.4.2. Ubuntu Desktop 18.04.1 LTS (TESTIPC2)</h5>
 
Linux-ympäristöä varten tarvitsimme Linux-käyttöjärjestelmällä varustetun koneen. Aiomme myös myöhemmin liittää tämän testityöaseman OpenLDAP-palvelimen piiriin. Päätimme valita testiä varten Ubuntu Desktop 18.04.1 LTS 64-bittisen version. Samalla tavoin lisäsimme tämän testityöaseman VirtualBoxiinVirtualBox -palvelimeen (VMSERVER). Ladattiin tätä varten .ISO tiedosto netistä: (Komentokehotteessa saa sen helposti ladattua komennolla ```wget http://releases.ubuntu.com/18.04.1/ubuntu-18.04.1-desktop-amd64.iso```). Levykuvan siirto ```vbox``` käyttäjän kotihakemistoon tapahtuu samalla tavalla miten edellisessä kappaleessa tehtiin. VMSERVERillä loimme virtuaalikoneen:

- Tyyppi: Linux
- Versio: Ubuntu (64-bit)
- RAM-muistia: 2048 MB
- Hard disk: Create a virtual hard disk now
- Hard disk tyyppi: VDI | Dynamically allocated
- Kiintolevyn koko: 50 GB

Tämän jälkeen muokkasimme virtuaalikoneen asetuksia: Settings -> Storage -> Empty -> levyn kohdasta valittiin Choose Virtual Optical Disk File... ja lisättiin .ISO tiedosto tähän ```vbox``` käyttäjän kotihakemistosta (```/home/vbox)```. Tämän jälkeen laitettiin vielä verkkokortti siltaavaksi. Nyt virtuaalikone oli valmis asennettavaksi. Käynnistettiin virtuaalikone. 

Ensimmäiseksi aukesi asennusruutu:

![Ubuntu Desktop asennus](https://raw.githubusercontent.com/Eetu95/Open-source-IdM-solution/master/Kuvat/Ubuntu%20Desktop/Screenshot%20(1).png)
<br>
Kuva 64: Ubuntu Desktop asennus.
<br>
<br>
Valittiin käyttöjärjestelmän kieliksi English (1.) ja klikattiin "Install Ubuntu" (2.).

![Näppäimistön layout](https://raw.githubusercontent.com/Eetu95/Open-source-IdM-solution/master/Kuvat/Ubuntu%20Desktop/Screenshot%20(2).png)
<br>
Kuva 65: Näppäimistön valinta.
<br>
<br>

Seuraavaksi kysyttiin näppäimistön kieliasetuksia. Valittiin "Finnish" (1. ja 2.) ja klikattiin "Continue" (3.).

![Asennus tyyppi 1/2](https://raw.githubusercontent.com/Eetu95/Open-source-IdM-solution/master/Kuvat/Ubuntu%20Desktop/Screenshot%20(3).png)
<br>
Kuva 66: Asennus tyyppi (1/2).
<br>
<br>

Seuraavaksi kysyttiin halutaanko tehdä normaali asennus vai minimaalinen asennus. Koska emme halunneet mitään ylimääräistä asennettavan, valitsimme minimaalisen asennuksen (1.). Halusimme myös asentaa tarvittavat päivitykset (2.) sekä kolmannen osapuolen välttämättömät ohjelmat (3.). Jatkoimme eteenpäin klikkaamalla "Continue" (4.).

![Asennus tyyppi 2/2](https://raw.githubusercontent.com/Eetu95/Open-source-IdM-solution/master/Kuvat/Ubuntu%20Desktop/Screenshot%20(4).png)
<br>
Kuva 67: Asennus tyyppi (2/2).
<br>
<br>

Asennustyypiksi valittiin ensimmäinen vaihtoehto eli tyhjennetään koko kiintolevy ja asennetaan siihen Ubuntu (1.). Aloitimme asennuksen painamalla "Install Now" (2.).

![Varmistus](https://raw.githubusercontent.com/Eetu95/Open-source-IdM-solution/master/Kuvat/Ubuntu%20Desktop/Screenshot%20(5).png)
<br>
Kuva 68: Varmistus.
<br>
<br>

Hyväksyttiin tehtävät muutokset kiintolevylle painamalla "Continue" (1.).

![Sijainti](https://raw.githubusercontent.com/Eetu95/Open-source-IdM-solution/master/Kuvat/Ubuntu%20Desktop/Screenshot%20(6).png)
<br>
Kuva 69: Sijainti.
<br>
<br>

Sijainniksi valittiin "Helsinki" (1.) ja mentiin eteenpäin valitsemalla "Continue" (2.).

![käyttäjän luominen](https://raw.githubusercontent.com/Eetu95/Open-source-IdM-solution/master/Kuvat/Ubuntu%20Desktop/Screenshot%20(7).png)
<br>
Kuva 70: Käyttäjän luominen.
<br>
<br>

Seuraavaksi kysyttiin tietokoneen nimeä, käyttäjätunnusta ja salasanaa. Kirjoitimme nämä (1.) ja klikattiin Continue (2.).

![Ubuntu Desktop asennus](https://raw.githubusercontent.com/Eetu95/Open-source-IdM-solution/master/Kuvat/Ubuntu%20Desktop/Screenshot%20(8).png)
<br>
Kuva 71: Ubuntu Desktop asennus.
<br>
<br>

Ubuntu Desktop lähti asentumaan.

![asennus valmis](https://raw.githubusercontent.com/Eetu95/Open-source-IdM-solution/master/Kuvat/Ubuntu%20Desktop/Screenshot%20(9).png)
<br>
Kuva 72: Asennus valmis.
<br>
<br>

Asennus tuli valmiiksi ja virtuaalikone piti käynnistää uudelleen. Klikattiin Restart Now. Tämän jälkeen kirjauduimme työasemalle sisälle samoilla tunnuksilla, jotka teimme asennusvaiheessa. Avasimme tämän jälkeen Terminaalin (Ctrl+Alt+T). Asensimme tämän jälkeen ainoastaan SSH:n sekä laitoimme palomuurin päälle komennolla: ```sudo apt update && sudo apt-get install -y ssh && sudo ufw enable```

Seuraavaksi halusimme piilottaa käyttäjälistauksen, joka näkyy kirjautumisruudussa. Teimme sen seuraavanlaisesti:

1. Teemme ```gdm``` -tiedoston sijaintiin ```/etc/dconf/profile/``` komennolla:
    ```
    sudoedit /etc/dconf/profile/gdm
    ```
    Komennon jälkeen painoimme Enter. Kyseinen tiedosto avautui "Nano" -ohjelmaan. Laitoimme kyseiseen tiedostoon seuraavaa:
    ```
    user-db:user
    system-db:gdm
    file-db:/usr/share/gdm/greeter-dconf-defaults
    ```
    Suljimme ja tallensimme lopuksi tiedoston.

2. Avasimme seuraavaksi ```00-login-screen``` -tiedoston komennolla:
    ```
    sudoedit /etc/dconf/db/gdm.d/00-login-screen
    ```
    Komennon jälkeen painoimme Enter. Kyseinen tiedosto avautui myös "Nano" -ohjelmaan. Laitoimme tähän tiedostoon seuraavaa:
    ```
    [org/gnome/login-screen]
    # Do not show the user list
    disable-user-list=true
    ```
    Suljimme ja tallensimme lopuksi tiedoston.
 
3. Lopuksi päivitimme tehdyt muutokset komennolla:
    ```
    dconf update
    ```
    Komennon jälkeen painoimme Enter. Muutokset päivitetty ja käyttäjälistaus ei enää näy työaseman käynnistyessä.
 
<br>

Seuraavaksi aloimme liittämään työasemaan OpenLDAP -palvelimeen. Teimme tämän seuraavanlaisesti:
 
1. Avasimme ensiksi ````hosts````-tiedoston komennolla:
    ```
    sudoedit /etc/hosts
    ```
    Komennon jälkeen painoimme Enter. Tiedosto avautui. Lisäsimme riville numero 3 OpenLDAP -palvelimemme DNS-tiedot eli ip-osoite ja kirjallinen osoite mukaan lukien aliakset:
    ```
    172.28.171.15   ldap.pisnismiehet.local ldap
    ```
    Tallensimme ja suljimme lopuksi tiedoston.
 
2. Avasimme palomuurista porttinumerot 389 ja 636 komennolla:
    ```
    sudo ufw allow 389/tcp && sudo ufw allow 389 && sudo ufw allow 636/tcp && sudo ufw allow 636
    ```
    Komennon jälkeen painoimme Enter. Kyseiset portit avattiin.
 
3. Asensimme LDAP Clientin komennolla:
    ```
    sudo apt update && sudo apt-get install -y libnss-ldap libpam-ldap ldap-utils nscd
    ```
    Komennon jälkeen painoimme Enter. Jonkin ajan kulttua tuli ohjattu asennus, johon laitoimme seuraavat määritykset:
     
    - LDAP server Uniform Resource Identifier: ldap://<ldap-palvelimen ip-osoite>
    - Distinguished name of the search base: dc=ldap,dc=pisnismiehet,dc=local
    - LDAP version to use: 3
    - Make local root Database admin: Yes
    - Does the LDAP database require login: No
    - LDAP account for root: cn=admin,dc=ldap,dc=pisnismiehet,dc=local
    - LDAP root account password: <admin/root käyttäjän salasana>
 
4. Avattiin tiedosto ```nsswitch.conf``` komennolla:
    ```
    sudoedit /etc/nsswitch.conf
    ```
    Komennon jälkeen painoimme Enter. Tiedosto avautui "Nano" -ohjelmassa. Muutimme tiedossa olevat tiedot seuraavanlaisiksi:
    ```
    # /etc/nsswitch.conf
    #
    # Example configuration of GNU Name Service Switch functionality.
    # If you have the `glibc-doc-reference' and `info' packages installed, try:
    # `info libc "Name Service Switch"' for information about this file.

    passwd:         files systemd ldap
    # passwd: files ldap
    group:          files systemd ldap
    # group: files ldap
    shadow:         files ldap
    # shadow: files ldap
    gshadow:        files

    #hosts:          files mdns4_minimal [NOTFOUND=return] dns myhostname
    hosts:          files dns ldap
    networks:       files ldap

    protocols:      db files
    services:       db files
    ethers:         db files
    rpc:            db files

    # pre_auth-client-config # netgroup:       nis
    netgroup: nis
    ```
    Tallensimme ja suljimme lopuksi tiedoston.
 
5. Seuraavaksi avasimme ```common-session``` -tiedoston komennolla:
    ```
    sudoedit /etc/pam.d/common-session
    ```
    Komennon jälkeen painoimme Enter. Tiedosto avautui Nano -ohjelmaan. Varmistimme, että tiedoston lopussa on seuraavat tiedot, jotka huolehtivat muun muassa LDAP-käyttäjien kotihakemistojen luonnin automaattisesti:
    ```
    # and here are more per-package modules (the "Additional" block)
    session required        pam_unix.so
    session required        pam_mkhomedir.so umask=0022 skel=/etc/skel
    session optional        pam_ldap.so
    session optional        pam_systemd.so
    ```
    Tallensimme ja suljimme lopuksi tiedoston.
 
6. Avasimme seuraavaksi ```ldap.conf``` -tiedoston komennolla:
    ```
    sudoedit /etc/ldap.conf
    ```
    Komennon jälkeen painoimme Enter. Tiedosto avautui myös Nano-ohjelmassa. Muutimme tiedostosta seuraavat arvot:
    ```
    pam_password md5
    nss_base_group          ou=unixgroups,dc=ldap,dc=pisnismiehet,dc=local?sub
    ssl start_tls
    ```

    Tallensimme ja suljimme lopuksi tiedoston. Seuraavaksi avasimme saman nimisen tiedoston mutta eri sijainnista komennolla:
    ```
    sudoedit /etc/ldap/ldap.conf
    ```
    Komennon jälkeen painoimme Enter. Tiedosto avautui myös Nano -ohjelmaan, johon muutimme sekä lisäsimme seuraavat tiedot:
    ```
    BASE    dc=ldap,dc=pisnismiehet,dc=local
    URI     ldap://172.28.171.15/
    TLS_CACERT      /etc/ldap/ca_certs.pem
    TLS_REQCERT     allow
    ```
    Tallensimme ja suljimme lopuksi tiedoston.
 
<br>
 
Lopuksi siirsimme LDAP-palvelimen SSH-avaimet testityöasemaan seuraavanlaisesti:
 
1. Kirjauduimme SSH-yhteydellä LDAP-palvelimelle.
 
2. Aloitettiin SSH-agentti komennolla:
    ```
    sudo eval $(ssh-agent)
    ```
 
3. Lisäsimme SSH-avaimet agentille komennolla:
    ```
    ssh-add
    ```
 
4. Otimme seuraavaksi SSH-yhteyden TESTIPC2 -testityöasemaan komennolla:
    ```
    sudo ssh -A user@<TESTIPC2-ip-osoite>
    ```
 
5. Kopioitiin avaimet testityöasemalle komennolla:
    ```
    scp pisnismiehet@<TESTIPC2-ip-osoite>:/etc/ssl/certs/ca_server.pem ~/
    cat ~/ca_server.pem | sudo tee -a /etc/ldap/ca_certs.pem
    ```
 
6. Suljettiin SSH-yhteys testityöasemaan.
 
<br>
 
Lopuksi kokeilimme toimiiko yhteys TESTIPC2:sen ja OpenLDAP-palvelimen välillä komennolla:

```
ldapwhoami -H ldap://ldap.pisnismiehet.local -x -ZZ
```
Tulokseksi tuli ```anonymous```. Yhteys siis toimii.
 
<br>
 
<h5 id="ubuntu-server-16045-lts-testipalvelin">4.1.4.3. Ubuntu Server 16.04.5 LTS</h5>

Asensimme testipalvelimen myös VirtualBox -palvelimelle (VMSERVER). Testipalvelimen asennusprosessi on muuten sama kuin fyysisen palvelimen kanssa, mutta ero on ainoastaan se, että testipalvelin on VirtualBox -palvelimella. Käyttöjärjestelmä oli sama kuin fyysisellä tietokoneella: Ubuntu Server 16.04.5 LTS 64-bit. Asetimme myös tässäkin verkkokortin siltaavaksi kuten myös muiden testikoneiden osalta.
 
<br>
 
<h3 id="asennus">4.2. Asennus</h3>

1. Asennettiin openjdk8:
    ```
    sudo apt-get -y install openjdk-8-jdk
    ```
2. Asennettiin openjre8:
    ```
    sudo apt-get -y install openjdk-8-jre
    ```

3. Mentiin kansioon /opt:
    ```
    cd /opt
    ```

4. Ladattiin midpoint 3.8 (watt) midPointin sivuilta:
 
    ![midPoint 3.8 (Watt) - Download](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/midPoint/midPoint%203.8%20(Watt)%20-%20Download.PNG?raw=true)
    <br>
    Kuva 73: Ruudunkaappaus midPointin sivuilta.
    <br>
    <br>
 
    ```
    sudo wget https://evolveum.com/downloads/midpoint/3.8/midpoint-3.8-dist.tar.gz
    ```
     
5. Purettiin ladattu tervapallo (midpoint-3.8-dist.tar.gz):
    ```
    sudo tar -xvzf midpoint-3.8-dist.tar.gz
    ```
6. Vaihettiin kansio midpoint-3.8-dist kansioksi midpoint:
    ```
    mv /opt/midpoint-3.8-dist /opt/midpoint
    ```
7. Laitettiin midpoint <a href="https://wiki.evolveum.com/display/midPoint/Running+midPoint+with+systemd">käynnistymään palvelimen käynnistymisen yhteydessä automaattisesti</a>.
 Tehtiin uusi tiedosto /etc/systemd/system/midpoint.service,jonne laitettiin tämä sisältö:
    ```
    midpoint.service
    [Unit]
    Description=MidPoint Standalone Service
    ###Requires=postgresql.service
    ###After=postgresql.service
    [Service]
    User=root
    WorkingDirectory=/opt/midpoint
    ExecStart=/usr/bin/java -Xmx2048m -Dmidpoint.home=/opt/midpoint/var -jar /opt/midpoint/lib/midpoint.war
    SuccessExitStatus=143
    ###TimeoutStopSec=120s
    [Install]
    WantedBy=multi-user.target
    ```
8. Laitettiin midPoint palvelu päälle:
    ```
    sudo systemctl daemon-reload
    sudo systemctl enable midpoint
    ```

9. Laitettiin midPoint systemd palveluksi:
    ```
    sudo systemctl start midpoint
    ```

10. Sitten käynnistettiin palvelin uudelleen:
    ```
    sudo reboot
    ```
 

Tämän jälkeen midPoint oli asennettu.
 
<br>
 

<h3 id="konfigurointi">4.3. Konfigurointi</h3>
 
Seuraavaksi aloimme konfiguroimaan midPointtia käyttövalmiiksi.
 
<br>
 
<h4 id="tietokannan-maarittaminen">4.3.1. Tietokannan määrittäminen</h4>
 
Päätimme liittää fyysiselle midPoint palvelimellemme MariaDB tietokannan. Kokeilimme aluksi liittämistä virtuaalitestipalvelimella, jonka jälkeen liitimme sen fyysiselle palvelimelle. MidPointissa tulee mukana sulautettu tietokanta H2, jota suositellaan käytettävän vain testaukseen. Tästä syystä päätimme valita MariaDB tietokannan, sillä osaamme jo muutenkin hieman MySQL:ää. Toinen vaihtoehto olisi ollut PostgreSQL, mutta päädyimme MariDB:seen edellä mainitusta syystä. 
Aluksi palvelimelle tulee asentaa MariaDB:
```
$ sudo apt-get install -y mariadb-server
```
Asennuksen jälkeen kirjauduttiin MariaDB:seen root käyttäjällä:
```
$ sudo mysql -u root
```
Seuraavaksi luotiin tietokannan nimeltä midpoint:
```
CREATE DATABASE midpoint CHARACTER SET utf8 DEFAULT CHARACTER SET utf8 COLLATE utf8_bin DEFAULT COLLATE utf8_bin;
```
Luotiin käyttäjä midpoint ja asetettiin salasana:
```
GRANT ALL on midpoint.* TO ’midpoint’@’localhost’;
```
Testattiin, että tietokanta on luotu:
```
use midpoint;
```
Poistuttiin tietokannasta komennolla exit. Seuraavaksi muokkattiin config.xml tiedostoa, johon konfiguraatiomuutokset tehdään. Config.xml asentui midPoint asennuksen aikana ja se löytyy midPointin kotikansiosta (meillä se löytyy polusta /opt/midpoint/var).
```
$ sudoedit /opt/midpoint/var/config.xml
```
Lisättiin config.xml tiedostoon seuraavat rivit repositoryn kohdalle, jotka löytyivät midPointin MariaDB dokumentaatiosta:
```
<database>mariadb</database>
<jdbcUsername>midpoint</jdbcUsername>
<jdbcPassword>************</jdbcPassword>
<jdbcUrl>jdbc:mariadb://localhost:3306/midpoint?characterEncoding=utf8</jdbcUrl><!– it seems that jdbc://mysql works as well –>
```
![config.xml mariadb](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/midPoint/mariadb.png?raw=true)
<br>
Kuva 74: Ruudunkaappaus xml-tiedostosta.
<br>
<br>
Tallennettiin tiedoston muokkaukset. Seuraavaksi ajettiin SQL scriptti, jotta MariaDB yhdistyy midPoint palvelimelle:
```
$ cd /opt/midpoint/doc/config/sql/_all
$ sudo mysql -u root midpoint < mysql-3.8-all.sql
```
SQL-scriptin ajossa kesti noin viisi minuuttia. Seuravaaksi lisättiin palomuurisäännön 3306-portille, jota käytetään tietokannan liittämiseen.
```
$ sudo ufw allow 3306
$ sudo ufw allow 3306/tcp
```
Tämän jälkeen käynnistettiin koneen uudelleen:
```
$ sudo reboot
```
Käynnistyksen jälkeen midPoint toimii selaimella: ”IP-osoite”:8080/midpoint
Kirjauduttiin sisään ja tarkistettiin, että MariaDB on yhdistynyt midPoint palvelimeen. Sen pystyi tarkistaa kohdasta About.
![midPoint tietoja](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/midPoint/midPoint_about.png?raw=true)
<br>
Kuva 75: Ruudunkaappaus midPointin -käyttöliittymästä.
<br>
<br>
Repository URL kohdasta nähdään, mitä tietokantaa midPoint käyttää. MariaDB:n liittäminen midPointiin onnistui.
Luotiin seuraavaksi jokaiselle meidän projektiryhmän jäsenelle käyttäjä midPoint käyttöliittymästä: Users – New user.
Tarkistettiin seuraavaksi, että käyttäjät ovat todella tallentuneet MariaDB:n tietokantaan:
```
$ sudo mysql -u root
use midpoint;
SHOW TABLES;
SELECT * FROM m_user;
SELECT fullName_norm,oid FROM m_user;
```
![MariaDB käyttäjät](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/midPoint/mariadb_k%C3%A4ytt%C3%A4j%C3%A4t.png?raw=true)
<br>
Kuva 76: Kuvankaappaus MariaDB:n käyttäjistä.
<br>
<br>
Käyttäjien lisäys onnistui ja ne löytyvät MariaDB tietokannasta.
 
<br>
 
<h4 id="connectoreiden-maarittaminen">4.3.2. Connectoreiden määrittäminen</h4>
 
Jotta yrityksen järjestelmä voidaan tuoda IdM:n piirii, pitää se lisätä käyttämällä välikappaletta (Englanniksi: Connector). Välikappale (tai kuten viittaamme myöhemmin sanalla connector) ei ole fyysinen vaan koodattu pikku ohjelma. Seuraavassa kohdassa kerromme, kuinka lisäsimme TESTIPALVELIN, OPENLDAPSERVER sekä WINDOWSSERVER midPointin piiriin. Liitimme TESTIPALVELIN -palvelimen käyttämällä Unix-connectoria, OPENLDAPSERVERin sekä WINDOWSSERVERin käyttämällä LDAP-connectoria.
 
<br>

<h5 id="active-directory-connector">4.3.2.1. Active Directory connector</h5>

Active Directory connectorin avulla saadaan yhdistettyä midPoint Windows -käyttöjärjestelmän koneisiin. Active Directory connectoria varten tulee olla määritetty Windows Server, jossa on asennettuna Active Directory Domain services eli aktiivihakemisto. Active Directory asennus tehtiin jo Windows Serverin [esivalmisteluvaiheessa](#windows-palvelimen-perusmaaritykset). MidPointissa Active Directory connector oli jo valmiina asennettuna toisin kuin esimerkiksi Unix connectorissa. Ennen Active Directory connectorin toimivuutta tuli varmistaa, että Windows Serverin LDAP yhteys on suojattu. LDAP protokollaa käytetään Active Directoryn tiedonsiirroissa, josta suojattu protokolla on LDAPS. LDAP toimii portissa 389 ja LDAPS portissa 636. LDAPS suojasta varten pitää asentaa konfiguroida Active Directory Lightweight Directory Services (AD LDS) sekä luoda sertifikaatti Certification Authority roolin avulla. 

<h5>Active Directory Lightweight Directory Services asennus</h5>

Server Managerista valitaan Manage - Add Roles and Features.
![roles & features](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Windows%20Server/AD%20LDS/Capture.PNG?raw=true)
<br>
Kuva 77: Roles & Features.
<br>
<br>

Klikattiin Next.

![role-based or feature-based](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Windows%20Server/AD%20LDS/Capture1.PNG?raw=true)
<br>
Kuva 78: Role-based or Feature-based
<br>
<br>
Valittiin Role-based or feature-based installation. Klikattiin Next.

![palvelimen valinta](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Windows%20Server/AD%20LDS/Capture2.PNG?raw=true)
<br>
Kuva 79: Palvelimen valinta.
<br>
<br>

Valitaan mäidän palvelimen (meillä ei ole kuin yksi Windows palvelin). Klikattiin Next.

![AD LDS](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Windows%20Server/AD%20LDS/Capture3.PNG?raw=true)
<br>
Kuva 80: AD LDS.
<br>
<br>

Seuraavaksi valittiin asennettavaksi Active Directory Lightweight Services (kuvassa se oli jo asennettu). Klikattiin Next.

![ominaisuudet](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Windows%20Server/AD%20LDS/Capture4.PNG?raw=true)
<br>
Kuva 81: Ominaisuudet.
<br>
<br>

Ei valittu mitään ominaisuuksia. Klikattiin Next. 
![AD LDS ilmoitus](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Windows%20Server/AD%20LDS/Capture5.PNG?raw=true)
<br>
Kuva 82: AD LDS ilmoitus.
<br>
<br>

Seuraavaksi tuli ilmoitus siitä, mitä ollaan asentamassa. Klikattiin Next.

![vahvistus](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Windows%20Server/AD%20LDS/Capture6.PNG?raw=true)
<br>
Kuva 83: Vahvistus.
<br>
<br>

Seuraavaksi tuli vahvistus asennettavasta roolista. Klikattiin Install. 

![asennus valmis](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Windows%20Server/AD%20LDS/Capture7.PNG?raw=true)
<br>
Kuva 84: Asennus valmis.
<br>
<br>

Asennuksen jälkeen lähdettiin konfiguroimaan AD LDS roolia. Klikattiin Run the Active Directory Lightweight Directory Services Setup Wizard.

![AD LDS wizard](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Windows%20Server/AD%20LDS/Capture8.PNG?raw=true)
<br>
Kuva 85: AD LDS wizard.
<br>
<br>

Aukesi AD LDS konfigurointi-ikkuna. Klikattiin Next. 

![instanssi](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Windows%20Server/AD%20LDS/Capture9.PNG?raw=true)
<br>
Kuva 86: Instanssi.
<br>
<br>

Valittin instansiksi unique instance. Klikattiin Next.

Seuraavaksi piti määrittää instanssin nimi. Valittiin nimeksi PISNISMIEHET. Description kohtaan kirjoitettiin AD LDS instance. Klikattiin sitten Next.

Seuraavaksi piti määritellä LDAP ja LDAPS portit. Valittiin oletukset 50000 ja 50001, koska oletusportit 389 & 636 ovat jo tulleet käytöön Active Directoryn asennuksen jälkeen. Klikattiin Next.

Seuraavaksi piti määritellä Application Directory Partition. Valittiin uusi osiointi: Yes, create an application directory partition. Kirjoitetiin tähän CN=Midpoint,DC=PISNISMIEHET,DC=LOCAL
Klikattiin sitten Next.

Seuraavaksi kysyttiin mihin AD LDS data tallennetaan. Jätettiin oletukset ja klikattiin Next. 

![AD LDS palvelun käyttäjä](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Windows%20Server/AD%20LDS/Capture10.PNG?raw=true)
<br>
Kuva 87: AD LDS palvelun käyttäjä.
<br>
<br>

Seuraavaksi piti valitan käyttäjä AD LDS palveluun. Valittiin Network Service account ja klikattiin Next. Tuli varoitus vielä datan replikoinnista. Klikattiin vain Yes.

Seuraavaksi piti määritellä administrator käyttäjä AD LDS palvelulle. Valittin nykyinen kirjautunut käyttäjä. Klikattiin Next.

Seuraavaksi kysyttiin LDIF tiedostoja. Valittiin kaikki ja klikattiin Next. 

![LDIF tiedostojen vahvistus](https://github.com/Eetu95/Open-source-IdM-solution)
<br>
Kuva 88: LDIF -tiedtostojen vahvistus.
<br>
<br>

Seuraavaksi tuli vahvistus tiedostoista. Klikattiin Next.

![AD LDS konfigurointi valmis](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Windows%20Server/AD%20LDS/Capture12.PNG?raw=true)
<br>
Kuva 89: AD LDS konfigurointi valmis.
<br>
<br>

AD LDS konfigurointi oli nyt valmis. Klikattiin Finish.

Seuraavaksi kokeilimme AD LDS instanssiin. Avattiin ADSI Edit:
```
Start - Windows Administrative Tools - ADSI Edit
```

Klikkasimme sovelluksesta ADSI Edit kansiosta - Connect To...
Lisäsimme tähän seuraavat tiedot ja klikkasimme ok:

![ADSI Edit Connect to](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Windows%20Server/AD%20LDS/Capture13.PNG?raw=true)
<br>
Kuva 90: ADSI Edit Connect to.
<br>
<br>

AD LDS yhdistyi ja tämän jälkeen aukesi puunäkymä instassista.
 
<br>
 
<h5>Certification Authority asennus ja konfigurointi</h5>

Seuraavaksi piti asentaa Certificate Authority rooli, jotta saadaan tehtyä sertifikaatti. Tämä tehtiin samalla kuin AD LDS asennus, mutta valittiin rooliksi Active Directory Certificate Services eikä valittu muita ominaisuuksia. Valittiin Active Directory Certificate Services rooliksi Certification Authority:

![CA](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Windows%20Server/CA/Capture.PNG?raw=true)
<br>
Kuva 91: CA
<br>
<br>

Seuraavaksi asennettiin rooli.

![AD CS asennus valmis](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Windows%20Server/CA/Capture1.PNG?raw=true)
<br>
Kuva 92: AD CS asennus valmis.
<br>
<br>

Asennuksen jälkeen konfiguroimme sertifikaatti palvelun eli klikkasimme configure Active Directory Certificate Services on the destination server. Aukesi konfigurointi wizard. 

Valitsimme oletus tunnukset (credentials) Credentials -välilehdeltä. Klikattiin sitten Next. 

![Role Services](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Windows%20Server/CA/Capture2.png?raw=true)
<br>
Kuva 93: Role Services.
<br>
<br>

Tämän jälkeen Role Services välilehdeltä valittiin Certification Authority.

Seuraavaksi Setup Type välilehdeltä valittiin tyypiksi Enterprise CA, koska tietokone on domainissa ja Active Directory Domain Services on asennettuna. 

![CA tyyppi](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Windows%20Server/CA/Capture4.png?raw=true)
<br>
Kuva 94: CA tyyppi.
<br>
<br>

Seuraavalla välilehdellä eli CA Type valittiin CA tyypiksi Root CA.

![](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Windows%20Server/CA/Capture5.png?raw=true)
<br>
Kuva 95: Root CA.
<br>
<br>

Seuraavaksi piti määritellä avain Private Key välilehdellä. Valitsimme Create a new private key ja klikkasimme Next.

![avaimen kryptaus](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Windows%20Server/CA/Capture6.png?raw=true)
<br>
Kuva 96: Avaimen kryptaus.
<br>
<br>

Seuraavaksi piti määritellä avaimen kryptaus Cryptography välilehdellä. Valitsimme kryptauksen toimittajaksi RSA#Microsoft Software Key Storage Provider, algoritmiksi SHA256 ja pituudeksi 2048.

CA Name välilehdellä valitsimme Distinguished name suffixiksi: CN=Midpoint,DC=PISNISMIEHET,DC=LOCAL

Klikattiin sitten Next.

Validity Period välilehdellä valittiin avaimen voimassaoloajaksi 5 vuotta. Klikattiin sitten Next. 

Certificate Database välilehdeltä valittiin oletustietokannan sijainnit. Klikattiin Next.

Seuraavaksi Confirmation välilehellä hyväksyttiin konfiguraatiot ja klikattiin Configure. Kun konfiguraatio valmistui onnistuneesti, klikkasimme vain Close.
 
<br>

<h5>Sertifikaatin luonti</h5>

Kun CA on nyt asennettu ja konfiguroitu, lähdimme luomaan uuden SSL-sertifikaatin. Kirjoitimme Windowsin hakuun Manage computer certificates ja klikkasimme tätä asetusta.

Seuraavaksi klikkasimme puunäkymästä Personal - Certificates eli menimme tähän kyseiseen kansioon. Täällä näimme, että luotu sertifikaatti on voimassa.

Seuraavaksi varmistetaan, että tietokoneet, jotka ovat Domainissa pääsevät käsiksi luotuun yksityiseen avaimeen. Avattiin komentokehotteen (Command Prompt) admin-oikeuksilla ja kirjoitettiin komentokehotteeseen seuraava komento:

    certutil -verifystore MY

![cmd komento](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Windows%20Server/CA/Capture7.PNG?raw=true)
<br>
Kuva 97: cmd -komento.
<br>
<br>


Tämän saadun tuloksen perusteella mentiin nyt kansioon C:\ProgramData\Microsoft\Crypto\Keys\
Täältä löytyy nyt uusi luotu avain kryptatussa muodossa. Hiiren oikealla painikkeella klikattiin Properties ja välilehdeltä Security lisäsimme Luku ja ajo-oikeudet NETWORK SERVICE ryhmälle:

![oikeudet](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Windows%20Server/CA/Capture8.PNG?raw=true)
<br>
Kuva 98: Oikeudet.
<br>
<br>

Tämän jälkeen menimme takaisin Manage computer certificates asetuksiin. Personal - Certificates kansiosta hiiren oikealla painikkeella klikkasimme meidän sertifikaatin nimeä ja valitsimme All Tasks - Export...

![Export certificate](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Windows%20Server/CA/Capture9.png?raw=true)
<br>
Kuva 99: Export Certificate.
<br>
<br>

Aukesi sertifikaatin vienti-ikkuna. Klikkasimme Next.

![private key](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Windows%20Server/CA/Capture10.png?raw=true)
<br>
Kuva 100: Private Key.
<br>
<br>

Emme exportanneet yksityistä avainta eli valitsimme No, do not export the private key. Klikkasimme Next.

![formaatti](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Windows%20Server/CA/Capture11.png?raw=true)
<br>
Kuva 101: Formaatti.
<br>
<br>

Seuraavaksi piti valita sertifikaatin formaatti. Valitsimme Base-64 encoded X.509 (.CER). Klikkattiin sitten Next.

Tämän jälkeen kysyttiin sijaintia mihin sertifikaatti viedään. Valitsimme tähän työpöydän. Klikattiin sitten Next.

Sertifikaatin vieminen oli nyt valmis. Klikattiin Finish.

Seuraavaksi piti viedä sertifikaatti JRE Keystoreen, joka sijaitsi meidän tapauksessa täällä: ‪C:\Program Files\Java\jre1.8.0_191\bin\keytool.exe

Avasimme komentokehotteen polussa: C:\Program Files\Java\jre1.8.0_191\bin\ ja annoimme komennon:

    keytool -importcert -alias "pisnismiehet" -keystore "C:\Program Files\Java\jre1.8.0_191\lib\security\cacerts" -storepass changeit -file "C:\Users\azureuser\Desktop\pisnismiehet.cer"

Luotimme tähän sertifikaattiin: kirjoitimme "yes", jolloin sertifikaatti lisättiin JRE keystoreen. Nyt voidaan kokeilla LDAPS yhteyttä.

Kirjoitimme Windowsin hakuun ldp.exe. Tällä ohjelmalla voimme testata LDAPS yhteyttä. Klikattiin Connection ja testattiin yhteyttä.

![LDAPS yhteys](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Windows%20Server/CA/Capture12.PNG?raw=true)
<br>
Kuva 102: LDAPS -yhteys.
<br>
<br>

Kirjoitettiin Server kohtaan localhost ja portiksi 636 sekä SSL täppä päälle.

![LDAPS yhteys toimii](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Windows%20Server/CA/Capture13.PNG?raw=true)
<br>
Kuva 103: LDAPS yhteys toimii.
<br>
<br>

Se mitä ldp.exe ohjelma tuottaa tulokseksi viittaa siihen, että yhteys toimi. Jos ei toimisi niin näkyisi virheilmoitus.
 
<br>

<h5>Connectorin lisääminen</h5>

Kun LDAPS yhteys on saatu nyt toimimaan niin voidaan lisätä Active Directory connector midPointiin. Kirjauimme midPoint käyttöliittymään ja menimme kohtaan Import object ja valitsimme Embedded editor.

Seuraavaksi kopioimme midPointin dokumentaatiosta löytyvällä ohjeella seuraavan XLM-tiedoston, joka liittää Active Directory connectorin midPointiin: https://raw.githubusercontent.com/Evolveum/midpoint/master/samples/resources/ad-ldap/ad-ldap-medusa-medium.xml

Kopioimme koko tämän sisällön tiedoston sisällön midPointin GitHubista ja liitimme sen midPoint käyttöliittymään Embedded editor kohtaan.

Kun tiedosto kokonaisuudessaan on liitetty tekstikenttään sitä tulee muokata. Muun muassa <connectorConfiguration> tägien sisään tulee lisätä omat tiedot. Esimerkki:

    <connectorConfiguration xmlns:icfc="http://midpoint.evolveum.com/xml/ns/public/connector/icf-1/connector-schema-3">
        <icfc:configurationProperties xmlns:icfcldap="http://midpoint.evolveum.com/xml/ns/public/connector/icf-1/bundle/com.evolveum.polygon.connector-ldap/com.evolveum.polygon.connector.ldap.ad.AdLdapConnector">
            <icfcldap:host>172.28.171.60</icfcldap:host>
            <icfcldap:port>636</icfcldap:port>
            <icfcldap:baseContext>DC=pisnismiehet,DC=local</icfcldap:baseContext>
            <icfcldap:bindDn>CN=midpoint,CN=Users,DC=pisnismiehet,DC=local</icfcldap:bindDn>
            <icfcldap:connectionSecurity>ssl</icfcldap:connectionSecurity>
            <icfcldap:bindPassword>
                <t:clearValue>********</t:clearValue>
            </icfcldap:bindPassword>
            <icfcldap:pagingBlockSize>5</icfcldap:pagingBlockSize> <!-- ridiculously small, just to test paging -->
        </icfc:configurationProperties>
        <icfc:resultsHandlerConfiguration>
			<icfc:enableNormalizingResultsHandler>false</icfc:enableNormalizingResultsHandler>
			<icfc:enableFilteredResultsHandler>false</icfc:enableFilteredResultsHandler>
			<icfc:enableAttributesToGetSearchResultsHandler>false</icfc:enableAttributesToGetSearchResultsHandler>
		</icfc:resultsHandlerConfiguration>
    </connectorConfiguration>

XML-tiedosto piti tarkistaa vielä kokonaisuudessaan läpi, koska XML tiedostoon pitää tehdä muitakin muutoksia. Kaikki kohdat, jossa lukee DC=win,DC=evolveum,DC=com tulee vaihtaa omiin domain tunnisteeseen, joka meidän tapauksessa oli DC=pisnismiehet,DC=local

Myös kohta @win.evolveum.com pitää vaihtaa -> @pisnismiehet.local

Meidän valmis malli Active Directory connectoria varten löytyy meidän GitHubista valmiina ilman Windows Serverin IP-osoitetta, joka tulisi <icfcldap:host> -kohtaan sekä Midpoint käyttäjän salasanaa, joka tulisi <t:clearValue> -kohtaan: https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Connectorit/ad-ldap-medusa-medium.xml

Kun XML-tiedosto on muokattu niin klikattiin Import object. Seuraavaksi mentiin kohtaan Resources vasemmasta listauksesta. Klikattiin Active Directory connectoria eli Medusa Active Directory (LDAP). Alhaalta klikattiin Edit configuration ja tarkistettiin, että tiedot ovat oikein.

![AD connector](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/midPoint/midPoint_ad_connector.PNG?raw=true)
<br>
Kuva 104: AD Connector.
<br>
<br>

Tämän jälkeen klikattiin Save and test connection.

![connection ok](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/midPoint/midPoint_connection_ok.PNG?raw=true)
<br>
Kuva 105: Connection OK.
<br>
<br>

 
<br>
 
<h5 id="ldap-connector">4.3.2.2. LDAP-connector</h5>
 
LDAP-palvelimen liittäminen midPointtiin onnistui seuraavanlaisesti midpointin käyttöliittymässä pääkäyttäjätunnuksilla:
 
1. Avattiin uusi välilehti selaimesta ja mentiin <a href="https://raw.githubusercontent.com/Evolveum/midpoint/master/samples/stories/unix-ldap/resources/ldap-posix.xml">GitHubiin</a> , josta tallennettiin (Ctrl+S) valmis XML-tiedostomalli omalle työpöydälle.
 
2. Avattiin XML-tiedosto esimerkiksi Notepad++ -ohjelmalla, johon teimme seuraavat muutokset:
    - ```dc=example,dc=com``` rivit korvattiin laittamalla näiden tilalle ```dc=ldap,dc=pisnismiehet,dc=local```
    - ```<name>OpenLDAP posix</name>``` arvo muutettiin arvoksi ```<name>OpenLDAP (OPENLDAPSERVER)</name>```
    - ```<icfcldap:host>localhost</icfcldap:host>``` arvon "localhost" tilalle laitettiin OPENLDAPSERVERin ip-osoite.
    - ```<clearValue>secret</clearValue>``` arvon "secret" tilalle muutettiin käyttäjän "idm" salasana, jos salasanaa on muutettu aikaisemmin joksikin muuksi. Esimerkiksi, jos uusi salasana on "HeiPoika91" tulee XML-arvoksi ```<clearValue>HeiPoika91</clearValue>```.

    Tallennettiin tehdyt muutokset. (Esimerkkitiedosto on myös saatavilla <a href="https://raw.githubusercontent.com/Eetu95/Open-source-IdM-solution/master/Roolit%20ja%20muut%20objektit/OpenLDAP/ldap-posix.xml">meidän GitHubista</a>).
 
3. Avattiin selaimella midPoint ja kirjauduttiin siihen sisälle pääkäyttäjätunnuksilla. Valittiin midPointin vasemmasta valikosta "Import object"
 
    ![](https://raw.githubusercontent.com/Eetu95/Open-source-IdM-solution/master/Kuvat/ldap-connector/Screenshot1.JPG)
    <br>
    Kuva 106: Valikko.
    <br>
    <br>

4. Seuraavaksi haettiin XML-tiedosto painamalla "Choose File" (1.). Kun tiedosto oli haettu, painoimme lopuksi "Import object" (2.). Jos tulee ruudun yläpuolelle vihreä palkki, oli tuonti onnistunut. Jos tuli punainen, XML-tiedoston sisältämissä arvoissa ja määrityksissä on jokin virhe. Tällöin kannattaa katsoa virheilmoitukset huolella, jotka näkyvät siinä samalla.
    
    ![](https://raw.githubusercontent.com/Eetu95/Open-source-IdM-solution/master/Kuvat/ldap-connector/Screenshot2.JPG)
    <br>
    Kuva 107: Haetaan XML -tiedosto.
    <br>
    <br>

5. Kun tuonti onnistui, siirryimme valikossa kohtaan ``` Resources -> List resources```
 
    ![](https://raw.githubusercontent.com/Eetu95/Open-source-IdM-solution/master/Kuvat/ldap-connector/Screenshot3.JPG)
    <br>
    Kuva 108: Ruudunkaappaus valikosta.
    <br>
    <br>
 
6. Valitsimme ruutuun avautuvasta listasta ```OpenLDAP (OPENLDAPSERVER)```
 
    ![](https://raw.githubusercontent.com/Eetu95/Open-source-IdM-solution/master/Kuvat/ldap-connector/Screenshot4.JPG)
    <br>
    Kuva 109: Ruudunkaappaus listasta.
    <br>
    <br>
 
7. Avautuvan sivun alalaidasta valittiin "Edit configuration"
 
    ![](https://raw.githubusercontent.com/Eetu95/Open-source-IdM-solution/master/Kuvat/ldap-connector/Screenshot5.JPG)
    <br>
    Kuva 110: Ruudunkaappaus sivun alalaidasta.
    <br>
    <br>
 
8. Avautui asetukset. Varmistettiin, että kuvassa korostetut kohdat on määritelty. Jos et näe kohtia, kannattaa painaa "Configuration" -otsikon viereisestä tyhjän boksin kuvasta, jolloin kaikki asetuksiin mahdollista määriteltävät kohdat tulee näkyviin. Etsi tällöin kuvassa korostetut kohdat. "Connection security" -kohdassa määritämme, että midPoint ottaa suojatun yhteyden (StartTLS) OpenLDAP -palvelimeen.
 
    ![](https://raw.githubusercontent.com/Eetu95/Open-source-IdM-solution/master/Kuvat/ldap-connector/Screenshot6.JPG)
    <br>
    Kuva 111: Ruudunkaappaus määrityksistä.
    <br>
    <br>
 
9. Kun kohta 8 oli hoidettu, kokeilimme yhteydenmuodostusta midPointin ja OpenLDAP-palvelimen välillä painamalla "Save and test connection".
 
    ![](https://raw.githubusercontent.com/Eetu95/Open-source-IdM-solution/master/Kuvat/ldap-connector/Screenshot7.JPG)
    <br>
    Kuva 112: Ruudunkaappaus.
    <br>
    <br>
 
10. Jos yhteys on toimiva, tulee vihreää kuten kuvassa. Jos ei toimi, tulee punaista ja virheilmoitus. Kannattaa tällöin tutkia virheilmoitusta ja korjata ongelma.
    
    ![](https://raw.githubusercontent.com/Eetu95/Open-source-IdM-solution/master/Kuvat/ldap-connector/Screenshot8.JPG)
    <br>
    Kuva 113: Yhteys toimii!
    <br>
    <br>
 
11. Lopuksi painoimme "Finish" ja päätimme onnistuneesti OpenLDAP-palvelimen liittämisen midPointin piiriin.

    ![](https://raw.githubusercontent.com/Eetu95/Open-source-IdM-solution/master/Kuvat/ldap-connector/Screenshot9.JPG)
    <br>
    Kuva 114: Määrityksen lopettelua.
 
<br>

<h5 id="unix-connector">4.3.2.3. Unix-connector</h5>
 
Seuraavaksi aloimme asentamaan ja määrittämään Unix-connectoria TESTIPALVELIN -testipalvelimen liittäistä varten.

<h5>Asennus ja määritys</h5>

Kloonattiin git repository <a href="https://github.com/Evolveum/ConnIdUNIXBundle.git">https://github.com/Evolveum/ConnIdUNIXBundle.git</a> ~/unix-connector -kansioon:

    $ sudo git clone https://github.com/Evolveum/ConnIdUNIXBundle.git

Mentiin unix-xonnector kansioon:

    $ cd ~/unix-connector

Rakennettiin unix-connector:

    $ sudo mvn clean package -DskipTests=true -P it

kopioitiin ~/unix-connector/target/org.connid.bundles.unix-1.0.jar -tiedosto opt/midpoint/var/icf-connectors -kansioon:

    $ sudo cp ~/unix-connector/target/org.connid.bundles.unix-1.0.jar  opt/midpoint/var/icf-connectors

Tehtiin ~/icf-connectors -kansion sisään /lib -kansio:

    $ sudo mkdir lib

Kopioitiin ~/unix-connector/target/dependencies/jsch-0.1.53.jar -tiedosto opt/midpoint/var/icf-connectors/lib -kansion sisään:

    $ sudo cp ~/unix-connector/target/dependencies/jsch-0.1.53.jar opt/midpoint/var/icf-connectors/lib

Käynnistettiin palvelin uudestaan:

    $ sudo reboot

Tehtiin tekninen Linux Ubuntu Desktop 18.04 -käyttäjä midPointille. Otettiin Ubuntuun ensin ssh-yhteys:

    $ sudo ssh pisnismiehet@(ip-osoite)

Luotiin uusi tekninen käyttäjä:

    $ sudo useradd -m midpoint
    $ sudo passwd (salasanasi)

Annettiin käyttäjälle "midpoint" oikeat oikeudet. Luotiin ensin tiedosto /etc/sudoers.d/midpoint, jonka sisään lisäsimme <a href="https://github.com/Evolveum/midpoint/blob/master/samples/resources/unix/midpoint-user-example.txt">midpointin GitHubista tämän</a> (GitHub -> Evolveum -> midpoint/samples/resources/unix/midpoint-user-example.txt):

    Host_Alias HOST = ALL

    midpoint HOST=(ALL) NOPASSWD: /usr/sbin/useradd,/usr/sbin/usermod,/usr/sbin/userdel,/usr/sbin/groupadd,/usr/sbin/groupmod,/usr/sbin/groupdel,/bin/mv,/usr/bin/passwd,/usr/bin/getent,/bin/echo,/usr/bin/tee,/bin/chown,/bin/chmod,/bin/mkdir,/usr/bin/groups,/usr/bin/id,/usr/bin/replace,/bin/rm,/bin/cat

Tallennettiin ja suljettiin tiedosto. Sitten lisäsimme unix-connector resurssin midPointiin. Ensin latasimme <a href="https://github.com/Evolveum/midpoint/blob/master/samples/resources/unix/resource-unix-advanced.xml">resurssin midPointin GitHubista</a>. Vaihdoimme xml-tiedostosta hostname, username ja password oikeiksi. Tallennettiin ja suljettiin xml-tiedosto. Lisäsimme sen midPontiin -> Configuration -> Import Object -> Choose File -> Import Object.

Sitten katsoimme asentuiko unix-connector oikein. Resource → List Resources → Unix -> Test connection.

![unix-connector-test-connection](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Unix-connector/Unix-connector-test-connection.PNG?raw=true)
<br>
Kuva 115: Unix -connectorin yhteyden testaus.
<br>
<br>

Yhteys toimi!
 
<br>

<h5 id="csv-connector">4.3.2.4.CSV-connector</h5>

CSV-connectorin avulla voidaan lisätä paljon käyttäjiä nopeasti midPoint IdM-järjestelmän piiriin. CSV connector lisättiin midPointiin XML-tiedoston avulla. MidPointin GitHubista hain CSV-connectorin XML-tiedoston ja kopioin sen leikepöydälle: https://raw.githubusercontent.com/Evolveum/midpoint/master/samples/book/2/resource-csv-hr.xml
Seuraavaksi liitin kopioidun midPointin käyttöliittymään. klikattiin Import object - Embedded editor, johon sitten liitettiin XML-tiedoston sisältö. Kun XML-tiedosto oli liitetty tekstikenttään, klikattiin Import object.
Resources kohdasta näkyy nyt, että CSV-connector on lisätty, nimi on HR System. Tämän jälkeen haettiin esimerkki CSV-tiedosto midPoint palvelimelle (MIDPOINTIDM), midPointin kotikansioon.
 1. Otettiin SSH-yhteys MIDPOINTIDM palvelimelle.
 2. Mentiin midPointin kotikansioon: 
 
```
$ cd /opt/midpoint/var
```

 3. Haettiin esimerkki CSV-tiedosto wget-komennolla:
 
```
$ sudo wget https://raw.githubusercontent.com/Evolveum/midpoint/master/samples/book/2/hr.csv
```

 4. Kopioitiin tiedostopolku, johon CSV-tiedosto vietiin:
 
```
$ pwd
 /opt/midpoint/var
```

 5. Muokattiin HR System resurssia midPointin käyttöliittymässä. Mentiin kohtaan Recourses - HR System - Edit configuration.
 6. Edit configutration kohdasta muutettiin tiedostopolku (File Path):
 
 ```
/opt/midpoint/var
```

 ![HR Sytem konfiguraatio](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/HR/hr_configuration.PNG?raw=true)
<br>
Kuva 116: HR System konfiguraatio.
<br>

 7. Tallennettiin konfiguraatio ja testattiin yhteys. Klikattiiin Save and Test Connection. Tämän jälkeen klikattiin Finish.
 ![HR System yhteys ok](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/HR/hr_connection_ok.PNG?raw=true)
<br>
Kuva 117: HR System yhteys ok.
<br>
 
 8. HR System resurssin välilehdeltä Accounts - Repository päästään lisämään käyttäjiä CSV-tiedostosta midPointin käyttöliittymään. Klikattiin esimerkkikäyttäjän asetuksia ja valittiin Import.
 ![HR System import](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/HR/hr_import.PNG?raw=true)
<br>
Kuva 118: HR System import.
<br>
 
 9. Importtauksen jälkeen tuli ilmoitus onnistuneesta viedystä käyttäjästä. Kyseinen käyttäjä muuttui myös LINKED tilaan.
 ![HR System import ok](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/HR/hr_import_ok.PNG?raw=true)
 <br>
Kuva 119: HR System import ok.
<br>
 
 10. Importattu käyttäjä näkyy nyt midPointin Users -kohdassa.
 ![HR uusi käyttäjä](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/HR/hr_user.PNG?raw=true)
<br>
Kuva 120: HR uusi käyttäjä.
<br>
 
 
<h4 id="suojatun-web-yhteyden-maaritys-https3">4.3.3. Suojatun web-yhteyden määritys (https)</h4>

Suojattua yhteyttä tarvitaan, jotta midPointin tietojen eheys ja luottamuksellisuus pysyy turvassa käyttäjän ja sivuston eli midPointin välillä. Otimme HTTPS suojauksen käyttöön midPoint palvelimella, jotta midPointin käyttöliittymä on suojattu. Suojauksen huomaa selaimella siitä, että selain käyttää https:// yhteyttä osoitepalkissa.

Koska meillä ei ole rahallista budjettia meidän projektissa, emme voineet hankkia kunnollista sertifikaattia, koska se olisi maksanut jonkin verran. Näin ollen käytimme itseallekirjoitettua sertifikaattia. Joudumme myös määrittelemään käänteisen välityspalvelimen, jotta sertifikaatin käyttö midPointin käyttöliittymässä on mahdollista.

Suojatun yhtyeden määritys onnistui seuraavanlaisesti:

1. Suojattua yhteyttä varten tarvitsi asentaa Apache2 komennoilla:

```
sudo apt-get update
sudo apt-get install apache2 -y
```
Latauksessa ja asennuksessa kesti tovin.
 
2. Laitettiin seuraavaksi Apache2:sta ssl-moduuli päälle komennolla:
```
sudo a2enmod ssl
```
Komennon antamisen jälkeen painoimme Enter. Moduuli meni päälle.
 
3. Käynnistettiin Apache2 uudelleen komennolla:
```
sudo service apache2 restart
```
4. Luodaan uusi sijainti itseallekirjoitetulle sertifikaatille:
```
sudo mkdir /etc/apache2/ssl
```
Komennon antamisen jälkeen painoimme Enter. Uusi sijainti luotiin.
 
5. Itseallekirjoitetun sertifikaatin loimme komennolla:
```
sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /etc/apache2/ssl/apache.key -out /etc/apache2/ssl/apache.crt
```
Mitä komento tekee:

- openssl = CLI työkalu, jolla luodaan ja hallitaan OpenSSL sertifikaatteja, avaimia ja muita tiedostoja.
- req = alikomento, jolla kerrotaan että halutaan käyttää X.509 CSR:ää. X.509 on julkisenavaimen infrastruktuuri standardi, jota
SSL ja TLS noudattavat. Teimme siis uuden X.509 sertin.
- "-x509" = modifioi aikaisempaa alikomentoa kertomalla apuohjelmalle, että halutaan tehdä itsekirjoitettu sertifikaatti sen sijaan että tehtäisiin
sertifikaatin allekirjoitus pyyntö.
- "-nodes" = Kertoo OpenSSL:lle että se voi ohittaa sertifikaatin suojauksen tunnuslauseen. Apachen pitää pystyä
lukemaan tiedosto ilman, että käyttäjä puuttuu siihen silloin kun palvelin käynnistyy. Tunnuslause (passphrase)
estäisi tämän toteutumisen, koska meidän pitäisi aina syöttää se jokaisen uudelleenkäynnistyksen yhteydessä.
- "-days 365" = Tämä asettaa sertifikaatin voimassaolo ajan 365 päiväksi.
- "-newkey rsa":2048 =Tällä määritellään uuden sertifikaatin ja avaimen luonti samaan aikaan. Rsa:2048 kertoo että pitää
tehdä RSA avain, joka on 2048 bittiä pitkä.
- "-keyout" = Kertoo OpenSSL:lle minne luotu yksityinen avaintiedosto pistetään.
- "-out" = Kertoo OpenSSL:lle minne sertifikaatti pistetään.

Komentoon piti luoda tiedot meistä:
```
Country Name (2 letter code) [AU]:FI
State or Province Name (full name) [Some-State]:Uusimaa
Locality Name (eg, city) []:Helsinki
Organization Name (eg, company) [Internet Widgits Pty Ltd]:Pisnismiehet
Organizational Unit Name (eg, section) []:Projectgroup
Common Name (e.g. server FQDN or YOUR name) []:*palvelimen IP-osoite*
Email Address []:markus.nissinen@myy.haaga-helia.fi
```
 
6. Siirryimme root -käyttäjäksi komennolla:
```
sudo su
```
 
7. Käänteistä välityspalvelinta varten joudumme sallimaan neljän eri moduulin käytön. Nämä sallimme komennoilla:
```
sudo a2enmod proxy
sudo a2enmod proxy_http
sudo a2enmod proxy_balancer
sudo a2enmod lbmethod_byrequests
```
 
8. Käynnistimme taas Apache2:sen uudelleen:
```
sudo systemctl restart apache2
```
9. Avasimme seuraavan tiedoston komennolla:
```
sudo nano /etc/apache2/sites-available/default-ssl.conf
```
Tiedosto avautui Nano- ohjelmassa.
 
10. Muutimme "default-ssl.conf" -tiedostosta seuraavat kohdat:
```
# ServerAdmin markus.nissinen@myy.haaga-helia.fi
# ServerName 172.28.230.27
DocumentRoot /var/www/html
ProxyPass / http://127.0.0.1:8080/
ProxyPassReverse / http://127.0.0.1:8080/

#   SSL Engine Switch:
#   Enable/Disable SSL for this virtual host.
SSLEngine on

#   A self-signed (snakeoil) certificate can be created by installing
#   the ssl-cert package. See
#   /usr/share/doc/apache2/README.Debian.gz for more info.
#   If both key and certificate are stored in the same file, only the
#   SSLCertificateFile directive is needed.
SSLCertificateFile      /etc/apache2/ssl/apache.crt
SSLCertificateKeyFile /etc/apache2/ssl/apache.key

```
Tallensimme ja suljimme lopuksi tiedoston.
 
11. Avasimme tämän jälkeen seuraavan tiedoston:
```
sudoedit /etc/apache2/sites-available/000-default.conf
```
Tiedosto avautui myös Nano -ohjelmaan.
 
12. Muutimme "000-default.conf" -tiedostosta seuraavat kohdat:
```
ServerName http://172.28.230.27
Redirect /secure https://172.28.230.27
Redirect permanent / https://172.28.230.27

# ServerAdmin webmaster@localhost
# DocumentRoot /var/www/html
```
Tallensimme ja suljimme lopuksi tiedoston.
 
13. Aktivoimme Apachen SSL Virtuaalihostin komennolla:
```
sudo a2ensite default-ssl.conf
```
 
14. Käynnistimme lopuksi Apachen uudelleen komennolla:
```
sudo service apache2 restart
```
15. Jouduimme lisäksi tekemään ```application.yml``` -tiedoston midPointin asennuskansioon sijaintiin ```/opt/midpoint/var/``` komennolla:
```
sudoedit /opt/midpoint/var/application.yml
```
Komennon jälkeen painoimme Enter. Tiedosto avautui "Nano" -ohjelmassa.
 
16. Lisättiin tiedostoon seuraavat konfiguraatiot:
```
server.address: 127.0.0.1
server.port: 8080
server.session.timeout: 60
server.use-forward-hearders: true
server.tomcat.internal-proxies: 127.0.0.1
```
Tallensimme ja lopuksi suljimme tiedoston.
 
17. Käynnistettiin midPoint palvelimen uudelleen:
```
sudo reboot
```
 

Käynnistyksen jälkeen testattiin Apachen toimivuutta. Kirjoitettiin selaimeen:
```
https://*palvelimen IP-osoite*
```
Tällöin tuli herja siitä, että sertifikaatti ei ole luotettava. Tämä johtuu siitä, koska sertifikaatti on itse allekirjoitettu eikä hankittu valtuutetulta taholta. Ohitettiin herja Chromessa vain klikkaamalla Advanced ja ``` Proceed to https://*palvelimen IP-osoite*```
![https Chrome](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/chrome_https.PNG?raw=true)
<br>
Kuva 121: Sertifikaattivaroitus (Chrome)
<br>
<br>

Kokeilimme myös uudelleenohjauksen toimivuutta. Kirjoitettiin selaimeen ```http://*palvelimen IP-osoite*```
Selain uudelleenohjasi suojattuun sivustoon: ```https://*palvelimen IP-osoite*```

Avautui midPointin kirjautumisruutu.
![midPoint kirjautumisruutu](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/midPoint/midPoint_kirjautumisruutu.PNG?raw=true)
<br>
Kuva 122: midPointin kirjautumisruutu.
<br>
<br>
Uudelleenohjaus toimi. Selain uudelleenohjasi suojattuun midPointin kirjautumisruutuun. Myöskin aiempi tapa miten midPointin käyttöliittymään kirjaudutaan ei enää toimi. Eli ```http://*palvelimen IP-osoite*:8080/midpoint/``` ei enää toimi.
 
<br>
 
<h4 id="roolien-seka-muiden-objektien-lisaaminen">4.3.4. Roolien sekä muiden objektien lisääminen</h4>
 
Nyt kun midPointin sekä kohdejärjestelmien välinen yhteys toimii, pitää meidän seuraavaksi määritellä midPointtiin roolit sekä muut tarvittavat objektit, joiden ansiosta provisiointi eli muutoksien ajaminen midPointista kohdejärjestelmiin onnistuu.
 
<br>
 
<h5 id="openldap">4.3.4.1. OpenLDAP</h5>
 
Jouduimme tuomaan midPointtiin seuraavat tiedostot (nämä löytyvät myös meidän GitHub -sivuilta):

- extension-posix.xsd (<a href="https://raw.githubusercontent.com/Evolveum/midpoint/master/samples/stories/unix-management/extension-unix.xsd">Valmistajan GitHub</a>) (<a href="https://raw.githubusercontent.com/Eetu95/Open-source-IdM-solution/master/Roolit%20ja%20muut%20objektit/OpenLDAP/extension-posix.xsd">Meidän GitHub</a>)
    - Tämä tiedoston ansiosta midPoint tukee Unix-järjestelmissä käytettyjä GID ja UID -arvoja.
- role-meta-ldapgroup.xml (<a href="https://raw.githubusercontent.com/Evolveum/midpoint/master/samples/stories/unix-ldap/roles/role-meta-ldapgroup.xml">Valmistajan GitHub</a>) (<a href="https://raw.githubusercontent.com/Eetu95/Open-source-IdM-solution/master/Roolit%20ja%20muut%20objektit/OpenLDAP/role-meta-ldapgroup.xml">Meidän GitHub</a>)
    - Tiedoston ansiosta LDAP-ryhmien teko muihin kuin Unix-järjestelmiin on mahdollista. Tämä luo ```Roles -> List roles``` sijainnin alle uuden ryhmän nimeltään "LDAP Group Metarole".
- role-meta-unix-group.xml (<a href="https://raw.githubusercontent.com/Evolveum/midpoint/master/samples/stories/unix-ldap/roles/role-meta-unix-group.xml">Valmistajan GitHub</a>) (<a href="https://raw.githubusercontent.com/Eetu95/Open-source-IdM-solution/master/Roolit%20ja%20muut%20objektit/OpenLDAP/role-meta-unix-group.xml">Meidän GitHub</a>)
    - Tiedoston ansiosta LDAP-ryhmien teko Unix-järjestelmiin on mahdollista. Tämä luo ```Roles -> List roles``` sijainnin alle uuden ryhmän nimeltään "LDAP Unix Group Metarole".
- sequence-gidnumber.xml (<a href="https://raw.githubusercontent.com/Evolveum/midpoint/master/samples/stories/unix-ldap/other/sequence-gidnumber.xml">Valmistajan GitHub</a>) (<a href="https://raw.githubusercontent.com/Eetu95/Open-source-IdM-solution/master/Roolit%20ja%20muut%20objektit/OpenLDAP/sequence-gidnumber.xml">Meidän GitHub</a>)
    - Tiedoston ansiosta midPoint osaa generoida automaattisesti GID-arvoja.
- sequence-uidnumber.xml (<a href="https://raw.githubusercontent.com/Evolveum/midpoint/master/samples/stories/unix-ldap/other/sequence-uidnumber.xml">Valmistajan GitHub</a>) (<a href="https://raw.githubusercontent.com/Eetu95/Open-source-IdM-solution/master/Roolit%20ja%20muut%20objektit/OpenLDAP/sequence-uidnumber.xml">Meidän GitHub</a>)
    - Tiedoston ansiosta midPoint osaa generoida automaattisesti UID-arvoista.
 
Aloitimme ensimmäisenä tuomaan "extension-posix.xsd" -tiedoston midPointtiin seuraavanlaisesti:

1. Otimme SSH-yhteyden "MIDPOINTIDM" -palvelimeen. Kirjauduimme sisälle pääkäyttäjän tunnuksilla.

2. Siirryimme seuraavaksi root -käyttäjäksi komennolla:
    ```
    sudo su
    ```
    Komennon jälkeen painoimme Enter. 
 
3. Menimme sijaintiin ```/opt/midpoint/var/schema``` komennolla:
    ```
    cd /opt/midpoint/var/schema
    ```
    Komennon jälkeen painoimme Enter. Siirryttiin uuteen sijaintiin.
 
4. Ladattiin ```extension-posix.xsd``` midPointin kehittäjän Evolveumin GitHub -sivuilta komennolla:
    ```
    wget https://raw.githubusercontent.com/Evolveum/midpoint/master/samples/stories/unix-management/extension-unix.xsd
    ```
    Komennon jälkeen painoimme Enter. Tiedoston latauksessa kesti tovin.
 
5. Käynnistimme "MIDPOINTIDM" -palvelimen uudelleen komennolla:
    ```
    sudo reboot
    ```
    Komennon jälkeen painoimme Enter. Palvelin aloitti uudelleen käynnistyksen ja tiedosto on tuotu midPointtiin onnistuneesti!

Toimme muut tiedostot midPointtiin seuraavanlaisesti:

1. Ladattiin jokainen tiedosto omalle tietokoneelle talteen.
2. Avattiin selain ja mentiin midPointin sivulle. Kirjauduttiin sisälle pääkäyttäjän tunnuksilla.
3. Vasemmasta valikosta valittiin "import object".
4. Seuraavaksi haettiin haluttu tiedosto painamalla "Choose File". Kun tiedosto oli haettu, painoimme lopuksi "Import object".
5. Tiedosto tuotiin onnistuneesti.
 
Loimme seuraavaksi uuden ryhmän Unix-järjestelmän pääkäyttäjiä varten (sudo), johon halutut henkilöt liitetään lopuksi. Ryhmän nimi oli "sudoers".

Valitsimme midPointin vasemmasta valikosta ```Roles -> New role```.

Tämän jälkeen teimme seuraavat määrityset:
 
**"Basic" -välilehti**

Properties
 
| Kohta  | Arvo  |
| --- | --- |
| Name | sudoers |
| Display name | Pääkäyttäjät |
| Description | OpenLDAP:n pääkäyttäjät (Unix/Linux). Lisää käyttäjä tähän ryhmään, jos haluat sille pääkäyttäjäoikeudet *nix -järjestelmiin. |
| Subtype | sudo |
| Identifier | sudo |

Options
 
| Kohta  | Arvo  |
| --- | --- |
| Force | (Kohta valittu) |
| Execute afrer all approvals | (Kohta valittu)
 

**"Assigments" -välilehti**

Lisättiin ryhmä "LDAP Unix Group Metarole" -ryhmä painamalla vihreää "+" -painiketta ja valittiin edellä mainittu ryhmä avautuvasta listasta ja painettiin "Add".


Painoimme lopuksi "Preview changes" ja sitten "Save". Ryhmä oli luotu.
 
<br>
 
Loimme seuraavaksi peruskäyttäjille oman ryhmän nimeltään "openldap_basic_users_unix":

**"Basic" -välilehti**

Properties
 
| Kohta  | Arvo  |
| --- | --- |
| Name | openldap_basic_users_unix |
| Display name | OpenLDAP peruskäyttäjät - Unix/Linux |
| Description | OpenLDAP:n peruskäyttäjät (Unix/Linux). Lisää käyttäjä tähän ryhmään, jos haluat sille perus käyttäjäoikeudet *nix -järjestelmiin. |
| Subtype | openldap_basic_users_unix |
| Identifier | openldap_basic_users_unix |

Options
 
| Kohta  | Arvo  |
| --- | --- |
| Force | (Kohta valittu) |
| Execute afrer all approvals | (Kohta valittu)
 

**"Assigments" -välilehti**

Lisättiin ryhmä "LDAP Unix Group Metarole" -ryhmä painamalla vihreää "+" -painiketta ja valittiin edellä mainittu ryhmä avautuvasta listasta ja painettiin "Add".
 
Painoimme lopuksi "Preview changes" ja sitten "Save". Ryhmä oli luotu. 
 
<br>

Jokaiselle käyttäjälle täytyy myös luoda oma henkilökohtainen ryhmä. Tämä vaaditaan, jos halutaan kirjautua *nix -järjestelmiin (Unix & Linux).

Henkilökohtainen ryhmä tehtiin seuraavanlaisesti (HUOMIO! PALAA TÄHÄN KOHTAAN MYÖHEMMIN, JOS ET OLE LISÄNNYT VIELÄ HALUTTUJA KÄYTTÄJIÄ MIDPOINTTIIN!):

**"Basic" -välilehti**

Properties
 
| Kohta  | Arvo  |
| --- | --- |
| Name | (käyttäjän käyttäjänimi eli username) |
| Display name | (käyttäjän käyttäjänimi eli username) |
| Description | Käyttäjäryhmä käyttäjälle (käyttäjän nimi eli name) (Käyttäjätunnus:(käyttäjän käyttäjätunnus eli username)). Ryhmäliitosta tarvitaan ainakin silloin, jos kirjaudutaan Linux työasemalle tai palvelimelle graaffisesta käyttöliittymästä käsin. HUOMIO: TÄMÄ RYHMÄLIITOS EI MÄÄRITTELE KÄYTTÄJÄN KÄYTTÖOIKEUKSIA! |
| Subtype | (käyttäjän käyttäjänimi eli username) |
| Identifier | (käyttäjän käyttäjänimi eli username) |
| gidNumber | (sama mikä käyttäjälle määritelty uid-arvo on)

Activation

| Kohta  | Arvo  |
| --- | --- |
| Administrative status | Enabled |

Options
 
| Kohta  | Arvo  |
| --- | --- |
| Force | (Kohta valittu) |
| Execute afrer all approvals | (Kohta valittu)


**"Assigments" -välilehti**

Lisättiin ryhmä "LDAP Unix Group Metarole" -ryhmä painamalla vihreää "+" -painiketta ja valittiin edellä mainittu ryhmä avautuvasta listasta ja painettiin "Add".
 
Painoimme lopuksi "Preview changes" ja sitten "Save". Ryhmä oli luotu.

<br>

<h5 id="unix">4.3.4.2. Unix (Unix -connector)</h5>
 
Toimme ensiksi roolin, jonka avulla voimme myöhemmin tehdä roolit pää- ja peruskäyttäjiä varten.
 
Ladattiin rooli <a href="https://github.com/Evolveum/midpoint/tree/master/samples/stories/unix-management">midPointin GitHubista</a>. Lisättiin xml-tiedosto, joka lisää "advanced scenarios" ominaisuuksia. Configuration -> Import Objects -> Choose File -> resource-unix-advanced.xml -> Import Object (On hyvä pistää "check" -merkki ennen lisäystä kohtiin "Keep oid" ja "Overwrite existing object".

Sitten lisäsimme metaroolin midPoint roolille. Tämä lisää ryhmänteko mahdollisuuden kohde Linux-koneelle. Configuration -> Import Objects -> Choose File -> role-assignment-inducement-metarole.xml -> Import Object.
 
Loimme seuraavaksi midPointtiin roolin pääkäyttäjiä varten nimeltään "sudo" ja peruskäyttäjiä varten nimeltään "user".

Aloitimme tekemään ensimmäiseksi "sudo" -roolin. Valitsimme midPointin vasemmasta valikosta ```Roles -> New role```.

Tämän jälkeen teimme seuraavat määrityset:
 
**"Basic" -välilehti**

Properties
 
| Kohta  | Arvo  |
| --- | --- |
| Name | sudo |
| Display name | sudo |
| Description | Linux -pääkäyttäjäoikeudet (UNIX-connector). Lisää käyttäjä tähän ryhmään, jos haluat sille pääkäyttäjäoikeudet testipalvelimeen. |
| Subtype | root |
| Subtype | sudo |

Options
 
| Kohta  | Arvo  |
| --- | --- |
| Force | (Kohta valittu) |
| Execute afrer all approvals | (Kohta valittu)
 

**"Assigments" -välilehti**

Lisättiin ryhmä "Assignemnt & Inducement UNIX Group Metarole" -ryhmä painamalla vihreää "+" -painiketta ja valittiin edellä mainittu ryhmä avautuvasta listasta ja painettiin "Add".


Painoimme lopuksi "Preview changes" ja sitten "Save". Ryhmä oli luotu.
 
Seuraavaksi loimme "user" -roolin. Valitsimme midPointin vasemmasta valikosta ```Roles -> New role```.

Tämän jälkeen teimme seuraavat määrityset:
 
**"Basic" -välilehti**

Properties
 
| Kohta  | Arvo  |
| --- | --- |
| Name | user |
| Display name | user |
| Description | Linux -peruskäyttäjäryhmä (UNIX-connector).Lisää käyttäjä tähän ryhmään, jos haluat sille perus käyttöoikeudet testipalvelimeen. |

Options
 
| Kohta  | Arvo  |
| --- | --- |
| Force | (Kohta valittu) |
| Execute afrer all approvals | (Kohta valittu)
 

**"Assigments" -välilehti**

Lisättiin ryhmä "Assignemnt & Inducement UNIX Group Metarole" -ryhmä painamalla vihreää "+" -painiketta ja valittiin edellä mainittu ryhmä avautuvasta listasta ja painettiin "Add".
 
<br>

<h2 id="testaus">5. Testaus</h2>
 
Aloitimme testaamisen luomalla ensimmäiseksi käyttäjätunnuksen, sekä henkilökohtaisen käyttäjäryhmän midPointtiin. Tämän jälkeen liitimme sen aiemmin luotuihin connectoreiden rooleihin. Tämän jälkeen kokeilimme kirjautumista kohdejärjestelmiin.

Lopuksi kokeilimme jäädyttää käyttäjä midPointissa ja kuinka se vaikuttaa mahdollisuuteen kirjatua haluttuihin kohdejärjestelmiin.

Kirjauduimme sisään midPointtiin verkkoselaimen kautta pääkäyttäjän tunnuksilla.
 
<br>
 
<h3 id="kayttajien-luonti-midpointtiin">5.1. Käyttäjien luonti midPointtiin</h3>
 
Käyttäjät luotiin midPointtiin seuraavalaisesti:
 
1. Käyttöliittymän vasemman puoleisesta valikosta valittiin ```Users -> New user```
 
    ![](https://raw.githubusercontent.com/Eetu95/Open-source-IdM-solution/master/Kuvat/Testaus/Screenshot%20(1).png)
    <br>
    Kuva 123: Ruudunkaappaus valikosta.
    <br>
    <br>
 
2. Määriteltiin ruudussa näkyviin kohtiin ainakin seuraavat kohdat:

    Properties

    | Kohta  | Arvo  |
    | --- | --- |
    | Name (Käyttäjänimi) | ullanieminen |
    | Description (Kuvaus) | Pääkäyttäjä. |
    | Subtype (Alityyppi) | ullanieminen |
    | Full name (Koko nimi) | Ulla Nieminen |
    | Given name (Etunimi) | Ulla |
    | Family name (Sukunimi) | Nieminen |
    | Title (Titteli) | Suunnittelija |
    | Email (Sähköpostiosoite) | ulla.nieminen@testiposti.fi |
    | Telephone (Puhelinnumero) | +358123456789 |
     
    ![](https://raw.githubusercontent.com/Eetu95/Open-source-IdM-solution/master/Kuvat/Testaus/Screenshot%20(2).png)
    <br>
    Kuva 124: Ruudunkaappaus määrityksistä (1/2).
    <br>
    <br>
     

    Activation

    | Kohta  | Arvo  |
    | --- | --- |
    | Administrative status (Käyttäjän status) | Enabled (Aktiivinen) |
    | Valid from (Voimassa alkaen) | <Tämän hetkinen aika 12-tunnin muodossa ja päivämäärä>
     
    Password

    | Kohta  | Arvo  |
    | --- | --- |
    | Value (Arvo) | <Käyttäjälle haluttu salasana>

    Options

    | Kohta  | Arvo  |
    | --- | --- |
    | Force (Pakota) | <Rasti boksissa> |
    | Execute after all approvals (Suorita kaikkien suoritusten jälkeen) | <Rasti boksissa>

    ![](https://raw.githubusercontent.com/Eetu95/Open-source-IdM-solution/master/Kuvat/Testaus/Screenshot%20(3).png)
    <br>
    Kuva 125: Ruudunkaappaus määrityksistä (2/2).
    <br>
    <br>

3. Katsottiin tehtävät muutokset painamalla "Preview changes". Muutokset vaikuttivat ihan ok. 

    ![](https://raw.githubusercontent.com/Eetu95/Open-source-IdM-solution/master/Kuvat/Testaus/Screenshot%20(4).png)
    <br>
    Kuva 126: Ruudunkaappaus esikatselusta (1/2).
    <br>
    <br>
    Lopuksi painettiin sivun alhaalta "Save".

    ![](https://raw.githubusercontent.com/Eetu95/Open-source-IdM-solution/master/Kuvat/Testaus/Screenshot%20(5).png)
    <br>
    Kuva 127: Ruudunkaappaus esikatselusta (2/2).
    <br>
    <br>
 
    Ullan käyttäjätunnus luotiin onnistuneesti!
 
    ![](https://raw.githubusercontent.com/Eetu95/Open-source-IdM-solution/master/Kuvat/Testaus/Screenshot%20(6).png)
    <br>
    Kuva 128: Ruudunkaappaus ilmoituksesta.
    <br>
    <br> 

Teimme Matti Nimeiselle tunnukset samalla tavalla paitsi kohta 2 tehtiin seuraavanlaisesti:

Properties

| Kohta  | Arvo  |
| --- | --- |
| Name (Käyttäjänimi) | mattinieminen |
| Description (Kuvaus) | Pääkäyttäjä. |
| Subtype (Alityyppi) | mattinieminen |
| Full name (Koko nimi) | Matti Nieminen |
| Given name (Etunimi) | Matti |
| Family name (Sukunimi) | Nieminen |
| Title (Titteli) | Testaaja |
| Email (Sähköpostiosoite) | matti.nieminen@testiposti.fi |
| Telephone (Puhelinnumero) | +358129876543 |

Activation

| Kohta  | Arvo  |
| --- | --- |
| Administrative status (Käyttäjän status) | Enabled (Aktiivinen) |
| Valid from (Voimassa alkaen) | <Tämän hetkinen aika 12-tunnin muodossa ja päivämäärä>
    
Password

| Kohta  | Arvo  |
| --- | --- |
| Value (Arvo) | <Käyttäjälle haluttu salasana>

Options

| Kohta  | Arvo  |
| --- | --- |
| Force (Pakota) | <Rasti boksissa> |
| Execute after all approvals (Suorita kaikkien suoritusten jälkeen) | <Rasti boksissa>

<br>
 
<h3 id="kayttajan-liittaminen-active-directoryn-kayttajaksi">5.2. Käyttäjän liittäminen Active Directoryn käyttäjäksi</h3>

Uusi käyttäjä "Ulla Nieminen" liitettiin Active Directoryn käyttäjäksi seuraavanlaisesti:
 
1. midPointin vasemmasta valikosta valittiin ```Users -> List users```
 
2. Käyttäjälistauksesta valittiin "ullanieminen"

    ![](https://raw.githubusercontent.com/Eetu95/Open-source-IdM-solution/master/Kuvat/Testaus/Screenshot%20(7).png)
    <br>
    Kuva 129: Ruudunkaappaus listauksesta.
    <br>
    <br> 

3. Valittiin välilehdestä "Projections" (1.). Tämän jälkeen painettiin rattaan kuvaa (2.) ja lopuksi "Add projection" (3.).

    ![](https://raw.githubusercontent.com/Eetu95/Open-source-IdM-solution/master/Kuvat/Testaus/Screenshot%20(8).png)
    <br>
    Kuva 130: Ruudunkaappaus.
    <br>
    <br> 
 
4. Valittiin avautuneesta "Choose object" -ikkunasta "Medusa Active Directory (LDAP) (1.) ja kuitattiin valinta painamalla "Add" (2.).

    ![](https://raw.githubusercontent.com/Eetu95/Open-source-IdM-solution/master/Kuvat/Testaus/Screenshot%20(9).png)
    <br>
    Kuva 131: Ruudunkaappaus listauksesta.
    <br>
    <br> 
 
5. Katsottiin että "Options" -kohdassa on samat valittuna mitä kuvan kohdassa 1. Lopuksi valittiin "Save" (2.). Nyt käyttäjä oli liitetty Active Directoryn piiriin onnistuneesti!

    ![](https://raw.githubusercontent.com/Eetu95/Open-source-IdM-solution/master/Kuvat/Testaus/Screenshot%20(10).png)
    <br>
    Kuva 132: Ruudunkaappaus kohdasta.
    <br>
    <br> 

Matti Nieminen liitettiin samalla tavalla Active Directoryyn.
 <br>

<h3 id="kayttajan-liittaminen-testipalvelin-palvelimeen-unix-connector">5.3. Käyttäjän liittäminen TESTIPALVELIN -palvelimeen (Unix Connector)</h3>
 
Liitimme Ulla Niemisen TESTIPALVELIN -palvelimen pääkäyttäjäksi ja Matti Niemisen seuraavanlaisesti:
 
1. midPointin vasemmasta valikosta valittiin ```Users -> List users```
 
2. Käyttäjälistauksesta valittiin "ullanieminen"

    ![](https://raw.githubusercontent.com/Eetu95/Open-source-IdM-solution/master/Kuvat/Testaus/Screenshot%20(7).png)
    <br>
    Kuva 133: Ruudunkaappaus listauksesta.
    <br>
    <br> 
 
3. Valittiin välilehdestä "Assignments".
 
4. Seuraavaksi painettiin vihreää nappia.
 
5. Avautui "Select object(s)" -ikkuna. Koska Ulla oli pääkäyttäjä, valitsimme listasta rooli nimeltään "sudo" ja painettiin listan lopusta "Add" -painiketta.
 
6. Katsottiin että "Options" -kohdassa on samat valittuna mitä kuvan kohdassa 1. Lopuksi valittiin "Save" (2.). Nyt käyttäjä oli liitetty TESTIPALVELIN -palvelimen käyttäjäksi onnistuneesti!

    ![](https://raw.githubusercontent.com/Eetu95/Open-source-IdM-solution/master/Kuvat/Testaus/Screenshot%20(10).png)
    <br>
    Kuva 134: Ruudunkaappaus kohdasta.
    <br>
    <br> 

Matti Nieminen lisättiin peruskäyttäjäksi samalla tavalla paitsi kohdassa 5 valittiin sen sijaan rooliksi "user".
 
<br>
 
<h3 id="kayttajan-liittaminen-openldapn-kayttajaksi">5.4. Käyttäjän liittäminen OpenLDAP:n käyttäjäksi</h3>
 
Liitimme Ulla Niemisen OpenLDAP:n käyttäjäksi seuraavanlaisesti:
 
1. midPointin vasemmasta valikosta valittiin ```Users -> List users```
 
2. Käyttäjälistauksesta valittiin "ullanieminen"

    ![](https://raw.githubusercontent.com/Eetu95/Open-source-IdM-solution/master/Kuvat/Testaus/Screenshot%20(7).png)
    <br>
    Kuva 135: Ruudunkaappaus listauksesta.
    <br>
    <br> 
 
3. Valittiin välilehdestä "Assignments".
 
4. Seuraavaksi painettiin vihreää nappia.
 
5. Avautui "Select object(s)" -ikkuna. Koska Ulla oli pääkäyttäjä, valitsimme listasta rooli nimeltään "sudoers" ja painettiin listan lopusta "Add" -painiketta.

6. Katsottiin että "Options" -kohdassa on samat valittuna mitä kuvan kohdassa 1. Lopuksi valittiin "Save" (2.).

    ![](https://raw.githubusercontent.com/Eetu95/Open-source-IdM-solution/master/Kuvat/Testaus/Screenshot%20(10).png)
    <br>
    Kuva 136: Ruudunkaappaus kohdasta.
    <br>
    <br> 
 
7. Valittiin uudelleen käyttäjälistauksesta "ullanieminen"
 
8. Otettiin itselle talteen "Basic" -välilehdeltä näkyvän "Unix UID number" arvon. Tässä tapauksessa se oli 1114.
 
9. Valittiin midPointin vasemmasta valikosta ```Roles -> New role```
 
10. Luotiin Ulalle oma henkilökohtainen ryhmä. Laitoimme seuraavat arvot:

    **"Basic" -välilehti**

    Properties
    
    | Kohta  | Arvo  |
    | --- | --- |
    | Name | ullanieminen |
    | Display name | ullanieminen |
    | Description | Käyttäjäryhmä käyttäjälle Ulla Nieminen (Käyttäjätunnus: ullanieminen). Ryhmäliitosta tarvitaan ainakin silloin, jos kirjaudutaan Linux työasemalle tai palvelimelle graaffisesta käyttöliittymästä käsin. HUOMIO: TÄMÄ RYHMÄLIITOS EI MÄÄRITTELE KÄYTTÄJÄN KÄYTTÖOIKEUKSIA! |
    | Subtype | ullanieminen |
    | Identifier | ullanieminen |
    | gidNumber | 1114 |

    Activation

    | Kohta  | Arvo  |
    | --- | --- |
    | Administrative status | Enabled |

    Options
    
    | Kohta  | Arvo  |
    | --- | --- |
    | Force | (Kohta valittu) |
    | Execute afrer all approvals | (Kohta valittu)


    **"Assigments" -välilehti**

    Lisättiin ryhmä "LDAP Unix Group Metarole" -ryhmä painamalla vihreää "+" -painiketta ja valittiin edellä mainittu ryhmä avautuvasta listasta ja painettiin "Add".
    
    Painoimme lopuksi "Preview changes" ja sitten "Save". Ryhmä oli luotu.
     
11. midPointin vasemmasta valikosta valittiin ```Users -> List users```
 
12. Käyttäjälistauksesta valittiin "ullanieminen"

    ![](https://raw.githubusercontent.com/Eetu95/Open-source-IdM-solution/master/Kuvat/Testaus/Screenshot%20(7).png)
    <br>
    Kuva 137: Ruudunkaappaus listasta.
    <br>
    <br> 
 
13. Valittiin välilehdestä "Assignments".
 
14. Seuraavaksi painettiin vihreää nappia.
 
15. Avautui "Select object(s)" -ikkuna. Valitsimme listasta henkilökohtainen ryhmä nimeltään "ullanieminen" ja painettiin listan lopusta "Add" -painiketta.
 
16. Katsottiin että "Options" -kohdassa on samat valittuna mitä kuvan kohdassa 1. Lopuksi valittiin "Save" (2.). Nyt käyttäjä oli liitetty OpenLDAP -palvelimen käyttäjäksi onnistuneesti!

    ![](https://raw.githubusercontent.com/Eetu95/Open-source-IdM-solution/master/Kuvat/Testaus/Screenshot%20(10).png)
    <br>
    Kuva 138: Ruudunkaappaus kohdasta.
    <br>
    <br> 

Matti Nieminen lisättiin peruskäyttäjäksi samalla tavalla paitsi kohdassa 5 valittiin sen sijaan rooliksi "openldap_basic_users_unix", kohta 10 oli seuraava:

Properties

| Kohta  | Arvo  |
| --- | --- |
| Name | mattinieminen |
| Display name | mattinieminen |
| Description | Käyttäjäryhmä käyttäjälle Matti Nieminen (Käyttäjätunnus: mattinieminen). Ryhmäliitosta tarvitaan ainakin silloin, jos kirjaudutaan Linux työasemalle tai palvelimelle graaffisesta käyttöliittymästä käsin. HUOMIO: TÄMÄ RYHMÄLIITOS EI MÄÄRITTELE KÄYTTÄJÄN KÄYTTÖOIKEUKSIA! |
| Subtype | mattinieminen |
| Identifier | mattinieminen |
| gidNumber | 1115 |

Activation

| Kohta  | Arvo  |
| --- | --- |
| Administrative status | Enabled |

Options

| Kohta  | Arvo  |
| --- | --- |
| Force | (Kohta valittu) |
| Execute afrer all approvals | (Kohta valittu)

 
Kohta 15:ssa Matti liitettiin ryhmään "mattinieminen". 

<br>

<h3 id="kayttajan-kayttooikeudet-midpointin-kayttoliittymaan">5.5. Käyttäjän käyttöoikeudet midPointin käyttöliittymään</h3>
 
Määritimme Ulalle ja Matille oikeudet midPointin käyttöliittymän osalta. Emme haluneet heistä pääkäyttäjiä siihen, koska silloin kummatkin pystyisivät hallitsemaan myös muita käyttäjiä. Teimme heistä sen sijaan loppukäyttäjän (End user). Tällöin kummatkin pääsevät ainoastaan vaihtamaan salasanan, jättämään pääkäyttäjälle pyynnön saada käyttö-oikeus tiettyyn järjestelmän sekä näkemään kumpiekin tämän hetkiset oikeudet järjestelmiin ilman mahdollisuutta muokata niitä.

Teimme tämän seuraavanlaisesti:

1. midPointin vasemmasta valikosta valittiin ```Users -> List users```
 
2. Käyttäjälistauksesta valittiin haluttu käyttäjä.

3. Valittiin välilehdestä "Assignments".
 
4. Seuraavaksi painettiin vihreää nappia.
 
5. Avautui "Select object(s)" -ikkuna. Valitsimme listasta henkilökohtainen ryhmä nimeltään "End user" ja painettiin listan lopusta "Add" -painiketta.
 
6. Katsottiin että "Options" -kohdassa on samat valittuna mitä kuvan kohdassa 1. Lopuksi valittiin "Save" (2.). Nyt käyttäjälle oli määritetty oikeanlaiset käyttöoikeudet midPointin käyttöliittymään.

    ![](https://raw.githubusercontent.com/Eetu95/Open-source-IdM-solution/master/Kuvat/Testaus/Screenshot%20(10).png)
    <br>
    Kuva 139: Ruudunkaappaus kohdasta.
    <br>
    <br> 
     
<br>

<h3 id="havaintoja-testauksesta">5.6. Havaintoja testauksesta</h3>
 
Kaikkiin haluttuihin järjestelmiin pääsi kirjautumaan sisälle määritellyillä oikeuksilla lukuun ottamatta Active Directory. Siinä emme kerenneet aikataulullisista syistä tekemään roolia, joka tekee järjestelmänvalvojan tunnukset joten AD:lle määrittyy ainoastaan käyttäjä perusoikeuksilla. 

Jos nimessä on ääkkösiä, ne eivät näy nimessä LDAP-käyttäjien osalta. Tämä siksi, koska OpenLDAP:n "gecos" -määritys ei salli ääkkösiä.

Kokeilimme käyttäjätunnuksen jäädytyksen vaikutuksia kohdejärjestelmin kirjautumisiin. Jäädytimme Ulla Niemisen tunnukset menemällä midPointin vasemmassa valikosta valitsemalla ```Users -> List users```. Etsimme käyttäjälistauksesta Ullan ja painoimme alinapista (1.) ja valitsimme "Disable" (2.). 

![](https://raw.githubusercontent.com/Eetu95/Open-source-IdM-solution/master/Kuvat/Testaus/Screenshot%20(11).png)
<br>
Kuva 140: Ruudunkaappaus listasta.
<br>
<br> 
 
Jäädyttämisen jälkeen kirjautuminen TESTIPALVELIN -palvelimeen ja TESTIPC1:seen ei onnistunut, kirjautuminen TESTIPC2:seen kuitenkin onnistui. Tämä siksi, koska OpenLDAP:ssa ei ole tunnusten jäädytysmahdollisuutta. Tämä ongelma on myös midPointin kehittäjän <a href="https://wiki.evolveum.com/display/midPoint/LDAP+Servers+Summary">Evolveumin tiedossa.</a> Tässä tapauksessa kannattaa poistaa käyttäjältä OpenLDAP:n roolit kohdasta "Assignments". ei myöskään pääse kirjautumaan jäädytyksen jälkeen sisälle.
 
<br>

<h3 id="lokitus">6. Lokitus</h3>
 
Seuraavaksi tutkimme midPointin lokitusta.
 
<br>

<h4 id="eclipse-midPoint-log-viewer">6.1. Log Viewer</h4>

MidPoint on kehittänyt työkalun nimeltä <a href="https://wiki.evolveum.com/display/midPoint/Log+Viewer">"Log Viewer"</a>, jolla pystyy helposti tutkimaan suuria lokitiedostoja. Log Viewer on Eclipse plugini, joka näyttää loki tiedostot hyvin järjestettynä, käyttämällä Eclipse "Outline" ja "Problems" näkymiä.

Eclipse midPoint Log Viewerin ominaisuuksiin kuuluu mm. "Showing log outline", "Showing error, warning and information messages", "Folding (collapse + expand)", "Permanently removing unnecessary lines", "Objects and threads dictionary", "OID highlighting and associated information display", "Logfile preprocessing: LogTrimmer tool", "Logfile erasing: Tuncater tool", "Performance tuning".
 
<br>

<h4 id="audit-log-viewer">6.2. Audit Log Viewer</h4>

![Audit Log Viewer](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/midPoint%20lokit/Audit_Log_Viewer1.PNG?raw=true)
<br>
Kuva 141: Audit Log Viewer.
<br>
<br>

MidPointista löytyy "Audit Log Viewer" -näkymä, jossa näkee kaikki midPointin lokit. Lokeja pystyy suodattamaan mm. ajakajakson, tapahtumatyypin, kohteen, aloittajan yms. mukaan.

![Audit Log Viewer](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/midPoint%20lokit/Audit_Log_Viewer2.PNG?raw=true)
<br>
Kuva 142: Audit Log Viewer.
<br>
<br>

Lokit voi avata, jolloin niistä saa  tarkempaa tietoa. Mm. Timestamp, Event identifier, Event Type, Event Stage, Initiator, Target ref., Outcome, Session Identifier, Resource name, Object Name, Execution result jne.

Lokeista näkyy mm. käyttäjien luonnit/poistamiset, roolien lisäykset, tehtävänannot, istunnot jne.
 
<br>
 
<h3 id="yhteenveto">7. Yhteenveto</h3>

Projekti oli mielestämme haastava omiin taitotasoihimme nähden. Opimme paljon IdM-järjestelmän toiminnallisuuksista ja sen toteutuksesta. IdM-järjestelmät ennen projektia olivat tuttuja vain pintapuolisesta aiemman työkokemuksen kautta muutamalle projektiryhmän jäsenelle. Jokainen projektiryhmän jäsen käytti projektin tekoon noin 170 tuntia. Projektin suunnittelua ei otettu huomioon. Projekti lähti vauhdikkaasti liikkeelle aluksi eri avoimen lähdekoodin IdM-järjestelmien vertailuissa. Kun saimme valittua parhaimman IdM-järjestelmän eli midPointin vertailujen perusteella, niin projektin tahti hidastui. IdM-järjestelmän toteutuksessa ja connectoreiden liittämisessä midPoint järjestelmään tuotti lukuisia ongelmia. Osasyynä tähän oli muun muassa midPointin kehittäjän dokumentaation laadun sekä ajantasaisuuden puute. Ongelmatilanteisiin saimme apua etsimällä tietoa Internetistä sekä jossakin määrin midPointin postituslistalta. Emme mielestämme ehtineet saada kaikkea irti midPoint IdM-järjestelmästä, mitä olimme suunnitelleet, koska suuri osa ajasta kului ongelmien ratkaisemiseen. Esimerkiksi Active Directory connector ei toimi vieläkään odotetulla tavalla, mutta toimii kuitenkin riittävissä määrin. On vaikea sanoa, jos olisimme valinneet toisen IdM-järjestelmä midPointin sijaan, niin olisiko toteutus ollut vaivattomampaa. Projektin alkuvaiheessa kokeilimme rinnakkain midPoint ja Apache Syncope IdM-järjestelmiä, mutta päädyimme lopulta midPoint IdM-järjestelmää, koska se tuki enemmän ominaisuuksia. Apache Syncope vaikutti jossakin määrin helpommalta toteuttaa, mutta ilman ongelmia ei olisi siitäkään selvitty.

Projektia varten Haaga-Helia tarjosi meille fyysiset palvelinkoneet Servulasta, joita saimme käyttää vapaasti. Kaikki projektissa käyttämämme resurssit saimme ilmaiseksi ja käytimme Ubuntu Server 16.04.5 LTS, Ubuntu Desktop 16.04.5 LTS & 18.04.1 LTS, Windows Server 2016 Datacenter ja Windows 10 Pro -käyttöjärjestelmiä. Kaikki käyttöjärjestelmäversiot olivat 64-bittisiä. Testasimme aina aluksi midPoint -järjestelmää virtuaaliympäristössä, jonka jälkeen toteutimme saman fyysiselle palvelinkoneelle. Projektissa käyttämämme midPoint IdM-järjestelmä on yrityskäyttöön. MidPointin kehittäjän mukaan järjestelmä soveltuu hyvinkin suurelle yritykselle (jopa 100 000 käyttäjää). Mielestämme midPointissa on potentiaalia soveltua yrityksen IdM-järjestelmäksi, mutta riippuen yrityksen koosta midPoint IdM-järjestelmän ylläpitäminen vaatisi monia työntekijöitä, koska projektin perusteella midPoint IdM-järjestelmä ei vaikuta kovin yksinkertaiselta ja helpolta käyttää. Saimme projektin aikana suojattua kaikki yhteydet midPoint IdM-järjestelmän ja connectoreiden välillä (Unix/Linux, Active Directory, OpenLDAP) itseallekirjoitetulla SSL-sertifikaatilla. Jos halutaan muussa kuin kokeilumielessä käyttää midPoint IdM-järjestelmää niin silloin tulisi ostaa virallinen SSL-sertifikaatti. Myös verkkotunnus on järkevää hankkia, jotta midPointin osoite on helppo muistaa. Kaikin puolin projekti midPoint IdM-järjestelmän oli jokaiselle projektiryhmän jäsenelle erittäin opettavainen, josta on varmasti hyötyä myös tulevaisuudessa.

![Järjestelmäkartta](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/midPoint/J%C3%A4rjestelm%C3%A4kartta.jpg?raw=true)
<br>
Kuva 143: Järjestelmäkartta projektista.
<br>
<br>

 
<h3 id="lahteet">8. Lähteet</h3>
 
Ask Ubuntu. 2016. How to find path to java?. Luettavissa: <a href="https://askubuntu.com/questions/772235/how-to-find-path-to-java">https://askubuntu.com/questions/772235/how-to-find-path-to-java</a>. Luettu: 29.10.2018

Ask Ubuntu. 2017. OpenLDAP error configuring StartTLS: ldap_modify: Other (e.g., implementation specific) error (80). Luettavissa: <a href="https://askubuntu.com/questions/936382/openldap-error-configuring-starttls-ldap-modify-other-e-g-implementation-sp">https://askubuntu.com/questions/936382/openldap-error-configuring-starttls-ldap-modify-other-e-g-implementation-sp</a>. Luettu: 14.11.2018.

Chandrasekaran, R. 2017. Step by Step Guide to Setup LDAPS on Windows Server. Luettavissa: <a href=https://blogs.msdn.microsoft.com/microsoftrservertigerteam/2017/04/10/step-by-step-guide-to-setup-ldaps-on-windows-server/>https://blogs.msdn.microsoft.com/microsoftrservertigerteam/2017/04/10/step-by-step-guide-to-setup-ldaps-on-windows-server/</a>. Luettu 5.11.2018.

cyberciti.biz. 2017. How to see/get a list of MySQL/MariaDB users accounts. Luettavissa: <a href=https://www.cyberciti.biz/faq/how-to-show-list-users-in-a-mysql-mariadb-database/>https://www.cyberciti.biz/faq/how-to-show-list-users-in-a-mysql-mariadb-database/</a>. Luettu 10.10.2018.
 
Ellingwood, J. 2014. How To Create a SSL Certificate on Apache for Ubuntu 14.04. Luettavissa: <a href="https://www.digitalocean.com/community/tutorials/how-to-create-a-ssl-certificate-on-apache-for-ubuntu-14-04">https://www.digitalocean.com/community/tutorials/how-to-create-a-ssl-certificate-on-apache-for-ubuntu-14-04</a>. Luettu: 14.11.2018.
 
Ellingwood, J. 2014. How To Encrypt OpenLDAP Connections Using STARTTLS. Luettavissa: <a href="https://www.digitalocean.com/community/tutorials/how-to-encrypt-openldap-connections-using-starttls">https://www.digitalocean.com/community/tutorials/how-to-encrypt-openldap-connections-using-starttls</a>. Luettu: 14.11.2018.

Evolveum. 2017. How to connect a Resource in midPoint 3.6. Luettavissa: <a href="https://www.youtube.com/watch?v=HBYZpZ22fDo">https://www.youtube.com/watch?v=HBYZpZ22fDo</a>. Luettu 29.10.2018.

Gnome. 2018. Disable the user list. Luettavissa: <a href="https://help.gnome.org/admin/system-admin-guide/stable/login-userlist-disable.html.en">https://help.gnome.org/admin/system-admin-guide/stable/login-userlist-disable.html.en</a>. Luettu: 21.11.2018.

Heddings, L. 2006. Change Ubuntu Server from DHCP to a Static IP Address. Luettavissa: <a href=https://www.howtogeek.com/howto/ubuntu/change-ubuntu-server-from-dhcp-to-a-static-ip-address/>https://www.howtogeek.com/howto/ubuntu/change-ubuntu-server-from-dhcp-to-a-static-ip-address/</a>. Luettu 5.10.2018.
 
Hoffman, C. 2012. How To Customize Ubuntu’s Message of the Day. Luettavissa: <a href="https://www.howtogeek.com/104708/how-to-customize-ubuntus-message-of-the-day/">https://www.howtogeek.com/104708/how-to-customize-ubuntus-message-of-the-day/</a>. Luettu: 8.10.2018.
 
Horsfall, D. 2007. Re: Listening on multiple ports for openldap 2.3.33. Luettavissa: <a href="https://www.openldap.org/lists/openldap-software/200702/msg00196.html">https://www.openldap.org/lists/openldap-software/200702/msg00196.html</a>. Luettu: 14.11.2018.
 
HowtoForge. 2018. Managing a Headless VirtualBox Installation with phpvirtualbox (Ubuntu 16.04 LTS). Luettavissa: <a href="https://www.howtoforge.com/tutorial/managing-a-headless-virtualbox-installation-with-phpvirtualbox-on-ubuntu-16.04/">https://www.howtoforge.com/tutorial/managing-a-headless-virtualbox-installation-with-phpvirtualbox-on-ubuntu-16.04/</a>. Luettu: 29.10.2018. 
 
Httpd Wiki. 2017. Redirect Request to SSL. Luettavissa: <a href="https://wiki.apache.org/httpd/RedirectSSL">https://wiki.apache.org/httpd/RedirectSSL</a>. Luettu: 14.11.2018.
 
Huculak, M. 2017. How to create a Linux virtual machine on Windows 10 using Hyper-V. Luettavissa: <a href="https://www.windowscentral.com/how-run-linux-distros-windows-10-using-hyper-v">https://www.windowscentral.com/how-run-linux-distros-windows-10-using-hyper-v</a>. Luettu: 31.10.2018.
 
KnowITFree, 2017. How to add a new schema to openLDAP 2.4. Katsottavissa: <a href="https://www.youtube.com/watch?v=qAedVMMunk8">https://www.youtube.com/watch?v=qAedVMMunk8</a>. Katsottu: 2.11.2018.

LinOxide. 2018. How to Hide Grub Menu in Boot of your Linux Machine. Luettavissa: <a href="https://linoxide.com/linux-how-to/hide-grub-boot-linux/">https://linoxide.com/linux-how-to/hide-grub-boot-linux/</a>. Luettu: 8.10.2018.
 
Lumina Networks. 2017. Installing Zip and Unzip for Ubuntu. Luettavissa: <a href="https://www.luminanetworks.com/docs-lsc-610/Topics/SDN_Controller_Software_Installation_Guide/Appendix/Installing_Zip_and_Unzip_for_Ubuntu_1.html">https://www.luminanetworks.com/docs-lsc-610/Topics/SDN_Controller_Software_Installation_Guide/Appendix/Installing_Zip_and_Unzip_for_Ubuntu_1.html</a>. Luettu: 26.10.2018.
 
Microsoft. 2016. Install the Hyper-V role on Windows Server. Luettavissa: <a href="https://docs.microsoft.com/en-us/windows-server/virtualization/hyper-v/get-started/install-the-hyper-v-role-on-windows-server">https://docs.microsoft.com/en-us/windows-server/virtualization/hyper-v/get-started/install-the-hyper-v-role-on-windows-server</a>. Luettu: 31.10.2018.

monline. 2012. How to configure phpLDAPadmin to connect to an LDAP server via SSL (ie. ldaps). Luettavissa: <a href="http://muzso.hu/2012/03/29/how-to-configure-phpldapadmin-to-connect-to-an-ldap-server-via-ssl-ie.-ldaps">http://muzso.hu/2012/03/29/how-to-configure-phpldapadmin-to-connect-to-an-ldap-server-via-ssl-ie.-ldaps</a>. Luettu: 14.11.2017.

Mounir, N. 2017. How to create a domain on Windows Server. Luettavissa: <a href=https://win10faq.com/create-domain-windows-server/>https://win10faq.com/create-domain-windows-server/</a>. Luettu 22.10.2018.
 
Nissinen, M. 2018. AVOIMEN LÄHDEKOODIN IDM-JÄRJESTELMÄN VERTAILU (6/7). Luettavissa: <a href="https://opensourceidm.wordpress.com/2018/10/03/avoimen-lahdekoodin-idm-jarjestelman-vertailu-3/">https://opensourceidm.wordpress.com/2018/10/03/avoimen-lahdekoodin-idm-jarjestelman-vertailu-3/</a>. Luettu: 3.10.2018.

Noris, I. 2016. LDAP PosixAccount and PosixGroup Management. Luettavissa: <a href="https://wiki.evolveum.com/display/midPoint/LDAP+PosixAccount+and+PosixGroup+Management#LDAPPosixAccountandPosixGroupManagement-Setup">https://wiki.evolveum.com/display/midPoint/LDAP+PosixAccount+and+PosixGroup+Management#LDAPPosixAccountandPosixGroupManagement-Setup</a>. Luettu: 9.11.2018.

Noris, I. 2017. MariaDB. Luettavissa: <a href=https://wiki.evolveum.com/display/midPoint/MariaDB>https://wiki.evolveum.com/display/midPoint/MariaDB</a> Luettu: 10.10.2018.

Oracle. 2018. Download VirtualBox. Luettavissa. <a href="https://www.virtualbox.org/wiki/Downloads">https://www.virtualbox.org/wiki/Downloads</a>. Luettu: 29.10.2018.
 
Parttimaa, J. 2018. AVOIMEN LÄHDEKOODIN IDM-JÄRJESTELMÄN VERTAILU (4/7). Luettavissa: <a href="https://opensourceidm.wordpress.com/2018/10/03/avoimen-lahdekoodin-idm-jarjestelman-vertailu-4-7/">https://opensourceidm.wordpress.com/2018/10/03/avoimen-lahdekoodin-idm-jarjestelman-vertailu-4-7/</a>. Luettu: 3.10.2018.
 
Papiernik, M. 2017. How To Use Apache as a Reverse Proxy with mod_proxy on Ubuntu 16.04. Luettavissa: <a href="https://www.digitalocean.com/community/tutorials/how-to-use-apache-as-a-reverse-proxy-with-mod_proxy-on-ubuntu-16-04">https://www.digitalocean.com/community/tutorials/how-to-use-apache-as-a-reverse-proxy-with-mod_proxy-on-ubuntu-16-04</a>. Luettu: 14.11.2018.

Patankar, M. 2017. SHA-256 Self Signed Certificate for Windows Server 2012 R2. Luettavissa: <a href=https://blogs.msdn.microsoft.com/mayurpatankar/2017/09/01/sha-256-self-signed-certificate-for-windows-server-2012-r2/>https://blogs.msdn.microsoft.com/mayurpatankar/2017/09/01/sha-256-self-signed-certificate-for-windows-server-2012-r2/</a>. Luettu 9.11.2018.

Raj. 2017. Configure LDAP Client on Ubuntu 16.04 / Debian 8. Luettavissa: <a href="https://www.itzgeek.com/how-tos/linux/ubuntu-how-tos/configure-ldap-client-on-ubuntu-16-04-debian-8.html">https://www.itzgeek.com/how-tos/linux/ubuntu-how-tos/configure-ldap-client-on-ubuntu-16-04-debian-8.html</a>. Luettu: 21.11.2018.
 
Semancik, R. 2017. Trying MidPoint. Luettavissa: <a href="https://wiki.evolveum.com/display/midPoint/Trying+MidPoint">https://wiki.evolveum.com/display/midPoint/Trying+MidPoint</a>. Luettu: 1.10.2018.

Semancik, R. 2018. Practical Identity
Management with midPoint. Luettavissa: <a href=https://evolveum.com/wp-content/uploads/2018/04/practical-idm-with-midpoint-1.1.pdf>https://evolveum.com/wp-content/uploads/2018/04/practical-idm-with-midpoint-1.1.pdf</a>. Luettu 29.10.2018. 

Semancik, R. 2018. Active Directory with LDAP connector. Luettavissa: <a href="https://wiki.evolveum.com/display/midPoint/Active+Directory+with+LDAP+connector#ActiveDirectorywithLDAPconnector-RecommendedConnector">https://wiki.evolveum.com/display/midPoint/Active+Directory+with+LDAP+connector#ActiveDirectorywithLDAPconnector-RecommendedConnector</a>. Luettu: 2.11.2018.

SK. 2015. Install OpenLDAP In Ubuntu 15.10 And Debian 8. Luettavissa: <a href="https://www.unixmen.com/install-openldap-in-ubuntu-15-10-and-debian-8/">https://www.unixmen.com/install-openldap-in-ubuntu-15-10-and-debian-8/</a>. Luettu: 31.10.2018.
 
Ubuntu Documentation. 2018. OpenLDAP Server. Luettavissa: <a href="https://help.ubuntu.com/lts/serverguide/openldap-server.html.en">https://help.ubuntu.com/lts/serverguide/openldap-server.html.en</a>. Luettu: 31.10.2018.
 
Vultr.com. 2015. Setting an SSH Motd on Ubuntu 14.04. Luettavissa: <a href="https://www.vultr.com/docs/setting-an-ssh-motd-on-ubuntu-14-04">https://www.vultr.com/docs/setting-an-ssh-motd-on-ubuntu-14-04</a>. Luettu: 8.10.2018.

Wallem, J. 2017. How to install OpenLDAP and phpLDAPadmin on Ubuntu 16.04. Luettavissa: <a htef="https://www.techrepublic.com/article/how-to-install-openldap-and-phpldapadmin-on-ubuntu-16-04/">https://www.techrepublic.com/article/how-to-install-openldap-and-phpldapadmin-on-ubuntu-16-04/"></a>. Luettu: 31.10.2018.
 
Wallen, J. 2016. How to install phpVirtualBox for cloud-based VirtualBox management. Luettavissa: <a href="https://www.techrepublic.com/article/how-to-install-phpvirtualbox-for-cloud-based-virtualbox-management/">https://www.techrepublic.com/article/how-to-install-phpvirtualbox-for-cloud-based-virtualbox-management/</a>. Luettu: 31.10.2018.
 
Wallen, J. 2018. How to install phpLDAPadmin on Ubuntu 18.04. Luettavissa: <a href="https://www.techrepublic.com/article/how-to-install-phpldapadmin-on-ubuntu-18-04/">https://www.techrepublic.com/article/how-to-install-phpldapadmin-on-ubuntu-18-04/</a>. Luettu: 31.10.2018.

Wallen, J. 2016. How to populate an LDAP server with users and groups via phpLDAPadmin. Luettavissa: <a href="https://www.techrepublic.com/article/how-to-populate-an-ldap-server-with-users-and-groups-via-phpldapadmin/">https://www.techrepublic.com/article/how-to-populate-an-ldap-server-with-users-and-groups-via-phpldapadmin/</a>. Luettu: 31.10.2018.
 
weichbrodt.me. 2018. Install and configure OpenLDAP on Debian 8 (Jessie). Luettavissa: <a href="https://weichbrodt.me/tutorial:ldap:installopenldap">https://weichbrodt.me/tutorial:ldap:installopenldap</a>. Luettu: 31.10.2018.
 
!robot. 2018. Manage Headless VirtualBox Host On Ubuntu 16.04 LTS With PhpVirtualBox, Apache2 And PHP 7.1. Luettavissa: <a href="https://websiteforstudents.com/manage-headless-virtualbox-host-on-ubuntu-16-04-lts-with-phpvirtualbox-apache2-and-php-7-1/">https://websiteforstudents.com/manage-headless-virtualbox-host-on-ubuntu-16-04-lts-with-phpvirtualbox-apache2-and-php-7-1/</a>. Luettu: 29.10.2018.
 
!robot. 2018. VirtualBox 5.2 On Ubuntu 16.04 LTS Server (Headless). Luettavissa: <a href="https://websiteforstudents.com/virtualbox-5-2-on-ubuntu-16-04-lts-server-headless/">https://websiteforstudents.com/virtualbox-5-2-on-ubuntu-16-04-lts-server-headless/</a>. Luettu: 29.10.2018.
