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
                <span>4.1.2.3. </span><a href="#openldap-serverin-asennus-hyper-vn-virtuaalipalvelimeen">OpenLDAP serverin asennus Hyper-V:n virtuaalipalvelimeen</a><br>
                <span>4.1.2.4. </span><a href="#phpLDAPadmin-web-kayttoliittyman-asennus-ja-konfigurointi">phpLDAPadmin -web-käyttöliittymän asennus ja konfigurointi</a><br>
                <span>4.1.2.5. </span><a href="#suojatun-yhteyden-maaritys">Suojatun yhteyden määritys</a><br>
          </ol>
          <span>4.1.3. </span><a href="#virtualbox-palvelimen-asennus-ja-konfigurointi-vmserver-keskusyksikkoon">VirtualBox -palvelimen asennus ja konfigurointi "VMSERVER" -keskusyksikköön</a><br>
          <ol>
                <span>4.1.3.1. </span><a href="#phpVirtualbox-web-kayttöliittyman-asennus-ja-konfigurointi">phpVirtualbox -web-käyttöliittymän asennus ja konfigurointi</a><br>
                <span>4.1.3.2. </span><a href="#suojatun-yhteyden-maaritys">Suojatun yhteyden määritys</a><br>
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
          <span>4.3.3. </span><a href="#suojatun-yhteyden-konfigurointi">Suojatun yhteyden konfigurointi</a><br>
      </ol>
      </ol>
 <span>5. </span><a href="#testaus">Testaus</a><br>
 <span>6. </span><a href="#yhteenveto">Yhteenveto</a><br>
 <span>7. </span><a href="#lahteet">Lähteet</a><br>
</ol>

<h2 id="johdanto">Johdanto</h2>
 
Tässä raportissa kerromme kuinka avoimen lähdekoodiin perustuvan Identiteetinhallintajärjestelmän saa käyttöön (asennus ja määritys) sekä kuinka sillä voidaan hallita Unix/Linux -palvelien, OpenLDAP-palvelimen sekä Windows -domainin käyttäjiä. Käytämme projektissa Evolveumin "midPoint" nimistä avoimen lähdekoodin identiteetinhallintajärjestelmää.

Käynnistimme projektin kyseisestä aiheesta, koska muutamat projektiryhmän jäsenet ovat työssään joutuneet tekemään
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


<h2 id="yleista-idm-jarjestelmista-identity-management-system">Yleistä IdM-järjestelmistä (Identity Management System)</h2>
 
IdM-järjestelmä (Englanniksi: Identity Management System, Suomeksi: Identiteetinhallintajärjestelmä) on järjestelmä, jonka avulla voidaan keskitetysti hallita yrityksen eri tietojärjestelmiä, palveluita, tietokantoja, ohjelmistoja sekä ohjelmien käyttöoikeuksia että pääsynhallintaa. IdM:n ansiosta yritys pystyy helposti pitämään huolen siitä ketkä työntekijät pääsevät käyttämään mitäkin tietojärjestelmiä sekä palveluita ja ketkä taas eivät. IdM-järjestelmiä on hyvin erilaisia ja hyvin erilaisina kokonaisuuksina.

