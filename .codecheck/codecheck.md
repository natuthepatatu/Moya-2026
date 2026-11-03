# CODECHECK certificate 2026-029
## [10.5281/zenodo.23666248](10.5281/zenodo.23666248)
[![CODECHECK logo](codecheck_logo.svg)](<https://codecheck.org.uk>)



## Table 1: CODECHECK summary





Item | Value
:--- | :----
Title | *Do Laypeople Endorse the Axioms of Inequality Measurement? Outcomes Report of a Preregistered Replication and Extension of Amiel and Cowell (1992) in a U.S. General-Population Sample*
Author(s) | Cristóbal Moya (ORCID: 0000-0002-7176-4775), Carsten Schröder (ORCID: 0000-0002-6406-595X), Philipp Lersch (ORCID: 0000-0003-3863-8301)
Reference | [https://doi.org/10.71240/lcyc.829503](https://doi.org/10.71240/lcyc.829503)
Repository | [https://doi.org/10.5281/zenodo.23666248](https://doi.org/10.5281/zenodo.23666248)
Codechecker(s) | Nataliia Petliak (ORCID: 0009-0008-3939-1244)
Date of check | *2026-10-22*
Summary | The authors' computational reproduction workflow completed successfully and generated the expected PDF report. An initial Docker build issue was resolved by explicitly selecting the target platform.



## Table 2: Summary of output files generated





File | Comment | Size (b)
:--------------------- | :----------------------------------- | -------:
`outcomes_report_pub.pdf` | Reproduced 25-page PDF report containing the analyses, tables, and figures. The complete report is included in this certificate. | 634352






This check is based on the commit `7c308139fb97cc621d1c9b703a87e1575c41214e`.



## Summary




The authors' computational reproduction workflow completed successfully and generated the expected PDF report. An initial Docker build issue was resolved by explicitly selecting the target platform.



## CODECHECKER notes

### Computational environment

The CODECHECK was performed on an Apple Silicon Mac running macOS.

The certificate-generation environment uses Python 3.12.15, Jupyter, and Typst 0.15.1.

The authors provide a Docker-based reproduction environment with R 4.6.0, Quarto 1.10.18, and an R package snapshot dated 2026-08-03 from Posit Package Manager.

Docker 28.5.1 was installed and the Docker engine was running.

### Reproduction procedure

The computational reproduction followed the four-step Docker workflow described in the authors' `README.md`.

**Steps 1–2: Download and extract the reproduction package**

The reproduction materials were downloaded from the authors' [OSF repository](https://doi.org/10.17605/OSF.IO/8Z2UV) and extracted into the local CODECHECK working directory.

The downloaded archive (`8z2uv-osfstorage-archive.zip`) contained a nested archive (`inequality-axioms-repro-20260831.zip`).

The extracted package includes the Quarto source document (`output/outcomes_report_pub.qmd`), minimal anonymized datasets under `data/minimal/`, a `Dockerfile`, a `Makefile`, and reproduction instructions. Separate licenses are provided for the code and data.

Extraction completed successfully. No modifications were made to the authors' source files or configuration.

**Step 3: Build the Docker image**

The initial Docker build was attempted from the root of the extracted reproduction package using the command specified in the README:

```bash
docker build -t ineq-axioms-repro:1.0 .
```

The build failed after approximately 62 seconds during the installation of Quarto 1.10.18.

The container was running on ARM64, but the Dockerfile attempted to install the AMD64 version of Quarto. This resulted in the following error:

```text
dpkg: error processing archive /tmp/quarto.deb (--install):
package architecture (amd64) does not match system (arm64)
```

The Dockerfile specifies `ARG TARGETARCH=amd64`, which was not overridden during the initial build. Consequently, the downloaded Quarto package did not match the container architecture.

The build terminated with exit code 1. The failure was caused by an architecture mismatch in the supplied Docker configuration when building on Apple Silicon.

To address the mismatch without modifying the authors' Dockerfile, the build was retried with the target platform explicitly set to AMD64:

```bash
docker build --platform linux/amd64 -t ineq-axioms-repro:1.0 .
```

This uses Docker's AMD64 emulation on the Apple Silicon host. The command differs from the authors' instructions only by the addition of `--platform linux/amd64`.

The second build completed successfully in 355.8 seconds, including installation of Quarto 1.10.18 and the required R packages. The resulting image was tagged `ineq-axioms-repro:1.0`.

No modifications to the authors' files were necessary.

**Step 4: Render the report**

After successfully building the Docker image for AMD64, the report was rendered using the exact command provided in the authors' README:

```bash
docker run --rm -v "$PWD":/work ineq-axioms-repro:1.0
```

Docker reported a platform mismatch warning because the AMD64 image was running on an ARM64 host:

```text
WARNING: The requested image's platform (linux/amd64) does not match
the detected host platform (linux/arm64/v8) and no specific platform
was requested
```

The warning did not prevent execution.

Quarto completed all 89 processing steps, including the code chunks generating the analyses, tables, and figures. Pandoc and Typst then compiled the document successfully.

The process completed without errors and generated the expected output:

```text
output/outcomes_report_pub.pdf
```

The authors' source files and configuration remained unchanged.

### Results and observations

The reproduction workflow completed successfully using the authors' Docker environment with AMD64 emulation on the Apple Silicon host. The expected PDF was generated without modifying the authors' source files.

The reproduced PDF was visually inspected, and the tables and figures appeared to render correctly. A direct comparison with the published figures was not possible because they were not loading on the Lifecycle Journal website at the time of the check.

No detailed numerical comparison with the published report was performed.

## Recommendations to the authors

The Dockerfile currently downloads the AMD64 version of Quarto regardless of the container architecture, causing the default Docker build to fail on ARM64 systems such as Apple Silicon Macs.

Consider updating the Dockerfile to support multiple architectures or documenting the need to build with `--platform linux/amd64` on ARM64 hosts.

It would also be helpful to export each figure as a separate graphics file, in addition to the complete PDF report. This would make it easier to inspect individual figures, trace them back to the code that generated them, and include them explicitly in the reproduction manifest.

## Manifest files

Summary of all reproduced output files (tables, text files, figures, ...).


### `output/outcomes_report_pub.pdf`
Comment: *Reproduced 25-page PDF report containing the analyses, tables, and figures. The complete report is included in this certificate.*

![Reproduced 25-page PDF report containing the analyses, tables, and figures. The complete report is included in this certificate. — page 1](<outputs/_pdf_pages/outcomes_report_pub/page-001.png>)\n\n![Reproduced 25-page PDF report containing the analyses, tables, and figures. The complete report is included in this certificate. — page 2](<outputs/_pdf_pages/outcomes_report_pub/page-002.png>)\n\n![Reproduced 25-page PDF report containing the analyses, tables, and figures. The complete report is included in this certificate. — page 3](<outputs/_pdf_pages/outcomes_report_pub/page-003.png>)\n\n![Reproduced 25-page PDF report containing the analyses, tables, and figures. The complete report is included in this certificate. — page 4](<outputs/_pdf_pages/outcomes_report_pub/page-004.png>)\n\n![Reproduced 25-page PDF report containing the analyses, tables, and figures. The complete report is included in this certificate. — page 5](<outputs/_pdf_pages/outcomes_report_pub/page-005.png>)\n\n![Reproduced 25-page PDF report containing the analyses, tables, and figures. The complete report is included in this certificate. — page 6](<outputs/_pdf_pages/outcomes_report_pub/page-006.png>)\n\n![Reproduced 25-page PDF report containing the analyses, tables, and figures. The complete report is included in this certificate. — page 7](<outputs/_pdf_pages/outcomes_report_pub/page-007.png>)\n\n![Reproduced 25-page PDF report containing the analyses, tables, and figures. The complete report is included in this certificate. — page 8](<outputs/_pdf_pages/outcomes_report_pub/page-008.png>)\n\n![Reproduced 25-page PDF report containing the analyses, tables, and figures. The complete report is included in this certificate. — page 9](<outputs/_pdf_pages/outcomes_report_pub/page-009.png>)\n\n![Reproduced 25-page PDF report containing the analyses, tables, and figures. The complete report is included in this certificate. — page 10](<outputs/_pdf_pages/outcomes_report_pub/page-010.png>)\n\n![Reproduced 25-page PDF report containing the analyses, tables, and figures. The complete report is included in this certificate. — page 11](<outputs/_pdf_pages/outcomes_report_pub/page-011.png>)\n\n![Reproduced 25-page PDF report containing the analyses, tables, and figures. The complete report is included in this certificate. — page 12](<outputs/_pdf_pages/outcomes_report_pub/page-012.png>)\n\n![Reproduced 25-page PDF report containing the analyses, tables, and figures. The complete report is included in this certificate. — page 13](<outputs/_pdf_pages/outcomes_report_pub/page-013.png>)\n\n![Reproduced 25-page PDF report containing the analyses, tables, and figures. The complete report is included in this certificate. — page 14](<outputs/_pdf_pages/outcomes_report_pub/page-014.png>)\n\n![Reproduced 25-page PDF report containing the analyses, tables, and figures. The complete report is included in this certificate. — page 15](<outputs/_pdf_pages/outcomes_report_pub/page-015.png>)\n\n![Reproduced 25-page PDF report containing the analyses, tables, and figures. The complete report is included in this certificate. — page 16](<outputs/_pdf_pages/outcomes_report_pub/page-016.png>)\n\n![Reproduced 25-page PDF report containing the analyses, tables, and figures. The complete report is included in this certificate. — page 17](<outputs/_pdf_pages/outcomes_report_pub/page-017.png>)\n\n![Reproduced 25-page PDF report containing the analyses, tables, and figures. The complete report is included in this certificate. — page 18](<outputs/_pdf_pages/outcomes_report_pub/page-018.png>)\n\n![Reproduced 25-page PDF report containing the analyses, tables, and figures. The complete report is included in this certificate. — page 19](<outputs/_pdf_pages/outcomes_report_pub/page-019.png>)\n\n![Reproduced 25-page PDF report containing the analyses, tables, and figures. The complete report is included in this certificate. — page 20](<outputs/_pdf_pages/outcomes_report_pub/page-020.png>)\n\n![Reproduced 25-page PDF report containing the analyses, tables, and figures. The complete report is included in this certificate. — page 21](<outputs/_pdf_pages/outcomes_report_pub/page-021.png>)\n\n![Reproduced 25-page PDF report containing the analyses, tables, and figures. The complete report is included in this certificate. — page 22](<outputs/_pdf_pages/outcomes_report_pub/page-022.png>)\n\n![Reproduced 25-page PDF report containing the analyses, tables, and figures. The complete report is included in this certificate. — page 23](<outputs/_pdf_pages/outcomes_report_pub/page-023.png>)\n\n![Reproduced 25-page PDF report containing the analyses, tables, and figures. The complete report is included in this certificate. — page 24](<outputs/_pdf_pages/outcomes_report_pub/page-024.png>)\n\n![Reproduced 25-page PDF report containing the analyses, tables, and figures. The complete report is included in this certificate. — page 25](<outputs/_pdf_pages/outcomes_report_pub/page-025.png>)\n


## Citing this document




Nataliia Petliak (*2026-10-22*). CODECHECK Certificate 2026-029. CODECHECK Community on Zenodo. [10.5281/zenodo.23666248](10.5281/zenodo.23666248)



## About CODECHECK





This certificate confirms that the codechecker could independently reproduce the results of a computational analysis given the data and code from a third party. A CODECHECK does not check whether the original computation analysis is correct. However, as all materials required for the reproduction are freely available by following the links in this document, the reader can then study for themselves the code and data.



## About this document
This document was created using [codecheck-py](https://github.com/codecheckers/codecheck-py/) (a Python-based template for creating [CODECHECK](https://codecheck.org.uk/) certificates). The CODECHECK details are filled into a [jupyter notebook](https://jupyter.org/) which is then converted into Markdown via [nbconvert](https://nbconvert.readthedocs.io/). Afterwards it gets converted into [Typst](https://typst.app/) using [cmarker](https://typst.app/universe/package/cmarker/) and then into PDF using Typst. `sh notebook_to_pdf.sh` will regenerate the report file.

```python
import session_info2 as si
si.session_info(os=True, cpu=True, gpu=True, dependencies=True)
```




```bash
ipykernel	7.4.0
debugpy	1.8.22
requests	2.34.2
tornado	6.6
pyzmq	27.2.0
numpy	2.5.4
pandas	3.0.6
packaging	26.3
charset-normalizer	3.5.2
idna	3.20
six	1.17.0
jupyter_core	5.9.1
jupyter_client	8.10.0
PyYAML	6.0.3
urllib3	2.8.0
ipython	9.17.1
python-dateutil	3.0.0
platformdirs	4.13.5
traitlets	5.16.1
certifi	2026.10.19
appnope	1.0.0
session-info2	0.4.2
psutil	7.2.2
pymupdf	2.1
Pygments	2.21.0
comm	0.2.3
typing_extensions	4.16.0
----	----
Python	3.12.15 (main, Sep 30 2026, 22:04:19) [Clang 21.0.0 (clang-2100.3.34.2)]
OS	macOS-26.6.2-arm64-arm-64bit
CPU	14/14 logical CPU cores, arm
GPU	No GPU found
Updated	2026-11-03 09:55
```




## License
The original authors' code is licensed under the MIT License (`LICENSE`),
while the data and stimuli are licensed under Creative Commons Attribution
4.0 International (CC BY 4.0; `LICENSE-DATA`).
The license files are included in the downloaded reproduction archive available from the [OSF repository](https://doi.org/10.17605/OSF.IO/8Z2UV).
The content of the `.codecheck` directory and this report are licensed
under the [CC BY 4.0 license](https://creativecommons.org/licenses/by/4.0/).
