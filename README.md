# LatticeGNN: Mechanics-Informed GNN for Crack Path Prediction

[![Python 3.8+](https://img.shields.io/badge/python-3.8+-blue.svg)](https://www.python.org/)
[![PyTorch](https://img.shields.io/badge/PyTorch-EE4C2C?logo=pytorch&logoColor=white)](https://pytorch.org/)
[![PyG](https://img.shields.io/badge/PyTorch_Geometric-3C2179?logo=pytorch&logoColor=white)](https://pytorch-geometric.readthedocs.io/)
[![Abaqus](https://img.shields.io/badge/Abaqus-FEA_Simulation-005A9C)](https://www.3ds.com/)

A Mechanics-Informed Graph Neural Network (GNN) framework designed to predict crack propagation paths in complex lattice structures and heterogeneous materials using Abaqus finite element simulation data.

---

## Key Features

- **Graph Topology Extraction**: Parses Abaqus `.inp` files and `.csv` status outputs to construct lattice graph models.
- **Physics-Informed GNN**: Utilizes `TransformerConv` with multi-head attention to capture node-level and edge-level mechanical interactions.
- **Topological Crack Restoration**: Built-in algorithms to reconstruct macroscopic strut fracture paths from microscopic element damage states.
- **High-Quality Visualizations**: Automatic plot generation comparing Abaqus Ground Truth against GNN predictions.

---

## Results Preview

| Abaqus Ground Truth | GNN Prediction Path |
| :---: | :---: |
| ![Ground Truth](real_crack_ground_truth.png) | ![GNN Prediction](local_predict_epoch_01.png) |

> **Note**: The framework automatically aggregates micro-element damage states back into full macroscopic lattice strut fractures, ensuring physical continuity along the crack path.

---

## Installation & Requirements

Ensure you have PyTorch and PyTorch Geometric installed.

```bash
# Clone the repository
git clone [https://https://github.com/Xycircle/crack-prediction-gnn](https://github.com/Xycircle/LatticeGNN-Crack-Prediction.git)
cd LatticeGNN-Crack-Prediction

# Install dependencies
pip install torch torch-geometric pandas matplotlib numpy

##Quick Start

### 1. Model Training
To train the GNN on preprocessed lattice graph datasets (`.pt` files):

```bash
python train_local.py

###2. Visualize Abaqus Real Crack Path
Place your Abaqus .inp mesh file and .csv status export into the repository directory, then run:

```Bash
python draw_exact_real_crack.py

##Network Architecture

The core model LatticeGNN leverages stacked Transformer Convolution layers integrated with global context pooling and edge feature concatenation:

Node/Edge Features ──> [TransformerConv 1] ──> Global Pooling Context 1
                           │
                       [TransformerConv 2] ──> Global Pooling Context 2
                           │
                       [TransformerConv 3] + Residual Connection
                           │
                    Edge Concatenation ──> Classifier MLP ──> Fracture Probability
##Project Structure
├── train_local.py            # GNN training logic with Focal Loss & validation visualization
├── draw_exact_real_crack.py  # Auto-retrieval script for rendering Abaqus Ground Truth
├── truss_strut_graph_data.pt # Preprocessed graph dataset (Example)
└── README.md                 # Project documentation

##Citation & Contact