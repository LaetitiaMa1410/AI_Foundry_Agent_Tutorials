<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "8164484c16b1ed3287ef9dae9fc437c1",
  "translation_date": "2025-07-23T08:53:54+00:00",
  "source_file": "10-ai-agents-production/README.md",
  "language_code": "fi"
}
-->
# AI-agentit tuotannossa: Havainnointi ja arviointi

Kun AI-agentit siirtyvät kokeellisista prototyypeistä todellisiin sovelluksiin, niiden käyttäytymisen ymmärtäminen, suorituskyvyn seuraaminen ja tuotosten järjestelmällinen arviointi tulevat tärkeiksi.

## Oppimistavoitteet

Tämän oppitunnin jälkeen osaat tai ymmärrät:
- Agenttien havainnoinnin ja arvioinnin keskeiset käsitteet
- Tekniikat agenttien suorituskyvyn, kustannusten ja tehokkuuden parantamiseksi
- Mitä ja miten arvioida AI-agenttejasi järjestelmällisesti
- Kuinka hallita kustannuksia AI-agenttien käyttöönotossa tuotannossa
- Kuinka instrumentoida AutoGenilla rakennetut agentit

Tavoitteena on antaa sinulle tiedot, joiden avulla voit muuttaa "mustan laatikon" agenttisi läpinäkyviksi, hallittaviksi ja luotettaviksi järjestelmiksi.

_**Huom:** On tärkeää ottaa käyttöön turvallisia ja luotettavia AI-agentteja. Tutustu myös oppituntiin [Luotettavien AI-agenttien rakentaminen](./06-building-trustworthy-agents/README.md)._

## Jäljet ja spanit

