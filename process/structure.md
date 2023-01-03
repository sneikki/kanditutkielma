#Aihe

Käsittelen työssäni sumeita tiivisteitä. Tarkastelen niitä erityisesti
haittaohjelmien tunnistamisen näkökulmasta pohtien seuraavia kysymyksiä:
* Kuinka sumeat tiivisteet suoriutuvat haittaohjelmien tunnistamisessa aiempiin menetelmiin nähden?
* Voidaanko sumeita tiivisteitä hyödyntää mielekkäästi/tehokkaasti haittaohjelmien tunnistamisessa?
* Onko sumeiden tiivisteiden luotettavauus ja vakaus riittävä haittaohjelmien tunnistamiseen?
* Millaisin menetelmin sumeita tiivisteitä voidaan johtaa harhaan?
* Millaisia eroja erityyppisten ohjelmistojen välillä on?
* Millaisia puutteita sumeissa tiivisteissä ilmenee erilaisissa ympäristöissä?

**Otsikko:** Sumeat tiivisteet

## Table of contents

**1 Johdanto** (1 sivu)

**2 Sumea tiiviste** (4 sivua)

2.1 Samankaltaisuus

2.3 Kontekstista riippuva tiiviste

**Kuva:** Visuaalinen esitys tiivistysprosessista

**Taulukko:** vakiokokoisten lohkojen puutteen havainnollistaminen

2.4 Tilastollisesti epätyypilliset piirteet / Lohkotiiviste

**Kuva:** Visuaalinen esitys tiivistysprosessista
	
**3 Sumean tiivistämisen ohjelmistot** (5 sivua)

3.1 ssdeep

**Taulukko:** esimerkki ssdeep-ohjelmiston käytöstä komentorivillä

3.2 sdhash

3.3 mvhash-b

**4 Soveltaminen haittaohjelmien torjunnassa** (5 sivua)

4.1 Edellytykset

4.2 Tunnistaminen sumealla tiivisteellä

4.3 Tunnistamisen välttäminen

**5 Sumeiden tiivisteiden haasteet** (3 sivua)

5.1 Kootusti edellisen luvun tulosten vertailua ohjelmistojen välillä, rajoittavia tekijöitä

5.2 Tarkoituksellinen hämäys

**Kuva:** kuva naamiointia ennen

**Kuva:** kuva naamioinnin jälkeen

**6 Yhteenveto** (1 sivu)
	
# 1. Johdanto (1 sivu)

# 2. Sumeat tiivisteet (4 sivua)
Tarkoittaen käytännössä että tässä luvussa käsitellään
fuzzy hashien tyypit abstraktilla tasolla.

**Kuva:** Flow chart sumean tiivisteen generoinnista
1. Input file
2. Detect trigger conditions to determine file shard location
3. Calculate every fragment hash value
4. Compression mapping of each hash value
5. Connect all compressed hash values
6. Output the file’s fuzzy hash value 

* Samankaltaisuus
		* Ei määriteltävissä eksaktisti
		* Voi esittää lukemattomalla tavalla
		* Löydettävä homologioita
				* Tilanteesta ja valitusta menetelmästä
					riippuu millä tavoin homologioita etsitään. 
* Are themselves a family similar hash functions 
* Types of fuzzy hashes
	* Context triggered piecewise hash
		* match if all inputs have a rather large part in common
		* example software: ssdeep
	* Statistically impropbable features
		* match if enough features exist in all inputs
		* example software: sdhash
	* Block based hash
			* example software: mvhash-b

Briefly describe the concept of piecewise hashing. Not more than
a couple of paragraphs. Then proceed to CTPH:
Discuss the context, what it offers. Keep disscussion on abstract level,
don't go into details on rolling hash etc. A little more comprehensize discussion
than on piecewise hashing, but also keep this brief.

**Keywords:**
* rolling hash
* block size
* trigger value
* comparison

Briefly explain the concept of BBH/SIF. Again not too long but still
reasonably longer amount of time should be spent on this matter as
I hardly have any information. Maintain decent level of abstractness.

**Keywords:**
* features
* bloom filters
* majority voting

## Todo
* study block based hashing

# 3. Sumean tiivistämisen ohjelmistot (5 sivua)

## ssdeep
family: context triggred piecewise hash
feature extraction: context detection with Alder-32 rolling hash
distance function: weighted edit distance
fixed sized
ssdeep is sensitive to byte ordering

## sdhash
family: statistically impropbable features
feature extraction: winnowing to select entropy estimates
feature generation: Bloom filter
distance function: average of the maximum of per-filter in one set AND
	each counterpart filter
variable lenght

## mvhash-b
family: block based hash
feature extraction: majority vote followed by RLE
feature generation: Bloom filter
distance function: Average the minimums of per-filter in one set XOR
	each counterpart filters

## Todo
* bloom filter DONE
* ssdeep, sdhash, mvhash-b DONE
* statistically impropbable features DONE
* block based hash DONE
* edit distance

# 4. Soveltaminen haittaohjelmien torjunnassa (5 sivua)

Write a short introduction of 1-3 paragraphs about detecting malware.
Discuss briefly common meethods of malware detection.

* Haittaohjelma-analyysin vaatimukset (näille lähde)
	* Skaalautuvuus
	* Tehokkuus
	* Luotettavuus
	* Tarkkuus
* Olemassaolevat haittaohjelmien tunnistusmenetelmät puutteineen
	* Havaitut haittaohjelmat tiivistetään kryptografisella
		tiivistefunktiolla (MD5, SHA-1 jne.)
	* Tiivisteet talletetaan indeksiin
	* Epäilyttävälle ohjelmistolle luodaan tiiviste
	* Tiivistettä verrataan indeksiin talletettuihin tiivisteisiin
	* Osuma tarkoittaa epäillyn ohjelman olevan lähes varmuudella
		jokin tunnettu haittaohjelma
	* Yksinkertainen mutta mustavalkoinen
		*	Muutettua ohjelmaa ei voida yhdistää tiivisteen
			perusteella alkuperäiseen
* Sumeat tiivisteet
	* Vertailua keskenään
	* Vertailua perinteisiin menetelmiin
	* Huomioitavaa
	* Etuja, puutteita
		*	Vaativuus
		*	Tiivisteen koko
		* Ohjelmistojen erot tarkkuudessa tai suorituskyvyssä
		* Tiivistetyyppin lähestymistavan vaikutus haittaohjelmien torjunnassa
	* Algoritmien ja ohjelmistojen piireet, sopivuus tehtävään jne.,
		ei kuitenkaan harhauttamiseen ja hyökkäyksen näkökulmasta.
	* Huomioitavaa:
		* When choosing a software
			* Accuracy at identifying similar content
			* Robustness to attack
			* Time to calculate digest
			* Time to perform a nearest neighbor search
			* Time and suitability for large scale clustering
			* Size of the digest (fixed size is preferred)
		* Fixed size fingerprint does not allow for meaningful comparison between a smaller
			file and a significantly larger one (Hashing and Data Fingerprinting in Digital Forensics)

# 5. Sumean tiivistyksen haasteet (3 sivua)

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
* Pakattu data
* Tulosten tulkinnan subjektiivisuus
* Pieni syöte

	
# 6. Yhteenveto (1 sivu)
