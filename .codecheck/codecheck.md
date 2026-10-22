# CODECHECK certificate 2026-029
## [None](None)
[![CODECHECK logo](codecheck_logo.svg)](<https://codecheck.org.uk>)



## Table 1: CODECHECK summary





Item | Value
:--- | :----
Title | *Do Laypeople Endorse the Axioms of Inequality Measurement? Outcomes Report of a Preregistered Replication and Extension of Amiel and Cowell (1992) in a U.S. General-Population Sample*
Author(s) | Cristóbal Moya (ORCID: 0000-0002-7176-4775), Carsten Schröder (ORCID: 0000-0002-6406-595X), Philipp Lersch (ORCID: 0000-0003-3863-8301)
Reference | [https://doi.org/10.71240/lcyc.829503](https://doi.org/10.71240/lcyc.829503)
Repository | [https://doi.org/10.17605/OSF.IO/8Z2UV](https://doi.org/10.17605/OSF.IO/8Z2UV)
Codechecker(s) | Nataliia Petliak
Date of check | *2026-10-22*
Summary | The authors' computational reproduction workflow completed successfully using Docker with AMD64 emulation on an Apple Silicon host. The expected PDF report was generated. The initial Docker build failed due to an architecture mismatch, which was resolved by explicitly targeting linux/amd64 without modifying the authors' files.



## Table 2: Summary of output files generated





File | Comment | Size (b)
:--------------------- | :----------------------------------- | -------:
`outcomes_report_pub.pdf` | Reproduced PDF report containing the analyses, tables, and figures | 634352






This check is based on the commit `2f301f91624777fc11c912e2667fc74255fee9aa`.



## Summary




The authors' computational reproduction workflow completed successfully using Docker with AMD64 emulation on an Apple Silicon host. The expected PDF report was generated. The initial Docker build failed due to an architecture mismatch, which was resolved by explicitly targeting linux/amd64 without modifying the authors' files.



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

No other issues were encountered during the reproduction workflow.

## Manifest files

Summary of all reproduced output files (tables, text files, figures, ...).


### `output/outcomes_report_pub.pdf`
Comment: *Reproduced PDF report containing the analyses, tables, and figures*

![Reproduced PDF report containing the analyses, tables, and figures](<outputs/output/outcomes_report_pub.pdf>)



## Citing this document




Nataliia Petliak (*2026-10-22*). CODECHECK Certificate 2026-029. CODECHECK Community on Zenodo. [None](None)



## About CODECHECK





This certificate confirms that the codechecker could independently reproduce the results of a computational analysis given the data and code from a third party. A CODECHECK does not check whether the original computation analysis is correct. However, as all materials required for the reproduction are freely availableby following the links in this document, the reader can then study for themselves the code and data.



## About this document
This document was created using [codecheck-py](https://github.com/codecheckers/codecheck-py/) (a Python-based template for creating [CODECHECK](https://codecheck.org.uk/) certificates). The CODECHECK details are filled into a [jupyter notebook](https://jupyter.org/) which is then converted into Markdown via [nbconvert](https://nbconvert.readthedocs.io/). Afterwards it gets converted into [Typst](https://typst.app/) using [cmarker](https://typst.app/universe/package/cmarker/) and then into PDF using Typst. `sh notebook_to_pdf.sh` will regenerate the report file.

```python
import session_info2 as si
si.session_info(os=True, cpu=True, gpu=True, dependencies=True)
```




```bash
urllib3	2.8.0
ipython	9.17.1
ipykernel	7.4.0
platformdirs	4.13.5
comm	0.2.3
packaging	26.3
psutil	7.2.2
charset-normalizer	3.5.2
appnope	1.0.0
jupyter_client	8.10.0
certifi	2026.10.19
pyzmq	27.2.0
PyYAML	6.0.3
python-dateutil	3.0.0
idna	3.20
traitlets	5.16.1
debugpy	1.8.22
Pygments	2.21.0
numpy	2.5.4
typing_extensions	4.16.0
jupyter_core	5.9.1
requests	2.34.2
tornado	6.6
pandas	3.0.6
session-info2	0.4.2
six	1.17.0
----	----
Python	3.12.15 (main, Sep 30 2026, 22:04:19) [Clang 21.0.0 (clang-2100.3.34.2)]
OS	macOS-26.6.2-arm64-arm-64bit
CPU	14/14 logical CPU cores, arm
GPU	No GPU found
Updated	2026-10-22 12:38
```




## License
The original authors' code is licensed under the MIT License (`LICENSE`),
while the data and stimuli are licensed under Creative Commons Attribution
4.0 International (CC BY 4.0; `LICENSE-DATA`).
The license files are included in the downloaded reproduction archive available from the [OSF repository](https://doi.org/10.17605/OSF.IO/8Z2UV).
The content of the `.codecheck` directory and this report are licensed
under the [CC BY 4.0 license](https://creativecommons.org/licenses/by/4.0/).
