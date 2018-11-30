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


### IdM-järjestelmien dokumentaatiot:
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


### Avoimen lähdekoodin IdM-järjestelmien valintakriteerit

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

## 4. Midpoint<div id='midpoint'></div>

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
### 1.	Esivalmistelut<div id='esivalmistelut'></div>

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

Asennamme Identiteetinhallintajärjestelmän työasemaan "MIDPOINT", VirtualBox-palvelimen testityöasemia sekä testipalvelinta varten työasemaan "VMSERVER" sekä Windows -palvelimen työasemaan "WINDOWSSERVER". Toisin sanoen nämä edellä mainitut työasemat toimivat palvelinkäytössä.


#### a.	Ubuntu Server asennus ja konfigurointi

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

##### Palvelimen perusmääritykset

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

#### b.	Windows Server asennus ja konfigurointi

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

##### Windows palvelimen perusmääritykset

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

#### c.	Testityöasemien sekä testipalvelimen asennus ja konfigurointi

##### Windows 10
Testityöasemia käytimme virtuaaliympäristössä Oracle VM VirtualBoxissa. Latasimme Windows 10 virtuaalikoneen modern.ie sivustolta. Sivustolta kohdasta Virtual Machines päästiin valitsemaan ladattava virtuaalikone. Valitsimme koneeksi MSEdge on Win10 (x64) Stable (17.17134) ja alustaksi VirtualBox. Latasimme .ZIP tiedoston, jossa VirtualBoxin image oli. 

![VirtualBox import](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Windows%2010%20VM/Capture_1.PNG?raw=true)

Toimme (import) Windows 10 virtuaalikoneen imagen VirtualBoxiin. Sen saa tehtyä valitsemalla VirtualBoxista File - Import Appliance... 
Laitoimme VirtualBoxissa verkkokortin siltaavaksi (Bridged Adapter), jotta IP-osoitteet ovat verkon mukaisia eikä VirtualBoxin omia. Tämän sai tehtyä muokkaamalla virtuaalikoneen asetuksia VirtualBoxissa:
```
Settings - Network - Adapter 1 - Attached to: Bridged Adapter
```

![MSEdge - Win10](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Windows%2010%20VM/Capture_2.PNG?raw=true)

Tämän jälkeen virtuaalikone oli valmiina käynnistettäväksi. Käynnistettiin kone, jolloin haluttiin liittää se Domainiin. Teimme seuraavat asiat:
<li>IPv6 pois päältä
<li>IPv4 verkkokorttiin DNS osoitteeksi Windows palvelimen IP-osoite
<li>Network Discovery päälle
<li>Etäyhteyden salliminen
<li>Tietokoneen nimen muuttaminen (TESTIPC1)

Tämän jälkeen liitettiin Windows testityöasema domainiin: 
```
Control Panel - System and Security - System - Change settings - Change
```
Valittiin täppä, että liitetään domainiin ja kirjoitettiin domain nimi. Seuraavaksi kysyttiin domainin Admin käyttäjän tunnuksia. Kirjoitettiin ne ja domainin liitos onnistui. Virtuaalikone kirjautui ulos ja takaisin. Virtuaalikoneesta nyt näki, että kone on liitoksissa domainiin esimerkiksi System asetuksista.

Testattiin seuraavaksi, että Active Directory toimii. Windows palvelimella loimme uuden käyttäjän Active Directoryyn:
```
Start - Windows Administrative Tools - Active Directory Users and Computers - pisnismiehet.local - Users - New - User
```
Käyttäjän luonti-ikkunaan kirjoitimme käyttäjätunnuksen ja tietoja käyttäjästä sekä luotiin käyttäjälle salasana. Tämän jälkeen kun käyttäjä oli luotu niin testattiin kirjautua käyttäjälle testityöasemaa käyttäen. Kirjautuminen onnistui ja varmistuttiin siitä, että testityöasema on liitoksissa domainiin.

##### Ubuntu Desktop

