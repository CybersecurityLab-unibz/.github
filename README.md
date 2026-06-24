The central hub for CSLab's repository naming conventions, rules, and lab-wide policies.

# CSLab GitHub Organization Guidelines

Welcome to the Cybersecurity Lab (CSLab) GitHub organization. To maintain a professional, searchable, and reproducible academic environment, all lab members and collaborators are expected to follow these standardized guidelines for repository naming, categorization, and structuring.

## 1. Standardized Naming Convention

All repositories must follow a strict four-part naming structure. To balance web visibility with Python environment compatibility, use hyphens to separate the main blocks, but use underscores (`snake_case`) for the project name itself.

**Format:** `[output_type]-[domain]-[year]-[project_name]`

> **Note on Length:** To keep repository and file names concise, any `[project_name]` or `[Title]` must consist of a maximum of 5 main keywords, acronyms, or core concepts.

### 1. Output Type (First Prefix)
Choose the prefix that best describes the artifact being produced:
* **`paper`**: Replication packages, LaTeX source files, or data tied directly to a manuscript.
* **`tool`**: Reusable standalone scripts, CLI utilities, and scrapers.
* **`eval`**: Cross-domain evaluations and metric frameworks.
* **`archive`**: Centralized indexes or collections linking to other repositories.
* **`doc`**: Non-code outputs like slides, presentations, and documentation.
* **`project`**: Broad, multi-phase research pipelines.

### 2. Domain (Second Prefix)
Choose the prefix that best describes the scientific area of the repository:
* **`ml`**: Machine learning models, deep learning frameworks, and AI fine-tuning.
* **`ids`**: Network security, operational technology (OT), and intrusion detection systems.
* **`vuln`**: Vulnerability mining, CVE parsing, and exploit analysis.
* **`crypto`**: Cryptographic research, formal verification, and algebraic proofs.

*(Example: A machine learning tool developed in 2026 for class imbalance should be named `tool-ml-2026-beyond_balance`. A 2025 intrusion detection evaluation should be named `eval-ids-2025-cross_domain`).*

* **Paper Exception:** If the repository is for a paper replication package, replace `[project_name]` with `[Event]-[AuthorName]-[Title]`.
**Format:** `paper-[domain]-[year]-[Event]-[AuthorName]-[Title]`
*(Example: `paper-crypto-2026-SFSCON-Firstname_Lastname-Blind_Signatures`)*

---

## 2. Categorization, Topics, and Labels

To make our lab's research discoverable to the global academic community, every repository must be properly tagged.

### Repository Topics (Metadata Tags)
Navigate to the repository's **About** section and add 5 to 10 descriptive topics. 
* **Domain Tags:** `cybersecurity`, `intrusion-detection`, `cryptography`, `vulnerability-management`
* **Methodology Tags:** `machine-learning`, `unsupervised-learning`, `llm`, `sast`
* **Technology Tags:** `python`, `pytorch`, `flask`, `d3js`

### Issue & Pull Request Labels
When managing tasks, or bugs, use the organization's standardized issue labels (e.g., `bug`, `enhancement`, `data-processing`). Organization Owners manage these global labels to ensure consistency across all projects.

---

## 3. Folderization & Repository Architecture

A flat directory (dumping all scripts and data into the root folder) is strictly prohibited. Use standard software engineering architectures.

### Standard Code Repositories
Every tool, model, or pipeline must feature a clean root directory containing only configuration files:

```text
/src                # All source code and Python modules
/data               # Datasets (Always split into /raw and /output)
/docs               # Architecture diagrams and extended notes
/tests              # Unit tests and validation scripts
requirements.txt    # Standardized dependency list
.gitignore          # MUST block /venv, __pycache__, and large /data files
README.md           # Project description, installation, and usage instructions
```

---

## 4. Specialized Lab Archives
Certain repositories act as lab-wide utilities rather than single projects. These perpetual archives are exempt from the standard domain and year requirements. They require highly specific folder structures:

### The Dissemination Archive (`doc-presentations`)
This repository houses all CSLab slides, conference talks, and PhD milestones. To prevent clutter, files must never be placed in the root directory. They must be categorized by **Event Type** and **Year**:

**Rule:** Always upload the source file (`.pptx`, `.key`) using the naming convention: `[Event]-[Year_or_Date]-[AuthorName]-[Title].[extension]`.

```text
/Conferences
    /2025
    /2026
/PhD_Milestones
    /RSPs
    /Defenses
/Industry_Events
    /2026
        Meeting-20260228-Firstname_Lastname-Anomaly_Detection.pptx
```


### The Replication Package Collection (`archive-replication_packages`)
This repository serves as a single, central master index linking to the code for all of the lab's published research papers. Instead of copying files directly into this master index, we use **Git Submodules** to cleanly point to each project's individual repository.

* **The One-to-One Rule:** Every published paper or distinct research project must have its own **single, dedicated standalone repository** (e.g., `paper-ids-2026-SFSCON-Firstname_Lastname-Anomaly_Detection`). Do not combine multiple papers or unrelated projects into one repository. 
* **Master Index Integration:** Once a paper is accepted, its dedicated standalone repository is added as a submodule inside this `archive-replication_packages` index. No raw data or scripts should ever be uploaded directly here.
* **External Usage:** The master `README.md` must clearly explain how external researchers can clone the entire collection of nested submodules using `git clone --recurse-submodules`.

---

## 5. Minimum README Requirements

Every repository in the CSLab organization must contain a `README.md` that includes:
1. **Title & Badges:** A clear title and standard badges (e.g., Build status, Python version).
2. **Abstract:** A 2-3 sentence overview of what the code does.
3. **Citation:** If the repository is tied to a paper, provide the BibTeX citation block.
4. **Prerequisites:** Any system-level requirements (e.g., Docker, Tesseract-OCR).
5. **Installation:** Step-by-step terminal commands to create virtual environments and install dependencies.
6. **Usage:** Example commands on how to execute the code or pipeline.
7. **License:** A clearly stated open-source license (e.g., MIT, Apache 2.0) explicitly outlining how external researchers are allowed to use, modify, and distribute the code and datasets.