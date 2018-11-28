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
 
