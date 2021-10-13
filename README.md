# Groupe Koha/ABES

Le groupe **Koha-ABES de l'Hackathon Koha 2021** a évalué les **services web de
l'ABES** dans la perspective de leur utilisation depuis le SIGB Koha. 

![Abes](img/logo-abes.svg)
![KohaLa](img/logo-kohala.png)

CONTENU :

- [Groupe Koha/ABES](#groupe-kohaabes)
  - [Participants](#participants)
  - [Bilan](#bilan)
    - [Fonctionnalités unifiées](#fonctionnalités-unifiées)
    - [Notices biblio](#notices-biblio)
    - [Notices d'autorité](#notices-dautorité)

## Conception et développement d'un plugin expérimental (par Tamil)

- [Plugin KohaLa-Abes](https://github.com/AssoKohala/Koha-Plugin-KohaLa-AbesWS)
  
## Participants

- ABES :
  - Mickaël Seror, seror@abes.fr
  - Thomas Michaux, michaux@abes.fr
  - François Mistral, mistral@abes.fr
- KohaLa :
  - Aurore Sorieux, aurore.sorieux@univ-rennes2.fr
  - Asyeh Ghafourian, asyeh.ghafourian@bulac.fr
  - Olivier Delangle, olivier.delangle@univ-amu.fr
  - Julien Sicot, julien.sicot@univ-rennes2.fr
  - Sonia Bouis, sonia.bouis@univ-lyon3.fr
  - Frédéric Demians, f.demians@tamil.fr
  - Matthias Meusburger, matthias.meusburger@biblibre.com

Services Web considérés :

Voir : https://abes.fr/api-et-web-services/
et : http://documentation.abes.fr/sudoc/manuels/administration/aidewebservices/index.html

-   [**Iln2rcr**](http://documentation.abes.fr/aideidrefdeveloppeur/co/MicroWebIln2rcr.html) : renvoie la liste des n°RCR utilisant un même Système de Gestion de Bibliothèque (n°ILN)
-   [**rcr2iln**](http://documentation.abes.fr/aideidrefdeveloppeur/co/MicroWebRcr2iln.html) : renvoie les n°ILN de rattachement associés à une liste de [n°RCR](http://documentation.abes.fr/aideidrefdeveloppeur/co/MicroWebRcr2iln.html#kFootBsktN3f "RCR : Répertoire des Centre de Ressources (Infobulle)")
-   [**merged**](http://documentation.abes.fr/aideidrefdeveloppeur/co/MicroWebMerged.html) : renvoie l’identifiant d’une notice valide à partir de l’identifiant d’une notice devenue obsolète suite à fusion
-   [**merged inversé**](http://documentation.abes.fr/aideidrefdeveloppeur/co/MicroWebMerged_inv.html) : indique l’identifiant d’une notice devenue obsolète à partir de l’identifiant d’une notice valide, suite à une fusion
-   [**BiblioControl**](http://documentation.abes.fr/sudoc/manuels/administration/aidewebservices/index.html#BiblioControl) Ce webservice fournit pour un RCR la liste des notices bibliographiques ayant au moins une anomalie au regard des contrôles effectués (puisqu'un même PPN peut en avoir plusieurs - il y aura de fait plusieurs lignes dans le rapport)
-   [**multiwhere**](http://documentation.abes.fr/sudoc/manuels/administration/aidewebservices/index.html#multiwhere) Ce webservice permet de localiser (RCR de localisation) plusieurs documents à partir de leur identifiant (PPN)
-  [**biblio**](http://documentation.abes.fr/aideidrefdeveloppeur/co/MicroWebBiblio.html) : renvoie la liste des ressources bibliographiques Sudoc liées à une notice d’autorité
-   [**idref2id**](http://documentation.abes.fr/aideidrefdeveloppeur/co/MicroWebIdref2id.html) : fournit les identifiants d’une dizaine d’autres systèmes (à spécifier dans la requête) à partir d’un identifiant IdRef
-   [**id2idref**](http://documentation.abes.fr/aideidrefdeveloppeur/co/MicroWeb_ServiceId2idref.html) : fournit un identifiant IdRef à partir d’identifiants d’autres systèmes (à spécifier dans la requête)
-   [**frbn2ppn / ocn2ppn / dnb2ppn / ucatb2ppn / frcairninfo2ppn**](http://documentation.abes.fr/sudoc/manuels/administration/aidewebservices/index.html#IdentifiantSudocExterne) : renvoient un identifiant de notice Sudoc (n°PPN) à partir d’un identifiant de notice issue d’une autre base
-   [**isbn2ppn / ean2ppn / issn2ppn**](http://documentation.abes.fr/sudoc/manuels/administration/aidewebservices/co/IdentifiantSudoc.html) : renvoient les identifiants de notice Sudoc (n°PPN) à partir d’identifiants normalisés (ISBN, EAN, ISSN)
-   [**métarevues**](http://documentation.abes.fr/sudoc/manuels/administration/aidewebservices/co/metarevues.html) : génère l’historique complet  d’une revue – imprimée et/ou électronique – à partir d’un identifiant notice Sudoc (n°PPN) 
-   [**multiwhere**](http://documentation.abes.fr/sudoc/manuels/administration/aidewebservices/co/multiwhere.html) : liste les bibliothèques du réseau Sudoc possédant un même document
-   [**nnt2ppn**](http://documentation.abes.fr/sudoc/manuels/administration/aidewebservices/co/MicroWebServiceNNT.html) : renvoie un identifiant de notice Sudoc (n°PPN) à partir du Numéro National de Thèses (NNT)
-   [**ppn2nnt**](http://documentation.abes.fr/sudoc/manuels/administration/aidewebservices/co/MicroWebServiceNNT.html) : renvoie le Numéro National de Thèses (NNT) à partir d’un identifiant de notice Sudoc (n°PPN)
-   [**unimarc2marcxml**](http://documentation.abes.fr/sudoc/manuels/administration/aidewebservices/co/SudocMarcXML.html) : à partir de leur n°PPN, les notices Sudoc en UNIMARC sont renvoyées au format MarcXML
-   [**ppn2epn**](http://documentation.abes.fr/sudoc/manuels/administration/aidewebservices/co/MicroWebServicePPN2EPN.html) : renvoie le numéro d’exemplaire (EPN) lié à un RCR à partir d’un ou de plusieurs PPN
-   [**id2kbart**](http://documentation.abes.fr/aidebacon/index.html#WebserviceId2) : permet de savoir à quel(s) bouquet(s) appartient un document en fonction de son identifiant
-   [**AlgoLiens**](http://documentation.abes.fr/sudoc/manuels/controle_bibliographique/algoliens/) ce webservice permet à chaque bibliothèque du réseau Sudoc de savoir quelles sont les notices où manque un lien à une notice d'autorité dans leurs zones de liens
-   [**SciencePlus**](https://scienceplus.abes.fr/) La base de données scienceplus.abes.fr expose les métadonnées de corpus de publications scientifiques numériques (revues, ebooks, articles, chapitres) pour lesquelles l'Abes a obtenu le droit de réutilisation de la part des éditeurs, notamment dans le cadre des programmes d’achat de documentation sous licence nationale (ISTEX et CollEx-Persée).


Autres outils proposés par et pour la communauté autour de ces webservice : 
- [Checksudoc](http://domybiblio.net/check_sudoc/), développé par Yves Tomic
- [e-PPNator](http://akareup.alwaysdata.net/controlequalite.html), développé par Pierre Marige
- [ezlibrapi](https://t.co/JS9YGntwRA), développé par université catholique de Lille
- [Algoliens-web](https://github.com/abes-esr/algoliens-web), développé par Sylvain Machefert au sein de l'université Bordeaux Montaigne
- [eplouribousse](https://eplouribousse1.di.unistra.fr/), développé et maintenu par l'université de Strasbourg
- [KaliDoS (Qualité des Données du Sudoc)](https://github.com/abes-esr/kalidos),  développée par des étudiants du Master Informatique de l'Université Lyon 1, en collaboration avec la BU
- [sudoc-toolkit](https://github.com/abes-esr/sudoc-toolkit), développé par Géraldine Geoffroy (SCD Université Nice Sophia Antipolis)
- [Abacaxi - The Library Metadata Hub](https://github.com/nicomo/abacaxi), développé par Nicolas Morin
- [VérifSudoc](https://applintern.scd.univ-paris-diderot.fr/verifsudoc/), développé par l'université de Paris


## Bilan

Le groupe a identifié les besoins suivants d'améliorations des WS de l'ABES :

### Fonctionnalités unifiées

Les fonctionnalités des trois services web (multiwhere, bibliocontrol,
AlgoLiens) gagneraient à être unifiées :

- **multiwhere** est le modèle à suivre.

- **JSON** — Réponses de bibliocontrol et AlgoLiens en JSON. Cela facilite la 
  consommation des services web par les applications, comme un plugin Koha.

- **Filtrage** par ILN/RCR/PPN et Unica. Le filtrage par PPN manque à bibliocontrol et
  AlgoLiens. Le filtrage par PPN est nécessaire pour proposer des services
  d'identification des anomalies de catalogage directement depuis Koha, en
  affichage d'une notice ou dans un rapport de chargement quotidien de notices.

- **Autorités** — AlgoLiens détecte dans les notices bibliographiques les zones où le lien est manquant vers une notice d'autorité. Il n'existe pas à l'heure actuelle un 
webservice qui contrôle les anomalies dans les notices d'autorité.

- **Webservice bibliocontrol** — Ce webservice contrôle actuellement que 3 zones dans les notices bibliographiques : présence d'une 225 sans 410 ou 461 ; code de fonction 000 (code de fonction indéterminé) en zone 700, 701 ou 702 ; présence simultanée d'une zone 181 et d'une 200 $b.
 
### Notices bibliographiques

Nous nous sommes attachés pour les notices bibliographiques à repérer les anomalies qui peuvent concerner l'ensemble des types de documents signalés dans le Sudoc. Mais il serait peut-être intéressant de voir s'il serait possible, selon certains types de document, de repérer en plus les zones indispensables attendues. Ce repérage pourrait se faire soit sur la 008 et/ou les 181, 182 et 183. Exemples :

- pour une carte : 008 (Ka) et/ou 181 $ccri. La notice doit avoir la zone 206 (données mathématiques)
- pour une ressource électronique : 008 (Oa, Ob etc.) et/ou 182 $cc. La notice doit avoir la zone 230 et les différentes zones de notes (303, 304, 307, 337 etc.)

Les anomalies qui doivent être repérées dans les notices bibliographiques :

**Zones obligatoires** — L'absence de zones (ou sous-zones) obligatoires est
détectée :

- 106 $a
- 181
- 182
- 183
  
**Zones ou sous-zones interdites** — La présence de certaines zones ou sous-zones est détectée comme étant
une anomalie :

- 008 $a 'y' et 'B'
- 200 $b
- 210 sauf type doc Ab, Ad, Ob, Od pour notices créées avant 01/01/2020
- 309

**Sous-zones de liens** — L'absence de liens est détectée comme étant une anomalie :

- Vers notices d'autorités :
  - 500 $3 
  - 6XX $3 (si $2 = 'rameau' ou 'Fmesh')
  - 7XX $3
  
- Vers notices bibliographiques :
  - 410 $0

**Conditionnels** — Les conditions suivantes (on pourrait leur trouver un nom)
sont détectées comme des erreurs :

| Zone  | Condition                                     |
| ----- | --------------------------------------------- |
| 100   | $a contient 'X' ET ind1 = 0                   | 
| 104   | $d <> 'ba' ET $c = 'y'                        |
| 104   | $f <> 'fr'                                    |                                      
| 200   | présence ($f) ET absence (7XX)                  |
| 225   | présence (225) ET absence (410) OU absence (461)|
| 410   | présence (410) ET absence (225)               |
| 7XX   | présence (7XX) ET absence (200 $f)            |
| 700   | présence (700) ET présence 710 ou 720         |
| 7XX   | $4 = '000'                                    |

**Divers**

- **100 $a et 214 (ou 210)** — Possibilité de détecter que la date enregistrée en 100 $a concorde avec la date indiquée en 214 (ou 210) ?

- **Utilisation Tf** — Possibilité de détecter qu'une Tf est employée dans une zone 6XX autre que 608 (vérification ensuite pour voir si la forme constitue le sujet ?)

- **7XX selon $4** — Possibilité, selon certains codes de fonction, de
  repérer l’utilisation d’une mauvaise étiquette en 7XX ? Exemples : un
  préfacier (code fonction 080) doit être en 702 et pas en 700 ou 701 ; un
  commissaire priseur (code fonction 065) doit être en 700 ou 701 et pas en 702

### Notices d'autorité

Nous nous sommes concentrés à repérer les anomalies concernant les Personnes physiques (Td).

**Zones obligatoires** — L'absence de zones (ou sous-zones) obligatoires est
détectée :

- 200 $9
- 200 $c (à confirmer avec le pôle Autorités de l’Abes)
- 400 $9
- 810 $a

**Conditionnels** — Les conditions suivantes (on pourrait leur trouver un nom)
sont détectées comme des erreurs :

| Zone  | Condition                                     |
| ----- | --------------------------------------------- |
| 103   | présence $a et $b qui contiennent autres caractères que [0-9X] (chiffres arabes et la lettre X) |
| 103   | $a='XXXX' et $b='XXXX                         | 
| 103   | présence $a et $b ET absence (200 $f)         | 
| 106   | $a <> '0'                                     | 
| 106   | $b <> '1'                                     | 
| 106   | $c <> '0'                                     | 
| 200   | présence ($f) ET absence (103)                |
| 300   | type_doc (Td) ET présence (300)               | 
| 340   | type_doc (Td) ET absence (340)                |
| 810   | contient @                                    |
