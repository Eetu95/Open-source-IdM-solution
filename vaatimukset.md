# Vaatimukset

| Vaatimus  |  Lisätietoja   |
|---|---|
|IdM-järjestelmä pyörii Linux-palvelimella   |Säästytään näin ollen lisenssikustannuksissa, kun ei tarvitse käyttää maksullista käyttöjärjestelmää.    |
|IdM oltava avoimeen lähdekoodiin perustuva ja kaikille ilmainen   | Säästytään muun muassa lisenssikustannuksilta, kun IdM-järjestelmän hankinnasta ei tarvitse maksaa.   |
|Lisenssi sallii kaupallisen toiminnan ja järjestelmämuutokset  | Voidaan käyttää IdM-järjestelmää näin ollen yritysympäristössä ja voidaan sitä halutessaan myös kehittää.  |
|Ainakin tuki tunnettuihin järjestelmiin ja palvelujen rajapintoihin (muun muassa Microsoft Active Directory, Linux,  Tietokannat, LDAP). Tapahtumarajapintoja ja valmiita connectoreita on tarjolla. IdM on yleisellä tasolla kattava (On mahdollisuus tehdä esimerkiksi custom rajapintoja ja connectoreita) |   |
|Tapahtumien kirjaus lokeihin, jäljitettävyys on mahdollista | Jotta nähdään kuka on käyttö-oikeuden tilannut, mitä on tilattu, kenelle on tilattu sekä koska on tilattu ja onko tapahtuma käyttäjätunnus vai käyttäjäryhmätasoisesti.|
|Eri salasana eri tasoisiin palveluihin eli IdM-järjestelmä tukee muiden järjestelmien omia käytäntöjä   | Jos ei haluta käyttää samoja tunnuksia eri järjestelmiin.   |
|IdM:n ja järjestelmien välinen yhteys on salattu, jotta hyökkääjä ei voi saada selville kuuntelemalla liikenteessä liikkuvaa sensitiivistä tietoa (käyttäjätunnukset ja salasanat)   | Vältytään hakkereiden liikenteen salakuuntelulta ja välimieshyökkäyksiltä.    |
|IdM-järjestelmästä löytyy valmistajalta/kehittäjältä dokumentaatiota   | Jotta järjestelmän asennus, käyttö ja ylläpito on vaivattomampaa.   |
|IdM-järjestelmää kehitetään aktiivisesti   |Jotta järjestelmää voidaan käyttää huoletta kauan, siihen saadaan tietoturvapäivityksiä sekä muita parannuksia ja ei tarvitse heti vaihtaa toiseen järjestelmään.   |
|Goverance   |Voidaan valvoa ja tarkistaa, että halutut yrityksen asettamat vaatimukset toteutuvat esimerkiksi salasanavaatimukset ja että vain tietyt henkilöt pääsevät kirjautumaan tiettyihin järjestelmiin ja palveluihin.   |
|Toimeksiantojen hyväksyntämahdollisuus   |Jotta joku toinen henkilö voi hyväksyä jonkun toisen henkilön pyynnön saada oikeudet tiettyyn järjestelmään/palveluun. Esimerkiksi esimies hyväksyy alaisensa pyynnön saada oikeudet kirjautua tietokantaan.   |
|Salasanojen hallinta   | Voidaan halutessaan esimerkiksi resetoida tietyn henkilön salasanan, jos se häneltä vaikkapa unohtui.   |
|Tunnusten jäädytys ja poisto   | Jotta voidaan välttyä irtisanottujen henkilöiden pääsy järjestelmiin ja palveluihin.  |
|Henkilö- ja käyttäjätunnusprofiilien muokkausmahdollisuus   | Jos esimerkiksi työtekijän titteli ja työnkuva muuttuu, voidaan nämä tiedot kätevästi päivittää ajan tasalle.  |
|Hakumahdollisuus   |Voidaan helposti etsiä esimerkiksi halutun henkilön henkilötili ja käyttäjäprofiili tiettyyn järjestelmään ja palveluun.   |
|Raporttien luontimahdollisuus   | Voidaan tehdä tulosteet, joissa esimerkiksi nähdään tietyn henkilön oikeudet tiettyihin järjestelmiin ja palveluihin.  |
|Vaarallisten työyhdistelmien tunnistus tehtävätasoisesti   | Esimerkiksi sama henkilö ei saa luoda oikeuksia ja hyväksyä niitä itselleen johonkin kohdejärjestelmään tai palvelu.  |
|Mahdollisuus manuaaliprovisiointiin   |Tukeeko valittavat mahdollisuudet esimerkiksi radiobuttoneita, checkboxeja jne.   |
|Soveltuu myös suureen yritykseen   |  Käyttöoikeuksia voi olla esimerkiksi yli 7000  |

## Lähteet
* https://www.vahtiohje.fi/web/guest/hyvaa-hallintokaytantoa-tukevan-kayttovaltuuksien-hallintaympariston-arkkitehtuuri 

* https://syncope.apache.org/ 

* https://opitietosuojaa.fi/index.php/fi/52-tyokalupakki/sopimusliitteet/52-kayttovaltuusperiaatteet 

* https://tutcris.tut.fi/portal/files/3087873/linden_identiteetin_ja_paasynhallinta.pdf 

* https://www.itewiki.fi/tarjonta/identiteetinhallinta-kayttajahallinta 

* Plyhm, J & Hallikas, J. 24.9.2018.
