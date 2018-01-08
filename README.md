# Nimerlab ATACseq pipeline

This pipeline is a wrapper around the Kundaje lab atac_pipeline for use with Pegasus at SCCC at the University of Miami.
https://github.com/kundajelab/atac_dnase_pipelines

## Instructions for installation and use:

### This pipeline is compatable with UM Pegasus using project nimerlab

1. If conda is not installed: 
	- wget https://repo.continuum.io/miniconda/Miniconda3-latest-Linux-x86_64.sh 
	- bash Miniconda3-latest-Linux-x86_64.sh
2. After installation type the following commands:
	- module rm python
	- conda env create -f /projects/ctsi/nimerlab/DANIEL/tools/nimerlab-pipelines/ATACseq/environment.yml
	- echo 'export PATH=/projects/ctsi/nimerlab/DANIEL/tools/.bds:$PATH' >>~/.bash_profile
3. Copy 'ATACseq-experimental-file.yml' into your run folder.
4. One yaml file per experiment (or or two biological replicates with input). Rename your experiment file as needed and edit the file to fit your experiment using any text editor. 
6. Copy 'ATACseq.sh' into your run folder.
7. From your run folder, submit this command for each experiment, changing *** as needed::
	- bsub -q bigmem -n 1 -R 'rusage[mem=60000]' -W 120:00 -o ATACseq***.out -e ATACseq***.err <<< 'module rm python;source activate chipseq-pipeline:./ATACseq.sh ***.yml' 
8. In case of error, use the above command to pick up from last completed step.