![](https://raw.githubusercontent.com/Eetu95/Open-source-IdM-solution/master/Kuvat/IdM_esimerkki.jpg)
Kuva 1: Havainnollistava esimerkki Indentiteetinhallintajärjestelmästä (IdM)
 
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


<h2 id="idm-jarjestelmien-vertailu">IdM-järjestelmien vertailu</h2>

Etsimme ensin Googlettamalla avoimen lähdekoodin IdM-järjestelmiä. Otimme vertailuun seuraavat, joita löysimme:
<li><a href="https://syncope.apache.org/">Apache Syncope</a></li>
<li><a href="https://evolveum.com/midpoint/">MidPoint</a></li>
<li><a href="https://backstage.forgerock.com/docs/idm">OpenIDM</a></li>
<li><a href="http://www.soffid.com/">Soffid</a></li>
<li><a href="https://www.keycloak.org/">Keycloak</a></li>
<li><a href="http://www.unity-idm.eu/">Unity</a></li>
<li><a href="https://www.openiam.com/">OpenIAM</a></li>
<li><a href="https://www.shibboleth.net/">Shibboleth</a></li>
<li><a href="https://wso2.com/identity-and-access-management/">WSO2 Identity Server</a></li>
<li><a href="https://www.gluu.org/">Gluu</a></li>
<li><a href="http://www.josso.org/install.html">Josso</a></li>
<li><a href="https://www.freeipa.org/page/Main_Page">FreeIPA</a></li>
<li><a href="http://aerobase.org/">Aerobase</a></li>


<br>


<h3 id="idm-jarjestelmien-dokumentaatiot">IdM-järjestelmien dokumentaatiot</h3>
 
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


<h3 id="avoimen-lahdekoodin-idm-jarjestelmien-valintakriteerit">Avoimen lähdekoodin IdM-järjestelmien valintakriteerit</h3>

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

<a href="https://trends.google.fi/trends/explore?date=2016-09-01%202018-09-01&q=keycloak,josso,wso2%20identity%20server,gluu%20server,freeipa">Kaavio kahden vuoden ajalta:</a>

![trends_2v_vertailu_SUOSITUIMMAT_keycloak_josso_wso2identityserver_gluuserver_freeipa](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Trends/trends_2v_vertailu_SUOSITUIMMAT_keycloak_josso_wso2identityserver_gluuserver_freeipa.PNG?raw=true)

<a href="https://trends.google.fi/trends/explore?date=all&q=keycloak,josso,wso2%20identity%20server,gluu%20server,freeipa">Kaavio koko ajalta:</a>

![trends_kokoaika_vertailu_SUOSITUIMMAT_keycloak_josso_wso2identityserver_gluuserver_freeipa](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Trends/trends_kokoaika_vertailu_SUOSITUIMMAT_keycloak_josso_wso2identityserver_gluuserver_freeipa.PNG?raw=true)

Etsimme myös tietoa Amazonista ja Safari Books Onlinesta mm. kuinka monta kirjaa kustakin järjestelmästä on kirjoitettu. Suurimmasta osasta IdM-järjestelmistä ei löytynyt julkaistuja kirjoja. IdM-järjestelmät, joista löytyi julkaistuja kirjoja olivat: OpenIDM (Amazon), Keycloak (Safari), Shibboleth (Safari), WSO2 Identity Server (Safari) ja Josso (Safari).

Lisäsimme vertailuumme löytämämme uuden avoimen lähdekoodin IdM-järjestelmän nimeltä Grouper: <a href="https://www.internet2.edu/products-services/trust-identity/grouper/#service-overview">https://www.internet2.edu/products-services/trust-identity/grouper/#service-overview</a>

<li>Dokumentaatio löytyy osoitteesta: <a href="https://spaces.at.internet2.edu/display/TI/TI.25.1">https://spaces.at.internet2.edu/display/TI/TI.25.1</a></li>

<li>Muutamat ulkomaiset yliopistot käyttävät Grouper IdM-järjestelmää: <a href="https://idm.unl.edu/grouper">https://idm.unl.edu/grouper</a></li>

Etsimme muita referenssejä vertailun kohteena oleville avoimen lähdekoodin IdM-järjestelmille. Löydettiin myös suomalaisia yrityksiä ja järjestöjä, jotka käyttävät joitakin vertailussamme olevista IdM-järjestelmistä. Löydettiin mm. että <a href="http://www.tirasa.net/customer/university-of-helsinki.html">Helsingin Yliopisto käyttää Apache Syncopea</a>

<h3 id="alustavat-vaatimukset">Alustavat vaatimukset</h3>

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

<h3 id="vertailu-ja-aputaulukko">Vertailu- ja aputaulukko</h3>

![vertailutaulukko](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Vertailu/vertailutaulukko.jpg?raw=true)

Tässä vertailutaulukossa näkyy vertaulumme varsinainen tulos ja se miten päädyimme valintaan. Huom! Jotkin vaatimukset ovat kriittisempiä kuin toiset, joka johtaa kriittisemmän vaatimuksen täyttävän järjestelmän suosimiseen. Lataa PDF <a href="https://opensourceidm.files.wordpress.com/2018/10/vertailutaulukko.pdf">tästä</a>.
<br>
<br>
![aputaulukko](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Vertailu/aputaulukko.jpg?raw=true)

Aputaulukko selventää vertailutaulukon lukua. Lataa PDF <a href="https://opensourceidm.files.wordpress.com/2018/10/aputaulukko.pdf">tästä</a>.

<h2 id="midpoint">Midpoint</h2>

Vertailtuamme IdM-järjestelmiä ja kriteereidemme perusteella eniten ominaisuuksia ja pisteitä omisti midPoint IdM-järjestelmä kuin mikään muu IdM-järjestelmä, mistä syystä päädyimme juuri tähän järjestelmään. Vahvaksi toiseksi ehdokkaaksi valiutui Apache Syncope, joka muuten midPointin kanssa sisälsi melkein identtiset ominaisuudet kuin midPoint, mutta midPoint IdM-järjestelmä tuki enemmän muita järjestelmiä ja rajapintoja. Järjestelmät ja rajapinnat, joita midPoint tukee ovat:
<li>Active Directory
<li>Unix/Linux
<li>Office365
<li>Google Apps
<li>SAP
<li>Box
<li>Drupal
<li>Atlassian ohjelmat (JIRA, Nitbucket, Confluence)
<li>Lotus Notes
<li>tietokannat
<li>LDAP
<li>CSV

Tosin kaikissa connectoreissa ja rajapinnoissa käyttäjätietojen synkronointi ei valmistajan mukaan toimi esimerkiksi Atlassian tuotteiden ja Oraclen kanssa. Omien connectoreiden teko on myös mahdollista midPontissa. Tämän projektin aikana kokeilimme Active Directory, Unix/Linux, LDAP ja CSV connectoreita.
 
<h3 id="esivalmistelut">Esivalmistelut</h3>

Valittuamme midPoint IdM-järjestelmän ryhdyimme tekemään esivalmisteluja IdM-järjestelmää varten. Tarkoituksena oli, että kokeilemme mahdollisimman montaa connectoria. Tätä varten tarvitsimme sekä Linux että Windows käyttöjärjestelmillä varustetut työasemat. Aluksi aina kokeilimme midPointin käyttöä sekä työasemien asennusta ja konfigurointia virtuaaliympäristössä. Käytössämme oli Oracle VM VirtualBox, jonne loimme virtuaalikoneita testauksia varten. Myöhemmin kuitenkin teimme samat muutokset fyysisellä työasemalla, johon midPoint IdM-järjestelmä asennettiin, kun virtuaaliympäristössä saatiin haluttu lopputulos toimimaan. 

Projektia tehdessämme tarvitsimme seuraavan laitteistokokoonpanon:
<li>Kolme (3) keskusyksikköä</li>
<li>Neljä (4) virtuaalista tietokonetta</li>

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
| TESTIPC1 | Windows 10 (64-bit) | 1 | 2048 Mt | 50 Gt | 128 Mt |
|TESTIPALVELIN | Ubuntu Server 16.04.5 LTS (64-bit) | 1 | 1024 Mt | 10 Gt | 16 Mt |  
 
Tämän lisäksi asenamme Windows -palvelimeen OpenLDAP -virtuaalipalvelimen Hyper-V:n kautta. Käyttöjärjestelmältään se on myös Ubuntu Server 16.04.5 LTS (64-bit).
 

<h4 id="ubuntu-server-asennus-ja-konfigurointi-midpointidm-keskusyksikkoon">Ubuntu Server asennus ja konfigurointi "MIDPOINTIDM" -keskusyksikköön</h4>

Ensimmäisenä esivalmisteluvaiheena oli Linux palvelimen käyttöjärjestelmän asennus ja konfigurointi. MidPoint järjestelmä asennetaan tähän käyttöjärjestelmään. Valitsimme palvelimeksi Ubuntu Server 16.04.5 LTS 64-bittisen version. Asensimme käyttöjärjestelmän fyysiselle tietokoneelle USB-livetikun avulla. Valitsimme tietokoneesta käynnistystavaksi USB boottauksen, jolloin pääsimme asentamaan käyttöjärjestelmää. 

![käyttöjärjestelmän kielen valinta](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Ubuntu%20Server%2016.04.5%20LTS%20asennuksen%20ruutukaappaukset/Vaihe%20(01).png?raw=true)

Heti ensimmäiseksi ”USB-boottauksen” jälkeen ja kun tuli asennusruutu näkyviin, painoimme F2:sta (1.) ja valitsimme käyttöjärjestelmän kieleksi englannin (2.). Hyväksyimme valinnan painamalla Enter.

![näppäimistön kieli](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Ubuntu%20Server%2016.04.5%20LTS%20asennuksen%20ruutukaappaukset/Vaihe%20(02).png?raw=true)

Tämän jälkeen painoimme F3:sta (1.) ja valitsimme näppäimistön kieleksi suomen (2.). Hyväksyimme valinnan painamalla Enter.

![ubuntu server asennus](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Ubuntu%20Server%2016.04.5%20LTS%20asennuksen%20ruutukaappaukset/Vaihe%20(03).png?raw=true)

Aloitimme tänän jälkeen asennuksen valitsemalla ”Install Ubuntu Server” nuolinäppäimillä ja hyväksymällä valinnan painamalla Enter.

![palvelimen kieli](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Ubuntu%20Server%2016.04.5%20LTS%20asennuksen%20ruutukaappaukset/Vaihe%20(04).png?raw=true)

Avautui ohjattu asennus. Valitsimme nuolinäppäimillä palvelimen kieleksi englannin eli ”English”. Hyväksyimme valinnan painamalla Enter.

![sijainti](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Ubuntu%20Server%2016.04.5%20LTS%20asennuksen%20ruutukaappaukset/Vaihe%20(05).png?raw=true)

Seuraavassa kohdassa piti valita sijainti. Koska sijaintimme on Suomi, valitsimme ”other”. Jatkoimme eteenpäin painamalla Enter.

![sijainti_europe](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Ubuntu%20Server%2016.04.5%20LTS%20asennuksen%20ruutukaappaukset/Vaihe%20(06).png?raw=true)

Sitten valitsimme ”Europe”. Hyväksyimme sen painamalla Enter.

![sijainti_finland](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Ubuntu%20Server%2016.04.5%20LTS%20asennuksen%20ruutukaappaukset/Vaihe%20(07).png?raw=true)

Lopulta valitsimme "Finland". Hyväksyimme tämänkin painamalla Enter.

![näppäimistön kieli_UTF-8](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Ubuntu%20Server%2016.04.5%20LTS%20asennuksen%20ruutukaappaukset/Vaihe%20(08).png?raw=true)

Koska valitsemamme maa ja kieli eivät muka sopineet yhteen, jouduimme valitsemaan ”United States – en_US.UTF-8”. Hyväksyimme valinnan painamalla Enter.

![hostname](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Ubuntu%20Server%2016.04.5%20LTS%20asennuksen%20ruutukaappaukset/Vaihe%20(09).png?raw=true)

Annoimme järjestelmän hostnameksi ”MIDPOINTIDM” (1.). Jatkoimme tämän jälkeen eteenpäin valitsemalla tabilla ”Continue” (2.) ja hyväksymällä valinta painamalla Enter.

![pääkäyttäjän nimi](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Ubuntu%20Server%2016.04.5%20LTS%20asennuksen%20ruutukaappaukset/Vaihe%20(10).png?raw=true)

Seuraavaksi piti kertoa luotavan pääkäyttäjän koko nimi. Laitoimme nimeksi projektiryhmämme nimen eli ”Pisnismiehet” (1.). Kun olimme tämän kirjoittanut, valitsimme tabilla ”Continue” (2.) ja hyväksyimme valinnan painamalla Enter.

![käyttäjätunnus](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Ubuntu%20Server%2016.04.5%20LTS%20asennuksen%20ruutukaappaukset/Vaihe%20(11).png?raw=true)

Käyttäjätunnukseksi ehdotettiin kuvan mukaisesti projektiryhmämme nimeä ilman isoa alkukirjainta (1.). Jatkoimme eteenpäin valitsemalla tabilla ”Continue” (2.) ja hyväksyimme valinnan painamalla Enter.

![salasana](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Ubuntu%20Server%2016.04.5%20LTS%20asennuksen%20ruutukaappaukset/Vaihe%20(12).png?raw=true)

Seuraavaksi loimme hyvän salasanan käyttäjälle ”pisnismiehet” (1.). Jatkoimme eteenpäin valitsemalla tabilla ”Continue” (2.) ja hyväksyimme valinnan painamalla Enter.

![salasanan toisto](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Ubuntu%20Server%2016.04.5%20LTS%20asennuksen%20ruutukaappaukset/Vaihe%20(13).png?raw=true)

Toistimme seuraavaksi salasanan (1.). Jatkoimme eteenpäin valitsemalla tabilla ”Continue” (2.) ja hyväksyimme valinnan painamalla Enter.

![kotihakemiston kryptaus](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Ubuntu%20Server%2016.04.5%20LTS%20asennuksen%20ruutukaappaukset/Vaihe%20(14).png?raw=true)

Seuraavaksi kysyttiin, halutaanko kotihakemisto kryptata. Koska halusimme näin tehdä tietoturvallisuuden parentamiseksi valitsimme nuolinäppäimillä valinnan ”Yes” ja hyväksyimme valinnan painamalla Enter.

![aikavyöhyke](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Ubuntu%20Server%2016.04.5%20LTS%20asennuksen%20ruutukaappaukset/Vaihe%20(15).png?raw=true)

Asennusohjelma ehdotti aikavyöhykkeeksi ”Europe/Helsinki”. Se oli oikein ja valitsimme nuolinäppäimillä ”Yes” ja hyväksyimme sen painamalla Enter.

![kiintolevyn osiointi](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Ubuntu%20Server%2016.04.5%20LTS%20asennuksen%20ruutukaappaukset/Vaihe%20(16).png?raw=true)

Seuraavaksi kysyttiin palvelimen kiintolevyn osioinnista, mitä sille tehdään. Meillä ei ollut tarvetta alkaa kryptaamaan levyä, joten valitsimme nuolinäppäimillä  ”Guided – use entire disk and set up LVM” ja painoimme Enter.Toinen syy sille miksi emme lähteneet kryptaamaan levyä oli se, että tällöin SSH-yhteydenotto palvelimen uudelleenkäynnistyksen yhteydessä ei olisi onnistunut ilman fyysistä käyntiä palvelimella. Tällöin olisimme joutuneet antamaan fyysisesti palvelimelle kryptauksen salasanan.

![osioitava kiintolevy](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Ubuntu%20Server%2016.04.5%20LTS%20asennuksen%20ruutukaappaukset/Vaihe%20(17).png?raw=true)

Seuraavaksi kysyttiin osioitavaa kiintolevyä.  Valitsimme haluamamme ja jatkoimme eteenpäin painamalla Enter. (Kuvassa näkyvä levy ei ole aivan oikea, sillä imitoimme asennusta Oracle VM VirtualBoxissa kuvankaappausten takia.)

![hyväksytään muutokset](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Ubuntu%20Server%2016.04.5%20LTS%20asennuksen%20ruutukaappaukset/Vaihe%20(18).png?raw=true)

Hyväksyimme kirjoitettavat muutokset liittyen osiointiin valitsemalla nuolinäppäimillä ”Yes” ja kuittaamalla valinta painamalla Enter.

![kiintolevyn osioinnin koko](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Ubuntu%20Server%2016.04.5%20LTS%20asennuksen%20ruutukaappaukset/Vaihe%20(19).png?raw=true)

Seuraavaksi jouduimme kertomaan kuinka suuren osan kiintolevystä halusimme osioida. Valitsimme koko levyn koon eli kirjoitimme ”max” (1.). Tämän jälkeen valitsimme tabilla ”Continue” (2.) ja hyväksyimme sen painamalla Enter.

![yhteenveto](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Ubuntu%20Server%2016.04.5%20LTS%20asennuksen%20ruutukaappaukset/Vaihe%20(20).png?raw=true)

Hyväksyimme yhteenvedon tehtävistä muutoksista liittyen kiintolevyyn osiointiin valitsemalla nuolinäppäimillä ”Yes” ja hyväksymällä valinta painamalla Enter.

![asennus käynnistyy](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Ubuntu%20Server%2016.04.5%20LTS%20asennuksen%20ruutukaappaukset/Vaihe%20(21).png?raw=true)

Dataa aletaan kopioimaan levylle.

![proxy](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Ubuntu%20Server%2016.04.5%20LTS%20asennuksen%20ruutukaappaukset/Vaihe%20(22).png?raw=true)

Seuraavaksi kysyttiin välityspalvelimen (proxy) osoitetta. Emme tarvitse valityspalvelinta, joten jätimme kohdan tyhjäksi ja valitsimme tabilla ”Continue” ja hyväksyimme valinnan painamalla Enter.

![päivitykset](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Ubuntu%20Server%2016.04.5%20LTS%20asennuksen%20ruutukaappaukset/Vaihe%20(23).png?raw=true)

Seuraavaksi kysyttiin kuinka halumme hallita palvelimelle tulevia päivityksiä. Halusimme, että tietoturvapäivitykset asentuu automaattisesti, joten valitsimme nuolinäppäimillä ”Install security updates automatically” ja painoimme sitten Enter.

![ohjelmat](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Ubuntu%20Server%2016.04.5%20LTS%20asennuksen%20ruutukaappaukset/Vaihe%20(24).png?raw=true)

Tuli listaus mitä ohjelmia halutaan meidän asentavan palvelimelle. Valitsimme, että palvelimelle asennetaan standardeja järjestelmän hyötyohjelmia (esimerkiksi palomuuri) ja OpenSSH server, jotta voimme ottaa palvelimeen SSH-yhteyden (1.). Valinnan jälkeen jatkoimme eteenpäin valitsemalla ”Continue” (2.) ja hyväksymällä se painamalla Enter.

![ohjelmien asennus](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Ubuntu%20Server%2016.04.5%20LTS%20asennuksen%20ruutukaappaukset/Vaihe%20(25).png?raw=true)

Haluttuja ohjelmia alettiin asentamaan. Tässä ei kestänyt kauan.

![grub lataaja](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Ubuntu%20Server%2016.04.5%20LTS%20asennuksen%20ruutukaappaukset/Vaihe%20(26).png?raw=true)

Kun halutut ohjelmat oli asennettu, alettiin asentamaan GRUB -käynnistyksen lataajaa, jonka ansioista voidaan palvelin käynnistää asennettuun käyttöjärjestelmäämme.

![grub käynnistyksenlataaja](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Ubuntu%20Server%2016.04.5%20LTS%20asennuksen%20ruutukaappaukset/Vaihe%20(27).png?raw=true)

Tuli ilmoitus, jossa kysyttiin, että halutaanko GRUB asentaa pääasialliseksi käynnistyksenlataajaksi. Valitsimme ”Yes” eli kyllä ja hyväksyimme valinnan painamalla ”Enter”.

![asennuksen viimeistely](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Ubuntu%20Server%2016.04.5%20LTS%20asennuksen%20ruutukaappaukset/Vaihe%20(28).png?raw=true)]

