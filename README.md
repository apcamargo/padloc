<a href="https://github.com/leightonpayne/padloc/LICENSE" alt="License"><img src="https://img.shields.io/github/license/leightonpayne/padloc" /></a> <a href="https://github.com/leightonpayne/padloc/" alt="Last update"><img src="https://img.shields.io/github/last-commit/leightonpayne/padloc?label=last%20update" /></a> <a href="https://github.com/leightonpayne/padlocDB/releases" alt="Release"><img src="https://img.shields.io/github/v/release/leightonpayne/padlocDB" /></a> 

# PADLOC: Prokaryotic Antiviral Defence LOCator

## About

PADLOC is a software tool for indentifying antiviral defence systems in prokaryotic genomes.

## Citation

tbd

## Installation

PADLOC can be installed by cloning or downloading this github repository.

1. Clone repo:

```bash
git clone https://github.com/leightonpayne/padloc $HOME/padloc
```

2. Run setup script:

```bash
$HOME/padloc/script/setup.sh
```

## Test

- Type `padloc` to output help information
- Type `padloc --version` to output version information

## Usage

### Input

padloc requires a genome in the form of an amino acid fasta file `*.faa`, the accompanying feature table file `*_feature_table.txt` of the particular genome, and a directory to store the output.

### Output

The output of a typical padloc run contains the following:

```
output
├── domtblout
│   └── *.domtblout         <- Domain table files generated by HMMER.
├── *_pdlcout.csv           <- padloc output file.
├── *_around.csv            <- information for genes around the identified defence systems.
├── *_within.csv            <- information for genes within the identified defence systems.
└── *.gff                   <- GFF annotation file for identified defence systems.
```

If the same output directory is used when processing multiple genomes, `*.domtblout` files will accumulate in the `domtblout/` directory. If the `*.domtblout` file already exists for a particular genome, `hmmsearch` will not be run again for that genome unless `--append` is specified. In which case, the output of `hmmsearch` will be appended to the existing `*.domtblout` file. When processing multiple genomes in batches, this allows for the pipeline to be resumed if it is interrupted.

### Examples

```
# 
padloc --fasta genome.faa

# Use multiple cpus and save output to mydir 
padloc --fasta --mydir --cpu 4

# 
padloc --fasta --mydir --cpu --append 

#
padloc
```



### Command line options

```
Usage: 
    padloc [options] --fasta <f> --featbl <f> --out <d>

Required:
    --fasta <f>     
        Path to the input fasta file (*.faa) 
    --featbl <f>    
        Path to the input feature table file (*_feature_table.txt) 
    --out <d>       
        Path to the output directory <d>

Optional:
    --cpu <n>       
        Set number of cpus to <n>, the default is 1
    --raw-out       
        Include a summarised raw output file for each genome searched
    --append        
        Append the hmmer output to exisitng results in out_dir/domtblout/
    --cleanup
        Remove domtblout/ from the output directory if left over from 
        previous runs
    -h, --help      
        Display this help message
```



## PADLOC-DB

The database used by PADLOC is 

## Issues

Bugs and feature requests can be submitted to the [Issues tab](https://github.com/leightonpayne/padloc/issues).

## Dependencies

Dependencies are installed automatically when running `scripts/setup.sh`.

- **R**  
  *R Core Team (2018). R: A language and environment for statistical computing. R Foundation for Statistical Computing, Vienna, Austria. https://www.R-project.org/.*

- **tidyverse**  

- **yaml**  
  *Stephens, J., et al. (2018). yaml: Methods to Convert R Data to YAML and Back. https://CRAN.R-project.org/package=yaml*
- **getopt**  
  *Davis, T., et al. (2019). getopt: C-Like 'getopt' Behavior. https://CRAN.R-project.org/package=getopt*

### Tools

- **HMMER3**  
  *Finn, R.D., Clements, J., and Eddy, S.R. (2011). HMMER web server: interactive sequence similarity searching. Nucleic Acids Res 39, W29–W37.*