# Installation

## Setup Conda and Mapping Environment

### Install conda from miniconda or anaconda.

* IMPORTANT: select python 3
* [miniconda \(recommended\)](https://conda.io/miniconda.html)
* [anaconda \(larger\)](https://www.anaconda.com/download/)

### Add channels

```text
# run these command to add bioconda into your conda channel, 
# the order of these 3 line matters
conda config --add channels defaults
conda config --add channels bioconda
conda config --add channels conda-forge
```

### Create mapping environment and install required packages

This command will create a conda environment called "mapping" and install all required packages for you. The `mapping_env.yaml` file contains the detail about the environment, you can download that file below.

```text
# conda is a bit slow, this step will take ~30 min in my server, 
# but you only need to do this once.
conda env create -f mapping_env.yaml
```

{% file src=".gitbook/assets/mapping\_env.yaml" caption="mapping\_env.yaml" %}

{% hint style="info" %}
[Why using conda environment?](other/faq.md#why-using-conda-environment)
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

git clone https://github.com/lhqing/cemba_data.git
cd cemba_data
pip install .
```

### Install Allcools

```text
# enter mapping env first

git clone https://github.com/lhqing/ALLCools.git
cd ALLCools
pip install .
```

### Update YAP or Allcools

```text
# enter mapping env first

cd /path/to/yap/or/allcools/
git pull
pip install .
```

