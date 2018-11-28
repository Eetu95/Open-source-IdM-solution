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
      <li><a href="#esivalmistelut">Esivalmistelut</a></li>
      <ol>
          <li><a href="#ubuntu-server-asennus-ja-konfigurointi">Ubuntu Server asennus ja konfigurointi</a></li>
          <li><a href="#windows-server-asennus-ja-konfigurointi">Windows Server asennus ja konfigurointi</a></li>
          <li><a href="#testityoasemien-seka-testipalvelimen-asennus-ja-konfigurointi">Testityöasemien sekä testipalvelimen asennus ja konfigurointi</a></li>
      </ol>
      <li><a href="#asennus">Asennus</a></li>
      <li><a href="#konfigurointi">Konfigurointi</a></li>
      <ol>
          <li><a href="#tietokannan-maarittaminen">Tietokannan määrittäminen</a></li>
          <li><a href="#connectoreiden-maarittaminen">Connectoreiden määrittäminen</a></li>
          <li><a href="#suojatun-yhteyden-konfigurointi">Suojatun yhteyden konfigurointi</a></li>
      </ol>
      </ol>
 <li><a href="#testaus">Testaus</a></li>
 <li><a href="#yhteenveto">Yhteenveto</a></li>
 <li><a href="#lahteet">Lähteet</a></li>
</ol>

## Johdanto<div id='johdanto'></div>
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


## Yleistä IdM-järjestelmistä (Identity Management System)<div id='yleista'></div>
IdM-järjestelmä (Englanniksi: Identity Management System, Suomeksi:
Identiteetinhallintajärjestelmä) on järjestelmä,
jonka avulla voidaan keskitetysti hallita yrityksen eri tietojärjestelmiä,
palveluita, tietokantoja, ohjelmistoja sekä ohjelmien käyttöoikeuksia että
pääsynhallintaa. IdM:n ansiosta yritys pystyy helposti pitämään huolen siitä ketkä työntekijät pääsevät käyttämään mitäkin tietojärjestelmiä sekä palveluita ja ketkä taas eivät. IdM-järjestelmiä on hyvin erilaisia ja hyvin erilaisina kokonaisuuksina.

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


## IdM-järjestelmien vertailu<div id='idm-jarjestelmien-vertailu'></div>

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

IdM-järjestelmien dokumentaatiot:
=======
<br>
<li>Apache Syncope: <a href="https://syncope.apache.org/docs/">https://syncope.apache.org/docs/</a></li>
<li>MidPoint: <a href="https://wiki.evolveum.com/display/midPoint/Documentation">https://wiki.evolveum.com/display/midPoint/Documentation</a></li>
<li>OpenIDM: <a href="https://backstage.forgerock.com/docs/idm">https://backstage.forgerock.com/docs/idm</a></li>
<li>Soffid: <a href="http://www.soffid.com/products-and-services/open-source-sso-and-identity-and-access-management/">http://www.soffid.com/products-and-services/open-source-sso-and-identity-and-access-management/</a></li>
<li>Keycloak: <a href="https://www.keycloak.org/documentation.html">https://www.keycloak.org/documentation.html</a></li>
<li>Unity: <a href="http://www.unity-idm.eu/documentation/unity-2.6.2/manual.html">http://www.unity-idm.eu/documentation/unity-2.6.2/manual.html</a></li>
<li>OpenIAM: <a href="http://docs41.openiam.com/">http://docs41.openiam.com/</a></li>
<li>Shibboleth: <a href="https://wiki.shibboleth.net/confluence/#all-updates">https://wiki.shibboleth.net/confluence/#all-updates</a></li>
<li>WSO2 Identity Server: <a href="https://github.com/wso2/product-is/">https://github.com/wso2/product-is/</a></li>
<li>Gluu: <a href="https://gluu.org/docs/">https://gluu.org/docs/</a></li>
<li>Josso: <a href="http://docs.atricore.com/josso2/2.4.0/josso-reference-guide/html/en-US/JOSSO_Reference.html">http://docs.atricore.com/josso2/2.4.0/josso-reference-guide/html/en-US/JOSSO_Reference.html</a></li>
<li>FreeIPA: <a href="https://www.freeipa.org/page/Documentation">https://www.freeipa.org/page/Documentation</a></li>
<li>Aerobase: <a href="http://aerobase.org/documentation">http://aerobase.org/documentation</a></li>

### Avoimen lähdekoodin IdM-järjestelmien valintakriteerit [lisenssit, versionhallinta (GitHub), Google Scholar, Google Trends, Kirjat (Amazon, Safari Books Online)] ].

Katsoimme kyseisten avoimen lähdekoodin IdM-järjestelmien lisenssit läpi. Laitoimme ne ylös vertailudokumenttiin ja selitimme ne. Lisäsimme lähteet, joista ilmenee lisenssit ja mitä ne pitävät sisällään.

![Apache 2.0 -lisenssi](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Vertailu/Apache%202.0%20-lisenssi.PNG?raw=true)

Jan konsultoi työpaikallaan IdM-järjestelmän vaatimuksista, mm. mitä mieltä kollegat olivat vaatimuksista ja mitä voisi vielä lisätä. Otimme ne huomioon vertailussamme.

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

### Alustavat vaatimukset

#### Vaatimukset

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