Asennusta viimeisteltiin.

![valmis asennus](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Ubuntu%20Server%2016.04.5%20LTS%20asennuksen%20ruutukaappaukset/Vaihe%20(29).png?raw=true)

Asennus oli valmis! Käynnistimme palvelimen uudelleen valitsemalla nuolinäppäimillä ”Continue” ja hyväksymällä se painamalla Enter. Palvelin käynnistyi uudelleen ja irroitimme USB-asennustikun palvelinlaitteesta.

<h5 id="palvelimen-perusmaaritykset">Palvelimen perusmääritykset</h5>

Kirjauduimme palvelimelle sisään pääkäyttäjänä, jonka jälkeen teimme heti seuraavat toimenpiteet:

Laitoimme palomuurin päälle
Teimme palomuurin säännön, joka sallii SSH-yhteyden
Latasimme ja asensimme kaikki päivitykset, jonka jälkeen käynnistimme palvelimen uudelleen.

Teimme nämä seuraavalla komentoskriptillä:

```
sudo ufw enable && sudo ufw allow ssh && sudo apt update && sudo apt upgrade -y && sudo apt autoremove -y && reboot
```

Kun palvelin oli käynnistynyt uudelleen, asetimme siihen staattisen IP-osoitteen. Avasimme tiedoston, johon IP-osoitemääritykset tehdään komennolla:

