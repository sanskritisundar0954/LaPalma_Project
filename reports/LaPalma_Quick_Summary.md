# La Palma Volcano 2021 – EO–SAR Change Detection Summary

## Project Overview
This analysis demonstrates EO–SAR change detection over the Cumbre Vieja eruption (Sep–Dec 2021) on La Palma, Canary Islands.

## Data Acquisition
- **Sentinel-2 (Optical):** B4 (Red, 20 m resolution)
  - PRE:  2021-09-01 to 2021-09-15
  - POST: 2021-12-15 to 2021-12-31
- **Sentinel-1 (SAR):** VV polarization, IW mode (20 m resolution)
  - PRE:  2021-09-01 to 2021-09-15 (median composite)
  - POST: 2021-12-15 to 2021-12-31 (median composite)

## Processing Steps
1. **Coregistration:** All rasters reprojected to Sentinel-2 PRE grid (EPSG:4326, bilinear resampling)
2. **Radiometric Calibration:** S1 VV converted to sigma0 (dB), clipped to [-30, 5] dB
3. **Change Detection:**
   - S2–S2 change: |ΔB4| > 0.08 (8% reflectance difference)
   - S1–S1 change: |ΔVVVV| > 0.15 dB
   - Morphological closing (disk=3) for noise reduction
4. **Fusion:** Logical AND and OR of optical and SAR masks

## Key Results

| Metric | Value |
|--------|-------|
| Total grid pixels | 855,144 |
| Valid pixels (no NaN) | 855,144 |
| S2 change pixels | 427,410 |
| S1 change pixels | 816,111 |
| Pixels in both S2 & S1 (AND) | 427,378 |
| Pixels in either S2 or S1 (OR) | 816,143 |
| Fraction AND / valid | 0.4998 (~49.98%) |
| Fraction OR / valid | 0.9544 (~95.44%) |

## Quality Checks
- **S2 high-variance (noisy) pixels:** 85,515
- **S1 high-variance (noisy) pixels:** 85,515
- **S2 mask after small-object removal (50 px):** 424,650 pixels
- **S1 mask after small-object removal (50 px):** 816,111 pixels

## Sensor Comparison
- **S2 (Optical)** is sensitive to vegetation change and bare ground exposure (lava flows appear dark red in B4).
- **S1 (SAR)** is sensitive to surface roughness; smooth lava shows low backscatter.
- **Fusion (OR):** Combined mask captures both optical and SAR signatures for robust change detection.

## False Positives / Negatives
- **False positives:** High-variance areas (mountainous slopes, water) may show spurious change; flagged in QC overlay.
- **False negatives:** Very fresh lava with similar thermal properties to surrounding may not trigger thresholds.
- **Recommendations:** Manual inspection of edge cases; threshold tuning for specific use cases.

## Deliverables
- Change maps: `LaPalma_S2_change.tif`, `LaPalma_S1_change.tif`, `LaPalma_fusion_OR_S2_S1.tif`
- QC figures: `LaPalma_temporal_analysis_simple.png`, `LaPalma_quality_checks.png`, `LaPalma_QC_overlay.png`
- Report: This summary + full PDF

## Workflow Reproducibility
All steps are documented in the Jupyter notebook (`notebooks/LaPalma_EO_SAR_Change.ipynb`) with cell‑by‑cell execution.
