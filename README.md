#LAffAb
Licensed under the Non-Profit Open Software License version 3.0.

This repository contains the RosettaScripts xmls needed to run the CADAbRe design steps and some examples. The method is described in our preprint ([Link to paper](https://www.biorxiv.org/content/10.64898/2025.12.10.693474v1)). Questions, comments, and suggestions can be sent to ariel.tennenhouse@weizmann.ac.il.

## Citations
Please cite our preprint as well as IMGT and RosettaScripts 
- Giudicelli, V., Chaume, D. & Lefranc, M.-P. IMGT/GENE-DB: a comprehensive database for human and mouse immunoglobulin and T cell receptor genes. Nucleic Acids Res. 33, D256–61 (2005).
- Tennenhouse, A. et al. Structure-based design of antibody repertoires with drug-like properties. bioRxiv https://doi.org/10.64898/2025.12.10.693474 (2025).
- Fleishman SJ, Leaver-Fay A, Corn JE, Strauch EM, Khare SD, Koga N, Ashworth J, Murphy P, Richter F, Lemmon G, Meiler J, Baker D. RosettaScripts: a scripting language interface to the Rosetta macromolecular modeling suite. PLoS One. 2011;6(6):e20161. doi: 10.1371/journal.pone.0020161. Epub 2011 Jun 24. PMID: 21731610; PMCID: PMC3123292.

## Installation
You will need to either have Rosetta installed or install it from http://www.rosettacommons.org. CADAbRe uses git version d9d4d5dd3fd516db1ad41b302d147ca0ccd78abd

## Running CADAbRe

### Step 1: Relax the structures of the parental antibodies
We recommend relaxing the parental structures before design. A RosettaScripts xml for running the relax can be found at xmls/Relax.xml and example pdbs can be found in example_pdbs. Please note that in our protocol for CADAbRe, we run the initial relax 15 times and take the lowest-scoring one. The output for the example pdbs can be found in example_pdbs_relaxed. Each relax job should take about 15 minutes to run on one CPU. 

### Step 2: Threading combinations of human germlines on each parental structure
An example xml for running the threading can be found at xmls/CADAbRe.xml. Examples of several germline combinations threaded on the relaxed structure of PDB ID 3NAA can be found in example_pdbs_threaded. Each threading job should take about 5 minutes to run on one CPU. 

### Step 3: Selecting allowed CDR H3 point mutations based on each selected stucture
Example xmls for running the alanine scan and hydrogen-bond scan can be found at xmls/alascan.xml and xmls/alascan_Hbond.xml, respectively. Files summarizing the results from the alanine and hydrogen-bond scan on PDB ID 3NAA can be found at example_scanning_summaries/3naa_alascan.log and example_scanning_summaries/3naa_Hbond.log, respectively. Each position should take about one minute to run on one CPU. 

An example xml for modeling all allowed point CDR H3 point mutations can be found at xmls/filterscan.xml. An example file summarizing the mutations allowed at each CDR H3 position based on the per-residue frequency data for PDB ID 3NAA can be found at example_scanning_summaries/3naa_allowd_muts.resfile. A file summarizing the results for PDB ID 3NAA can be found at example_scanning_summaries/3naa_4.resfile. Each mutation modeled at each position should take about one minute to run on one CPU.