```
sudoedit /etc/network/interfaces
```

Avautui ”interfaces” -tiedosto, johon laitoimme seuraavat määritykset:

![interfaces määritykset](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/etc_network_interfaces.png?raw=true)

<h4 id="windows-server-2016-asennus-ja-konfigurointi-windowsserver-keskusyksikkoon">Windows Server 2016 asennus ja konfigurointi "WINDOWSERVER" -keskusyksikköön</h4>

Seuraavaksi asensimme Windows Server 2016 Datacenter 64-bittisen version fyysiselle tietokoneelle, jota tarvisimme, jotta saamme tähän koneeseen tehtyä Active Directoryn ja yhdistettyä sen midPointiin. Kokeilimme aluksi Windows Serverin asennusta Oraclen VM VirtuaBoxiin, jotta voisimme testata sitä Windows Serveriä sitä kautta. Ilmeni kuitenkin ongelmia Windowsin aktivoinnin kanssa myöhemmin. Kun veimme (export) valmiin VirtualBoxin Windows Serverin imagen talteen, johon oli liitetty tuoteavain huomattiin, että kun tuotiin (imnport) image takaisin VirtualBoxiin niin Windowsia ei oltu enää aktivoitu ja piti hankkia uusi tuoteavain. Tästä syystä on aihetta välttää Windowsin käyttöä virtuaaliympäristössä ainakin niiltä osin, jos tuodaan ja viedään VirtualBoxin imageja. Virtuaalikoneita voidaan käyttää kuitenkin esimerkiksi phpVirtualBox palvelimella, jolloin vältytään imagejen tuomisesta ja viemisestä. 

Aloitimme Windows Server 2016 Datacenter 64-bittisen version asennuksen fyysiselle tietokoneelle USB-livetikun avulla.

![kielen ja ajan valinta](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Windows%20Server/Screenshot%20(1).png?raw=true)

Valitsimme asennusnäkymästä käyttöjärjestelmän kieleksi englannin [English (United States)]. Ajan ja valuutan määritykseksi valittiin suomenkieliset määritteet [Finnish (Finland)]. Näppäimistön kieleksi valittiin Suomi (Finnish).
Seuraavaksi klikattiin Next.

![lisenssin ehdot](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Windows%20Server/Screenshot%20(2).png?raw=true)

