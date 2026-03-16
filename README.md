# LAffAb
Licensed under the Non-Profit Open Software License version 3.0.

This repository contains the RosettaScripts xmls needed to run the LAffAb design steps and some examples. The method is described in our preprint ([Link to paper](https://www.biorxiv.org/content/10.1101/2025.11.26.690765v3)). Questions, comments, and suggestions can be sent to ariel.tennenhouse@weizmann.ac.il.

## Citations
Please cite our preprint and RosettaScripts 
- Tennenhouse, A. et al. Structure-based design of antibody repertoires with drug-like properties. bioRxiv https://doi.org/10.64898/2025.12.10.693474 (2025).
- Fleishman SJ, Leaver-Fay A, Corn JE, Strauch EM, Khare SD, Koga N, Ashworth J, Murphy P, Richter F, Lemmon G, Meiler J, Baker D. RosettaScripts: a scripting language interface to the Rosetta macromolecular modeling suite. PLoS One. 2011;6(6):e20161. doi: 10.1371/journal.pone.0020161. Epub 2011 Jun 24. PMID: 21731610; PMCID: PMC3123292.

## Installation
You will need to either have Rosetta installed or install it from http://www.rosettacommons.org. CADAbRe uses git version d9d4d5dd3fd516db1ad41b302d147ca0ccd78abd

## Running LAffAb

### Step 1: Relax the structures of the parental antibodies
We recommend relaxing the parental structure before design. A RosettaScripts xml for running the relax can be found at xmls/Relax.xml and an example pdb can be found in example_pdb. Please note that in our LAffAb protocol, we run the initial relax 15 times and take the lowest-scoring one. The output for the example pdb is in example_pdb_relaxed. Each relax job should take about 15 minutes to run on one CPU. 

### Step 2: Creating a PSSM for the light and heavy chains of the variable fragment separately
A PSSM should be made for the light and heavy chains separately following the approach described here:
([Link to paper](https://www.cell.com/molecular-cell/fulltext/S1097-2765(18)30266-1))


### Step 3: Selecting allowed CDR point mutations
Example xmls for running the alanine scan and hydrogen-bond scan can be found at xmls/alascan.xml and xmls/alascan_Hbond.xml, respectively. Files summarizing the results from the alanine and hydrogen-bond scan on the example pdb can be found at example_scanning_summaries/1mlc_alascan.log and example_scanning_summaries/1mlc_Hbond.log, respectively. Each position should take about one minute to run on one CPU. 

An example xml for modeling all allowed point mutations can be found at xmls/filterscan.xml. An example file summarizing the mutations allowed at each CDR position based on the per-residue frequency data for the example pdb can be found at example_scanning_summaries/allowed_muts.resfile. A file summarizing the results for the example pdb can be found at example_scanning_summaries/example_4.resfile. Each mutation modeled at each position should take about one minute to run on one CPU.

### Step 4: Combinatorial enumeration of allowed point mutations
An example xml for running the combinatorial enumeration can be found at xmls/combinatorial_enumeration.xml. An example pdb file created for the example pdb can be found at example_CDR_enumeration/example_CDR_design.pdb.gz. Each design job should take about two minutes to run on one CPU. 
