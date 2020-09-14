# MCCS example for SARS-CoV-2

This repository contains the intermediate and output data involved in the process of MCCS virtual screening against the determined SARS-CoV-2 3CL structure using approved drugs on [DrugBank].

1_drugbank_smiles
---

This directory contains two lists of small molecular SMILES extracted from the [DrugBank database]. One is of all drugs and the other approved drugs.

The original [DrugBank database] was downloaded on January 3, 2020.

2_covid19_structure_[step1,2,4]
---

This directory contains the receptor and ligand PDB files splitted from the crystal structure of COVID-19 main protease (3CL) in complex with an inhibitor N3 ([PDB ID - 6LU7](https://www.rcsb.org/structure/6LU7)), as well as converted PDBQT files and predicted pKa values for the ligand.

3_drugbank_pdbqt_[step5,6,7]
---

This directory contains the converted PDBQT files and predicted pKa values for all drugs on [DrugBank].

4_covid19_scoring_output_[step9]
---

This directory contains the [jdock] scoring output (residue energy contribution vectors represented in .csv and conformations represented in .pdbqt) of the covid19 complex. The script used to acquire this looks like

```
jdock -r receptor.pdbqt -l ligand.pdbqt -o covid19_scoring_output -sp
```

5_drugbank_docking_output_[step10]
---

This directory contains the complete [jdock] docking output (residue energy contribution vectors represented in .csv and conformations represented in .pdbqt) for the approved drugs on [DrugBank]. The script used to acquire this looks like

```
jdock -r receptor.pdbqt -l drugbank_pdbqt $(pdbm -L ligand.pdb) -o drugbank_docking_output
```

Note that some of the input ligands did not succeed in docking and are not included in this directory. The number of successful results is 1,814.

6_similarity_search_output_[step11]
---

This directory contains the complete output of [mccsx] similarity search in the [DrugBank] approved library for the COVID-19 vector pattern. The script used to acquire this looks like

```
mccsx search -l drugbank_docking_output -p covid19_scoring_output -o similarity_search_output
```

[DrugBank]: https://www.drugbank.ca/
[DrugBank database]: https://www.drugbank.ca/releases/latest
[jdock]: https://github.com/stcmz/jdock
[mccsx]: https://github.com/stcmz/mccsx