Hyväksyimme lisenssin ehdot laittomalla täpän kohtaan "I accept the license terms" ja klikkasimme Next.

![käyttöjärjestelmän valinta](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Windows%20Server/Screenshot%20(3).png?raw=true)  

Seuraavaksi piti valita haluttu käyttöjärjestelmä. Vaihtoehtoina oli Windows Server 2016 Datacenter versio käyttöliittymällä tai ilman. Valitsimme käyttöjärjestelmän käyttöliittymällä [Windows Server 2016 Datacenter (Desktop Experience)] ja klikkasimme Next.

![asennustyypin valinta](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Windows%20Server/Screenshot%20(4).png?raw=true)

Seuraavaksi asennusvaiheessa piti valita asennustyypin valinta. Valitsimme ensimmäisen vaihtoehdon: "Upgrade: Install Windows and keep files, settings, and applications". Vaikka meillä ei ollut ennestään asennettuna Windows käyttöjärjestelmää tietokoneella, niin tämä valinta ei haittaa, koska kyseisessä valinnassa on maininta, että nämä tiedostot, asetukset ja sovellukset säilyvät vain jos Windows käyttöjärjestelmä on valmiiksi asennettuna. 

![kiintolevylle asennus](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Windows%20Server/Screenshot%20(5).png?raw=true)

Seuraavaksi piti valita levy, jolle käyttöjärjestelmä asennetaan (tässä ei näy oikeaa levyä, koska imitoimme asennusta VirtualBoxissa). Valitsimme levyn ja klikkasimme Next.

<h5 id="windows-palvelimen-perusmaaritykset">Windows -palvelimen perusmääritykset</h5>

Asennettuamme Windows Server 2016 Datacenter 64-bittisen version fyysiselle koneelle, aktivoimme aluksi Windowsin. Windowsin voi aktivoida seuraavasti antamalla tuoteavaimen:
```
Settings - Update & Security - Activation
```

Tämän jälkeen asetimme palvelimelle staattisen IP-osoiteen:
```
Network and Sharing Center - Connections: - Properties - Internet Protocol Version 4 - Properties 
```
Lisättyämme IP-osoitteen, verkkomaskin ja oletusyhdyskäytävän osoitteen staattiseksi asetimme DNS-osoitteiksi Haaga-Helian omat DNS-osoitteet, koska teimme projektia Haaga-Helian tiloissa. Otimme myös IPv6 kokonaan pois käytöstä kohdasta Internet Protocol Version 6 ottamalla täpän siitä pois.

Seuraavaksi laitoimme Network Discoveryn päälle, jotta testityöasemat löytävät palvelimen:
```
File Explorer - Network - Network discovery is turned off. - Turn On Network Discovery
```

Tämän jälkeen vaihdoimme tietokoneen nimeksi WINDOWSSERVER ja laitoimme Remote Desktop yhteyden päälle: 
```
System - Change settings - Change 
```
```
System - Remote settings - Allow remote connections to this computer
```

Käynnistimme koneen tässä vaiheessa uudestaan. Näiden perusmääritysten jälkeen ryhdyimme asentamaan Active Directorya. Avasimme Server Managerin, josta klikkasimme Manage - Add roles and Features.

![add roles and features](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Windows%20Server/Capture1.PNG?raw=true)

Aukesi asennusohjelma. Klikattiin Next. 

![role-based or feature-based installation](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Windows%20Server/Capture2.PNG?raw=true)

Seuraavaksi valitsimme kohdan Role-based or feature-based installation ja klikkasimme Next. 

![palvelimen valinta](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Windows%20Server/Capture3.PNG?raw=true)

Seuraavaksi piti valita tietokone, johon rooli aiotaan asentaan. Meille ei ollut muita kuin yksi vaihtoehto. Klikattiin Next.

![server roles](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Windows%20Server/Capture4.PNG?raw=true)

Seuraavaksi piti valita haluttu rooli, joka halutaan asentaa. Valitsimme Active Directory Domain Services, jonka jälkeen tuli pop-up, josta piti valita Add Features. 

![ad domain services](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Windows%20Server/Capture5.PNG?raw=true)

Klikattiin seuraavaksi Next kun Active Directory Domain Services oli valittu.

![group policy management](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Windows%20Server/Capture6.PNG?raw=true)

Seuraavassa vaiheessa varmistettiin, että Group Policy Management ominaisuus oli valittuna. Tämän jälkeen klikattiiin Next.

![AD DS](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Windows%20Server/Capture7.PNG?raw=true) 

Seuraavaksi tuli tietoa kyseisestä roolista. Klikattiin Next.

![confirmation](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Windows%20Server/Capture8.PNG?raw=true)

Varmistettiin seuraavaksi, että halutut ominaisuudet ja roolit tuli valittua. Näin olikin ja varmistettiin, että ei käynnistetä tietokonetta uudelleen vielä. Llikattiin Install.

![asennus valmis](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Windows%20Server/Capture9.PNG?raw=true)

Asennuksen jälkeen tuli vahvistus asennuksen onnistumisesta. Haluttiin konfiguroida domain controller heti, joten valittiin kohta "Promote this server to a domain controller"

![domain controller määritys](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Windows%20Server/Capture10.PNG?raw=true)

Aukesi uusi määritysikkuna. Valitsimme uuden domain nimen: Add a new forest - pisnismiehet.local. Tämän jälkeen klikattiin Next.

![DSRM](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Windows%20Server/Capture11.PNG?raw=true)

Seuraavaksi piti antaa salasana domainille, jos halutaan palauttaa Domain Controller. Annettiin salasana ja klikattiiin Next. 

![DNS delegation](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Windows%20Server/Capture12.PNG?raw=true)

Seuraavaksi kysyttiin, että halutaanko luoda DNS delegation. Emme halunneet, joten klikkasimme Next.

![NetBIOS nimi](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Windows%20Server/Capture13.PNG?raw=true)

Seuraavaksi määritysikkuna ehdotti NetBIOS nimeä. Hyväksyimme tämän ja klikkasimme Next.

![AD DS tietokanta](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Windows%20Server/Capture14.PNG?raw=true) 

Seuraavaksi ehdotettiin kansioita, johon tiedostot tallennetaan. Meille sopivat nämä ja klikkasimme Next.

![tarkastelu](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Windows%20Server/Capture15.PNG?raw=true)

Seuraavaksi tuli määriteltyjen asetusten tarkasteluruutu. Kaikki oli OK eli klikkasimme Next. 

![edellytykset AD DS](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Windows%20Server/Capture16.PNG?raw=true)

Seuraavaksi määritysohjelma tarkisti edellytykset AD DS:n määritykseen. Edellytykset olivat OK. Klikkasimme Install. Asennuksen jälkeen tietokone käynnistyi uudelleen ja käynnistyksen yhteydessä huomattiin, että tietokone on nyt liitetty Domainiin.
 
