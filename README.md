# SCA-BA-DG-Placement

**Comparison of Sine-Cosine and Bat Algorithm for Distributed Generation Placement**

Lindiasari Martha Yustika · Jangkung Raharjo · Rifki Rahman Nur Ikhsan · I Gede Putu Oka Indra Wijaya  
*JNTETI, 14(3), 199–206, 2025*  
[![DOI](https://img.shields.io/badge/DOI-10.22146%2Fjnteti.v14i3.19191-blue)](https://doi.org/10.22146/jnteti.v14i3.19191)

Sine-Cosine Algorithm vs Bat Algorithm for DG placement and sizing on the IEEE 9-bus system.

## Abstract

The enhancement of electricity distribution is a crucial factor in supporting sustainable development and reducing energy access inequality. To ensure the reliability and stability of energy systems, the integration of distributed generation (DG) has a significant role. Numerous studies have explored optimal DG placement using metaheuristic methods. The study evaluated the performance of both algorithms based on key indicators, including voltage profile improvement and power loss reduction, under normal load conditions and under a 10% load increase to simulate future demand growth. The methods employed were the sine-cosine algorithm (SCA) and the bat algorithm (BA). By comparing these two methods, this study aims to optimize the placement and sizing of DG units, with a case study based on the IEEE 9 bus system configuration. Load flow analysis was performed using Electric Transient Analysis Program (ETAP) software to validate the effectiveness of optimized DG placement under various scenarios. Key performance indicators, namely losses reduction and improvement of voltage profile, were evaluated to determine the relative strengths of each algorithm. The results show that both SCA and BA are effective in optimizing DG implementation. Specifically, SCA achieved reductions in active power losses by up to 85% and reactive power losses by 93%, outperforming BA in certain scenarios. Both algorithms enhance system reliability and stability. These findings highlight the potential of metaheuristic algorithms to address the challenges of modern energy systems and contribute to the broader goal of developing sustainable power systems.

## Contents

```
.gitignore
BA_DG.ipynb
SCA_DG.ipynb
```

## Data

Input data is **not included**. Place files in `data/` (notebooks) or next to the `.m` script (MATLAB):

| File | Columns |
|---|---|
| `dg9bus.xlsx` | (format: see code) |

## Requirements

Python. Python notebooks: `numpy`, `pandas`, `scipy`, `matplotlib` (as imported). MATLAB scripts: R2021a+.

## Citation

```bibtex
@article{Lindiasari_Martha_Yustika_2025, title={Comparison of Sine-Cosine and Bat Algorithm for Distributed Generation Placement}, volume={14}, ISSN={2301-4156}, url={http://dx.doi.org/10.22146/jnteti.v14i3.19191}, DOI={10.22146/jnteti.v14i3.19191}, number={3}, journal={Jurnal Nasional Teknik Elektro dan Teknologi Informasi}, publisher={Universitas Gadjah Mada}, author={Lindiasari Martha Yustika and Jangkung Raharjo and Rifki Rahman Nur Ikhsan and I Gede Putu Oka Indra Wijaya}, year={2025}, month=Aug, pages={199–206} }
```

## License

[![CC BY 4.0](https://img.shields.io/badge/License-CC%20BY%204.0-lightgrey.svg)](LICENSE)

Licensed under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/). **Attribution is required**: any use of this code, results, or figures, including in publications, must cite:

> Lindiasari Martha Yustika; Jangkung Raharjo; Rifki Rahman Nur Ikhsan; I Gede Putu Oka Indra Wijaya (2025). Comparison of Sine-Cosine and Bat Algorithm for Distributed Generation Placement. *Jurnal Nasional Teknik Elektro dan Teknologi Informasi*. https://doi.org/10.22146/jnteti.v14i3.19191
