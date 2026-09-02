# Contributing

Thank you for helping improve the Image Analysis Suite.

## Reporting a problem

Use the bug-report template and include:

- the notebook step in which the problem occurred;
- whether the immunofluorescence or chromogenic IHC module was used;
- the input file format and image dimensions;
- the Colab runtime type and package-version report;
- the segmentation model and relevant parameter values;
- the complete error message and the shortest sequence that reproduces it.

Do not upload confidential images, protected health information, access tokens, Google Drive credentials, or other sensitive material. A small synthetic or de-identified example is preferred when an image is needed to reproduce a problem.

## Proposing a change

1. Open an issue describing the problem or proposed feature.
2. Create a focused branch from `main`.
3. Make the smallest change that addresses the issue.
4. Test the affected workflow in a fresh Colab runtime.
5. Confirm that the notebook remains valid JSON and that no private data or credentials are present.
6. Open a pull request explaining what changed, why it changed, and how it was tested.

Keep generated outputs only when they are necessary to explain expected behaviour. Large image data and routine analysis outputs should remain outside the repository.

## Scientific changes

Changes to segmentation, measurement regions, threshold rules, score definitions, or default parameters can alter scientific results. Such pull requests should state the previous and proposed behaviour, provide a validation example, and identify any effect on backward comparability.

