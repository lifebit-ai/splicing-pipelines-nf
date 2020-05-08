# splicing-pipelines-nf
Anczukow-lab repository for the Nextflow splicing pipeline with `rMATS 4.0.2`.

## Introduction

The workflow processes raw data from FastQ inputs 
([FastQC](https://www.bioinformatics.babraham.ac.uk/projects/fastqc/),
    [Trimmomatic](http://www.usadellab.org/cms/?page=trimmomatic)), aligns the reads
        ([STAR](https://github.com/alexdobin/STAR)), performs transcript assembly and quantification
            ([StringTie](https://ccb.jhu.edu/software/stringtie/)), detects alternative splicing events
                ([rMATs](http://rnaseq-mats.sourceforge.net/)), and generates an interactive QC report
                    ([MultiQC](http://multiqc.info/)).

The pipeline is built using [Nextflow](https://www.nextflow.io), a workflow tool to run tasks across multiple compute infrastructures in a very portable manner. For example, it can be run on HPC (using [JAX](https://www.jax.org/)'s Sumner HPC) or on the cloud over ([Lifebit's CloudOS](https://lifebit.ai/cloudos) platform with AWS & GCloud). It comes with docker containers making installation trivial and results highly reproducible.

## Quick start on Sumner (JAX's HPC)

1) Check out the source code from `github`.

```bash
git clone https://github.com/TheJacksonLaboratory/splicing-pipelines-nf.git
cd splicing-pipelines-nf
```
2) Run test example to ensure the pipeline is working properly. 

EXAMPLE 1: human test data
To run: 
```bash
sbatch /projects/anczukow-lab/splicing_pipeline/splicing-pipelines-nf/examples/human_test/human_test_main.pbs
```

3) Then to execute on sumner, inspect the `main.pbs` script and edit or uncomment the specific `nextflow` run you would like to run.  To run the bash script using the `slurm` `sbatch` command:

```bash
sbatch main.pbs
```

4) Progress can be checked using:

```bash
squeue | grep [username]
```

or by tailing the output file:

```bash
tail splicing.[jobnumber].out
```

### To see the help message
```
nextflow run main.nf --help
```

## Documentation

Documentation about the pipeline, found in the [`docs/`](docs) directory:

1. [Intro to GitHub](docs/github.md)
2. [Pipeline overview](docs/pipeline_overview.md)
3. [Running the pipeline](docs/usage.md)
    * [Running on Sumner](docs/run_on_sumner.md)
    * [Running on CloudOS](docs/run_on_cloudos.md)

## Pipeline DAG
![splicing_pip_dag](https://raw.githubusercontent.com/lifebit-ai/images/master/jax_splicing/splicing_pip_dag.png)
