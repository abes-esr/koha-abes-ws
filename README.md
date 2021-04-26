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

- [multiwhere](http://documentation.abes.fr/sudoc/manuels/administration/aidewebservices/index.html#multiwhere)
- [merged](http://documentation.abes.fr/sudoc/manuels/administration/aidewebservices/index.html#merged)
- [bibliocontrol](http://documentation.abes.fr/sudoc/manuels/administration/aidewebservices/index.html#BiblioControl)
- [AlgoLiens](http://documentation.abes.fr/sudoc/manuels/controle_bibliographique/algoliens/index.html)
- [API SRU BNF](https://api.bnf.fr/fr/api-sru-catalogue-general)
- Vue XML notice SUDOC : https://www.sudoc.fr/{PPN}.xml

Autres outils étudiés : [Checksudoc](http://domybiblio.net/check_sudoc/), développé
par Yves Tomic et [e-PPNator](http://akareup.alwaysdata.net/controlequalite.html), développé par Pierre Marige

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

- **Autorités** — AlgoLiens détecte des anomalies de catalogage des autorités.
  Sur ce modèle, _bibliocontrol_ pourrait détecter des anomalies dans les
  notices bibliographiques.
  
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

Nous nous sommes restreints pour les notices d'autorité à repérer les anomalies concernant les Personnes physiques.

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
| 103   | $a et $b ne contiennent pas [0-9X] (chiffres arabes et la lettre X) |
| 103   | $a='XXXX' OU $b='XXXX
| 103   | présence $a OU $b ET absence (200 $f)
| 106   | ($a, $b, $c) contient '#'                     |
| 200   | présence ($f) ET absence (103)                |
| 300   | type_doc (Td) ET présence (300)               | 
| 340   | type_doc (Td) ET absence (340)                |
| 810   | contient @                                    |
