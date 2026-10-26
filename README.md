# Ipomoea_lacunosa_Reference_Genome
Ipomoea lacunosa: Reference Genome  Assembly of the I. lacunosa reference genome from PACBio HiFi long reads and scaffolding completed using HiC data.

(The README is ment as a summarized vision on the contents of this folder; see the other directories for further explanation)

## Ipomoea lacunosa: Reference Genome

## <u>Data Preparation</u>

## 1 -Moving the HiC and HiFi data

The data was located in Jim’s lab project directory. I moved it to my jlmlab scratch directory. 

## 2 -Convert Hifi bam file to fastq

Converted the hifi bam file to fastq format using **SAMtools fastq.**

## 3 -Convert HiC data from .bz2 to .gz

Used **bzcat** to convert HiC data from .bz2 to .gz. 

## <u>Assembly</u>

## 4 -Assembly with Hifiasm

**Hifiasm** is a program for fast haplotype-resolved de novo assembly initially designed for PacBio HiFi reads producing high-quality telomere-to-telomere assemblies. 

With the addition of Hi-C reads from the parents, hifiasm produces overall the best haplotype-resolved assembly depending on the homozygosity rate. (*I. purpurea* did not resolve into haplotypes). Sequencing produces short contigs (long reads in this case) and HiC data helps determine which peaces or contigs are closer together in the nucleus, helping to determine chromosomal structure and haplotype phasing more accurately.

The *I. lacunosa* genome assembly phased into the two haplotypes!

## <u>Scaffolding</u>

## 5 -Mapping Omni-C Reads

BWA includes three algorithms: **-backtrack, SW and MEM**. Here we use **MEM** because it is intended for long reads and faster. On its own **BWA** is a software package intended to map reads agains a reference genome. 

## 6 -HiC Scaffolding with Yahs (pre)

**Yahs** uses an algorithm that joins contigs by considering topological distribution of Hi-C signals in order to distinguish real interaction signals from mapping nosies. Yahs requires an indexed FASTA file of the contig sequences and a BAM/BED/BIN/PA5 file with the alignment results of Hi-C reads. 

**seqkit seq** is used to filter the scaffold file to remove contigs less than 500kb. This removes really short sequences that are difficult to place in the genome (used later). 

Using the non-filtered fasta file, **Juicer** processes the HiC data to produce the .hic file for **Juicebox** (visualization GUI). **JBAT** can help make assembly corrections.
