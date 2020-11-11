# GA blog post

## Concepts we focused on

- Reproducibility
- Scalability
- Portability
- Speed
- Standardisation
- Best practice

## Pipelines

- human_genomics_pipeline: https://github.com/ESR-NZ/human_genomics_pipeline
- vcf_annotation_pipeline: https://github.com/ESR-NZ/vcf_annotation_pipeline

We have developed two pipelines that are designed to complement one another. The first pipeline (human_genomic_pipeline) processes paired-end sequencing data using bwa and GATK4, taking the data from fastq to vcf. Quality control checks are also undertaken. The second pipeline filters the raw variants and annotates the vcf files using GATK4, SnpSift, VEP, genmod and dbSNP. Lastly, the vcf file can be optionally prepared for ingestion into scout, a user friendly, open source software that allows clinicians to explore the variants (http://www.clinicalgenomics.se/scout/).

### Features

- Open source - freely available in github
- Written in a workflow language (Snakemake)
- Deployable to a HPC or a single server
- Analyse exome or genome data
- Single sample or cohort/family analysis
- Run on CPU's or GPU's (parabricks)
- Species agnostic
- Regularly maintained
- Enthusiasm to support community contribution!

### How the pipelines are scalable
- Snakemake is flexible when handling variable numbers of samples and resource availabilities - Snakemake is a bit like Tetris, it's smart enough to know if and when more samples can be processed when they fit within the overall resource limits set by the user

### How the pipelines are reproducible
- Documentation to provide clear instruction on how to deploy the pipelines
- Open source - pipelines are available to reviewers in the peer review process
- Previous versions of the pipelines available because of version tracking in github
- User configuration of the pipeline settings are physically separated from the core pipeline, reducing the chance of unintentional changes to the core pipeline
- Log files written for nearly all steps in the pipeline
- The final report includes an interactive plot outlining the complete pipeline workflow and each file that was input and output by each rule/step

### How the pipelines are portable
- Minimal software requirements in order to run the pipelines - only [conda](https://docs.conda.io/en/latest/) which is commonly available on research servers and HPC's (and a parabricks licence and GPU/s if running GPU enabled)
- There are discussions underway about obtaining a Parabricks licence for NeSi - in this case, GPU accelerated pipeline runs could be available to researchers and students New Zealand wide that have access to NeSi
- Open source and available on github - can be easily cloned to any machine with a single git command
- Available resources (such as the maximum number of cores) can be set by the user, allowing the pipelines to be deployed on machines or HPC's with variable resource availabilities

### How the pipelines are speedy
- The pipelines are integrated with NVIDIA Clara Parabricks (https://www.nvidia.com/en-us/docs/parabricks/quickstart-guide/software-overview/). This means that the user can achieve *very significant* speedups when analysing a few samples by setting a single flag in the configuration file (if the user has a parabricks licence and GPU/s)
- The pipelines are scalable - many samples can be processed at one time

### How the pipelines encourage standardisation
- Open source - allows other labs in New Zealand to freely use the pipelines
- Designed to be species agnostic - we have developed these pipelines with human genomic data in mind. However, the pipelines have been designed to allow the user to analyse genomic data from other species by simply including their species specific reference genome and variant databases in the pipeline configuration file
- Available on github - the genomics/bioinformatics community is able and encouraged to contribute to the pipelines to further develop the pipelines to fit the needs of other labs in New Zealand
- GPU enabled runs using the NVIDIA Clara Parabricks is designed to match a CPU run by using the same software and parameters

### How the pipelines are best practice

- Designed to follow the current GATK best practice workflows for germline short variant discovery (https://gatk.broadinstitute.org/hc/en-us/articles/360035535932-Germline-short-variant-discovery-SNPs-Indels-)