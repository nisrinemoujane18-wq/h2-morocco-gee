# 🌍 H₂ Morocco — Cartographie Spatiale du Potentiel d'Hydrogène Vert

[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)
[![Platform: Google Earth Engine](https://img.shields.io/badge/Platform-Google%20Earth%20Engine-blue.svg)](https://earthengine.google.com/)
[![Status: Active](https://img.shields.io/badge/Status-Active-brightgreen.svg)]()

## 📌 Description

Ce dépôt contient le script **Google Earth Engine (GEE)** développé dans le cadre du Projet de Fin d'Études (PFE) réalisé à l'**IRESEN** (Institut de Recherche en Énergie Solaire et Énergies Nouvelles) — Département Hydrogène Vert.

L'objectif est d'identifier et de cartographier les **zones à haute potentialité** pour la production d'hydrogène vert au Maroc, en combinant :
- Analyse spatiale multi-critères (**MCDM/AHP**)
- Télédétection satellitaire (**Google Earth Engine**)
- Combinaison Linéaire Pondérée (**WLC**)

---

## 🗺️ Couverture Géographique

- **Territoire** : 12 régions administratives du Maroc (post-2015) + Sahara Occidental
- **Résolution spatiale** : 5 km
- **Période** : 2018–2022 (ressources énergétiques), 2010–2023 (température)

---

## 📂 Structure du Dépôt

```
h2-morocco-gee/
│
├── scripts/
│   └── h2_morocco_gee_v6.js      # Script GEE principal (version finale)
│
├── data/
│   └── README_data.md             # Description des sources de données
│
├── docs/
│   └── methodology.md             # Méthodologie AHP-WLC détaillée
│
├── outputs/
│   └── README_outputs.md          # Description des exports produits
│
├── README.md                      # Ce fichier
└── LICENSE                        # Licence MIT
```

---

## 🛰️ Sources de Données Satellitaires

| Critère | Source GEE | Résolution | Période |
|---------|-----------|------------|---------|
| GHI (Irradiation solaire) | ERA5-Land ECMWF | 9 km | 2018–2022 |
| Vitesse du vent (200 m) | ERA5-Land ECMWF | 9 km | 2018–2022 |
| Pente du terrain | SRTM 30m (USGS) | 30 m | Statique |
| Température de surface | MODIS MOD11A2 | 1 km | 2010–2023 |
| Distance zones urbaines | GPWv4 (CIESIN) | 1 km | 2020 |
| Distance routes/réseau | VIIRS Nighttime (NOAA) | 500 m | 2022 |
| Distance cours d'eau | HydroSHEDS (WWF) | 90 m | Statique |
| Distance barrages | JRC Global Surface Water 1.4 | 30 m | 1984–2021 |
| Distance côte maritime | JRC Global Surface Water 1.4 | 30 m | Global |

---

## ⚙️ Méthodologie

### Poids AHP par filière

| Critère | Solaire PV (%) | Éolien (%) |
|---------|---------------|------------|
| Ressource principale (GHI/Vent) | 35,4 | 40,2 |
| Pente | 23,8 | 20,8 |
| Température | 16,1 | 2,4 |
| Distance routes | 10,9 | 9,1 |
| Distance zones urbaines | 7,5 | 14,0 |
| Distance réseau électrique | 2,6 | 9,1 |
| Distance eau/barrages | 2,6 | 3,0 |
| Distance côte | 1,2 | 1,4 |

> **Ratios de Cohérence** : CR_Solaire = 0,030 < 0,10 ✅ | CR_Éolien = 0,036 < 0,10 ✅

### Score d'aptitude normalisé

```
S_j = (Σ w_k × c_kj) / S_max × 100
```

Avec masque d'exclusion : zones urbaines, eau permanente, neige, pente > 45°.

---

## 📍 Les 12 Sites Stratégiques

| Site | Région | Coordonnées |
|------|--------|-------------|
| Dakhla | Dakhla-Oued Ed-Dahab | 23.96°N, 15.65°O |
| Tarfaya | Laâyoune-Sakia El Hamra | 27.73°N, 12.95°O |
| Tan-Tan | Guelmim-Oued Noun | 28.44°N, 11.10°O |
| Agadir | Souss-Massa | 30.40°N, 9.53°O |
| Safi | Marrakech-Safi | 32.32°N, 9.23°O |
| Jorf Lasfar | Casablanca-Settat | 33.16°N, 8.60°O |
| Kénitra | Rabat-Salé-Kénitra | 34.26°N, 6.58°O |
| Tanger | Tanger-Tétouan-Al Hoceima | 35.73°N, 5.90°O |
| Meknès | Fès-Meknès | 33.89°N, 5.55°O |
| Nador | Oriental | 35.10°N, 2.85°O |
| Béni Mellal | Béni Mellal-Khénifra | 32.36°N, 6.35°O |
| Ouarzazate | Drâa-Tafilalet | 30.92°N, 6.89°O |

---

## 📤 Exports Produits (16 tâches GEE)

| # | Fichier | Description |
|---|---------|-------------|
| 01 | `01_Aptitude_Solaire_Norm.tif` | Score aptitude solaire PV normalisé |
| 02 | `02_Aptitude_Eolien_Norm.tif` | Score aptitude éolienne normalisé |
| 03 | `03_Aptitude_Hybride_Norm.tif` | Score aptitude hybride (moyenne) |
| 04 | `04_GHI_classe.tif` | GHI reclassifié (1–5) |
| 05 | `05_Vent_classe.tif` | Vitesse vent reclassifiée (1–5) |
| 06 | `06_Pente_classe.tif` | Pente reclassifiée (1–5) |
| 07 | `07_Temp_classe.tif` | Température reclassifiée (1–4) |
| 08 | `08_Cote_Mer_classe.tif` | Distance côte reclassifiée |
| 09 | `09_Villes_classe.tif` | Distance zones urbaines |
| 10 | `10_Routes_classe.tif` | Distance routes (proxy VIIRS) |
| 11 | `11_Elec_classe.tif` | Distance réseau électrique |
| 12 | `12_Rivieres_classe.tif` | Distance cours d'eau |
| 13 | `13_Barrages_classe.tif` | Distance barrages |
| 14 | `14_Masque_Exclusion.tif` | Masque zones exclues |
| 15 | `15_Extraction_12_Sites_H2.csv` | Scores aux 12 sites stratégiques |
| 16 | `16_Stats_Regions_H2.csv` | Statistiques moyennes par région |

---

## 🚀 Utilisation

### Prérequis
- Compte **Google Earth Engine** actif : [signup.earthengine.google.com](https://signup.earthengine.google.com/)
- Asset GEE des régions marocaines (shapefile fourni dans `/data/`)

### Étapes

1. **Ouvrir** le [Code Editor GEE](https://code.earthengine.google.com/)
2. **Copier** le contenu de `scripts/h2_morocco_gee_v6.js`
3. **Adapter** le chemin de l'asset régions :
   ```javascript
   var regions = ee.FeatureCollection('projects/VOTRE_PROJET/assets/regions');
   ```
4. **Exécuter** le script (`Run`)
5. **Lancer** les 16 tâches d'export depuis l'onglet `Tasks`
6. **Récupérer** les fichiers dans votre Google Drive (`H2_Vert_Maroc_Final_v6/`)

---

## 📊 Résultats Clés

| Rang | Région | Score Hybride (/100) |
|------|--------|---------------------|
|   1 | Dakhla-Oued Ed-Dahab | **69,6** |
|     2 | Guelmim-Oued Noun | **66,0** |
|      3 | Laâyoune-Sakia El Hamra | **63,5** |
| 4 | Souss-Massa | 62,6 |
| 5 | Drâa-Tafilalet | 60,5 |

---

## 👩‍💻 Auteurs

| Nom | Rôle | Institution |
|-----|------|-------------|
| **Moujane Nisrine** | Ingénieure PFE | ENSA Beni Mellal |
| **Lahni Maroua** | Ingénieure PFE | ENSC Kénitra |

**Encadrante industrielle** : Dr. Meryeme Azaroual (IRESEN)
**Institution** : IRESEN — Département Hydrogène Vert, Rabat, Maroc
**Période** : Février – Juin 2026

---

## 📄 Licence

Ce projet est sous licence **MIT** — voir le fichier [LICENSE](LICENSE) pour plus de détails.

---

## 📚 Citation

Si vous utilisez ce travail, merci de citer :

```bibtex
@misc{moujane_lahni_2026,
  author    = {Moujane, Nisrine and Lahni, Maroua},
  title     = {H2 Morocco GEE — Cartographie Spatiale du Potentiel d'Hydrogène Vert},
  year      = {2026},
  publisher = {GitHub},
  url       = {https://github.com/nisrinemoujane18-wq/h2-morocco-gee},
  note      = {PFE IRESEN — Département Hydrogène Vert}
}
```

---

## 🔗 Dépôts Associés

| Dépôt | Description |
|-------|-------------|
| [h2-morocco](https://github.com/maroualarhni/h2-morocco) | Plateforme principale (PyPSA, MILP, Streamlit) |
| [h2-morocco-ml](https://github.com/maroualarhni/h2-morocco-ml) | Module Machine Learning (Random Forest, Flask) |
| [h2-morocco-gee](https://github.com/nisrinemoujane18-wq/h2-morocco-gee) | Ce dépôt — Cartographie GEE |