<h5 id="hyper-vn-seka-uuden-virtuaalipalvelimen-asennus">Hyper-V:n sekä uuden virtuaalipalvelimen asennus</h5>
 
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

<h5 id="openldap-serverin-asennus-hyper-vn-virtuaalipalvelimeen">OpenLDAP serverin asennus Hyper-V:n virtuaalipalvelimeen</h5>

Asensimme OpenLDAP:n tyhjälle virtuaalipalvelimelle seuraavanlaisesti:

1. Aloitimme OpenLDAP:n asennuksen komennoilla:
    ```
    sudo apt-get update
    sudo apt-get install slapd ldap-utils -y
    ```
    Jokaisen komennon jälkeen painoimme Enter. Lataus ja asennus alkoi. Ohjatun asennuksen aikana kysyttiin luomaan järjestelmänvalvojan salasanan LDAP-hakemistolle. Loimme sen ruudussa olevien ohjeiden mukaan. Asennuksessa ei kestänyt kauan.
 
2. Muokkasimme tiedostoa "ldap.conf" -tiedostoa komennolla:
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
     
3. Seuraavaksi aloitimme LDAP:n konfiguroinnin komennolla:
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
     
4. Asensimme seuraavaksi SSL-komponentit komennolla:
    ```
    sudo apt-get install gnutls-bin ssl-cert -y
    ```
    Komennon antamisen jälkeen painoimme Enter. Latauksessa ja asennuksessa kesti tovin.
     
5. Teimme kansion SSL-mallitiedostoille komennolla:
    ```
    sudo mkdir /etc/ssl/templates
    ```
    Komennon antamisen jälkeen painoimme Enter. Kansio luotiin haluttuun sijaintiin.
 
6. Loimme "ca_server.conf" -tiedoston komennolla:
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
     
7. Loimme "ldap_server.conf" -tiedoston komennolla:
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
 
8. Aloitimme yksityisen SSL-avaimen luonnin ```certtool``` työkalulla komennolla:
    ```
    sudo certtool -p --outfile /etc/ssl/private/ca_server.key
    ```
    Komennon antamisen jälkeen painoimme Enter. Avain luotiin.
 
9. Kirjoitimme äsken tehdyn avaimen sijaintiin ```/etc/ssl/certs``` komennolla:
    ```
    sudo certtool -s --load-privkey /etc/ssl/private/ca_server.key --template /etc/ssl/templates/ca_server.conf --outfile /etc/ssl/certs/ca_server.pem
    ```
    Komennon antamisen jälkeen painoimme Enter. Tämä onnistui moitteetta.
 
10. Loimme seuraavaksi yksityisen avaimen LDAP-palvelimelle komennolla:
    ```
    sudo certtool -p --sec-param high --outfile /etc/ssl/private/ldap_server.key
    ```
    Komennon antamisen jälkeen painoimme Enter. Tämäkin onnistui moitteetta.
 
11. Kirjoitimme myös tämän avaimen ```/etc/ssl/certs``` sijaintiin komennolla:
    ```
    sudo certtool -c --load-privkey /etc/ssl/private/ldap_server.key --load-ca-certificate /etc/ssl/certs/ca_server.pem --load-ca-privkey /etc/ssl/private/ca_server.key --template /etc/ssl/templates/ldap_server.conf --outfile /etc/ssl/certs/ldap_server.pem
    ```
    Komennon antamisen jälkeen painoimme Enter. Tämäkin myös onnistui moitteetta.
     
12. Lisäsimme OpenLDAP:lle pääsyn LDAP palvelinavaimiin. Ensiksi sallimme ```openldap``` ryhmälle oikeaan ryhmään komennolla:
    ```
    sudo usermod -aG ssl-cert openldap
    ```
    Komennon annon jälkeen painoimme Enter.
     
12. Seuraavaksi määrittelimme ```openldap``` ryhmälle käyttöikeudet ```ldap_server.key``` -tiedostolle komennolla:
    ```
    sudo chown :ssl-cert /etc/ssl/private/ldap_server.key
    ```
    Komennon jälkeen painoimme Enter.
     
13. Annoimme seuraavaksi ```ssl-cert``` -ryhmälle lukuoikeudet samaiseen tiedostoon komennolla:
    ```
    sudo chmod 640 /etc/ssl/private/ldap_server.key
    ```
    Komennon jälkeen painoimme Enter.
     
14. Siiryimme seuraavaksi kotihakemistoon ja loimme tiedoston ```addcerts.ldif``` komennoilla:
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
 
15. Laitoimme tehdyt muutokset OpenLDAP-järjestelmään komennolla:
    ```
    sudo ldapmodify -H ldapi:// -Y EXTERNAL -f addcerts.ldif
    ```
    Komennon jälkeen painoimme Enter.
 
16. Käynnistimme OpenLDAP:n uudelleen komennolla:
    ```
    sudo service slapd force-reload
    ```
    Komennon jälkeen painoimme Enter.
 
17. Kopioitiin seuraavaksi ```ca_certs.pem``` toisesta sijainnista toiseen komennolla:
    ```
    sudo cp /etc/ssl/certs/ca_server.pem /etc/ldap/ca_certs.pem
    ```
    Komennon jälkeen painoimme Enter.
 
18. Kokeiltiin seuraavaksi toimiiko OpenLDAP:n yhteys komennolla:
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

MidPointin yhteyttä varten jouduimme tekemään vielä lisäkonfiguraatiota:

1. Siirryimme root-käyttäjäksi komennolla:
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
 
8. Avasimme palomuurista porttinumerot 389 ja 1389 komennolla:
    ```
    sudo ufw allow 389/tcp && sudo ufw allow 389 && sudo ufw allow 1389/tcp && sudo ufw allow 1389
    ```
    Komennon jälkeen painoimme Enter. 
 
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
 
8. 




<h4 id="virtualbox-palvelimen-asennus-ja-konfigurointi-vmserver-keskusyksikkoon">VirtualBox -palvelimen asennus ja konfigurointi "VMSERVER" -keskusyksikköön</h4>

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
 
<h4 id="phpvirtualbox-web-kayttöliittyman-asennus-ja-konfigurointi">phpVirtualBox -web-käyttöliittymän asennus ja konfigurointi</h4>

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

Pääsimme sisään. Seuraavaksi vaihdamme oletussalasanan omaan, parempaan salasanaan. Se onnistuu valitsemalla käyttliittymän valikosta ```File -> Change Password```. Avautuu ikkuna, johon pitää kertoa sekä vanha salasana, että uusi salasana kahdesti. Lopuksi hyväksytään muutokset painamalla OK.

