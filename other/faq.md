# FAQ

## How to check whether you are in the mapping environment?

```text
# when I login to server, my default python is in miniconda3/bin, 
# the base environment
$ which python
~/work/miniconda3/bin/python
(base)

# entering the mapping environment
$ conda activate mapping

# now I check the path of python again, it changed to my env dir
$ which python
~/work/miniconda3/envs/mapping/bin/python
(mapping)

# packages installed for mapping env all located at 
# ~/work/miniconda3/envs/mapping
```

## Why using a conda environment?

* Using environment make sure all the mapping related package is handled by conda and pip in a stand-alone place. 
* It will not impact any of your other installed packages and vise versa.
* The only drawback of using the environment is you need to activate the environment every time. Because everything is only installed for that environment.

## What is the PlateInfo file?

* A plain text file with experimental, library, and barcoding information.
* **This file needs to be made manually for each library.**
* The main content of this file is the **PCR index information for each plate in the library**, so the pipeline can properly **demultiplex and name the raw FASTQ files** with that information.

## What is the MappingConfig file?

* It contains all the parameters of the mapping pipeline in [INI format](https://en.wikipedia.org/wiki/INI_file)
* Briefing on INI format:

  ```text
  ; comment start with semicolon
  [section1]
  key1=value1
  key2=value2

  [section2]
  key1=value1
  key2=value2
  ```

* Currently, the pipeline doesn’t allow you to change the sections and keys, so just change values according to your needs.

## What is Snakemake?

[Snakemake](https://snakemake.github.io/) is a package for writing a reproducible pipeline. It uses `Snakefile` to describe all steps of a pipeline. During demultiplex, I prepared this file for you and saved it in each of the subdirectories. All you need to do is execute these files \(via snakemake, commands also summarized during demultiplexing\).

## What is netCDF4?

