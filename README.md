# Multiplex Immunofluorescence and Chromogenic IHC Analysis Suite

[![Open in Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/arunviswanathan91/ImageAnalysis/blob/main/Final_copy_of_MultiplexIF_Analysis_Suite.ipynb)
[![Save a copy to Google Drive](https://img.shields.io/badge/Save_a_copy-Google_Drive-4285F4?logo=googledrive&logoColor=white)](https://drive.google.com/uc?export=copy&id=1Ud3Y_YBN2NAudNDyiVo6NRUnrPKjif-B)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Repository validation](https://github.com/arunviswanathan91/ImageAnalysis/actions/workflows/validate.yml/badge.svg)](https://github.com/arunviswanathan91/ImageAnalysis/actions/workflows/validate.yml)
[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.22260636.svg)](https://doi.org/10.5281/zenodo.22260636)

An interactive Google Colab workflow for quantitative analysis of multiplex immunofluorescence images and chromogenic immunohistochemistry images. The notebook guides the user through image import, channel assignment, segmentation, measurement, threshold review, visualization, and export.

The main notebook is [Final_copy_of_MultiplexIF_Analysis_Suite.ipynb](Final_copy_of_MultiplexIF_Analysis_Suite.ipynb).
<figure>
  <img src="[your-image-url.jpg](https://github.com/arunviswanathan91/ImageAnalysis/blob/main/assets/graphical%20abstract.png)" alt="Abstract showing the processing pipeline of the colab notebook">
  <figcaption><i>Figure 1: This is your image caption.</i></figcaption>
</figure>
## Start here

1. Click **Open in Colab** above.
2. In Colab, select **Runtime > Change runtime type > T4 GPU**.
3. Run the environment setup cell once. The runtime may restart after package installation. If it does, continue with Step 2 and do not rerun the setup cell in the same session.
4. Load an image or select a Google Drive folder for batch processing.
5. Follow the widgets in order and inspect the segmentation masks, measurement regions, distributions, and classification overlays before export.

To keep an editable copy in your own Google Drive, click **Save a copy to Google Drive**. If the copy prompt is unavailable, open the notebook in Colab and select **File > Save a copy in Drive**.

## Analysis modules

### Multiplex immunofluorescence

- Imports OIR, CZI, LIF, ND2, TIFF, PNG, and JPEG images.
- Assigns biological roles to any number of image channels.
- Segments nuclei with Cellpose models, with optional MicroSAM support.
- Supports nuclear masks, distance-based expansion, and watershed-based cell masks.
- Measures native image intensity per cell without normalizing the source values.
- Provides interactive positivity thresholds and cell classification.
- Generates spatial maps, population summaries, scatter plots, and morphology measurements.
- Exports cell-level tables, summary tables, and publication-quality TIFF and SVG figures.

### Chromogenic immunohistochemistry

- Imports RGB TIFF, PNG, and JPEG images for individual or batch analysis.
- Performs H-DAB colour deconvolution using the Ruifrok and Johnston vectors implemented in scikit-image.
- Accepts custom stain vectors for other chromogenic stains.
- Supports cell-based measurement in nuclear, perinuclear-ring, and whole-cell compartments.
- Supports area-based scoring for extracellular, matrix, or diffuse targets that have no cellular denominator.
- Provides optional negative-control calibration, automated threshold initialization, manual threshold review, H-score calculation, and stained-area scoring.
- Exports per-cell or per-area results, threshold metadata, quality-control summaries, and figures.

## Supported inputs

| Module | Formats | Notes |
| --- | --- | --- |
| Multiplex immunofluorescence | `.oir`, `.czi`, `.lif`, `.nd2`, `.tif`, `.tiff`, `.png`, `.jpg`, `.jpeg` | Proprietary formats use BioIO or native fallback readers. |
| Chromogenic IHC | `.tif`, `.tiff`, `.png`, `.jpg`, `.jpeg` | Images must be standard RGB brightfield images. |

For batch analysis, organize images into folders that represent samples, conditions, experiments, or markers. The notebook displays the detected structure before analysis and allows assignments to be reviewed.

## Outputs

Depending on the selected module and options, the notebook can produce:

- per-cell measurement tables in CSV format;
- grouped and per-file summary tables in CSV or XLSX format;
- segmentation, mask, channel, classification, and spatial-map figures;
- TIFF and SVG figure exports;
- H-score, stained-area, and threshold quality-control tables for chromogenic IHC;
- ZIP archives for convenient download or transfer to Google Drive.

Generated data, source images, and result folders are intentionally excluded from version control. Do not commit confidential, identifiable, or unpublished image data to this public repository.

## Interpretation and quality control

Automated segmentation and threshold values are starting points. Inspect representative masks and classification overlays before accepting a batch. Use the same measurement settings and threshold scope for samples that will be compared.

For chromogenic IHC, optical density and H-score are semiquantitative measurements. They should be reported as staining measurements or agreement with a reference assessment, not as direct measurements of antigen concentration. A matched technical negative control can establish the negative/weak boundary without assuming that the sample batch contains a negative population.

This research workflow is not validated for clinical diagnosis or treatment decisions.

## External validation

The analysis flow has been evaluated using independent, publicly available image datasets for both the fluorescence and chromogenic branches. The external datasets used for validation are listed below so that the analyses can be independently reproduced or compared against the source material.

| Branch | External validation dataset | Validation use | Links |
| --- | --- | --- | --- |
| Multiplex immunofluorescence | **TONSIL-1 t-CyCIF** | Highly multiplexed fluorescence tonsil data used to evaluate the fluorescence analysis workflow, including segmentation and downstream single-cell measurements. | [Dataset](https://www.synapse.org/Synapse:syn17865732/) · [Paper](https://doi.org/10.1038/s41597-019-0332-y) |
| Chromogenic IHC | **HER2-IHC-40x** | High-resolution HER2 IHC breast-cancer images used to evaluate the chromogenic IHC workflow and staining/scoring measurements. | [Dataset](https://zenodo.org/records/15179608) · [Paper](https://doi.org/10.1016/j.dib.2025.111922) |
| Chromogenic IHC | **Human Protein Atlas cancer pathology images** | Cancer IHC images spanning different antibodies, with expert staining annotations, used as an independent reference for testing the chromogenic workflow across markers and staining intensities. | [Human Protein Atlas](https://www.proteinatlas.org) · [Pathology Atlas paper](https://doi.org/10.1126/science.aan2507) |

The repository contains dedicated validation notebooks for the two analysis branches:

- [Fluorescence branch validation](validation/FL_branch_validation.ipynb)
- [Chromogenic IHC branch validation](validation/IHC_branch_validation.ipynb)

These validation exercises support research-use benchmarking and reproducibility; they do not constitute clinical validation of the workflow.

## Reproducibility

The notebook installs its direct dependencies in the first setup cell and prints the versions present in the active Colab runtime. [requirements.txt](requirements.txt) records the direct software requirements, and [ENVIRONMENT.md](ENVIRONMENT.md) records the reference environment used for the first public release. Google Colab runtime images change over time, so retain the printed version report with each analysis.

## Citation



## Contributing and support

Bug reports and feature requests are welcome through [GitHub Issues](https://github.com/arunviswanathan91/ImageAnalysis/issues). Please read [CONTRIBUTING.md](CONTRIBUTING.md) before submitting code or example data.

## License

The notebook and repository documentation are released under the [MIT License](LICENSE). Third-party packages, pretrained models, and image-reader components remain subject to their own licenses and terms.
