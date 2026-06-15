# 📦 Données — H₂ Morocco GEE

## Fichiers à fournir

### `regions/` — Shapefile des régions marocaines

Le shapefile des 12 régions administratives du Maroc (post-2015) doit être
uploadé comme **asset Google Earth Engine** dans votre projet GEE.

**Source** : Découpage administratif officiel post-2015 (CAECE / HCP Maroc)

**Étapes pour uploader dans GEE :**
1. Aller dans [code.earthengine.google.com](https://code.earthengine.google.com/)
2. Panneau gauche → **Assets** → **New** → **Shape files**
3. Uploader les fichiers `.shp`, `.shx`, `.dbf`, `.prj`
4. Nommer l'asset : `regions`
5. Mettre à jour le chemin dans le script :
   ```javascript
   var regions = ee.FeatureCollection('projects/VOTRE_PROJET/assets/regions');
   ```

## Sources de données GEE (accès public)

Toutes les autres données sont accessibles directement depuis GEE
sans téléchargement préalable :

| Dataset GEE ID | Description |
|----------------|-------------|
| `ECMWF/ERA5_LAND/DAILY_AGGR` | Rayonnement solaire + vent |
| `USGS/SRTMGL1_003` | Modèle Numérique de Terrain |
| `MODIS/061/MOD11A2` | Température de surface (LST) |
| `CIESIN/GPWv411/GPW_Population_Density/...` | Densité de population |
| `NOAA/VIIRS/DNB/MONTHLY_V1/VCMSLCFG` | Lumières nocturnes |
| `WWF/HydroSHEDS/15ACC` | Réseau hydrographique |
| `JRC/GSW1_4/GlobalSurfaceWater` | Eau de surface permanente |
| `MODIS/061/MCD12Q1` | Occupation du sol |
