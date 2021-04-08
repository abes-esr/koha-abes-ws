# Groupe Koha/ABES

Le groupe **Koha-ABES de l'Hackaton Koha 2021** a évalué les **services web de
l'ABES** dans la perspective de leur utilisation depuis le SIGB Koha. 

## Participants

- ABES :
  - Michael Serror
  - Thomas Michaux
  - François Mistral, mistral@abes.fr
- KohaLa :
  - Aurore Sorieux, aurore.sorieux@univ-rennes2.fr
  - Asyeh Ghafourian, asyeh.ghafourian@bulac.fr
  - olivier Delangle, olivier.delangle@univ-amu.fr
  - Julien Sicot, julien.sicot@univ-rennes2.fr
  - Sonia Bouis, sonia.bouis@univ-lyon3.fr
  - Frédéric Demians, f.demians@tamil.fr
  - Matthias Meusburger, matthias.meusburger@biblibre.com

Services Web considérés :

- multiwhere
- bibliocontrol
- AlgoLiens

Autre outil étudié : [Checksudoc](http://domybiblio.net/check_sudoc/), développé
par Yves Tomic.

## Bilan

Le groupe a identifié les besoins suivants d'améliorations des WS de l'ABES :

### Fonctionnalités unifiées

Les fonctionnalités des trois services web (multiwhere, bibliocontrol,
AlgoLiens) gagneraient à être unifiées :

- **multiwhere** est le modèle à suivre.

- **JSON** — Réponses de bibliocontrol et AlgoLiens en JSON. Cela facilite la 
  consommation des services web par les applications, comme un plugin Koha.

- **Filtrage** par ILN/RCR/PPN. Le filtrage par PPN manque à bibliocontrol et
  AlogLiens. Le filtrage par PPN est nécessaire pour proposer des services
  d'indentification des anomalies de catalogage directement depuis Koha, en
  affichage d'une notice ou dans un rapport de chargement quotidien de notices.

- **Autorités** — AlgoLiens détecte des anomalies de catalogage des autorités.
  Sur ce modèle, _bibliocontrol_ pourrait détecter des anomalies dans les
  autorités.

### Notices biblio

Les anomalies qui doivent être repérées dans les notices biblio :

**Zones obligatoires** — L'absence de zones (ou sous-zones) obligatoires est
détectée :

- 106 $a
- 181
- 182
- 183
- 6xx $2
  
**Zones interdites** — La présence de certaines zones est détectée comme étant
une anomalie :

- 309

**Sous-zones de liens**
- Vers autorités :
  - 500 $3 
  - 6xx $3 (si $2 = 'rameau' ou 'Fmesh')
  - 7xx $3
- Vers notices :
  - 419 $0

**Conditionnels** — Les conditions suivantes (on pourrait leur trouver un nom)
sont détectées comme des erreurs :

| Zone  | Condition                                     |
| ----- | --------------------------------------------- |
| 100   | $a contient 'X' ET ind1 <> 1                  |
| 104   | $d <> 'ba' ET $c = 'y'                        |
| 104   | $f <> 'fr'                                    |
| 200   | $b <> ''                                      |
| 200   | $f <> '' ET pas_de_zone(7xx)                  |
| 241   | absence(214) ET notice < 'janvier 2020'       |
| 210/4 | type_doc ∈ (Ab, Ad, Ob, Od) ET absence(214) (ou 210 avant 1/1/2020) |
| 225   | présence(225) ET absence(410) ET absence(461) |
| 410   | présence(410) ET absence(225)                 |
| 7xx   | $4 = '000'                                    |

**Divers**

- **7xx selon $4** — Possibilité, en fonction de certains codes de fonction, de
  repérer l’utilisation d’une mauvaise étiquette en 7XX ? Exemples : Un
  préfacier (code fonction 080) doit être en 702 et pas en 700 ou 701 Un
  commissaire priseur (code fonction 065) doit être en 700 ou 701 et pas en 702

### Notices d'autorité

**Zones obligatoires** — L'absence de zones (ou sous-zones) obligatoires est
détectée :

- 200$9
- 200$c (à confirmer avec le pôle Autorités de l’Abes)
- 400$9
- 810

**Conditionnels** — Les conditions suivantes (on pourrait leur trouver un nom)
sont détectées comme des erreurs :

| Zone  | Condition                                     |
| ----- | --------------------------------------------- |
| 103   | $a et $b ne contiennent pas [0-9X] (chiffres arabes et la lettre X) |
| 103   | $a='XXX' OU $b='XXX                           |
| 106   | ($a, $b, $c) contient '#'                     |
| 200   | présence($f) ET absence(103)                  |
| 300   | type_doc(Td) ET présence(300)                 |
| 340   | type_doc(Td) ET absence(340)                  |
| 810   | contient @                                    |
