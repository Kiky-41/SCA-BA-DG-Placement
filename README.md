# SCA-BA-DG-Placement

**Comparison of Sine-Cosine and Bat Algorithm for Distributed Generation Placement**

Lindiasari Martha Yustika · Jangkung Raharjo · Rifki Rahman Nur Ikhsan · I Gede Putu Oka Indra Wijaya  
*JNTETI, 14(3), 199–206, 2025*  
[![DOI](https://img.shields.io/badge/DOI-10.22146%2Fjnteti.v14i3.19191-blue)](https://doi.org/10.22146/jnteti.v14i3.19191)

Sine-Cosine Algorithm vs Bat Algorithm for DG placement and sizing on the IEEE 9-bus system.

## Abstract

The enhancement of electricity distribution is a crucial factor in supporting sustainable development and reducing energy access inequality. To ensure the reliability and stability of energy systems, the integration of distributed generation (DG) has a significant role. Numerous studies have explored optimal DG placement using metaheuristic methods. The study evaluated the performance of both algorithms based on key indicators, including voltage profile improvement and power loss reduction, under normal load conditions and under a 10% load increase to simulate future demand growth. The methods employed were the sine-cosine algorithm (SCA) and the bat algorithm (BA). By comparing these two methods, this study aims to optimize the placement and sizing of DG units, with a case study based on the IEEE 9 bus system configuration. Load flow analysis was performed using Electric Transient Analysis Program (ETAP) software to validate the effectiveness of optimized DG placement under various scenarios. Key performance indicators, namely losses reduction and improvement of voltage profile, were evaluated to determine the relative strengths of each algorithm. The results show that both SCA and BA are effective in optimizing DG implementation. Specifically, SCA achieved reductions in active power losses by up to 85% and reactive power losses by 93%, outperforming BA in certain scenarios. Both algorithms enhance system reliability and stability. These findings highlight the potential of metaheuristic algorithms to address the challenges of modern energy systems and contribute to the broader goal of developing sustainable power systems.



## Proposed method

Two metaheuristics are applied to the same DG siting-and-sizing problem and compared. A candidate is a pair (bus, DG capacity); the objective is total active-power loss, and ETAP load flow validates each candidate at normal load and at a 10% load increase. SCA updates every candidate with a sine or cosine step around the best solution. BA updates a velocity from a frequency, then adds a local random walk controlled by loudness and pulse rate.

### Problem formulation

$$P_{\text{loss}}=\sum_{i=1}^{N}\sum_{j=1}^{N}G_{ij}\left(V_i^2+V_j^2-2V_iV_j\cos(\theta_i-\theta_j)\right),$$

subject to

$$V_{\min}\le V_i\le V_{\max},\qquad \sum P_{\text{gen}}=\sum P_{\text{load}}+P_{\text{loss}},\qquad P_{DG,\min}\le P_{DG,i}\le P_{DG,\max}.$$

Line losses are also written as $P_{\text{loss}}=I^2R$.

### Notation

| Symbol | Meaning | Unit |
|---|---|---|
| $N$ | number of buses | – |
| $V_i,\theta_i$ | voltage magnitude and angle at bus $i$ | p.u., rad |
| $G_{ij}$ | real part of the bus admittance matrix | p.u. |
| $I,R$ | line current and resistance | A, Ω |
| $P_{\text{loss}}$ | total active-power loss | MW |
| $V_{\min},V_{\max}$ | voltage limits | p.u. |
| $P_{DG,i}$ | DG capacity at bus $i$ | MW |
| $\mathbf{X}_i$ | position of agent/bat $i$ | – |
| $\mathbf{X}^{\ast}$ | best position | – |
| $r_1$–$r_4$ | uniform random numbers | – |
| $a$ | SCA control parameter, 2 → 0 | – |
| $t,T$ | iteration and iteration cap | – |

### Sine–Cosine Algorithm

The control parameter falls linearly:

$$r_1=a-t\frac{a}{T},\qquad a=2.$$

Each coordinate moves with either a sine or a cosine term:

$$X_i^{t+1}=
\begin{cases}
X_i^{t}+r_1\sin(r_2)\left|r_3X^{\ast}-X_i^{t}\right|, & r_4\lt0.5,\\
X_i^{t}+r_1\cos(r_2)\left|r_3X^{\ast}-X_i^{t}\right|, & r_4\ge0.5,
\end{cases}$$

with $r_2\sim\mathcal{U}(0,2\pi)$, $r_3\sim\mathcal{U}(0,2)$ and $r_4\sim\mathcal{U}(0,1)$. The sine and cosine branches give the search two different approach shapes, and the shrinking $r_1$ reduces the step as the run proceeds.

### Bat Algorithm

Each bat has a frequency, a velocity and a position:

$$f_i=f_{\min}+(f_{\max}-f_{\min})\beta,\qquad \mathbf{v}_i^{t}=\mathbf{v}_i^{t-1}+\left(\mathbf{x}_i^{t-1}-\mathbf{x}^{\ast}\right)f_i,\qquad \mathbf{x}_i^{t}=\mathbf{x}_i^{t-1}+\mathbf{v}_i^{t},$$

where $\beta\sim\mathcal{U}(0,1)$. The frequency scales the pull toward the best bat, and the velocity carries momentum from the previous iteration.

A local random walk is applied around the current best:

$$\mathbf{x}_{\text{new}}=\mathbf{x}_{\text{old}}+\epsilon\bar A^{t},\qquad \epsilon\sim\mathcal{U}(-1,1),$$

where $\bar A^{t}$ is the mean loudness. Loudness and pulse rate are then updated:

$$A_i^{t+1}=\alpha A_i^{t},\qquad r_i^{t+1}=r_i^{0}\left(1-e^{-\gamma t}\right).$$

Loudness decays so later iterations make smaller local moves, while the pulse rate rises so the bat relies more on the current best.

### Settings and reported outcome

10 agents, 100 iterations; the bus index is clipped to the bus range and the DG capacity to 0–500 kW. SCA reduces active-power losses by up to 85% and reactive-power losses by 93%, and both algorithms improve the voltage profile, with SCA ahead in several scenarios.

### Implementation note

The notebooks optimise a proxy built from line impedance, length and transformer MVA, with DG capacity reducing the loss contribution of branches connected to the DG bus. The paper's loss values and voltage profiles come from ETAP load flow. Use the notebooks for the optimisation logic, not as a replacement for the ETAP validation.
### Reported result
Across the tested DG placements SCA reduces active-power losses by up to 85% and reactive-power losses by 93%; BA reaches lower reductions. Both improve the voltage profile at normal load and at the 10% load increase.

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


## Results

### Scenario 1, IEEE 9-bus, no DG

| Bus | Voltage (p.u.) | Condition |
|---|---|---|
| Bus 1 | 1.0000 | nominal |
| Bus 2 | 1.0400 | overvoltage |
| Bus 3 | 1.0200 | above nominal |
| Bus 4 | 0.9300 | undervoltage |
| Bus 5 | 0.9500 | undervoltage |
| Bus 6 | 0.9500 | undervoltage |
| Bus 7 | 1.0100 | above nominal |
| Bus 8 | 1.0100 | above nominal |
| Bus 9 | 1.0000 | nominal |

Without DG the feeder has three undervoltage buses (4, 5 and 6 between 0.93 and 0.95 p.u.) and four buses at or above nominal, with bus 2 at 1.04 p.u. The undervoltage group defines the placement target in the two DG scenarios.

### Scenario 2, normal load with DG, both pick bus 6

| Algorithm | DG size (kW) | Active loss (MW) | Reactive loss (MVAR) | Active reduction | Reactive reduction |
|---|---|---|---|---|---|
| Base, no DG | - | 34.70 | 31.16 | - | - |
| SCA | 250 | 5.35 | 2.06 | 85% | 93% |
| BA | 299 | 30.96 | 11.98 | 11% | 61% |

Both algorithms place DG at bus 6 but size it differently. SCA uses 250 kW and removes 85% of active and 93% of reactive loss, keeping every bus near 1.00 p.u.; BA uses 299 kW and removes 11% and 61%, while pushing some buses slightly above nominal.

### Scenario 3, load +10% with DG

| Algorithm | Active loss (MW) | Reactive loss (MVAR) | Active reduction | Reactive reduction | Voltage note |
|---|---|---|---|---|---|
| Base, load +10% | 34.70 | 31.16 | - | - | - |
| SCA | 30.80 | 11.88 | 11% | 62% | stays within limits |
| BA | 34.70 | 29.01 | 0% | 6.9% | bus 4 and bus 5 fall to 0.93 and 0.94 p.u. |

With load up 10% SCA holds active loss at 30.80 MW and reactive loss at 11.88 MVAR, 11% and 62% below the loaded base case, and keeps voltage inside limits. BA removes nothing on active power (34.70 MW, 0%) and 6.9% on reactive power, with buses 4 and 5 sagging to 0.93 and 0.94 p.u.


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