Linux-ympäristöä varten tarvitsimme Linux-käyttöjärjestelmällä varustetun koneen. Päätimme valita tätä varten Ubuntu Desktop 16.04.5 LTS 64-bittisen version. Samalla tavoin lisäsimme tämän testityöaseman VirtualBoxiin. Ladattiin tätä varten .ISO tiedosto netistä: http://releases.ubuntu.com/16.04/. VirtualBoxissa loimme virtuaalikoneen:
<li>Tyyppi: Linux
<li>Versio: Ubuntu (64-bit)
<li>RAM-muistia: 2048 MB
<li>Hard disk: Create a virtual hard disk now
<li>Hard disk tyyppi: VDI | Dynamically allocated
<li>Kiintolevyn koko: 20 GB

Tämän jälkeen muokkasimme virtuaalikoneen asetuksia: Settings - Storage - Empty -levyn kohdasta valittiin Choose Virtual Optical Disk File... ja lisättiin .ISO tiedosto tähän. Tämän jälkeen laitettiin vielä verkkokortti siltaavaksi. Nyt virtuaalikone oli valmis asennettavaksi. Käynnistettiin virtuaalikone. 

Ensimmäiseksi aukesi asennusruutu:

![Ubuntu Desktop asennus](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Ubuntu%20Desktop/Screenshot%20(1).png?raw=true)

Valittiin käyttöjärjestelmän kieliksi English ja klikattiin Install Ubuntu.

![Ubuntu Desktop päivitykset](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Ubuntu%20Desktop/Screenshot%20(2).png?raw=true)

Seuraavassa kohdassa kysyttiin päivitysten asennusta ja kolmen osapuolen ohjelmia asennettavaksi. Valittiin nämä molemmat ja klikattiin Continue.

![Asennus tyyppi](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Ubuntu%20Desktop/Screenshot%20(3).png?raw=true)

Seuraavaksi kysyttiin asennustyypin tapaa. Valittin Erase disk and Install Ubuntu. Klikattiin sitten Install now. 

![varmistus](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Ubuntu%20Desktop/Screenshot%20(4).png?raw=true)

Tuli vielä varmistus kyseisestä valinnasta. Klikattiin Continue. 

![aikavyöhyke](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Ubuntu%20Desktop/Screenshot%20(5).png?raw=true)

Seuraavaksi kysyttiin sijaintia. Valittiin Helsinki ja klikattiin Continue. 

![näppäimistön layout](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Ubuntu%20Desktop/Screenshot%20(6).png?raw=true)

Seuraavaksi kysyttiin näppäimistön kieliasetuksia. Valittiin Finnish ja klikattiin Continue.

![käyttäjän luominen](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Ubuntu%20Desktop/Screenshot%20(7).png?raw=true)

Seuraavaksi kysyttiin tietokoneen nimeä, käyttäjätunnusta ja salasanaa. Kirjoitimme nämä ja klikattiin Continue.

![Ubuntu Desktop asennus](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Ubuntu%20Desktop/Screenshot%20(8).png?raw=true)

Ubuntu Desktop lähti asentumaan.

![asennus valmis](https://github.com/Eetu95/Open-source-IdM-solution/blob/master/Kuvat/Ubuntu%20Desktop/Screenshot%20(9).png?raw=true)

Asennus tuli valmiiksi ja virtuaalikone piti käynnistää uudelleen. Klikattiin Restart Now.
Tässä vaiheessa emme tehneet enempää esivalmisteluja Ubuntu Desktop -käyttöjärjestelmään liittyen.

##### Ubuntu Server 

Testipalvelimen asensimme myös VirtualBoxiin, jotta voimme testata midPointin käyttöä siellä ensin ennenkuin siirrämme valmiit tuotokset fyysiselle Ubuntu Serverille. Testipalvelimen asennusprosessi on muuten sama kuin fyysisen palvelimen kanssa, mutta ero on ainoastaan se, että testipalvelin on VirtualBoxissa. Käyttöjärjestelmä oli sama kuin fyysisellä tietokoneella: Ubuntu Server 16.04.5 LTS 64-bit. 