# Cell-type Specific Gene Networks and Drivers in Rheumatoid Arthritis

<img align="right" src="https://github.com/Aurelien-Pelissier/RA-drug-discovery/blob/main/img/PANDA.png" width=400>

The increasing number of available large RNA-seq datasets, combined with genome-wide association studies (GWAS), differential gene expression (DEG) studies, and gene regulatory networks (GRN) analyses have to potential to lead to the discovery of novel therapeutics. Yet, despite this progress, our ability to translate GWAS and DEG analyses into an improved mechanistic understanding of many diseases remains limited, as different analyses often disregard information about the cell-types mediating the disease.

In this repository, We compute sample-specific GRNs which enables the use of statistical techniques to compare network properties between phenotypic groups. Then, we leverage this collection of networks to rank transcription factors (TFs) according to their contribution to the observed differential gene expression between RA and control. 

### This repository support our publication:

[[1]](localhost) Pelissier A*, Laragione T*, Martinez MR, & Gulko PS. Cell-type Specific Gene Networks and Drivers in Rheumatoid Arthritis (2023). Planned.

[//]: <> (Pelissier A*, Laragione T*, Martinez MR, & Gulko PS. BACH1 as key regulator in RA 2023. Planned.)

&nbsp;

## Constructing cell-type specific gene regulatory network
In this work, Gene regulatory netowkrs are bipartite graphs, with edges connecting TF and their target gene (TG). Each edge has a weight representing the probability of a regulatory interaction between the connected nodes.
Briefly, PANDA integrates gene expression data with prior knowledge about TF-binding motif and protein-protein interactions by optimizing the weights of edges in the networks with iterative steps. Applied to our data, PANDA produced fully connected and directed networks of TFs to their target genes, comprising 644 TFs and 18992 genes.
- Cell-specific gene expression matrix. In this study we used bulk but you can also use single cell and average them out to make it equivalent, available in `Data/RA_gene_expression`
- Prior knowledge about TF-TF interactions and TF binding motif, available in `Data/PANDA_prior_knowledge`
Run the script `src/PANDA_network.py` to compute the network and analyse their edges.

&nbsp;

Then, we used LIONESS [3] to estimate an individual gene regulatory network for each sample in the population. We can then use this collection of network to make differential analysis of their edges.

<p align="center">
  <img src="https://github.com/Aurelien-Pelissier/RA-drug-discovery/blob/main/img/LIONESS.png" width=500>
</p>

Then, we used LIONESS [3] to estimate an individual gene regulatory network for each sample in the population.

&nbsp;

## Key driver analysis
We use mergeomics [4]. You need:
Some network for your analysis. We used the GIANT network, downloaded at https://giant-v2.princeton.edu/download/.
- Run the script `src/KDA_analysis.py`

&nbsp;

## Experimental validation
In our article we focused on Synovial fibroblast and detected FOSL1, THBS1 and CFH as potential novel key regulators.
We performed silencing experiment on RA cell line and provide the results in `Data/silencing_experiments/silencing_data.xlsx`
- Run the script `src/silencing_analysis.py` to run the statistical test and combine the p-values with the Brown-Fisher method.

&nbsp;

## Reference
[2] Glass, Kimberly, et al. "Passing messages between biological networks to refine predicted interactions." PloS one 8.5 (2013): e64832.

[3] Kuijjer, Marieke Lydia, et al. "Estimating sample-specific regulatory networks." Iscience 14 (2019): 226-240.

[4] Shu, Le, et al. "Mergeomics: multidimensional data integration to identify pathogenic perturbations to biological systems." BMC genomics 17.1 (2016): 1-16.


