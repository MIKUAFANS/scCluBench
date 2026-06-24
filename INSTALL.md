# Installation Guide

## Prerequisites

- Python >= 3.8
- CUDA >= 11.0 (optional, for GPU support)

## Installation

### 1. Create Virtual Environment (Recommended)

```bash
# Using conda
conda create -n scclubench python=3.8
conda activate scclubench

# Or using venv
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
```

### 2. Install Dependencies

```bash
pip install -r requirements.txt
```

## Dependency Overview

### Core Dependencies (Required)

| Package | Version | Purpose |
|---------|---------|---------|
| numpy | >=1.21.0 | Array operations |
| scipy | >=1.7.0 | Scientific computing |
| pandas | >=1.3.0 | Data manipulation |
| scikit-learn | >=0.24.0 | ML algorithms & metrics |

### Deep Learning Frameworks

| Package | Version | Used By |
|---------|---------|---------|
| torch | >=1.10.0 | Most models (DEC, scDCC, scMAE, GNN models) |
| torchmetrics | >=0.6.0 | PyTorch metrics |
| tensorflow | >=2.8.0 | DESC, scDeepCluster, scNAME, scziDesk |

### Single-cell Analysis

| Package | Version | Purpose |
|---------|---------|---------|
| scanpy | >=1.8.0 | scRNA-seq preprocessing |
| anndata | >=0.7.6 | Handling h5ad files |
| h5py | >=3.1.0 | HDF5 file I/O |

### Graph & Network Analysis

| Package | Version | Used By |
|---------|---------|---------|
| python-igraph | >=0.9.0 | scGNN (Louvain clustering) |
| networkx | >=2.6.0 | Graph operations in GNN models |
| jgraph | >=0.2.0 | Cell type DAG operations |
| pronto | >=2.4.0 | Ontology processing |

### Dimensionality Reduction & Clustering

| Package | Version | Purpose |
|---------|---------|---------|
| umap-learn | >=0.5.0 | UMAP embeddings |
| MulticoreTSNE | >=0.1 | Fast t-SNE |
| munkres | >=1.1.4 | Hungarian algorithm for accuracy |

### Visualization (Analysis Scripts)

| Package | Version | Purpose |
|---------|---------|---------|
| matplotlib | >=3.4.0 | Basic plotting |
| seaborn | >=0.11.0 | Statistical visualization |
| pyecharts | >=1.9.0 | Sankey diagrams |
| snapshot-selenium | >=0.0.2 | Chart rendering |

### Utilities

| Package | Version | Purpose |
|---------|---------|---------|
| tqdm | >=4.62.0 | Progress bars |
| loguru | >=0.5.3 | Logging |
| natsort | >=7.1.0 | Natural sorting |

## Model-Specific Requirements

### PyTorch-based Models
- **DEC, scDCC, scMAE, scDeepCluster**: torch only
- **GNN models** (AttentionAE-sc, scDSC, scGAE, scGNN, scCDCG): torch + graph libraries

### TensorFlow-based Models
- **DESC, scDeepCluster, scNAME, scziDesk**: tensorflow

### Hybrid Models
- **scDeepCluster**: Uses both TensorFlow and PyTorch

## GPU Support

For GPU acceleration with PyTorch:
```bash
# Install PyTorch with CUDA support
pip install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu118
```

For GPU acceleration with TensorFlow:
```bash
pip install tensorflow[and-cuda]
```

## Troubleshooting

### python-igraph Installation Issues

If you encounter issues installing `python-igraph`:

**On Ubuntu/Debian:**
```bash
sudo apt-get install libigraph0-dev
pip install python-igraph
```

**On macOS:**
```bash
brew install igraph
pip install python-igraph
```

**On Windows:**
```bash
conda install -c conda-forge python-igraph
```

### MulticoreTSNE Installation Issues

If `MulticoreTSNE` fails to install:
```bash
# Alternative: use scikit-learn's TSNE
# The code will fall back automatically
```

### TensorFlow Compatibility

If you encounter TensorFlow compatibility issues, try:
```bash
pip install tensorflow==2.12.0  # Known stable version
```

## Verification

Test your installation:

```bash
python -c "import torch; print(f'PyTorch: {torch.__version__}')"
python -c "import tensorflow as tf; print(f'TensorFlow: {tf.__version__}')"
python -c "import scanpy; print(f'Scanpy: {scanpy.__version__}')"
python -c "import igraph; print(f'igraph: {igraph.__version__}')"
```

## Minimal Installation (Core Models Only)

If you only need specific models, you can install a minimal set:

```bash
# For PyTorch-based models only
pip install numpy scipy pandas scikit-learn torch torchmetrics scanpy anndata h5py munkres tqdm

# For TensorFlow-based models only
pip install numpy scipy pandas scikit-learn tensorflow scanpy anndata h5py munkres tqdm
```
