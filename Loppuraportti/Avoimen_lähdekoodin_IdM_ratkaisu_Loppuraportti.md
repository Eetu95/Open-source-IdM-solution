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
