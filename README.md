# HRTV and BRBV Genomic Analysis Pipeline

## Overview

This repository contains bioinformatics workflows and supporting files for genomic analysis of **Heartland virus (HRTV)** and **Bourbon virus (BRBV)** from Oxford Nanopore sequencing data.

The repository includes:

- ARTIC primer schemes for HRTV and BRBV
- Segment-specific reference sequences and primer coordinates
- Oxford Nanopore consensus genome generation using the ARTIC pipeline
- Segment-specific Nextstrain builds for phylogenetic and genomic epidemiology analyses
- Example consensus sequences generated from Nebraska HRTV and BRBV samples

Both viruses have segmented negative-sense RNA genomes and are therefore analyzed independently by genomic segment.

---

## Viruses

### Heartland virus (HRTV)

Heartland virus is a tick-borne phlebovirus in the family **Phenuiviridae**. Its genome consists of three RNA segments:

- **L** — Large segment
- **M** — Medium segment
- **S** — Small segment

Separate ARTIC primer schemes and Nextstrain builds are maintained for each segment.

### Bourbon virus (BRBV)

Bourbon virus is a tick-borne virus in the family **Orthomyxoviridae**. Its genome consists of six RNA segments.

Separate ARTIC primer schemes and Nextstrain builds are maintained for:

- Segment 1
- Segment 2
- Segment 3
- Segment 4
- Segment 5
- Segment 6

---

## Repository Structure

```text
HRTV-ARTIC-Analysis/
│
├── README.md
├── script.sh
│
├── schemes/
│   │
│   ├── HRTV/
│   │   │
│   │   ├── HRTV_L/
│   │   │   ├── HRTV_L.reference.fasta
│   │   │   ├── HRTV_L.reference.fasta.fai
│   │   │   └── HRTV_L.scheme.bed
│   │   │
│   │   ├── HRTV_M/
│   │   │   ├── HRTV_M.reference.fasta
│   │   │   ├── HRTV_M.reference.fasta.fai
│   │   │   └── HRTV_M.scheme.bed
│   │   │
│   │   └── HRTV_S/
│   │       ├── HRTV_S.reference.fasta
│   │       ├── HRTV_S.reference.fasta.fai
│   │       └── HRTV_S.scheme.bed
│   │
│   └── BRBV/
│       │
│       ├── BRBV_segment_1/
│       │   ├── BRBV_1.reference.fasta
│       │   ├── BRBV_1.reference.fasta.fai
│       │   └── BRBV_1.scheme.bed
│       │
│       ├── BRBV_segment_2/
│       │   ├── BRBV_2.reference.fasta
│       │   ├── BRBV_2.reference.fasta.fai
│       │   └── BRBV_2.scheme.bed
│       │
│       ├── BRBV_segment_3/
│       │   ├── BRBV_3.reference.fasta
│       │   ├── BRBV_3.reference.fasta.fai
│       │   └── BRBV_3.scheme.bed
│       │
│       ├── BRBV_segment_4/
│       │   ├── BRBV_4.reference.fasta
│       │   ├── BRBV_4.reference.fasta.fai
│       │   └── BRBV_4.scheme.bed
│       │
│       ├── BRBV_segment_5/
│       │   ├── BRBV_5.reference.fasta
│       │   ├── BRBV_5.reference.fasta.fai
│       │   └── BRBV_5.scheme.bed
│       │
│       └── BRBV_segment_6/
│           ├── BRBV_6.reference.fasta
│           ├── BRBV_6.reference.fasta.fai
│           └── BRBV_6.scheme.bed
│
├── nextstrain_builds/
│   │
│   ├── HRTV/
│   │   │
│   │   ├── HRTV_L/
│   │   │   ├── Snakefile
│   │   │   ├── data/
│   │   │   │   ├── metadata.tsv
│   │   │   │   └── sequences.fasta
│   │   │   └── config/
│   │   │       ├── reference.fasta
│   │   │       ├── heartland_segments.gb
│   │   │       ├── colors.tsv
│   │   │       ├── lat_longs.tsv
│   │   │       ├── auspice_config.json
│   │   │       └── exclude_clean_retry.txt
│   │   │
│   │   ├── HRTV_M/
│   │   │   ├── Snakefile
│   │   │   ├── data/
│   │   │   │   ├── metadata.tsv
│   │   │   │   └── sequence.fasta
│   │   │   └── config/
│   │   │       ├── reference.fasta
│   │   │       ├── heartland_M_segment.gb
│   │   │       ├── colors.tsv
│   │   │       ├── lat_longs.tsv
│   │   │       ├── auspice_config.json
│   │   │       └── exclude_clean_retry.txt
│   │   │
│   │   └── HRTV_S/
│   │       ├── Snakefile
│   │       ├── data/
│   │       │   ├── metadata_filtered.tsv
│   │       │   └── sequence_filtered.fasta
│   │       └── config/
│   │           ├── reference.fasta
│   │           ├── heartland_S_segment.gb
│   │           ├── colors.tsv
│   │           ├── lat_longs.tsv
│   │           ├── auspice_config.json
│   │           └── exclude_clean_retry.txt
│   │
│   └── BRBV/
│       │
│       ├── segment_1/
│       ├── segment_2/
│       ├── segment_3/
│       ├── segment_4/
│       ├── segment_5/
│       └── segment_6/
│
└── consensus_sequences/
    ├── HRTV/
    │   ├── *_Lseg.consensus.fasta
    │   ├── *_Mseg.consensus.fasta
    │   └── *_Sseg.consensus.fasta
    │
    └── BRBV/
        └── *.consensus.fasta
```

