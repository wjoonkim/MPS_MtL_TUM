# MPS – Molecular Dynamics Simulations: Mechanisms of Protein-Ligand Binding at TUM

A collection of Jupyter notebooks for running and analysing molecular dynamics (MD) simulations of protein–ligand complexes, developed as part of a research project at the Technical University of Munich (TUM). The workflow covers everything from system preparation and production MD to free energy calculations using umbrella sampling and the Weighted Histogram Analysis Method (WHAM).

## Repository Structure

```
MPS_MtL_TUM/
├── notebooks/                              # Jupyter notebooks (sequential workflow)
│   ├── 01_interface_visualisation.ipynb    # System setup and structure visualisation
│   ├── 02_tleap_build_protein_system.ipynb # Build explicit-water systems with tLeap
│   ├── 03_relaxation_explicit_water.ipynb  # Energy minimisation and equilibration
│   ├── 04_production_md.ipynb              # Production MD with pmemd
│   ├── 05_trajectory_analysis_pytraj_tutorial.ipynb  # Trajectory analysis with PyTraj
│   ├── 06_0_parameterize_FSC.ipynb         # Parameterise fusicoccin (FSC) with GAFF
│   ├── 06_1_traj_analy_FSC.ipynb           # FSC trajectory analysis (50 ns NPT)
│   ├── 07_TL_awk_int_atoms.ipynb           # Identify interface atoms
│   ├── 08_run_colv_multi_rmsd.ipynb        # Umbrella sampling with RMSD CVs
│   ├── 09_colv_traj_analy.ipynb            # Analyse collective-variable trajectories
│   ├── 10_wham_free_energy.ipynb           # Free energy via WHAM
│   ├── 11_hamiltonian.ipynb                # Hamiltonian replica exchange umbrella sampling
│   ├── 12_noLigand.ipynb                   # 14-3-3 / FSC system without ligand
│   └── 13_1of2.ipynb                       # HLA-B*2709 complexed with VIPR peptide
└── t38_seminar_07082024.pdf                # Seminar presentation (July 2024)
```

## Prerequisites

### External Software

| Tool | Purpose |
|------|---------|
| [AMBER](https://ambermd.org/) (≥ 22) | MD engine (`pmemd`), system builder (`tLeap`), and parameterisation tool (`antechamber`) |
| Python 3.9+ | All analysis notebooks |
| Jupyter Notebook / JupyterLab | Notebook execution |

### Python Dependencies

```bash
pip install numpy pandas scipy matplotlib seaborn \
            mdtraj pytraj MDAnalysis biopython \
            pymbar nglview jupyter
```

> **Note:** `pytraj` and `nglview` may require conda for easier installation:
> ```bash
> conda install -c conda-forge pytraj nglview
> ```

## Workflow Overview

The notebooks are designed to be run in order. A high-level summary of each phase is given below.

### 1 – System Preparation
| Step | Notebook | Description |
|------|----------|-------------|
| 1 | `01_interface_visualisation` | Load and visualise the protein structure; inspect binding interface |
| 2 | `02_tleap_build_protein_system` | Solvate and neutralise with tLeap; generate topology and coordinate files |

### 2 – Baseline Simulations
| Step | Notebook | Description |
|------|----------|-------------|
| 3 | `03_relaxation_explicit_water` | Multi-stage minimisation and NVT/NPT heating |
| 4 | `04_production_md` | NPT production run with pmemd |
| 5 | `05_trajectory_analysis_pytraj_tutorial` | RMSD, RMSF, hydrogen-bond, and contact analyses |

### 3 – Small-Molecule Parameterisation
| Step | Notebook | Description |
|------|----------|-------------|
| 6a | `06_0_parameterize_FSC` | Generate GAFF parameters for fusicoccin (FSC) using `antechamber` and `parmchk2` |
| 6b | `06_1_traj_analy_FSC` | Analyse the 50 ns NPT trajectory of the protein–FSC complex |

### 4 – Enhanced Sampling & Free Energy
| Step | Notebook | Description |
|------|----------|-------------|
| 7 | `07_TL_awk_int_atoms` | Extract and filter interface atoms for collective-variable (CV) definition |
| 8 | `08_run_colv_multi_rmsd` | Set up and run multi-window umbrella sampling along RMSD CVs |
| 9 | `09_colv_traj_analy` | Diagnose sampling and visualise CV distributions |
| 10 | `10_wham_free_energy` | Compute potential of mean force (PMF) with WHAM |
| 11 | `11_hamiltonian` | Hamiltonian replica exchange umbrella sampling for improved convergence |

### 5 – Case Studies
| Step | Notebook | Description |
|------|----------|-------------|
| 12 | `12_noLigand` | 14-3-3 σ + FSC stabilizer without the primary ligand (H⁺-ATPase peptide) |
| 13 | `13_1of2` | HLA-B*2709 complexed with a vasoactive intestinal peptide (VIPR) |

## Getting Started

1. **Clone the repository**
   ```bash
   git clone https://github.com/wjoonkim/MPS_MtL_TUM.git
   cd MPS_MtL_TUM
   ```

2. **Install dependencies** (see [Prerequisites](#prerequisites) above).

3. **Update file paths** – The notebooks contain absolute paths specific to the original development environment (e.g. `/home/wjoon21/project/...`). Search for these paths and replace them with the locations of your own input files (PDB structures, parameter files, etc.).

4. **Launch Jupyter**
   ```bash
   jupyter notebook notebooks/
   ```

5. **Run notebooks sequentially**, starting from `01_interface_visualisation.ipynb`.

## Key Methods

- **Force field**: AMBER ff19SB (protein), TIP3P (water), GAFF2 (small molecules)
- **Long-range electrostatics**: Particle Mesh Ewald (PME)
- **Enhanced sampling**: Umbrella Sampling along RMSD collective variables
- **Free energy**: Weighted Histogram Analysis Method (WHAM) via `pymbar`
- **Replica exchange**: Hamiltonian REMD for improved conformational sampling

## References

- [AMBER Tutorials](https://ambermd.org/tutorials/)
- [MDTraj Documentation](https://www.mdtraj.org/)
- [PyTraj Documentation](https://amber-md.github.io/pytraj/)
- [pymbar](https://github.com/choderalab/pymbar)
- Seminar slides: `t38_seminar_07082024.pdf`

## Author

**Won Joon Kim**  
Technical University of Munich (TUM)
