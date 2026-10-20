# Extraction of Transcription Factor Binding Site Sequences in *Escherichia coli*

**Author:** Andrea Villarruel García  
**Context:** Final project for an undergraduate Python course (2025)

## Overview

Transcription factors (TFs) regulate gene expression by recognizing and binding specific DNA regions. Identifying and analyzing these regions is important for understanding gene regulatory networks.

In this project, I developed a Python-based workflow to extract genomic sequences corresponding to previously identified transcription factor binding peaks in *Escherichia coli* K-12 MG1655.

The program combines genomic coordinates from a ChIP-seq peak dataset with a reference genome to generate individual FASTA files containing the sequences associated with each transcription factor.

The resulting files can be used in downstream analyses, such as DNA-binding motif discovery.

## Project objective

The main objective was to automate the extraction and organization of transcription factor binding site sequences from genomic data.

More specifically, the program was designed to:

1. Read an *E. coli* reference genome in FASTA format.
2. Process a tab-separated file containing transcription factor binding peaks.
3. Extract DNA sequences using their genomic coordinates.
4. Group the extracted sequences by transcription factor.
5. Generate individual FASTA files for downstream analysis.

## Data

The project uses two main inputs:

- **Reference genome:** *Escherichia coli* K-12 MG1655 (GenBank accession U00096.3).
- **Binding peak dataset:** A tab-separated file containing previously identified ChIP-seq peak regions, their genomic coordinates, and associated transcription factor information.

The dataset includes fields such as `Dataset_Ids`, `TF_name`, `Peak_start`, `Peak_end`, and `Peak_number`.

The program processes previously identified binding regions. It does not perform ChIP-seq read alignment or peak calling.

## Implementation

The workflow was implemented in Python and organized into separate modules:

| Module | Function |
|---|---|
| `genome.py` | Reads the reference genome and processes the peak table using pandas |
| `peaks.py` | Extracts genomic sequences and groups them by transcription factor |
| `io_utils.py` | Writes sequences to individual FASTA files |
| `main.py` | Coordinates execution and accepts command-line arguments |

The implementation includes basic input-file checks and genomic-coordinate validation.

## Results

The program generates FASTA files organized by transcription factor, with multiple binding-region sequences stored in each corresponding file.

The repository currently contains **139 per-factor FASTA files** in its output directories.

For example, the file `aaeR.fasta` contains sequences associated with binding peaks assigned to the transcription factor AaeR.

**Example output:** [aaeR.fasta](results/Archivos_Fasta/aaeR.fasta)

Each FASTA record includes an identifier and its corresponding extracted DNA sequence.

The extraction process reduces the need to manually locate and retrieve individual genomic intervals, preparing the sequences for further regulatory analysis.

## How to run

The modular implementation is located in `bin/extractor_secuencias/`.

**Dependency:** Python 3 and pandas.

Install pandas using `pip install pandas`.

From the repository root, the program can be executed with the following command:

`python bin/extractor_secuencias/main.py -f data/E_coli_K12_MG1655_U00096.3.txt -p data/union_peaks_file.tsv -o results/Archivos_Fasta/`

The arguments specify the reference genome (`-f`), peak dataset (`-p`), and output directory (`-o`).

## Scope and limitations

This project focuses on genomic sequence extraction and organization using previously identified transcription factor binding peaks.

The original project also considered motif discovery using MEME as a downstream step. However automated motif discovery is not implemented in the current repository.

The existing implementation was developed for a specific *E. coli* reference genome and input-file structure.

## Repository contents

- [bin/](bin/) — Python implementation
- [data/](data/) — Reference genome and peak data
- [results/](results/) — Generated FASTA sequences
- [doc/](doc/) — Project specifications, documentation, and proposed test cases

