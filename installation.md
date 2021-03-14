# Installation

## Setup Conda and Mapping Environment

### Install conda from miniconda or anaconda.

* IMPORTANT: select python 3
* [miniconda \(recommended\)](https://conda.io/miniconda.html)
* [anaconda \(larger\)](https://www.anaconda.com/download/)

### Conda init

After installed conda, use `conda init` on your favorite shell

```text
# e.g., bash or zsh
conda init bash

# you need to restart shell after conda init
```

### Add channels

```text
# run these command to add bioconda into your conda channel, 
# the order of these 3 line matters
conda config --add channels defaults
conda config --add channels bioconda
conda config --add channels conda-forge
```

### Create Environment With Required Packages

This command will create a conda environment called "mapping" and install all required packages for you. The `mapping_env.yaml` contains the detail about the environment, you can copy the content of that file below.

```text
# conda is a bit slow, this step will take ~30 min in my server, 
# but you only need to do this once.
conda env create -f mapping_env.yaml
```

### Content of mapping\_env.yaml file

```yaml
name: mapping
channels:
  - conda-forge
  - bioconda
  - defaults
dependencies:
  - python=3.7
  - pip
  - jupyter
  - jupyter_contrib_nbextensions
  - cutadapt=2.10
  - snakemake=5.17
  - bismark=0.20
  - samtools=1.9
  - picard
  - bedtools=2.29
  - star=2.7.3a
  - subread=2.0
  - bowtie2=2.3
  - bowtie=1.3
  - htslib=1.9
  - pysam=0.15
  - pytables
  - seaborn
  - matplotlib
  - pip:
    - papermill

```

{% hint style="info" %}
[Why using a conda environment?](other/faq.md#why-using-conda-environment)
{% endhint %}

### Activate the mapping environment

```text
# enter env
conda activate mapping

# exit env
conda deactivate
```

{% hint style="warning" %}
**Remember you need to run this command EVERY TIME before using the pipeline.**
{% endhint %}

{% hint style="info" %}
[How to check whether you are in the mapping environment?](other/faq.md#how-to-check-whether-you-are-in-the-mapping-environment)
{% endhint %}

## Install YAP and Allcools

### Install YAP

```text
# enter mapping env first

pip install cemba-data
```

### Update YAP

```text
# enter mapping env first
pip install --upgrade cemba-data
```

### Install Allcools

```text
# enter mapping env first
pip install allcools
```

### Update ALLCools

```text
# enter mapping env first
pip install --upgrade allcools
```

