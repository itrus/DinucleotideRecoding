# DinucleotideRecoding
CpG and TpA dinucleotide enrichment/depletion in nucleotide sequences

## Introduction

### Main information
#### This code performs **CpG and TpA dinucleotide enrichment/depletion** without affecting several parameters:

- amino acid sequence
- mononucleotide frequencies
- codon frequency (CAI, ENC, RSCU)
- GC and GC3 content

#### Affected parameters include:

- codon pair bias (CPB)
- other dinucleotide frequencies


### Running modes
The program has two modes:

- **STRICT** mode. Parameters listed above as non-affected ones are not affected in this mode.
- **NON-STRICT** mode. Parameters listed above as non-affected ones are affected in this mode.

You can combine both modes.

### Input parameters:

- *Dinucleotides for enrichment/depletion (CpG and TpA, no other variants for now)*
- Power of processing in the **STRICT** mode
  + CpG dinucleotide: **Power.CpG.strict** from -100% (maximal depletion) to +100% (maximal enrichment)
  + TpA dinucleotide: **Power.TpA.strict** from -100% (maximal depletion) to +100% (maximal enrichment)
- Power of processing in the **NON-STRICT** mode
  + CpG dinucleotide: **Power.CpG.non-strict** from -100% (maximal depletion) to +100% (maximal enrichment)
  + TpA dinucleotide: **Power.TpA.non-strict** from -100% (maximal depletion) to +100% (maximal enrichment)
- Initial input sequence should be one ORF and nothing else. You can provide any nucleotide sequence looking like ORF. Requirements:
  + No more than one STOP-codon. It should be located in the 3' end of the sequence.
  + Sequence should be made of codons. This means that it should be translated into amino acids using the standard translation table.
  + The sequence length should be divided by 3 without remainder.
- Speed parameter. This parameter defines the step size for power statistics plots. Thus, it has linear effect on the script execution time/speed (e.g. the speed of **1** is 100 times slower than the speed of **100**).
  + If it takes too long, adjust the "Script Runtime Speed". Correct values are **0-100**. While you can use any value that is  bigger than **0**, it is better for charts production to use values like **0.1, 0.5, 1, 2, 5, 10, 25**.
  + Use value of **0** to raise the speed of the whole script to maximum. However, this will remove some charts from the output.

### Final notes
#### Code efficiency

- CpG is optimized to 100%.
- TpA could be optimized by 5% more for Power <0% with additional S (serine) and R (arginine) processing.

#### CPB calculations

This script is capable to calculate CPB based on CPS scores published by:

* **Coleman et. al., 2008.** *DOI: 10.1126/science.1155761*
* **Gao et. al., 2015.** *DOI: 10.1016/j.virol.2015.07.012*
* **Kunec & Osterrieder, 2016.** *DOI: 10.1016/j.celrep.2015.12.011*

Formula is describes by **Coleman et. al. (2008)**.  
The script takes CPS scores from the **CPS_reference_dataset.csv** file that should be placed in the same folder with the current script. This file contains 11 references for CPS in different species. All of them will be used to report CPB at the end of this script. For plotting charts this script is using as default CPS calculated for human ORFeome by **Kunec & Osterrieder (2016)**. In order to change default CPS or to add additional species, please, modify the appropriate columns (#3-13) in the **CPS_ref.csv** file.  
If you don't need to calculate CPB, please change the **CPB.calculation** parameter to **FALSE**.

## ToDo list

* stop codons should be excluded from CPB analysis and the whole process of recoding
* matching errors should be catched up 
