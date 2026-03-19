# LAffAb
Licensed under the Non-Profit Open Software License version 3.0.

This repository contains the RosettaScripts xmls needed to run the LAffAb design steps and some examples. The method is described in our preprint ([Link to paper](https://www.biorxiv.org/content/10.1101/2025.11.26.690765v3)). Questions, comments, and suggestions can be sent to ariel.tennenhouse@weizmann.ac.il.

## Citations
Please cite our preprint, PROSS, the paper defining the CDR H3 residue frequencies, HuCAL PLATINUM, and RosettaScripts 
- Tennenhouse, A. et al. Energy-guided combinatorial co-optimization of antibody affinity and stability. bioRxiv (2025).
- Goldenzweig, A. et al. Automated structure- and sequence-based design of proteins for high bacterial expression and stability. Mol. Cell 70, 380 (2018).
- Zemlin, M. et al. Expressed Murine and Human CDR-H3 Intervals of Equal Length Exhibit Distinct Repertoires that Differ in their Amino Acid Composition and Predicted Range of Structures. J. Mol. Biol. (2003). 
- Prassler, J. et al. HuCAL PLATINUM, a synthetic Fab library optimized for sequence diversity and superior performance in mammalian expression systems. J. Mol. Biol. (2011).
- Fleishman, S. J. et al. RosettaScripts: a scripting language interface to the Rosetta macromolecular modeling suite. PLoS One 6, e20161 (2011).

## Installation
You will need to either have Rosetta installed or install it from http://www.rosettacommons.org. CADAbRe uses git version d9d4d5dd3fd516db1ad41b302d147ca0ccd78abd

## Running LAffAb
A flags file called "flags" is provided. The Rosetta database needs to be updated to the location of the Rosetta database corresponding to the Rosetta executable used. 

### Step 1: Relax the structures of the parental antibodies
We recommend relaxing the parental structure before design. A RosettaScripts xml for running the relax can be found at xmls/Relax.xml and an example pdb can be found in examples/example_pdb/. Please note that in our LAffAb protocol, we run the initial relax 15 times and take the lowest-scoring one. The output for the example pdb is in examples/example_pdb_relaxed/. Each relax job should take about 15 minutes to run on one CPU. 

### Step 2: Creating a PSSM for the light and heavy chains of the variable fragment separately
A PSSM should be made for the light and heavy chains separately following the approach described here:
([Link to paper](https://www.cell.com/molecular-cell/fulltext/S1097-2765(18)30266-1)).
An example combined PSSM including the light, heavy, and antigen chains can be found in examples/example_pssm/.
The example includes the antigen chain, which is only there as a placeholder. 

### Step 3: Selecting allowed CDR point mutations
Example xmls for running the alanine scan and hydrogen-bond scan can be found at xmls/alascan.xml and xmls/alascan_Hbond.xml, respectively. Files summarizing the results from the alanine and hydrogen-bond scan on the example pdb can be found at examples/example_alascan/. Each position should take about one minute to run on one CPU. 

An example xml for modeling all allowed point mutations can be found at xmls/filterscan.xml. An example file summarizing the mutations allowed at each CDR H3 position based on the per-position residue frequency data from HuCAL PLATINUM can be found at examples/example_point_muts/allowed_from_freq_data.resfile. The per-position residue frequency data is summarized in "H3_per_res_AA_freqs_data.csv". A file summarizing the results for the example pdb can be found at examples/example_point_muts/6mhr_resfile.resfile. This resfile already screened out mutations based on the alanine scans. Each mutation modeled at each position should take about one minute to run on one CPU.

### Step 4: Combinatorial enumeration of allowed point mutations
An example xml for running the combinatorial enumeration can be found at xmls/combinatorial_enumeration.xml. An example pdb file created for the example pdb can be found at examples/example_CDR_enumeration/ Each design job should take about two minutes to run on one CPU. 

### Step 5: EpiNNet (only if designing libraries)
A jupyter notebook for training EpiNNet can be found at https://github.com/Fleishman-Lab/htFuncLib-web-server (htFuncLib.ipynb)
