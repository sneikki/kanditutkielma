# 1. Johdanto

# 2. Taustoitus

* Haittaohjelma-analyysin tarpeet 
* Haittaohjelmien tunnistamisessa käytettyjä menetelmiä
* Olemassaolevat lähestymistavat puutteineen
* Homologia & samankaltaisuus

# 3. Paloittain määritellyt hajautusarvot

* Periaate
* Kuvaus
* Rolling hash
* ssdeep

# 4. Haittaohjelmien torjunta sumeilla tiivisteillä

* Haittaohjelman tunnistaminen
* Tiivisteiden indeksointi ja levittäminen
* Tehokkuus
* Edut/ongelmat

# 5. Haavoittuvuudet ja hyökkäykset

* Tulosten tarkoituksellinen manipulaatio
* Menetelmien heikkoudet
	* Semanttinen analyysin suosiminen syntaktisen sijaan

* Osuman aiheuttavien mutta semanttisesti erilaisten tiedostojen generointi
	*	Kuluttaa tutkintaresursseja
	* Lähde pyrki tuottamaan proseduraalissti kuvan, joka on semanttisesti tunnistamaton mutta jonka ssdeep yhdistää alkuperäiseen kuvaan
		*	Yritys ei onnistunut; ssdeep tunnisti kuvat
		* Lähde mainitsee potentiaalisia optimointimentelmiä

*	Semanttisesti identtisen mutta osumaa aiheuttamattoman tiedoston generointi
	* Ei voida havaita aiempien tiivisteiden perusteella; voidaan naamioida haitallista sisältöä
	* Lähde tutki ssdeep-, SDHASH- ja TLSH-ohjelmistojen luotettavuutta
		* Verrattiin eri tavoin muutettuja kuvatiedostoja alkuperäisiin
		* Verrattiin eri tavoin muutettuja tekstitiedostoja alkuperäisiin
		* Verrattiin eri tavoin muutettuja ohjelmakoodeja
		* Mainitsee erityisesti ohjelmakoodin tunnistamisen olevan haastavaa sumeilla tiivisteillä
		* ssdeep on tehoton samankaltaisten kuvien tunnistamisessa; sdhash ja TLSH ovat tehokkaita
				* sdhash ei yhdistänyt käännettyjä tai venytettyjä kuvia alkuperäisiin
		* Mainitsee erilaisia tapoja ohjelmakoodin muuttamiseen hämäystarkoituksessa
		* Erilaisilla muutoksilla on poikkeavia vaikutuksia tiivisteisiin; toiset muuttavat enemmän kuin toiset
	
# 6. Yhteenveto

