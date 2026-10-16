# Grand River Microbiome 2022

Analysis code for:
> Esser M. et al. (2026). *Host development and environment influence the microbiomes of aquatic insects and riparian spiders*. Environmental Microbiology. DOI: [to be added]

This repository contains the R Markdown scripts used to analyse bacterial microbiomes of larval and adult aquatic insects (Hydropsychidae, Chironomidae, Heptageniidae) and riparian spiders (Tetragnathidae and Araneidae) collected upstream and downstream of wastewater treatment plants in the Grand River, Ontario, Canada (2022).

## Data availability

| Data | Location |
|---|---|
| Raw 16S rRNA gene sequences (FASTQ) | NCBI SRA, BioProject [PRJNA1544676] |
| ASV table, taxonomy table, sample metadata, PICRUSt2 output | Zenodo: https://zenodo.org/records/19040149 |
| Sample metadata, site information, water chemistry | This repository (`data/`) |


## Getting started

1. Clone or download this repository and open `Grand-River-Microbiome-2022.Rproj` in RStudio.
2. Restore the exact package versions used in the analysis:

   ```r
   install.packages("renv")
   renv::restore()
   ```

   This reads `renv.lock` and installs the matching package versions into a project-local library, so results can be reproduced without version conflicts with packages already on your system.
3. Download the data files from Zenodo and place them in the `data/` folder, keeping the file names unchanged:

   | File | Content |
   |---|---|
   | `seqtab_v34_nochim_transposed_GrandRiver-MB23.csv` | Chimera-filtered ASV count table (DADA2) |
   | `taxatab_v34_silva138wsp_GrandRiver-MB23.csv` | ASV taxonomy (SILVA 138) |
   | `metadata_GrandRiver_MB23.csv` | Sample metadata (also included in this repository) |
   | `newpicrust2_out_pipeline-20251218.zip` | PICRUSt2 output; unzip into `data/newpicrust2_out_pipeline-20251218/` |

   The expected folder structure is:

   ```
   Grand-River-Microbiome-2022/
   ├── Grand-River-Microbiome-2022.Rproj
   ├── 1_Create_physeq_GrandRiver_MEsser.Rmd
   ├── ... (other scripts)
   └── data/
       ├── seqtab_v34_nochim_transposed_GrandRiver-MB23.csv
       ├── taxatab_v34_silva138wsp_GrandRiver-MB23.csv
       ├── metadata_GrandRiver_MB23.csv
       ├── 2022 site info.xlsx
       ├── 2022_water_chem.xlsx
       └── newpicrust2_out_pipeline-20251218/
   ```

4. Run the scripts in numerical order. Script 1 creates the phyloseq objects (saved to `R_output/ps_objects/`) that all later scripts load. Output folders (`R_output/`) are created automatically.

## Scripts

| Script | Content |
|---|---|
| `1_Create_physeq_GrandRiver_MEsser.Rmd` | Builds phyloseq objects; quality filtering, decontam, normalization|
| `2_GrandRiverMB_alphadiversity_MEsser.Rmd` | Alpha diversity |
| `3_GrandRiverMB_betadiversity_MEsser.Rmd` | Beta diversity (ordination, PERMANOVA) |
| `4_GrandRiverMB_barplots_MEsser.Rmd` | Taxonomic composition bar plots |
| `5_GrandRiverMB_MaAsLin3_MEsser.Rmd` | Differential abundance (MaAsLin3, ASV level) |
| `5.2_GrandRiverMB_MaAsLin3_Genus_MEsser.Rmd` | Differential abundance (MaAsLin3, genus level) |
| `10_GrandRiverMB_Relative_abundance_plot_endosymbionts...Rmd` | Endosymbiont relative abundance |
| `11_GrandRiverMB_euler_plots_vertical_turnover.Rmd` | Larval and and adult shared ASVs|
| `11_GrandRiverMB_trophic_transmission.Rmd` | Taxa shared between insects and spiders |
| `12_GrandRiverMB_picrust2_v2=3_namecorrection.Rmd` | Predicted functional profiles (PICRUSt2) |
| `13_GrandRiverMB_picrust2_PCoA.Rmd` | Ordination of predicted functional profiles |

## Software

Analyses were run in R 4.5.2 with phyloseq, vegan, MicEco, decontam, metagenomeSeq, MaAsLin3, tidyverse and ggplot2. Exact package versions are pinned in [`renv.lock`](renv.lock) — run `renv::restore()` to install them (see Getting started, step 2).

## Contact

Milena Esser – esserm@mcmaster.ca