Havainnointityökalut, kuten [Langfuse](https://langfuse.com/) tai [Azure AI Foundry](https://learn.microsoft.com/en-us/azure/ai-foundry/what-is-azure-ai-foundry), esittävät yleensä agenttien suoritukset jälkinä ja spaneina.

- **Jälki** edustaa agentin tehtävää alusta loppuun (esim. käyttäjän kyselyn käsittely).
- **Spanit** ovat yksittäisiä vaiheita jäljen sisällä (esim. kielimallin kutsuminen tai datan hakeminen).

![Jälkipuu Langfusessa](https://langfuse.com/images/cookbook/example-autogen-evaluation/trace-tree.png)

Ilman havainnointia AI-agentti voi tuntua "mustalta laatikolta" – sen sisäinen tila ja päättely ovat läpinäkymättömiä, mikä vaikeuttaa ongelmien diagnosointia tai suorituskyvyn optimointia. Havainnoinnin avulla agentit muuttuvat "lasilaatikoiksi", jotka tarjoavat läpinäkyvyyttä, mikä on olennaista luottamuksen rakentamisessa ja sen varmistamisessa, että ne toimivat tarkoitetulla tavalla.

## Miksi havainnointi on tärkeää tuotantoympäristöissä

AI-agenttien siirtyminen tuotantoympäristöihin tuo mukanaan uusia haasteita ja vaatimuksia. Havainnointi ei ole enää "mukava lisä", vaan kriittinen ominaisuus:

*   **Vianetsintä ja juurisyyn analysointi**: Kun agentti epäonnistuu tai tuottaa odottamattoman tuloksen, havainnointityökalut tarjoavat jäljet, joiden avulla virheen lähde voidaan paikantaa. Tämä on erityisen tärkeää monimutkaisissa agenteissa, jotka voivat sisältää useita LLM-kutsuja, työkalujen vuorovaikutuksia ja ehdollista logiikkaa.
*   **Viiveen ja kustannusten hallinta**: AI-agentit luottavat usein LLM:iin ja muihin ulkoisiin API:hin, jotka laskutetaan tokenien tai kutsujen perusteella. Havainnointi mahdollistaa näiden kutsujen tarkan seurannan, mikä auttaa tunnistamaan toiminnot, jotka ovat liian hitaita tai kalliita. Tämä mahdollistaa tiimien optimoida kehotteita, valita tehokkaampia malleja tai suunnitella työnkulkuja uudelleen hallitakseen operatiivisia kustannuksia ja varmistaakseen hyvän käyttäjäkokemuksen.
*   **Luottamus, turvallisuus ja vaatimustenmukaisuus**: Monissa sovelluksissa on tärkeää varmistaa, että agentit toimivat turvallisesti ja eettisesti. Havainnointi tarjoaa auditointijäljen agentin toimista ja päätöksistä. Tätä voidaan käyttää havaitsemaan ja lieventämään ongelmia, kuten kehotteen manipulointia, haitallisen sisällön tuottamista tai henkilötietojen väärinkäsittelyä. Esimerkiksi jälkiä voidaan tarkastella ymmärtääkseen, miksi agentti antoi tietyn vastauksen tai käytti tiettyä työkalua.
*   **Jatkuvat parannussilmukat**: Havainnointidata on iteratiivisen kehitysprosessin perusta. Seuraamalla, miten agentit toimivat todellisessa maailmassa, tiimit voivat tunnistaa parannuskohteita, kerätä dataa mallien hienosäätöä varten ja validoida muutosten vaikutukset. Tämä luo palautesilmukan, jossa tuotannon havainnot online-arvioinnista ohjaavat offline-kokeiluja ja -parannuksia, mikä johtaa agenttien suorituskyvyn jatkuvaan parantamiseen.

## Tärkeät seurattavat mittarit

Agentin käyttäytymisen seuraamiseksi ja ymmärtämiseksi on seurattava useita mittareita ja signaaleja. Vaikka tietyt mittarit voivat vaihdella agentin tarkoituksen mukaan, jotkut ovat yleisesti tärkeitä.

Tässä ovat yleisimmät mittarit, joita havainnointityökalut seuraavat:

**Viive:** Kuinka nopeasti agentti vastaa? Pitkät odotusajat heikentävät käyttäjäkokemusta. Viivettä tulisi mitata tehtävien ja yksittäisten vaiheiden osalta jäljittämällä agentin suorituksia. Esimerkiksi agentti, joka käyttää 20 sekuntia kaikkiin mallikutsuihin, voisi nopeutua käyttämällä nopeampaa mallia tai suorittamalla mallikutsut rinnakkain.

**Kustannukset:** Mikä on agentin suorituksen kustannus? AI-agentit luottavat LLM-kutsuihin, jotka laskutetaan tokenien perusteella, tai ulkoisiin API:hin. Usein toistuvat työkalujen käytöt tai useat kehotteet voivat nopeasti kasvattaa kustannuksia. Esimerkiksi, jos agentti kutsuu LLM:ää viisi kertaa vain marginaalisen laadun parantamiseksi, sinun on arvioitava, ovatko kustannukset perusteltuja, vai voisiko kutsujen määrää vähentää tai käyttää halvempaa mallia. Reaaliaikainen seuranta voi myös auttaa tunnistamaan odottamattomia piikkejä (esim. virheitä, jotka aiheuttavat liiallisia API-silmukoita).

**Pyyntövirheet:** Kuinka monta pyyntöä agentti epäonnistui? Tämä voi sisältää API-virheitä tai epäonnistuneita työkalukutsuja. Agentin tekemisestä kestävämmän näitä vastaan tuotannossa voi auttaa esimerkiksi varajärjestelmien tai uudelleenkokeilujen asettaminen. Esim. jos LLM-palveluntarjoaja A on alhaalla, voit vaihtaa varapalveluntarjoajaan B.

**Käyttäjäpalaute:** Suoran käyttäjäarvioinnin toteuttaminen tarjoaa arvokasta tietoa. Tämä voi sisältää eksplisiittisiä arvioita (👍peukku ylös/👎alas, ⭐1-5 tähteä) tai tekstikommentteja. Jatkuva negatiivinen palaute on merkki siitä, että agentti ei toimi odotetusti.

**Epäsuora käyttäjäpalaute:** Käyttäjien käyttäytyminen tarjoaa epäsuoraa palautetta, vaikka eksplisiittisiä arvioita ei annettaisi. Tämä voi sisältää esimerkiksi välittömän kysymyksen uudelleenmuotoilun, toistuvat kyselyt tai uudelleenkokeilupainikkeen klikkaukset. Esim. jos huomaat, että käyttäjät kysyvät toistuvasti samaa kysymystä, tämä on merkki siitä, että agentti ei toimi odotetusti.

**Tarkkuus:** Kuinka usein agentti tuottaa oikeita tai toivottuja tuloksia? Tarkkuuden määritelmät vaihtelevat (esim. ongelmanratkaisun oikeellisuus, tiedonhakutarkkuus, käyttäjätyytyväisyys). Ensimmäinen askel on määritellä, miltä onnistuminen agentin kohdalla näyttää. Voit seurata tarkkuutta automatisoitujen tarkistusten, arviointipisteiden tai tehtävän suoritusmerkintöjen avulla. Esimerkiksi jälkien merkitseminen "onnistuneiksi" tai "epäonnistuneiksi".

**Automaattiset arviointimittarit:** Voit myös asettaa automaattisia arviointeja. Esimerkiksi voit käyttää LLM:ää arvioimaan agentin tuotoksen, esim. onko se hyödyllinen, tarkka tai ei. On myös useita avoimen lähdekoodin kirjastoja, jotka auttavat arvioimaan agentin eri osa-alueita. Esim. [RAGAS](https://docs.ragas.io/) RAG-agenteille tai [LLM Guard](https://llm-guard.com/) haitallisen kielen tai kehotteen manipuloinnin havaitsemiseen.

Käytännössä näiden mittareiden yhdistelmä antaa parhaan kattavuuden AI-agentin tilasta. Tämän luvun [esimerkkivihkossa](../../../10-ai-agents-production/code_samples/10_autogen_evaluation.ipynb) näytämme, miltä nämä mittarit näyttävät todellisissa esimerkeissä, mutta ensin opimme, miltä tyypillinen arviointityönkulku näyttää.

## Instrumentoi agenttisi

Jälkitietojen keräämiseksi sinun on instrumentoitava koodisi. Tavoitteena on instrumentoida agenttikoodi tuottamaan jälkiä ja mittareita, jotka voidaan kerätä, käsitellä ja visualisoida havainnointialustalla.

**OpenTelemetry (OTel):** [OpenTelemetry](https://opentelemetry.io/) on noussut teollisuusstandardiksi LLM-havainnoinnissa. Se tarjoaa joukon API:ita, SDK:ita ja työkaluja telemetriatietojen tuottamiseen, keräämiseen ja viemiseen.

On olemassa monia instrumentointikirjastoja, jotka käärittävät olemassa olevat agenttikehykset ja tekevät OpenTelemetry-spanien viemisen havainnointityökaluun helpoksi. Alla on esimerkki AutoGen-agentin instrumentoinnista [OpenLit-instrumentointikirjastolla](https://github.com/openlit/openlit):

```python
import openlit

openlit.init(tracer = langfuse._otel_tracer, disable_batch = True)
```

Tämän luvun [esimerkkivihko](../../../10-ai-agents-production/code_samples/10_autogen_evaluation.ipynb) näyttää, kuinka instrumentoit AutoGen-agenttisi.

**Manuaalinen spanien luonti:** Vaikka instrumentointikirjastot tarjoavat hyvän perustan, on usein tapauksia, joissa tarvitaan yksityiskohtaisempaa tai mukautettua tietoa. Voit luoda spanit manuaalisesti lisätäksesi mukautettua sovelluslogiikkaa. Tärkeämpää on, että ne voivat rikastaa automaattisesti tai manuaalisesti luotuja spaneja mukautetuilla attribuuteilla (tunnetaan myös nimellä tagit tai metadata). Nämä attribuutit voivat sisältää liiketoimintakohtaista dataa, välilaskelmia tai mitä tahansa kontekstia, joka voi olla hyödyllistä vianetsinnässä tai analyysissä, kuten `user_id`, `session_id` tai `model_version`.

Esimerkki jälkien ja spanien manuaalisesta luomisesta [Langfusen Python SDK:lla](https://langfuse.com/docs/sdk/python/sdk-v3):

```python
from langfuse import get_client
 
langfuse = get_client()
 
span = langfuse.start_span(name="my-span")
 
span.end()
```

## Agentin arviointi

Havainnointi antaa meille mittareita, mutta arviointi on prosessi, jossa analysoidaan näitä tietoja (ja suoritetaan testejä) sen määrittämiseksi, kuinka hyvin AI-agentti toimii ja miten sitä voidaan parantaa. Toisin sanoen, kun sinulla on jäljet ja mittarit, miten käytät niitä agentin arvioimiseen ja päätösten tekemiseen?

Säännöllinen arviointi on tärkeää, koska AI-agentit ovat usein ei-deterministisiä ja voivat kehittyä (päivitysten tai mallin käyttäytymisen muutosten kautta) – ilman arviointia et tietäisi, toimiiko "älykäs agenttisi" todella hyvin vai onko se taantunut.

AI-agenttien arvioinnit voidaan jakaa kahteen kategoriaan: **offline-arviointi** ja **online-arviointi**. Molemmat ovat arvokkaita ja täydentävät toisiaan. Yleensä aloitetaan offline-arvioinnilla, sillä tämä on vähimmäisvaatimus ennen agentin käyttöönottoa.

### Offline-arviointi

![Datasetin kohteet Langfusessa](https://langfuse.com/images/cookbook/example-autogen-evaluation/example-dataset.png)

Tässä arvioidaan agenttia kontrolloidussa ympäristössä, tyypillisesti testidatojen avulla, ei live-käyttäjäkyselyiden. Käytät kuratoituja datasettiä, joissa tiedät, mikä on odotettu tulos tai oikea käyttäytyminen, ja ajat agenttisi niiden läpi.

Esimerkiksi, jos olet rakentanut matemaattisten sanallisten ongelmien ratkaisijan, sinulla voisi olla [testidatasetti](https://huggingface.co/datasets/gsm8k), jossa on 100 ongelmaa ja tunnetut vastaukset. Offline-arviointi tehdään usein kehityksen aikana (ja se voi olla osa CI/CD-putkia) parannusten tarkistamiseksi tai taantumien estämiseksi. Etuna on, että se on **toistettavissa ja voit saada selkeitä tarkkuusmittareita, koska sinulla on totuuspohja**. Voit myös simuloida käyttäjäkyselyitä ja mitata agentin vastauksia ihannetuloksiin nähden tai käyttää yllä kuvattuja automaattisia mittareita.

Offline-arvioinnin keskeinen haaste on varmistaa, että testidatasetti on kattava ja pysyy ajankohtaisena – agentti voi suoriutua hyvin kiinteästä testijoukosta, mutta kohdata hyvin erilaisia kyselyitä tuotannossa. Siksi testijoukkoja tulisi päivittää uusilla reunatapauksilla ja esimerkeillä, jotka heijastavat todellisia skenaarioita. Pieniä "savutesti"-tapauksia ja laajempia arviointijoukkoja kannattaa yhdistää: pienet joukot nopeisiin tarkistuksiin ja laajemmat laajempiin suorituskykymittareihin.

### Online-arviointi

![Havainnointimittareiden yleiskatsaus](https://langfuse.com/images/cookbook/example-autogen-evaluation/dashboard.png)

Tämä viittaa agentin arviointiin live-ympäristössä, eli todellisessa käytössä tuotannossa. Online-arviointi sisältää agentin suorituskyvyn jatkuvan seurannan todellisissa käyttäjävuorovaikutuksissa ja tulosten analysoinnin.

Esimerkiksi voit seurata onnistumisprosentteja, käyttäjätyytyväisyyspisteitä tai muita mittareita live-liikenteessä. Online-arvioinnin etuna on, että se **paljastaa asioita, joita et ehkä osannut ennakoida laboratorio-olosuhteissa** – voit havaita mallin ajautumisen ajan myötä (jos agentin tehokkuus heikkenee syötemallien muuttuessa) ja tunnistaa odottamattomia kyselyitä tai tilanteita, joita ei ollut testidatassasi. Se tarjoaa todellisen kuvan siitä, miten agentti käyttäytyy käytännössä.

Online-arviointi sisältää usein epäsuoran ja suoran käyttäjäpalautteen keräämisen, kuten aiemmin mainittiin, ja mahdollisesti varjotestien tai A/B-testien suorittamisen (joissa uusi agenttiversio toimii rinnakkain vanhan kanssa vertailua varten). Haasteena on, että live-vuorovaikutuksille voi olla vaikea saada luotettavia merkintöjä tai pisteitä – voit joutua tukeutumaan käyttäjäpalautteeseen tai alavirran mittareihin (esim. klikkasiko käyttäjä tulosta).

### Näiden yhdistäminen

Online- ja offline-arvioinnit eivät ole toisiaan poissulkevia; ne täydentävät toisiaan vahvasti. Online-seurannan havainnot (esim. uudet käyttäjäkyselytyypit, joissa agentti suoriutuu huonosti) voidaan käyttää offline-testidatasetin laajentamiseen ja parantamiseen. Vastaavasti agentit, jotka suoriutuvat hyvin offline-testeissä, voidaan ottaa luottavaisemmin käyttöön ja seurata online-ympäristössä.

Itse asiassa monet tiimit omaksuvat silmukan:

_arvioi offline -> ota käyttöön -> seuraa online -> kerää uusia epäonnistumistapauksia -> lisää offline-datasettiin -> hienosäädä agenttia -> toista_.

## Yleisiä ongelmia

Kun otat AI-agentteja käyttöön tuotannossa, saatat kohdata erilaisia haasteita. Tässä on joitakin yleisiä ongelmia ja mahdollisia ratkaisuja:

| **Ongelma**    | **Mahdollinen ratkaisu**   |
| ------------- | ------------------ |
| AI-agentti ei suorita tehtäviä johdonmukaisesti | - Hienosäädä agentille annettua kehotetta; ole selkeä tavoitteista.<br>- Tunnista, missä tehtävien jakaminen osatehtäviin ja niiden käsittely useilla agenteilla voi auttaa. |
| AI-agentti joutuu jatkuviin silmukoihin  | - Varmista, että sinulla on selkeät lopetusehdot, jotta agentti tietää, milloin prosessi päättyy.<br>- Käytä monimutkaisiin tehtäviin, jotka vaativat päättelyä ja suunnittelua, suurempaa mallia, joka on erikoistunut päättelyte

- Hienosäädä määritellyt parametrit, kehotteet ja työkalujen nimet.  |
| Moniagenttijärjestelmä ei toimi johdonmukaisesti | - Hienosäädä jokaiselle agentille annetut kehotteet varmistaaksesi, että ne ovat tarkkoja ja erottuvat toisistaan.<br>- Rakenna hierarkkinen järjestelmä käyttämällä "reititys"- tai ohjausagenttia määrittämään, mikä agentti on oikea. |

Monet näistä ongelmista voidaan tunnistaa tehokkaammin, kun käytössä on havainnointityökaluja. Aiemmin käsitellyt jäljitykset ja mittarit auttavat tarkasti paikantamaan, missä kohtaa agentin työnkulussa ongelmat ilmenevät, mikä tekee virheenkorjauksesta ja optimoinnista huomattavasti tehokkaampaa.

## Kustannusten hallinta

Tässä on joitakin strategioita tekoälyagenttien tuotantoon viemisen kustannusten hallintaan:

**Pienempien mallien käyttö:** Pienet kielimallit (Small Language Models, SLM) voivat suoriutua hyvin tietyissä agenttipohjaisissa käyttötapauksissa ja vähentävät kustannuksia merkittävästi. Kuten aiemmin mainittiin, arviointijärjestelmän rakentaminen suorituskyvyn ja suurempien mallien vertailuun on paras tapa ymmärtää, kuinka hyvin SLM suoriutuu käyttötapauksessasi. Harkitse SLM:ien käyttöä yksinkertaisiin tehtäviin, kuten aikomusten luokitteluun tai parametrien poimintaan, ja varaa suuremmat mallit monimutkaisempaan päättelyyn.

**Reititysmallin käyttö:** Samankaltainen strategia on käyttää erilaisia malleja ja kokoluokkia. Voit käyttää LLM/SLM-mallia tai palvelutonta funktiota reitittämään pyynnöt monimutkaisuuden perusteella parhaiten sopiville malleille. Tämä auttaa vähentämään kustannuksia ja varmistaa samalla suorituskyvyn oikeissa tehtävissä. Esimerkiksi yksinkertaiset kyselyt voidaan ohjata pienemmille, nopeammille malleille, ja kalliita suuria malleja käytetään vain monimutkaisiin päättelytehtäviin.

**Vastausten välimuistitus:** Yleisimpien pyyntöjen ja tehtävien tunnistaminen ja vastausten tarjoaminen ennen kuin ne kulkevat agenttijärjestelmän läpi on hyvä tapa vähentää samankaltaisten pyyntöjen määrää. Voit jopa toteuttaa prosessin, joka tunnistaa, kuinka samanlainen pyyntö on välimuistissa oleviin pyyntöihin, käyttämällä yksinkertaisempia tekoälymalleja. Tämä strategia voi merkittävästi vähentää kustannuksia usein kysytyissä kysymyksissä tai yleisissä työnkuluissa.

## Katsotaan, miten tämä toimii käytännössä

[Esimerkkivihkossa tämän osion kohdalla](../../../10-ai-agents-production/code_samples/10_autogen_evaluation.ipynb) näemme esimerkkejä siitä, miten voimme käyttää havainnointityökaluja agentin seurantaan ja arviointiin.

## Edellinen oppitunti

[Metakognition suunnittelumalli](../09-metacognition/README.md)

## Seuraava oppitunti

[MCP](../11-mcp/README.md)

**Vastuuvapauslauseke**:  
Tämä asiakirja on käännetty käyttämällä tekoälypohjaista käännöspalvelua [Co-op Translator](https://github.com/Azure/co-op-translator). Vaikka pyrimme tarkkuuteen, huomioithan, että automaattiset käännökset voivat sisältää virheitä tai epätarkkuuksia. Alkuperäistä asiakirjaa sen alkuperäisellä kielellä tulisi pitää ensisijaisena lähteenä. Kriittisen tiedon osalta suositellaan ammattimaista ihmiskäännöstä. Emme ole vastuussa väärinkäsityksistä tai virhetulkinnoista, jotka johtuvat tämän käännöksen käytöstä.