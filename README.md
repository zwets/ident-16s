# ident-16s

Rapid identification of bacterial species from FASTA contigs.

Home: https://github.com/zwets/ident-16s


## Introduction

`ident-16s` is a simple script that, in the spirit of the
[Small Tools Manifesto for Bioinformatics](https://github.com/pjotrp/bioinformatics),
leverages several other open source tools to perform rapid 16S rRNA
microbial identification.

`ident-16s` uses 
* [barrnap](https://github.com/tseemann/barrnap) to predict the locations
  of 16S rRNA genes in a set of FASTA sequences, then uses
* [unfasta](https://io.zwets.it/unfasta) to extract the gene sequence(s), and
* [BLAST](https://en.wikipedia.org/wiki/BLAST) to match these against reference sequences in the
  [Bacterial 16S rRNA database](https://www.ncbi.nlm.nih.gov/genomes/static/refseqtarget.html).
* The usual GNU tools (`grep`, `sed`, `awk`, ...) are the duct tape holding
  it all together.


## Usage

The script is self-contained.  Run it with the `--help` option to see usage
instructions:

    ./ident-16s --help


## Installing

As `ident-16s` is a plain `sh` script, it requires no installation.  However,
you will need to install its dependencies.  There are two ways to do this.

### Simple installation

1. Obtain `ident-16s` from GitHub:

        git clone 'https://github.com/zwets/ident-16s.git'

   The `ident-16s` script is now installed in directory `./ident-16s`:

        cd ./ident-16s
        ./ident-16s --help

1. Add `barrnap` to the directory:

        git clone 'https://github.com/tseemann/barrnap.git'

   Note: on Ubuntu you can conveniently do `sudo apt install barrnap`.

1. Add `unfasta` to the directory:

        git clone 'https://github.com/zwets/unfasta.git'

1. Add the `16S_ribosomal_RNA` database to the directory:

        wget -O - 'ftp://ftp.ncbi.nlm.nih.gov/blast/db/16S_ribosomal_RNA.tar.gz' | tar xz

1. Check that you have `blastn`:

        blastn -h

   If this gives a 'command not found' error, install it using your
   favourite package manager.  On Ubuntu: `sudo apt install ncbi-blast+`.

1. Run test

        ./ident-16s test/ecoli.fna.gz

   This will either succeed and you're done, or it may report missing
   dependencies that should be easily installable using your machine's
   package manager.

### Complex installation

The more experienced POSIX user may prefer to install the dependencies the
'proper' way.  That's fine.  You can install them anywhere you prefer, as
long as you make sure that `barrnap`, the `unfasta` scripts, and `blastn`
are on the `PATH`, and that the `16S_ribosomal_RNA` database is visible to
`blastn`.  The latter can be done by setting the `BLASTDB` or `NCBI` env
variables appropriately, and in the (weirdly hidden) `/etc/.ncbirc`.


---

#### License

ident-16s - Rapid identification of bacterial species from FASTA  
Copyright (C) 2017, 2021  Marco van Zwetselaar <io@zwets.it>

This program is free software: you can redistribute it and/or modify
it under the terms of the GNU General Public License as published by
the Free Software Foundation, either version 3 of the License, or
(at your option) any later version.

This program is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
GNU General Public License for more details.

You should have received a copy of the GNU General Public License
along with this program.  If not, see <http://www.gnu.org/licenses/>.

