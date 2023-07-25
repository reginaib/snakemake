The provided Snakemake workflow is designed to call SNPs on a subset of the 1000 Genomes dataset. The workflow takes advantage of Snakemake's rule-based approach to parallelize and manage the execution of various steps, making the analysis scalable and reproducible. The goal is to process whole exome sequencing data from 10 human individuals and generate relevant output files and tables.

Workflow Overview:

FastQC (Quality Control): The first step in the workflow performs FastQC analysis on the input fastq files to check their quality and generate quality control reports.

BWA Alignment: The workflow uses BWA (Burrows-Wheeler Aligner) to align the fastq files against the reference genome (hg19) and produces aligned BAM files.

Variant Calling (Samtools): The workflow utilizes Samtools to call variants from the aligned BAM files, producing a VCF file.

Variant Cleanup: The VCF file obtained from variant calling is further processed using vt tools to decompose, normalize, and filter the variants.

SNPEff Annotation: The cleaned VCF file is then annotated using SNPEff to identify the functional impact of variants.

Extra Assignment A (Flagstat): This extra assignment calculates the percentage of mapped reads for each input sample using Samtools flagstat.

Extra Assignment A (Table): The calculated percentage of mapped reads for each sample is aggregated into a table and plotted as a bar graph.

Usage and Rerun:

To run the Snakemake workflow, navigate to the working directory and execute the provided slurm batch script, "runsnakemake.slrm." The workflow is designed to be reproducible, and all the intermediate data (such as BAM files) are stored in the "data/work" folder on the VSC_SCRATCH, ensuring a clean and organized workspace for reruns.

Scalability and Multithreading:

The workflow is designed to take advantage of multi-core processing by using 8 cores during the execution of the BWA alignment step (rule bwa). This helps significantly reduce the runtime for the alignment process, making it scalable for larger datasets.



The workflow also includes solutions for the extra assignments:
The workflow calculates the percentage of mapped reads for each input sample using Samtools flagstat and generates a table and a bar graph displaying the results.
Report Generation:

The workflow is configured to automatically generate a report named "report.html" using Snakemake's built-in reporting capabilities (onsuccess rule). This report provides an overview of the workflow execution, showing the dependencies between rules and their status (success/failure). It is a useful tool for visualizing and sharing the workflow's results and progress.

Overall, the provided Snakemake workflow is well-structured, modular, and scalable, making it suitable for calling SNPs on a larger genomic dataset from the 1000 Genomes Project. It ensures easy reproducibility, error tracking, and efficient resource utilization, making it a robust solution for the given assignment.