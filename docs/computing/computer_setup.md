---
layout: default
title: Computer Set Up
parent: Computing
nav_order: 1
---

# Software Setup for New Computers
If you have taken delivery of a new computer, you may find the following list of software commonly used in fLuLab useful.

## Contents
- [1. Package managers](#1-package-managers)
- [2. Programming languages and IDEs](#2-programming-languages-and-ides)
- [3. Frequently Used CLI Software](#3-frequently-used-cli-software)
- [4. Frequently Used GUI Software](#3-frequently-used-gui-software)

## 1. Package managers
A **package manager** is a tool that automates installing, updating, configuring and removing software. Instead of downloading installers by hand and tracking down dependencies yourself, you ask the package manager for what you need and it handles the rest.

Package managers are the foundation of a reproducible computational research setup:

- **Dependency resolution:** Scientific software depends on specific versions of many other libraries. A package manager works out a compatible set and installs them together.
- **Reproducibility:** Environments can be exported to a file (e.g. `environment.yml` or `requirements.txt`), so collaborators and future you can recreate exactly the same setup.
- **Isolation:** Separate environments let different projects use different versions of the same software without conflicts.
- **Maintenance:** Updating or cleanly removing software is a single command, which keeps your machine tidy and secure.

Set these up first, as almost everything else on this page is installed through them.

### 1.1 Python environments and packages

#### 1.1.1 Anaconda / Miniconda

**What it is:** A cross-platform package and environment manager. Although it originated in the Python ecosystem, it can install software in many languages (R, C/C++ libraries, etc.) as well as general command-line tools.

**Which to choose:** We recommend **Miniconda**, a minimal installer containing only conda and its dependencies. Full Anaconda bundles hundreds of packages you probably won't use and takes much more disk space.

**Typical usage:**

```bash
# Create a new environment with a specific Python version
conda create -n myproject python=3.11

# Activate it
conda activate myproject

# Install packages
conda install numpy scipy matplotlib

# Export the environment for sharing
conda env export > environment.yml
```

**Tips:**

- Create one environment per project rather than installing everything into `base`.
- The `conda-forge` channel is community-maintained and has the widest package coverage.

#### 1.1.2 pip

**What it is:** Python's standard package installer, which pulls packages from the Python Package Index (PyPI).

**When to use it:** For packages not available through conda. Where a package exists in both, prefer conda within a conda environment. If you must mix them, install conda packages first and pip packages last, to avoid breaking the environment.

**Typical usage:**

```bash
pip install package-name
pip install -r requirements.txt
pip list
```

### 1.2 System package managers

#### 1.2.1 Homebrew (macOS)

**What it is:** A package manager for macOS that installs command-line tools and, via "casks", some graphical applications.

**Note:** For most of our work, Homebrew has been **largely superseded by conda**. Conda (especially with `conda-forge`) can install the command-line tools and libraries we need, in isolated and reproducible environments, and does so identically on macOS and Linux. We therefore recommend trying conda first. Homebrew remains useful for system-wide utilities and GUI applications that conda does not provide.

**Installation:** See [brew.sh](https://brew.sh).

```bash
brew install package-name
brew install --cask application-name
brew update && brew upgrade
```

#### 1.2.2 APT (Linux: Debian/Ubuntu)

**What it is:** The default system package manager on Debian-based Linux distributions such as Ubuntu. It installs system-level software and libraries and typically requires administrator (`sudo`) rights.

**Typical usage:**

```bash
sudo apt update
sudo apt install package-name
sudo apt upgrade
```

**Tip:** Use APT for system-level tools and drivers, and conda for project-specific scientific software.


## 2. Programming languages and IDEs

An **IDE** (integrated development environment) combines a code editor with tools for running code, debugging, managing projects and version control. Which language and editor you use is a matter of personal preference, and there is no obligation to use any of those listed below. The table summarises what is commonly used in the group.

| Language | Suggested IDE(s) |
|---|---|
| R | RStudio (or Positron) |
| Python | PyCharm, VS Code, or JupyterLab |
| Julia | VS Code |
| Bash | VS Code |
| Java / other JVM languages | IntelliJ IDEA |

### 2.1 R

**What it is:** A language and environment for statistical computing, data analysis and graphics, with a very large ecosystem of packages for statistics and bioinformatics.

**Our use:** Most (but not all) group members use R for their work. There is no obligation to use R, but you will find more people able to help if/when you encounter problems.

**Installation:**

- Download R from [CRAN](https://cran.r-project.org/) (installers for macOS, Windows and Linux).
- Alternatively, install it through conda: `conda install -c conda-forge r-base` (see the note on using R with conda in section 1.2).

**Check it works:**

```bash
R --version
```

**Packages:** See section 1.2 for CRAN and pak.

#### Suggested IDE: RStudio

The most widely used IDE for R, developed by Posit. It provides a console, script editor, plot and package panes, an environment viewer, and built-in support for R Markdown and Quarto documents. It is the best choice if you want help from other group members, as most people use it.

- **Installation:** Install R first, then download [RStudio Desktop](https://posit.co/download/rstudio-desktop/). It is free.
- Use RStudio Projects (`File > New Project`) so each analysis has its own working directory.
- If R is installed through conda, you may need to tell RStudio which R to use (`Tools > Global Options > General > R version`).
- **Positron** is Posit's newer, VS Code-based IDE for R and Python. It is a reasonable alternative if you work in both languages. Download it from [positron.posit.co](https://positron.posit.co/).
- R can also be used in [VS Code](#23-visual-studio-code-vs-code-shared-editor) via the R extension, though RStudio is better for most R work.

### 2.2 Python

**What it is:** A general-purpose language widely used for data analysis, machine learning, scripting and automation (e.g. NumPy, pandas, SciPy, scikit-learn, PyTorch).

**Important:** If you are using macOS or a mainstream Linux distribution, a version of Python will already be installed. It is inadvisable to use the system version routinely, because the operating system depends on it and changing it can break system tools. Instead, install and manage local environments using an appropriate package manager (see section 1.1).

**Installation (recommended):** Install [Miniconda](https://www.anaconda.com/docs/getting-started/miniconda/install) and create an environment with the Python version you need:

```bash
conda create -n myproject python=3.11
conda activate myproject
```

**Alternative:** Official installers are available from [python.org](https://www.python.org/downloads/), though these are less convenient for managing multiple versions and environments.

**Check it works** (with your environment activated):

```bash
which python      # should point inside your conda environment, not /usr/bin
python --version
```

#### Suggested IDEs

**PyCharm** is a full-featured Python IDE from JetBrains, with strong code navigation, refactoring, debugging and testing, and built-in support for conda environments and Jupyter notebooks. It is a good choice for larger Python projects and packages.

- **Installation:** Download [PyCharm](https://www.jetbrains.com/pycharm/download/) or install it via the [JetBrains Toolbox](#24-jetbrains-toolbox). JetBrains has recently reorganised its editions, so check the download page for which features are free and which require a subscription. Students and academic staff can often get free licences (see [JetBrains for education](https://www.jetbrains.com/community/education/)).
- Point PyCharm at your conda environment (`Settings > Project > Python Interpreter > Add Interpreter > Conda Environment`) rather than the system Python.

### 2.3 Julia

**What it is:** A high-level, high-performance language designed for numerical and scientific computing. It aims to combine the ease of writing of Python or R with speed approaching C, and is well suited to simulation, optimisation and differential equations.

**Installation:** The recommended route is [Juliaup](https://github.com/JuliaLang/juliaup), the official Julia version manager, which makes it easy to install and switch between Julia versions. Full instructions are on the [Julia downloads page](https://julialang.org/downloads/).

```bash
# macOS / Linux
curl -fsSL https://install.julialang.org | sh
```

**Packages:** Julia has a built-in package manager, Pkg. From the Julia REPL, press `]` to enter package mode:

```julia
] add DataFrames        # install a package
] update                # update installed packages
] status                # list installed packages
```

**Tip:** Use a separate project environment for each project (`] activate .`), analogous to conda environments. The resulting `Project.toml` and `Manifest.toml` files record your dependencies and should be committed to version control.

#### Suggested IDE: VS Code

**Installation:** Download from [code.visualstudio.com](https://code.visualstudio.com/). Do not confuse it with Visual Studio, which is a different product.

Install Julia first, then the official [Julia extension](https://marketplace.visualstudio.com/items?itemName=julialang.language-julia) in [VS Code](#23-visual-studio-code-vs-code-shared-editor). The extension will find Julia if `julia` is on your `PATH`.

### 2.4 Bash

**What it is:** A command-line shell and scripting language. You will use it to navigate the file system, run programs, chain tools together, and automate repetitive tasks and jobs on remote servers and clusters.

**Availability:**

- **Linux:** Bash is installed by default and is usually the default shell.
- **macOS:** Bash is installed, but the version is very old (3.2), and the default shell is now **zsh**. For everyday use zsh is similar enough that the commands in this wiki will work. If you need a newer Bash, install it with conda (`conda install -c conda-forge bash`) or Homebrew (`brew install bash`).

**Further information:** See the [GNU Bash manual](https://www.gnu.org/software/bash/manual/).

**Example:**

```bash
# Count the lines in every CSV file in the current directory
for f in *.csv; do
    echo "$f: $(wc -l < "$f") lines"
done
```

#### Suggested IDE: VS Code

Use [VS Code](#23-visual-studio-code-vs-code-shared-editor) with the **Bash IDE** and **ShellCheck** extensions. For quick edits on remote servers where no graphical interface is available, terminal editors such as `nano` (easiest to learn) or `vim` are useful.

### 2.7 Java

**What it is:** A general-purpose language that runs on the Java Virtual Machine (JVM). You are most likely to encounter it through Java-based bioinformatics tools, which you may need to run, modify or build.

**Installation:** You need a Java Development Kit (JDK). Options include [Eclipse Temurin](https://adoptium.net/) or, via conda, `conda install -c conda-forge openjdk`. IntelliJ IDEA can also download one for you on first use.

**Check it works:**

```bash
java -version
```

#### Suggested IDE: IntelliJ IDEA

JetBrains' flagship IDE for Java, Kotlin and other JVM languages. Download from [jetbrains.com/idea](https://www.jetbrains.com/idea/download/) or via the [JetBrains Toolbox](#24-jetbrains-toolbox). Many JetBrains IDEs share the same interface and keyboard shortcuts, so knowing PyCharm makes IntelliJ easier to learn, and vice versa.


## 3. Frequently Used CLI Software

Most of the command-line tools below can be installed with conda from the `bioconda` and `conda-forge` channels, which is the easiest way to keep versions consistent across the group (see section 1.1). We suggest installing them into a dedicated environment:

```bash
conda create -n phylo -c conda-forge -c bioconda iqtree mafft muscle mrbayes
conda activate phylo
```

### 3.1 IQ-Tree

**What it is:** A fast and widely used program for maximum-likelihood phylogenetic inference. It includes automatic model selection (ModelFinder), ultrafast bootstrap approximation, and tests for branch support and tree topology.

**Installation:**

- Download binaries from [iqtree.org](https://iqtree.org/) or the [GitHub releases page](https://github.com/iqtree/iqtree3/releases).
- Via conda: `conda install -c bioconda iqtree`
- Note that the name of the executable depends on the version (`iqtree2` or `iqtree3`). Check with the command below.

**Typical usage:**

```bash
iqtree3 --version
# Model selection + ML tree + 1000 ultrafast bootstraps, using all available cores
iqtree3 -s alignment.fasta -m MFP -B 1000 -T AUTO
```

**Tip:** The main output is the `.treefile` (Newick format), and the `.iqtree` file contains a human-readable report including the selected model.

### 3.2 MAFFT

**What it is:** A multiple sequence alignment program for nucleotide and protein sequences, notable for its speed and range of strategies, from fast approximate methods to more accurate iterative refinement.

**Installation:**

- Download from the [MAFFT website](https://mafft.cbrc.jp/alignment/software/).
- Via conda: `conda install -c bioconda mafft`
- Via Homebrew: `brew install mafft`
- Via APT: `sudo apt install mafft`

**Typical usage:**

```bash
# Let MAFFT choose an appropriate strategy
mafft --auto sequences.fasta > aligned.fasta

# Use all available cores
mafft --auto --thread -1 sequences.fasta > aligned.fasta
```

**Tip:** Always inspect alignments by eye (e.g. in AliView, section 4.1) before using them for tree inference.

### 3.3 Muscle

**What it is:** Another widely used multiple sequence alignment program, known for accuracy and for its ability to scale to large datasets in version 5 (which can also produce ensembles of alignments to assess alignment uncertainty).

**Installation:**

- Download from the [MUSCLE GitHub repository](https://github.com/rcedgar/muscle) (see also the [documentation](https://drive5.com/muscle5/)).
- Via conda: `conda install -c bioconda muscle`

**Typical usage:**

```bash
muscle -align sequences.fasta -output aligned.fasta
```

**Tip:** The command-line syntax changed substantially between version 3 and version 5 (version 3 used `-in` and `-out`). Check which version you have with `muscle -version`, and note the version in your methods.

### 3.4 NextStrain

**What it is:** An open-source toolkit for tracking and visualising pathogen evolution. It consists of the Nextstrain CLI (which manages the software and workflows), **Augur** (a bioinformatics toolkit for building phylogenetic analyses) and **Auspice** (an interactive visualisation of the results). Analyses are usually organised as reproducible Snakemake workflows.

**Installation:** Follow the [official installation guide](https://docs.nextstrain.org/en/latest/install.html). Several "runtimes" are supported (Docker, conda, Singularity, or native installation). Docker or conda are the simplest for most users.

```bash
# Check that your setup works
nextstrain check-setup
```

**Further information:** See the [Nextstrain documentation](https://docs.nextstrain.org/) and the public instance at [nextstrain.org](https://nextstrain.org/), where you can also view and share datasets.

### 3.5 MrBayes

**What it is:** A program for Bayesian phylogenetic inference using Markov chain Monte Carlo (MCMC), supporting a wide range of nucleotide, amino acid and morphological models.

**Installation:**

- Download from the [MrBayes website](https://nbisweden.github.io/MrBayes/) or [GitHub](https://github.com/NBISweden/MrBayes).
- Via conda: `conda install -c bioconda mrbayes`
- Via Homebrew: `brew install mrbayes`
- Via APT: `sudo apt install mrbayes`

**Typical usage:** Analyses are specified in a NEXUS file (data plus a `mrbayes` block of commands).

```bash
mb analysis.nex
```

**Tips:**

- Always check convergence (e.g. average standard deviation of split frequencies, effective sample sizes in [Tracer](https://github.com/beast-dev/tracer/releases)) before interpreting results.
- MrBayes can use MPI and the BEAGLE library to speed up large analyses.

### 3.6 BEAST-X

**What it is:** The latest generation of the BEAST (Bayesian Evolutionary Analysis Sampling Trees) software, a successor to BEAST v1.x. It performs Bayesian phylogenetic, phylogeographic and molecular clock analyses, with a focus on time-calibrated trees, and has substantial new methods for large datasets.

**Installation:**

- Download from [beast.community](https://beast.community/) or the [GitHub repository](https://github.com/beast-dev/beast-mcmc).
- Requires Java (the download normally includes what you need, but see the website for details).
- The [BEAGLE library](https://github.com/beagle-dev/beagle-lib) is strongly recommended to accelerate likelihood calculations.

**Included programs:** BEAST (the analysis engine), BEAUti (a graphical tool for setting up analyses), LogCombiner, and TreeAnnotator. Use [Tracer](https://github.com/beast-dev/tracer/releases) to inspect logs and check convergence.

**Typical usage:**

```bash
beast analysis.xml
```

> **More detail:** BEAST is covered in more depth on a separate page: [BEAST in fLuLab](LINK-TO-BEAST-PAGE). *(Replace with the link to your BEAST page.)*

### 3.7 BEAST2

**What it is:** An independently developed, separately maintained branch of BEAST, with a modular design that lets users add new models and methods through a package system. It is particularly popular for species-tree inference (\*BEAST/StarBEAST), epidemiological models (e.g. birth-death skyline) and a large number of community-developed extensions.

**Installation:**

- Download from [beast2.org](https://www.beast2.org/). Installers for macOS, Windows and Linux include a bundled Java runtime.
- Via conda: `conda install -c bioconda beast2`

**Included programs:** BEAST 2, BEAUti, TreeAnnotator, LogCombiner and the **Package Manager** (for installing add-on packages). Use [Tracer](https://github.com/beast-dev/tracer/releases) to check convergence.

**Typical usage:**

```bash
beast analysis.xml

# List and install add-on packages from the command line
packagemanager -list
packagemanager -add BEASTLabs
```

**Tip:** BEAST-X and BEAST2 use different XML formats and are **not interchangeable**. Take care to use the BEAUti belonging to the same program you will run, and record the version and packages used.

> **More detail:** BEAST is covered in more depth on a separate page: [BEAST in fLuLab](LINK-TO-BEAST-PAGE). *(Replace with the link to your BEAST page.)*

## 4. Frequently Used GUI Software

### 4.1 Aliview

**What it is:** A fast, lightweight viewer and editor for multiple sequence alignments. It handles large alignments well, and is useful for checking and manually correcting the output of MAFFT or MUSCLE, trimming ends, and translating sequences.

**Installation:** Download from the [AliView website](https://ormbunkar.se/aliview/). It is Java-based, so it runs on macOS, Windows and Linux.

**Tips:**

- Alignments can be opened in FASTA, NEXUS, PHYLIP and other common formats.
- Always eyeball alignments for misaligned regions, frameshifts and sequencing errors before building trees.

### 4.2 Obsidian

**What it is:** A note-taking application that stores your notes as plain Markdown files in a local folder. Notes can be linked together, which makes it useful for lab notebooks, project logs, meeting notes and building up a personal knowledge base.

**Installation:** Download from [obsidian.md](https://obsidian.md/). Please check the website for the current licence terms.

**Tips:**

- Because notes are plain text files, they can be backed up or version-controlled (e.g. with git) like any other files.
- Plugins can integrate Obsidian with Zotero (section 4.3), so you can cite papers directly in your notes.

### 4.3 Zotero

**What it is:** A free, open-source reference manager. It collects papers (with metadata and PDFs) from your browser, organises them into collections, and generates citations and bibliographies in Word, LibreOffice and Google Docs.

**Installation:**

- Download from [zotero.org/download](https://www.zotero.org/download/). Install both the desktop app and the **Zotero Connector** browser extension, which saves papers with one click.
- Create a free account to sync your library between computers.

**Tips:**

- The [Better BibTeX](https://retorque.re/zotero-better-bibtex/) plugin is very helpful if you write in LaTeX or Markdown, as it creates stable citation keys and keeps a `.bib` file up to date.
- Group libraries let the whole group share a common set of references.