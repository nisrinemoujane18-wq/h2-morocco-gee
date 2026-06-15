# 📤 Outputs — H₂ Morocco GEE

## Dossier Google Drive : `H2_Vert_Maroc_Final_v6/`

Après exécution des 16 tâches GEE, les fichiers suivants sont exportés :

## Cartes d'aptitude (GeoTIFF, 5 km, WGS84)

| Fichier | Type | Description |
|---------|------|-------------|
| `01_Aptitude_Solaire_Norm.tif` | Float [0–100] | Score aptitude solaire PV normalisé |
| `02_Aptitude_Eolien_Norm.tif` | Float [0–100] | Score aptitude éolienne normalisé |
| `03_Aptitude_Hybride_Norm.tif` | Float [0–100] | Moyenne solaire + éolien |

## Couches de critères reclassifiés (GeoTIFF)

| Fichier | Classes | Description |
|---------|---------|-------------|
| `04_GHI_classe.tif` | 1–5 | Irradiation solaire |
| `05_Vent_classe.tif` | 1–5 | Vitesse du vent à 200m |
| `06_Pente_classe.tif` | 1–5 | Pente du terrain |
| `07_Temp_classe.tif` | 1–4 | Température de surface |
| `08_Cote_Mer_classe.tif` | 1–4 | Distance à la côte |
| `09_Villes_classe.tif` | 1–4 | Distance zones urbaines |
| `10_Routes_classe.tif` | 1–4 | Distance routes (proxy VIIRS) |
| `11_Elec_classe.tif` | 1–4 | Distance réseau électrique |
| `12_Rivieres_classe.tif` | 1–4 | Distance cours d'eau |
| `13_Barrages_classe.tif` | 1–4 | Distance barrages |
| `14_Masque_Exclusion.tif` | 0/1 | Zones exclues (0) / valides (1) |

## Tableaux CSV

### `15_Extraction_12_Sites_H2.csv`
Scores d'aptitude aux coordonnées des 12 sites stratégiques.

Colonnes : `nom`, `region`, `01_Aptitude_Solaire_Norm`, `02_Aptitude_Eolien_Norm`,
`03_Aptitude_Hybride_Norm`, + toutes les couches de critères.

### `16_Stats_Regions_H2.csv`
Statistiques moyennes par région administrative (réduction spatiale à 5 km).

Colonnes : nom de région + moyennes de toutes les couches.

## Utilisation dans QGIS

1. Importer les fichiers `.tif` via **Couche → Ajouter une couche raster**
2. Appliquer une rampe de couleurs (ex. `RdYlGn` pour les aptitudes)
3. Ajouter la couche des 12 sites (CSV → Couche de texte délimité)
4. Exporter en PDF ou PNG pour publication