---

## ARTIC Consensus Genome Pipeline

Oxford Nanopore reads are processed using the **ARTIC field bioinformatics pipeline** with segment-specific primer schemes.

Each ARTIC scheme contains:

- `*.reference.fasta` — reference sequence
- `*.reference.fasta.fai` — FASTA index
- `*.scheme.bed` — ARTIC primer coordinates

HRTV has independent schemes for the L, M, and S segments, while BRBV has independent schemes for all six genomic segments.

### Software Requirements

- ARTIC field bioinformatics
- Medaka
- Minimap2
- Samtools
- Conda or Mamba

Example installation:

```bash
conda install -c bioconda artic
conda install -c bioconda medaka minimap2 samtools
```

---

## ARTIC Parameters

The pipeline uses Oxford Nanopore consensus generation with parameters including:

```text
--normalise 400
--medaka
--medaka-model r1041_e82_400bps_sup_v4.2.0
```

The Medaka model corresponds to R10.4.1 Oxford Nanopore sequencing using SUP basecalling.

---

## Running the ARTIC Analysis

### 1. Prepare sequencing reads

Use demultiplexed and basecalled FASTQ files as input.

### 2. Select the appropriate primer scheme

For HRTV:

```text
schemes/HRTV/HRTV_L
schemes/HRTV/HRTV_M
schemes/HRTV/HRTV_S
```

For BRBV:

```text
schemes/BRBV/BRBV_segment_1
schemes/BRBV/BRBV_segment_2
schemes/BRBV/BRBV_segment_3
schemes/BRBV/BRBV_segment_4
schemes/BRBV/BRBV_segment_5
schemes/BRBV/BRBV_segment_6
```

### 3. Run the analysis

```bash
bash script.sh
```

Paths and sample identifiers should be configured in `script.sh` before execution.

---

## ARTIC Output

Typical ARTIC output includes:

- `*.consensus.fasta` — final consensus genome
- `*.primertrimmed.rg.sorted.bam` — primer-trimmed read alignments
- `*.vcf` — variant calls
- `*.variants.tab` — variant summary
- `*.coverage_mask.txt` — low-coverage masking information

Consensus sequences can subsequently be used in phylogenetic or Nextstrain analyses.

---

# Nextstrain Analyses

Segment-specific Nextstrain builds are included for both HRTV and BRBV.

Each genomic segment is analyzed independently to preserve the evolutionary history of the segmented viral genome.

The builds use the standard Nextstrain/Augur workflow:

```text
sequence data
      ↓
alignment
      ↓
phylogenetic tree
      ↓
time-resolved tree
      ↓
ancestral reconstruction
      ↓
geographic trait reconstruction
      ↓
Auspice JSON
```

---

## HRTV Nextstrain Builds

Three independent HRTV builds are provided:

```text
HRTV_L
HRTV_M
HRTV_S
```

Each contains:

```text
Snakefile
data/
config/
```

The `data/` directory contains the curated viral sequences and associated metadata.

The `config/` directory contains:

- Reference genome
- GenBank annotation
- Geographic color configuration
- Latitude/longitude information
- Auspice configuration
- Sequence exclusion list

The `Snakefile` defines the reproducible Augur workflow used to construct the phylogenetic analysis.

---

## BRBV Nextstrain Builds

Six independent Bourbon virus builds are provided:

```text
segment_1
segment_2
segment_3
segment_4
segment_5
segment_6
```

Each build contains:

```text
Snakefile
data/
    metadata.tsv
    sequence.fasta
config/
    reference.fasta
    bourbon_segment_X.gb
    colors.tsv
    lat_longs.tsv
    auspice_config.json
    exclude_clean_retry.txt
    reference_accession.txt
```

The six segment-specific analyses allow evolutionary relationships to be evaluated independently across the BRBV genome.

---

## Author

**Zach Pella**

Nebraska Public Health Laboratory / University of Nebraska Medical Center
