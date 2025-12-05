# La Palma Volcano Eruption Analysis (EO-SAR)

**Remote Sensing & GIS Project** - Multi-sensor change detection of 2021 La Palma volcanic eruption using Sentinel-1 SAR + Sentinel-2 optical data.

## 🎯 Project Objective
Pre/post-eruption change detection (Sep 2021 → Dec 2021) within La Palma volcano exclusion zone.

## 📊 Data Sources
| Sensor | Pre-Eruption | Post-Eruption | Resolution |
|--------|--------------|---------------|------------|
| **Sentinel-1 SAR** | 2021-09-01 VV | 2021-12-15 VV | 20m |
| **Sentinel-2 Optical** | 2021-09-01 B04 | 2021-12-15 B04 | 20m |

## 🔬 Analysis Pipeline
1. **Data Preprocessing**: Calibration, clipping to ROI (GeoJSON)
2. **Co-registration**: SAR-Optical alignment
3. **Change Detection**: Difference thresholding
4. **SAR/Optical Fusion**: AND/OR logic masks
5. **Temporal Analysis**: Backscatter trends

## 📈 Key Visualizations
![QC Overlay](output/LaPalma_QC_overlay.png)
![Change Detection](output/LaPalma_aligned_clean_change.png)
![Temporal Analysis](output/LaPalma_temporal_analysis_simple.png)
![Quality Checks](output/LaPalma_quality_checks.png)

## 📁 Repository Structure