![](https://raw.githubusercontent.com/Eetu95/Open-source-IdM-solution/master/Kuvat/phpvirtualboxpassword.JPG)
 
<h5 id="suojatun-yhteyden-maaritys-2">Suojatun yhteyden määritys</h5>

<h4 id="testityoasemien-seka-testipalvelimen-asennus-ja-konfigurointi">Testityöasemien sekä testipalvelimen asennus ja konfigurointi</h4>

<h5 id="windows-10-testipc1">Windows 10 (TESTIPC1)</h5>
 
Testityöasemia käytimme meidän omassa VirtualBox-palvelimessa. Latasimme Windows 10 virtuaalikoneen <a href="modern.ie"> modern.ie sivustolta</a>, joka toimii 90 päivän lisenssillä. Kyseinen virtuaalikone toimii testityöasemana ja on nimeltään "TESTIPC1".

Kirjauduimme SSH-yhteydellä VirtualBox_palvelimeen (VMSERVER) ja kirjaudumme sisään tunnuksilla, jotka teimme VMSERVERI:n asennuksen yhteydessä
2. Latasimme TESTIPC1:sen modern.ie -sivulta komennolla:
    ```
    https://az792536.vo.msecnd.net/vms/VMBuild_20180425/VirtualBox/MSEdge/MSEdge.Win10.VirtualBox.zip
    ```
    Komennon jälkeen painoimme Enter. Virtuaalikonetta alettiin lataamaan ja siinä kesti tovin.
3. Purkasimme kansion kotihakemistoon komennolla:
    ```
    unzip MSEdge.Win10.VirtualBox.zip
    ```
5. Siirryimme seuraavaksi root- käyttäjäksi komennolla:
    ```
    sudo su
    ```
6. Siirsimme virtuaalikoneen imagen ```vbox``` käyttäjän kotihakemistoon komennolla:
    ```
    mv 'MSEdge - Win10.ova' /home/vbox/
    ```
    Komennon jälkeen panoimme Enter. Virtuaalikoneen image siirtyi haluttuun sijaintiin. Kirjauduimme lopuksi pois root-käyttäjästä komennolla ```exit```.

7. Kirjauduimme sisään VirtualBoxin web-käyttöliittymään ja valitsimme valikosta ```File -> Import Appliance... ``` Klikkattiin  avautuvasta ikkunasta kansion kuvaa
 
![](https://raw.githubusercontent.com/Eetu95/Open-source-IdM-solution/master/Kuvat/phpvirtualboximport.JPG)

 
    ja haimme virtuaalikoneen imagen ````vbox```` käyttäjän kotihakemistosta. Lopuksi painoimme ```OK```.
    ![](https://raw.githubusercontent.com/Eetu95/Open-source-IdM-solution/master/Kuvat/phpvirtualboxselect.JPG)
     
    Valtsimme se jälkeen ```Next >>``` ja katsoimme onko avautuvasta ikkunasta onko virtuaalikoneen asetukset ok. Muutimme nimeksi "TESTIPC1" ja laitoimme täpän kohtaan "Reinitialize the MAC address of all network cards". Lopuksi painoimme ```Import```. Testikone oli tuotu VirtualBox-palvelimelle onnistuneesti. Tämän jälkeen muutimme virtuaalikoneesta verkkokortin siltaavaksi, jotta se näkyy lähiverkossa muiden laitteiden joukossa. Teimme sen klikkaamalla hiiren oikealla virtuaalikonetta ja valitsemalla ```Settings -> Network -> Adapter 1 ``` ja drop-down valikosta valitsemalla "Bridged Adapter". 
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

<h5 id="ubuntu-desktop-18041-lts-testipc2">Ubuntu Desktop 18.04.1 LTS (TESTIPC2)</h5>
 
Linux-ympäristöä varten tarvitsimme Linux-käyttöjärjestelmällä varustetun koneen. Päätimme valita tätä varten Ubuntu Desktop 18.04.1 LTS 64-bittisen version. Samalla tavoin lisäsimme tämän testityöaseman VirtualBoxiinVirtualBox -palvelimeen (VMSERVER). Ladattiin tätä varten .ISO tiedosto netistä: (Komentokehotteessa saa sen helposti ladattua komennolla ```wget http://releases.ubuntu.com/18.04.1/ubuntu-18.04.1-desktop-amd64.iso```). Levykuvan siirto ```vbox``` käyttäjän kotihakemistoon tapahtuu samalla tavalla miten edellisessä kappaleessa tehtiin. VMSERVERillä loimme virtuaalikoneen:

<li>Tyyppi: Linux
<li>Versio: Ubuntu (64-bit)
<li>RAM-muistia: 2048 MB
<li>Hard disk: Create a virtual hard disk now
<li>Hard disk tyyppi: VDI | Dynamically allocated
<li>Kiintolevyn koko: 50 GB

Tämän jälkeen muokkasimme virtuaalikoneen asetuksia: Settings -> Storage -> Empty -> levyn kohdasta valittiin Choose Virtual Optical Disk File... ja lisättiin .ISO tiedosto tähän ```vbox``` käyttäjän kotihakemistosta (```/home/vbox)```. Tämän jälkeen laitettiin vielä verkkokortti siltaavaksi. Nyt virtuaalikone oli valmis asennettavaksi. Käynnistettiin virtuaalikone. 

Ensimmäiseksi aukesi asennusruutu:

![Ubuntu Desktop asennus](https://raw.githubusercontent.com/Eetu95/Open-source-IdM-solution/master/Kuvat/Ubuntu%20Desktop/Screenshot%20(1).png)

Valittiin käyttöjärjestelmän kieliksi English (1.) ja klikattiin "Install Ubuntu" (2.).

![Näppäimistön layout](https://raw.githubusercontent.com/Eetu95/Open-source-IdM-solution/master/Kuvat/Ubuntu%20Desktop/Screenshot%20(2).png)

Seuraavaksi kysyttiin näppäimistön kieliasetuksia. Valittiin "Finnish" (1. ja 2.) ja klikattiin "Continue" (3.).

![Asennus tyyppi 1/2](https://raw.githubusercontent.com/Eetu95/Open-source-IdM-solution/master/Kuvat/Ubuntu%20Desktop/Screenshot%20(3).png)

Seuraavaksi kysyttiin halutaanko tehdä normaali asennus vai minimaalinen asennus. Koska emme halunneet mitään ylimääräistä asennettavan, valitsimme minimaalisen asennuksen (1.). Halusimme myös asentaa tarvittavat päivitykset (2.) sekä kolmannen osapuolen välttämättömät ohjelmat (3.). Jatkoimme eteenpäin klikkaamalla "Continue" (4.).

![Asennus tyyppi 2/2](https://raw.githubusercontent.com/Eetu95/Open-source-IdM-solution/master/Kuvat/Ubuntu%20Desktop/Screenshot%20(4).png)

Asennustyypiksi valittiin ensimmäinen vaihtoehto eli tyhjennetään koko kiintolevy ja asennetaan siihen Ubuntu (1.). Aloitimme asennuksen painamalla "Install Now" (2.).

![Varmistus](https://raw.githubusercontent.com/Eetu95/Open-source-IdM-solution/master/Kuvat/Ubuntu%20Desktop/Screenshot%20(5).png)

Hyväksyttiin tehtävät muutokset kiintolevylle painamalla "Continue" (1.).

![Sijainti](https://raw.githubusercontent.com/Eetu95/Open-source-IdM-solution/master/Kuvat/Ubuntu%20Desktop/Screenshot%20(6).png)

Sijainniksi valittiin "Helsinki" (1.) ja mentiin eteenpäin valitsemalla "Continue" (2.).

![käyttäjän luominen](https://raw.githubusercontent.com/Eetu95/Open-source-IdM-solution/master/Kuvat/Ubuntu%20Desktop/Screenshot%20(7).png)

Seuraavaksi kysyttiin tietokoneen nimeä, käyttäjätunnusta ja salasanaa. Kirjoitimme nämä (1.) ja klikattiin Continue (2.).

![Ubuntu Desktop asennus](https://raw.githubusercontent.com/Eetu95/Open-source-IdM-solution/master/Kuvat/Ubuntu%20Desktop/Screenshot%20(8).png)

Ubuntu Desktop lähti asentumaan.

![asennus valmis](https://raw.githubusercontent.com/Eetu95/Open-source-IdM-solution/master/Kuvat/Ubuntu%20Desktop/Screenshot%20(9).png)

Asennus tuli valmiiksi ja virtuaalikone piti käynnistää uudelleen. Klikattiin Restart Now.
Tässä vaiheessa emme tehneet enempää esivalmisteluja Ubuntu Desktop -käyttöjärjestelmään liittyen.

<h5 id="ubuntu-server-16045-lts-testipalvelin">Ubuntu Server 16.04.5 LTS</h5>

Asensimme testipalvelimen myös VirtualBox -palvelimelle (VMSERVER). Testipalvelimen asennusprosessi on muuten sama kuin fyysisen palvelimen kanssa, mutta ero on ainoastaan se, että testipalvelin on VirtualBox -palvelimella. Käyttöjärjestelmä oli sama kuin fyysisellä tietokoneella: Ubuntu Server 16.04.5 LTS 64-bit. Asetimme myös tässäkin verkkokortin siltaavaksi kuten myös muiden testikoneiden osalta.
 
<h3 id="asennus">Asennus</h3>

Päivitettiin Ubuntu Server 16.04.5 LTS 64-bit.

    $ sudo apt-get update
    $ sudo apt-get upgrade

Asennettiin openjdk8

    $ sudo apt-get -y install openjdk-8-jdk

Asennettiin openjre8

    $ sudo apt-get -y install openjdk-8-jre

Mentiin kansioon /opt.

    $ cd /opt

Ladattiin midpoint 3.8 (watt) midPointin sivuilta.

![midPoint 3.8 (Watt) - Download](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/midPoint/midPoint%203.8%20(Watt)%20-%20Download.PNG?raw=true)

    $ sudo wget https://evolveum.com/downloads/midpoint/3.8/midpoint-3.8-dist.tar.gz

Purettiin ladattu tervapallo (midpoint-3.8-dist.tar.gz)

    $ sudo tar -xvzf midpoint-3.8-dist.tar.gz

Vaihettiin kansio midpoint-3.8-dist kansioksi midpoint.

    $ mv /opt/midpoint-3.8-dist /opt/midpoint

<a href="https://wiki.evolveum.com/display/midPoint/Running+midPoint+with+systemd">"Running midPoint with systemd"</a>. Laitettiin midpoint käynnistymään palvelimen käynnistymisen yhteydessä automaattisesti.

Tehtiin uusi tiedosto /etc/systemd/system/midpoint.service, jonne laitettiin tämä sisältö:

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

Laitettiin midPoint palvelu päälle:

    $ sudo systemctl daemon-reload
    $ sudo systemctl enable midpoint

Laitettiin midPoint systemd palveluksi:

    $ sudo systemctl start midpoint

Sitten käynnistettiin palvelin uudelleen.

    $ sudo reboot

Tämän jälkeen midPoint oli asennettu.

<h3 id="konfigurointi">Konfigurointi</h3>
 
<h4 id="tietokannan-maarittaminen">Tietokannan määrittäminen</h4>
 
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
Käyttäjien lisäys onnistui ja ne löytyvät MariaDB tietokannasta.

<h4 id="connectoreiden-maarittaminen">Connectoreiden määrittäminen</h4>

<h4 id="suojatun-yhteyden-konfigurointi">Suojatun yhteyden konfigurointi</h4>

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

<li>openssl = CLI työkalu, jolla luodaan ja hallitaan OpenSSL sertifikaatteja, avaimia ja muita tiedostoja.
<li>req = alikomento, jolla kerrotaan että halutaan käyttää X.509 CSR:ää. X.509 on julkisenavaimen infrastruktuuri standardi, jota
SSL ja TLS noudattavat. Teimme siis uuden X.509 sertin.
<li>-x509 = modifioi aikaisempaa alikomentoa kertomalla apuohjelmalle, että halutaan tehdä itsekirjoitettu sertifikaatti sen sijaan että tehtäisiin
sertifikaatin allekirjoitus pyyntö.
<li>-nodes = Kertoo OpenSSL:lle että se voi ohittaa sertifikaatin suojauksen tunnuslauseen. Apachen pitää pystyä
lukemaan tiedosto ilman, että käyttäjä puuttuu siihen silloin kun palvelin käynnistyy. Tunnuslause (passphrase)
estäisi tämän toteutumisen, koska meidän pitäisi aina syöttää se jokaisen uudelleenkäynnistyksen yhteydessä.
<li>-days 365 = Tämä asettaa sertifikaatin voimassaolo ajan 365 päiväksi.
<li>-newkey rsa:2048 =Tällä määritellään uuden sertifikaatin ja avaimen luonti samaan aikaan. Rsa:2048 kertoo että pitää
tehdä RSA avain, joka on 2048 bittiä pitkä.
<li>-keyout = Kertoo OpenSSL:lle minne luotu yksityinen avaintiedosto pistetään.
<li>-out = Kertoo OpenSSL:lle minne sertifikaatti pistetään.

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

Käynnistyksen jälkeen testattiin Apachen toimivuutta. Kirjoitettiin selaimeen:
```
https://*palvelimen IP-osoite*
```
Tällöin tuli herja siitä, että sertifikaatti ei ole luotettava. Tämä johtuu siitä, koska sertifikaatti on itse allekirjoitettu eikä hankittu valtuutetulta taholta. Ohitin herjan Chromessa vain klikkaamalla Advanced ja ``` Proceed to https://*palvelimen IP-osoite*```
![https Chrome](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/https_chrome.PNG?raw=true)
