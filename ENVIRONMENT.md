# Reference environment

The notebook is designed for Google Colab with a T4 GPU. Its setup cell installs the direct requirements and reports the versions present in the active runtime.

The following core versions were recorded in the notebook output used to prepare release 1.0.0 on 2026-09-02:

| Component | Version |
| --- | --- |
| Python | 3.13.15 |
| GPU | NVIDIA Tesla T4 |
| PyTorch | 2.11.0+cu128 |
| NumPy | 2.5.2 |
| SciPy | 1.18.1 |
| scikit-image | 0.26.0 |
| Cellpose | 4.2.1.1 |
| tifffile | 2026.8.23 |
| BioIO | 3.5.0 |
| bioio-bioformats | 2.0.0 |
| bffile | 0.1.1 |

Google Colab updates its Python, CUDA, and preinstalled packages periodically. For reproducibility, retain the setup cell's version report with the exported analysis and record the runtime type, segmentation model, model parameters, mask geometry, measurement compartment, and thresholds used.

The full notebook is not intended to run as an unattended command-line program. It requires interactive choices and, for most segmentation workflows, a GPU. The GitHub validation workflow therefore checks file and metadata integrity without executing the image-analysis cells.

## Proprietary image formats

OIR, CZI, LIF, and ND2 support depends on the corresponding reader and its external components. The setup cell reports reader failures explicitly. If Bio-Formats cannot initialize, follow the message printed by the notebook and verify the affected file format before starting a batch.

