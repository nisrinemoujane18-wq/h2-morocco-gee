# 📐 Méthodologie AHP-WLC — H₂ Morocco GEE

## 1. Vue d'ensemble

La méthodologie adoptée combine :
- **Google Earth Engine (GEE)** : traitement des données satellitaires à grande échelle
- **AHP** (Analytic Hierarchy Process, Saaty 1980) : pondération des critères
- **WLC** (Weighted Linear Combination) : agrégation spatiale

## 2. Critères d'évaluation

### 2.1 Ressources énergétiques

| Critère | Seuils de reclassification |
|---------|--------------------------|
| GHI (kWh/m²/an) | Cl.1 < 1650 / Cl.2: 1650-1950 / Cl.3: 1950-2100 / Cl.4: 2100-2150 / Cl.5 ≥ 2150 |
| Vent à 200m (m/s) | Cl.1 < 2,5 / Cl.2: 2,5-5 / Cl.3: 5-7,5 / Cl.4: 7,5-10 / Cl.5 ≥ 10 |

### 2.2 Orographie & Climat

| Critère | Seuils |
|---------|--------|
| Pente (°) | Cl.5: 1°-3° / Cl.4: 3°-5° et <1° / Cl.3: 5°-10° / Cl.2: 10°-45° / Cl.1: >45° |
| Température LST (°C) | Cl.4: 0-15 / Cl.3: 15-30 / Cl.2: 30-45 / Cl.1: >45 |

### 2.3 Accessibilité (proxy VIIRS)

| Critère | Seuils |
|---------|--------|
| Distance routes (km) | Cl.4: 0-5 / Cl.3: 5-10 / Cl.2: 10-20 / Cl.1: >20 |
| Distance réseau élec. | Cl.4: 0-10 / Cl.1: >10 |
| Distance zones urbaines | Cl.4: 10-40 / Cl.3: 2-10 / Cl.1: <2 et >40 |
| Distance cours d'eau | Cl.4: 0-15 / Cl.1: >15 |
| Distance barrages | Cl.4: 0-5 / Cl.3: 5-10 / Cl.2: 10-15 / Cl.1: >15 |
| Distance côte | Cl.4: 0-50 / Cl.3: 50-100 / Cl.2: 100-200 / Cl.1: >200 |

## 3. Poids AHP

### Filière Solaire PV (CR = 0,030)

| Critère | Poids |
|---------|-------|
| GHI | 27,6 % |
| Pente | 18,5 % |
| Température | 12,5 % |
| Routes | 10,9 % |
| Zones urbaines | 7,5 % |
| Réseau électrique | 2,0 % |
| Eau/barrages | 2,9 % × 2 |
| Côte | 1,2 % |

### Filière Éolienne (CR = 0,036)

| Critère | Poids |
|---------|-------|
| Vent 200m | 31,3 % |
| Pente | 16,2 % |
| Zones urbaines | 14,0 % |
| Routes | 9,1 % |
| Réseau électrique | 9,1 % |
| Eau/barrages | 3,4 % × 2 |
| Température | 2,4 % |
| Côte | 1,4 % |

## 4. Formule WLC

```
S_j = [Σ(w_k × c_kj)] / S_max × 100
```

- `S_j` : score normalisé du pixel j (0–100)
- `w_k` : poids AHP du critère k
- `c_kj` : classe du critère k au pixel j (1–5)
- `S_max` : score maximal théorique (4,596 solaire / 4,606 éolien)

## 5. Masque d'exclusion

Pixels exclus du calcul :
- Eau permanente (MODIS LC = 0, 11, 16)
- Zones urbaines denses (MODIS LC = 13)
- Neige/glace (MODIS LC = 15)  
- Pente > 45° (SRTM)

## 6. Score hybride

```
S_hybride = (S_solaire + S_eolien) / 2
```

## 7. Références

- Saaty, T.L. (1980). *The Analytic Hierarchy Process*. McGraw-Hill.
- Gorelick et al. (2017). Google Earth Engine. *Remote Sensing of Environment*, 202, 18–27.
- Ouchani et al. (2021). GIS-based multi-criteria analysis. *Renewable Energy*, 165, 300–315.
