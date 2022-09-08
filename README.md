# _2022_Johansson_GMMA_GFP
Scripts and output from "Global analysis of multi-mutants to improve protein function" by Johansson, Lindorff-Larsen and Winther.

Dependencies
------------
Runs with Rscript version 4.0.2 or newer.
Required packages: igraph, minpack.lm

Get the original data
---------------------
The file "amino_acid_genotypes_to_brightness.tsv" from
> Sarkisyan, K., Bolotin, D., Meer, M. et al. Local fitness landscape of the green fluorescent protein.
> Nature 533, 397–401 (2016). https://doi.org/10.1038/nature17995

should be put in the same directory as the scripts

Run scripts
-----------
GMMA is implemented in 5 scripts, gmma01-gmma05, that output biniary 'checkpoint files' to be used by the following scripts. The first script reads a csv text file (here prepared by an additional script gmma00) and the last script outputs a text file 'subst.csv' that contains the estimated substitution effects (in addition to several other output files). This modular structure makes it easy to rerun individual steps.

```bash
# parse the original data
Rscript gmma00_fetch_Sarkisyan.r

# structure data
Rscript gmma01_structure.r amino_acid_genotypes_to_brightness_parsed.tsv

# include various features from assignments dir for analysis - optional
Rscript gmma_assign.r gmma_structured.rda

# initial estimation of stability effects
Rscript gmma02_fit_individual.r

# graph analysis
Rscript gmma03_graph.r gmma_structured.rda

# global analysis based in initial estimated and graph analysis
Rscript gmma04_global_estimation.r

# process results incl. error analysis
Rscript gmma05_analysis.r gmma_fit_global.rda
```
Plot
----
The results are included in the output directory. The .csv files should be excel-readable. Note that we
use the residue numbering of the original data which is shifted 2 positions compared to conventional
numbering (uniprot, fpbase.org, etc).

Plot from the paper may be generated based on the content of the output directory using R-Studio
notebook, plots.Rmd


