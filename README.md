# Microcosm_Pelargonium-x-hortorum
Analysis of 16S (bacterial) and ITS (fungal) metabarcoding data from *Pelargonium × hortorum var. Silvia* rhizosphere samples under four treatments: water control, fertiliser, freshwater microalgae, and seawater microalgae.

## Study Design

| Code | Treatment | Description |
|------|-----------|-------------|
| GC | Water control | Water only |
| GN | Fertilizer | Water + nutrient fertilizer |
| GD | Freshwater microalgae | Microalgae biostimulant (freshwater) |
| GS | Seawater microalgae | Microalgae biostimulant (seawater) |

3 biological replicates per treatment (12 samples total per marker).



## Data Files

All input data is included in `data/` (~8.5 MB):

| File | Size | Description |
|------|------|-------------|
| `16S_ASV.tsv` | 243K | 16S ASV count table + taxonomy (QIIME2 export, DADA2 denoised, SILVA 138 classified) |
| `16S_Metadata.csv` | 0.5K | 16S sample metadata (SampleID, Group) |
| `16S_Rooted_tree.qza` | 199K | 16S rooted phylogenetic tree (for Faith's PD, UniFrac) |
| `ITS_ASV.tsv` | 112K | ITS ASV count table + taxonomy (QIIME2 export, DADA2 denoised, UNITE classified) |
| `ITS_Metadata.csv` | 0.5K | ITS sample metadata |
| `ITS_Rooted_tree.qza` | 183K | ITS rooted phylogenetic tree |
| `pgpb_mechanisms.csv` | 4.2K | Curated genus-to-PGPB-mechanism mapping with literature citations (67 entries) |
| `beneficial_fungi_guilds.csv` | 44K | FUNGuild genus-to-guild assignments with confidence scores and citations |
| `faprotax_report.txt` | 115K | FAPROTAX v1.2.5 output report (function-to-taxa mappings) |
| `funguild_db.json` | 7.7M | FUNGuild database (15,897 entries, genus-level trophic mode assignments) |

## Requirements

```
pip install -r requirements.txt
```

Dependencies: numpy, pandas, scipy, scikit-bio, matplotlib, seaborn, networkx, python-louvain

No R installation required — all analyses run in pure Python.

## How to Run

1. Install dependencies: `pip install -r requirements.txt`
2. Open `analysis.ipynb` in Jupyter Notebook or JupyterLab
3. Run all cells top to bottom (Sections 1-10)
4. Outputs are saved to `figures/` (PNG + SVG) and `tables/` (CSV)

Total runtime: ~5-10 minutes on a standard laptop.

## How to Adapt for Other Datasets

1. Replace files in `data/` with your own QIIME2-exported ASV tables, metadata, and trees
2. Update treatment codes and labels in Section 1 (Configuration)
3. Update sample ID lists if your naming convention differs
4. The PGPB and beneficial fungi databases can be replaced with your own curated mappings
5. FAPROTAX and FUNGuild databases can be updated to newer versions

## Methods Summary

- **Alpha diversity**: Rarefied to minimum sample depth; Kruskal-Wallis test across groups
- **Beta diversity**: PERMANOVA (999 permutations) via scikit-bio; PCoA ordination
- **Taxonomic composition**: Relative abundance at phylum (stacked bar) and genus (heatmap, log10) levels
- **PGPB mechanisms**: Curated literature-based genus-to-mechanism mapping; primary assignment (each genus counted once)
- **Beneficial fungi**: FUNGuild database genus-level trophic mode assignment; 5 broad guilds
- **FAPROTAX**: Per-sample reconstruction from function-to-taxa report; 12 non-redundant functions; bootstrap 95% CI (10,000 resamples)
- **FUNGuild**: Per-sample reconstruction from genus-level trophic modes; 5 broad guilds; bootstrap 95% CI

## Citations

- FAPROTAX: Louca, S., et al. (2016). *Paleobiology*, 42(4), 659-689.
- FUNGuild: Nguyen, N.H., et al. (2016). *Mycologia*, 108(2), 288-297.
- QIIME2: Bolyen, E., et al. (2019). *Nature Biotechnology*, 37, 852-857.
- SILVA 138: Quast, C., et al. (2013). *Nucleic Acids Research*, 41(D1), D590-D596.
- UNITE: Nilsson, R.H., et al. (2019). *Mycological Progress*, 18, 1261-1284.

## License

This analysis code is provided for reproducibility of the associated publication.
