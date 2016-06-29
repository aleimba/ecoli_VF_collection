[![DOI](https://zenodo.org/badge/doi/10.5281/zenodo.56686.svg)](http://dx.doi.org/10.5281/zenodo.56686)

ecoli_VF_collection
===================

This is a collection of **1069** protein sequences for ***Escherichia coli* virulence factors** (VFs).

* [Synopsis](#synopsis)
* [Description](#description)
    * [Why](#why)
    * [Strategy](#strategy)
    * [Format of the FASTA files](#format-of-the-fasta-files)
* [Usage](#usage)
    * [How to download](#how-to-download)
    * [Pipelines](#pipelines)
* [VF sources](#vf-sources)
    * [Databases](#databases)
    * [Publications](#publications)
* [Contributing](#contributing)
* [Similar resources](#similar-resources)
* [Citation](#citation)
* [License](#license)
* [Author - contact](#author---contact)
* [References](#references)
* [Changelog](#changelog)


## Synopsis
The **1069 VF protein sequences** are stored as respective VF class multi-FASTA **.faa* files in the subfolder [*/data*](/data) and the accompanying description of the VFs in the tab-delimited file [*/source/ecoli_VF_collection_description.tsv*](/source/ecoli_VF_collection_description.tsv).


## Description
### Why
Most of the publications scanning *E. coli* strains for VFs include a table or a supplemental file with a list of the VFs and the respective accession numbers or primer sequences. Few include the actual sequences for the VFs (mostly in unwieldy PDF format). In either case, getting the respective VF sequences for these publications is cumbersome and not replicable.

As a second resource, there are several comprehensive databases for VFs in existence (see [similar resources](#similar-resources)). But these databases can be difficult to handle and to download respective *E. coli* VFs. Also, these databases were not totally suitable for my purpose, because firstly they focus on intestinal pathogenic *E. coli* (IPEC) VFs and include only some extraintestinal pathogenic *E. coli* (ExPEC) VFs. Secondly, a consistent categorization of the VFs, especially in the FASTA IDs, is missing. E.g., a **major problem** of the virulence factor database ([VFDB](http://www.mgc.ac.cn/VFs/main.htm)) FASTA files is that they're not well annotated. Many FASTA entries only have the annotation "hypothetical protein", which is not very useful in determining the actual VF. Also, release 3 of the VFDB (see below [strategy](#strategy)) currently does not have a single download source or API and it's quite frustrating to click through the web interface manually for filtering and downloading.

This VF collection here should serve as a middle ground. An easy way to [download](#how-to-download) the VF sequences and an invitation to [contribute](#contributing) to the collection. To my knowledge, no other database allows such a crowd-sourced approach.

For now the VFs are only included as protein sequences, nucleotide sequences are a project for the future.


### Strategy
For gathering the *E. coli* VFs I first used the VFs from Petty *et al.*<sup id="a1">[1](#f1)</sup> as basis, a publication where the authors scanned a large ExPEC VF panel. Basically used the dataset from FigS6 of the publication which is listed in supplementary Excel spreadsheet one ([*Download Dataset_S01 (XLSX)*](http://www.pnas.org/content/suppl/2014/03/30/1322678111.DCSupplemental/sd01.xlsx)) in tab "Fig S6 seqfindr queries", except for the "UPEC specific genes".

Subsequently, looked through all three releases (R1<sup id="a2">[2](#f2)</sup>, R2<sup id="a3">[3](#f3)</sup>, and R3<sup id="a4">[4](#f4)</sup>; see [Q10](http://www.mgc.ac.cn/VFs/faq.htm#Q10) of the VFDB FAQ for a description; in VFDB's 2016 release now reorganized into non-redundant core setA and full dataset setB<sup id="a5">[5](#f5)</sup>) from the VFDB to include more suitable *E. coli* VFs (mostly IPEC VFs). R3 of the VFDB and its VF classification is the most comprehensive and thus was used as the first goto source to get VFs and the respective amino acid sequences. Then I filled up this collection with VFs from VFDB's R1 and R2 (descending quality of annotations and sequences in the VFDB releases).

As a final step I looked through primary literature on *E. coli* VFs or where *E. coli* strains were scanned for VFs (see below [publications](#publications)). The VFs in these publications were used to supplement the VF collection even more, especially with additional ExPEC VFs. The amino acid sequences of VFs, which are not present in VFDB, were collected manually from *E. coli* genomes or directly from [NCBI](https://www.ncbi.nlm.nih.gov/).

VF gene names<sup>§</sup>, descriptions (general description of the gene cluster/operon), accession numbers<sup>§</sup>, locus tags<sup>§</sup>, and respective *E. coli* reference strains<sup>§</sup> are listed in an overview tab-delimited file, [*/source/ecoli_VF_collection_description.tsv*](/source/ecoli_VF_collection_description.tsv) (<sup>§</sup> = if given). Additionally, this file includes the respective VF class (see below) and if the VF originates from a VFDB release or from a publication (keyword "manually"). The corresponding protein sequences are stored in respective VF class multi-FASTA files (**.faa*) in subfolder [*/data*](/data) and the FASTA IDs contain nearly all of the same information (see below [format of the FASTA files](#format-of-the-fasta-files)).

Each VF is categorized into one of the 12 VF classes, similar to VFDB R3. The FASTA files with the VF protein sequences are named correspondingly:

* Adhesion_invasion
* Autotransporter_T5SS
* CU_fimbriae
* Flagella
* Iron_uptake
* Other_virulence_gene
* Serum_resistance
* T2SS
* T3SS_TTSS
* T6SS
* Toxin
* Type_4_pilus

Not **all** VFs from the sources mentioned beforehand are included in the VF collection here. The amount of "putative" VFs, firstly, is quite overwhelming. Secondly, I wanted to focus on a more or less specific VF collection including the most important *E. coli* VFs. Hence, there's room for improvement (see below how to [contribute](#contributing)) and a collection like this really is not a one man job.

There are a couple of VF protein sequences, listed in the collection, which have a 100% identity (if interested use [`cd-hit`](http://weizhong-lab.ucsd.edu/cd-hit/) for clustering the VFs). Because all of them are included in different gene clusters/operons, these are still included for completeness. There's no general agreed upon ontology how to name *E. coli* VFs, very similar alleles of genes can be named differently, which adds to the confusion.


### Format of the FASTA files
For the FASTA ID/header line the following format is followed:
```bash
>locus_tag gene_name accession_number product_desc_text [Escherichia coli serotype strain replicon (PATHOTYPE)] (VF_class)
```

The SeqID in the FASTA header (the string following ">" until the next whitespace) is the corresponding locus tag, followed by the gene name, the accession number, and the product description. All are separated by a **single** space. **Whitespaces** in the product description ("/product") are **replaced** by underscores "**\_**". The reference strain is given in square brackets with optional extra information (e.g. "serotype" only if available and "replicon" only if VF encoded on a plasmid). "PATHOTYPE", given in **parentheses** (if available), is either APEC (avian pathogenic), DAEC (diffusely adherent), EAEC (enteroaggregative), EHEC (enterohemorrhagic), environmental (*E. coli* SMS-3-5), EPEC (enteropathogenic), ETEC (enterotoxigenic), ExPEC, MNEC (meningitis-associated), MPEC (mastitis-associated), NPEC (non-pathogenic), NTEC (necrotoxigenic), STEC (Shiga toxin-producing *E. coli*), UPEC (uropathogenic), or Shigella. Finally, each header line ends with the VF class in **parentheses**.

Locus tags are suitable as SeqID as the ID has to be **unique** over all sequences and locus tags are unique over all genomes. If a gene name or accession number is not present, a **"NA"** (not available) is included instead. There's one exception, VFs from VFDB's R3, either have a locus tag **or** a protein accession number as SeqID (the protein accession number is then duplicated in the ID line).


## Usage
### How to download
The dataset or the whole repository can be downloaded in several different ways: 

* Visit this [GitHub repository](https://github.com/aleimba/ecoli_VF_collection), click on *Clone or download* and then *Download ZIP*
* Or, on the website click on *releases* to download the latest release as a *ZIP* or gunzipped tarball (depending on the current state of the repo, doesn't have to be the most current VF collection version)
* Or, use `wget` or `curl` to get a packed archive of the latest commit of the master branch (the current state of the repository), e.g.:
    ```bash
    wget https://github.com/aleimba/ecoli_VF_collection/archive/master.tar.gz -O ecoli_VF_collection.tar.gz
    ```

* Or, clone the whole repository (current master branch) with `git`:
    ```bash
    git clone https://github.com/aleimba/ecoli_VF_collection.git

    ```

* To only get one file, e.g. one VF class multi-FASTA file, click on the [*/data*](/data) folder, there on the respective file, then the *Raw* button, and finally save the corresponding file from the browser. Of course, you can use the link to this file with `wget` or `curl`.


### Pipelines
This VF collection was designed for the [`prot_finder`](https://github.com/aleimba/bac-genomics-scripts/tree/master/prot_finder) pipeline (written for Zude *et al.*<sup id="a6">[6](#f6)</sup>), which can be used to search for query proteins (e.g. VFs) in a strain panel and to create a binary presence/absence matrix of the VFs (with `prot_binary_matrix.pl`) and based on this matrix get overall presence/absence statistics for groups of genomes (with `binary_group_stats.pl`). Because [`prot_finder`](https://github.com/aleimba/bac-genomics-scripts/tree/master/prot_finder) works with [**BLASTP**](http://blast.ncbi.nlm.nih.gov/Blast.cgi) it needs annotated coding sequences (CDS) in the strains of the strain panel. I recommend [Prokka](https://github.com/tseemann/prokka)<sup id="a7">[7](#f7)</sup> for fast automatic annotations.

In general, this VF collection can be used for whole genome shotgun sequencing (WGS) in bacterial diagnostics and strain typing. Notable pipelines for this purpose are:

* [SuperPhy](https://lfz.corefacility.ca/superphy/)<sup id="a8">[8](#f8)</sup>
* [Nullarbor](https://github.com/tseemann/nullarbor) from Torsten Seemann *et al.*
* [SRST2](https://github.com/katholt/srst2)<sup id="a9">[9](#f9)</sup> from Kathryn Holt *et al.*
* [Mykrobe predictor](http://www.mykrobe.com/)<sup id="a10">[10](#f10)</sup> from Zamin Iqbal *et al.*
* [WGSA - Whole Genome Sequence Analysis](http://www.wgsa.net/)
* [MicrobesNG](http://microbesng.uk/)
* CGE's [Bacterial Analysis Pipeline](https://cge.cbs.dtu.dk/services/cge)<sup id="a11">[11](#f11)</sup>


## VF sources
As mentioned in the [strategy](#strategy) the VFs here are mainly from Petty *et al.*<sup id="a1">[1](#f1)</sup> and VFDB<sup id="a2">[2](#f2)</sup><sup>,</sup><sup id="a3">[3](#f3)</sup><sup>,</sup><sup id="a4">[4](#f4)</sup><sup>,</sup><sup id="a5">[5](#f5)</sup>. These were supplemented with VFs from [primary literature](#publications).


### Databases
All three releases from VFDB (R1<sup id="a2">[2](#f2)</sup>, R2<sup id="a3">[3](#f3)</sup>, and R3<sup id="a4">[4](#f4)</sup>) were used.


### Publications
Quite a lot of publications were used to supplement the VF collection. I don't know if I listed all the publications I looked at here, a couple might have slipped through. Also, I didn't include **all** the VFs from these publications, at some point the VFs are quite overwhelming and start to overlap strongly (reaching a saturation plateau). But, I tried to get the most important ones (or let's say the ones that I am familiar with).

These publications are collected in a tab-delimited file alphabetically sorted by first author name [*/source/source_publications.tsv*](/source/source_publications.tsv). The file includes PubMed IDs (PMIDs), VF denominations included in the individual publications, and comments for a couple publications.


## Contributing
The VF collection is not complete, which is an impossible feat for one person. Thus, contributions (pull requests or [issues](https://github.com/aleimba/ecoli_VF_collection/issues)) to the VF collection by correcting errors or adding more VFs are very welcome and invited (if so a file with contributors will be included). If you want to contribute, please follow the [format standard](#format-of-the-fasta-files) and include additional [publications](#publications) in [*/source/source_publications.tsv*](/source/source_publications.tsv).

After all, the advantage of this GitHub VF collection is that it is not only easy to download but also easy to maintain and ideal for crowd-sourcing the content. Additionally, the repository can be forked to use it for a different purpose or if the initial maintainer abandoned the project.


## Similar resources
The following resources alternatively include collections of *E. coli* VFs (some already mentioned above in [why](#why) and [pipelines](#pipelines)):

* [VFDB](http://www.mgc.ac.cn/VFs/main.htm) (releases R1<sup id="a2">[2](#f2)</sup>, R2<sup id="a3">[3](#f3)</sup>, and R3<sup id="a4">[4](#f4)</sup>; now reorganised in the 2016 VFDB<sup id="a5">[5](#f5)</sup>), mainly [used](#strategy) for the VF collection here.
* [**PATRIC**](https://www.patricbrc.org/)<sup id="a11">[11](#f11)</sup>
* CGE's [**VirulenceFinder**](https://cge.cbs.dtu.dk/services/VirulenceFinder/)<sup id="a13">[13](#f13)</sup>
* [SuperPhy](https://lfz.corefacility.ca/superphy/)<sup id="a8">[8](#f8)</sup>


## Citation
For now cite the current version (***v0.1***) hosted on [zenodo](https://zenodo.org/):

Leimbach A. 2016. *ecoli_VF_collection: v0.1* **Zenodo** <https://github.com/aleimba/ecoli_VF_collection> [10.5281/zenodo.56686](http://dx.doi.org/10.5281/zenodo.56686)


## License
![CC BY 4.0 Logo](https://licensebuttons.net/l/by/4.0/88x31.png)

This work is licensed under a [Creative Commons Attribution 4.0 International License (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/), enclosed in the file [*LICENSE*](/LICENSE).


## Author - contact

Andreas Leimbach (aleimba[at]gmx[dot]de; Microbial Genome Plasticity, Institute of Hygiene, University of Muenster)


## References
<b id="f1">1: </b>Petty NK, Ben Zakour NL, Stanton-Cook M, Skippington E, Totsika M, Forde BM, Phan M-D, Gomes Moriel D, Peters KM, Davies M, Rogers BA, Dougan G, Rodriguez-Baño J, Pascual A, Pitout JDD, Upton M, Paterson DL, Walsh TR, Schembri MA, Beatson SA. 2014. Global dissemination of a multidrug resistant *Escherichia coli* clone. Proc Natl Acad Sci USA 111:5694–5699. [PMID: 24706808](https://www.ncbi.nlm.nih.gov/pubmed/24706808/). [↩](#a1)<br>
<b id="f2">2: </b>Chen L, Yang J, Yu J, Yao Z, Sun L, Shen Y, Jin Q. 2005. VFDB: a reference database for bacterial virulence factors. Nucleic Acids Res 33:D325-328. [PMID: 15608208](https://www.ncbi.nlm.nih.gov/pubmed/15608208/). [↩](#a2)<br>
<b id="f3">3: </b>Yang J, Chen L, Sun L, Yu J, Jin Q. 2008. VFDB 2008 release: an enhanced web-based resource for comparative pathogenomics. Nucleic Acids Res 36:D539-542. [PMID: 17984080](https://www.ncbi.nlm.nih.gov/pubmed/17984080/). [↩](#a3)<br>
<b id="f4">4: </b>Chen L, Xiong Z, Sun L, Yang J, Jin Q. 2012. VFDB 2012 update: toward the genetic diversity and molecular evolution of bacterial virulence factors. Nucleic Acids Res 40:D641-645. [PMID: 22067448](https://www.ncbi.nlm.nih.gov/pubmed/22067448/). [↩](#a4)<br>
<b id="f5">5: </b>Chen L, Zheng D, Liu B, Yang J, Jin Q. 2016. VFDB 2016: hierarchical and refined dataset for big data analysis--10 years on. Nucleic Acids Res 44:D694-697. [PMID: 26578559](https://www.ncbi.nlm.nih.gov/pubmed/26578559/). [↩](#a5)<br>
<b id="f6">6: </b>Zude I, Leimbach A, Dobrindt U. 2014. Prevalence of autotransporters in *Escherichia coli*: what is the impact of phylogeny and pathotype? Int J Med Microbiol 304:243–256. [PMID: 24239047](https://www.ncbi.nlm.nih.gov/pubmed/24239047/). [↩](#a6)<br>
<b id="f7">7: </b>Seemann T. 2014. Prokka: rapid prokaryotic genome annotation. Bioinformatics 30:2068–2069. [PMID: 24642063](https://www.ncbi.nlm.nih.gov/pubmed/24642063/). [↩](#a7)<br>
<b id="f8">8: </b>Whiteside MD, Laing CR, Manji A, Kruczkiewicz P, Taboada EN, Gannon VPJ. 2016. SuperPhy: predictive genomics for the bacterial pathogen *Escherichia coli*. BMC Microbiol 16:65. [PMID: 27067409](https://www.ncbi.nlm.nih.gov/pubmed/27067409/). [↩](#a8)<br>
<b id="f9">9: </b>Inouye M, Dashnow H, Raven L-A, Schultz MB, Pope BJ, Tomita T, Zobel J, Holt KE. 2014. SRST2: Rapid genomic surveillance for public health and hospital microbiology labs. Genome Med 6:90. [PMID: 25422674](https://www.ncbi.nlm.nih.gov/pubmed/25422674/). [↩](#a9)<br>
<b id="f10">10: </b>Bradley P, Gordon NC, Walker TM, Dunn L, Heys S, Huang B, Earle S, Pankhurst LJ, Anson L, de Cesare M, Piazza P, Votintseva AA, Golubchik T, Wilson DJ, Wyllie DH, Diel R, Niemann S, Feuerriegel S, Kohl TA, Ismail N, Omar SV, Smith EG, Buck D, McVean G, Walker AS, Peto TEA, Crook DW, Iqbal Z. 2015. Rapid antibiotic-resistance predictions from genome sequence data for Staphylococcus aureus and Mycobacterium tuberculosis. Nat Commun 6:10063. [PMID: 26686880](https://www.ncbi.nlm.nih.gov/pubmed/26686880/). [↩](#a10)<br>
<b id="f11">11: </b>Thomsen MCF, Ahrenfeldt J, Cisneros JLB, Jurtz V, Larsen MV, Hasman H, Aarestrup FM, Lund O. 2016. A Bacterial Analysis Platform: An Integrated System for Analysing Bacterial Whole Genome Sequencing Data for Clinical Diagnostics and Surveillance. PLoS ONE 11:e0157718. [PMID: 27327771](https://www.ncbi.nlm.nih.gov/pubmed/27327771/). [↩](#a11)<br>
<b id="f12">12: </b>Wattam AR, Abraham D, Dalay O, Disz TL, Driscoll T, Gabbard JL, Gillespie JJ, Gough R, Hix D, Kenyon R, Machi D, Mao C, Nordberg EK, Olson R, Overbeek R, Pusch GD, Shukla M, Schulman J, Stevens RL, Sullivan DE, Vonstein V, Warren A, Will R, Wilson MJC, Yoo HS, Zhang C, Zhang Y, Sobral BW. 2014. PATRIC, the bacterial bioinformatics database and analysis resource. Nucleic Acids Res 42:D581-591. [PMID: 24225323](https://www.ncbi.nlm.nih.gov/pubmed/24225323/). [↩](#a12)<br>
<b id="f13">13: </b>Joensen KG, Scheutz F, Lund O, Hasman H, Kaas RS, Nielsen EM, Aarestrup FM. 2014. Real-time whole-genome sequencing for routine typing, surveillance, and outbreak detection of verotoxigenic *Escherichia coli*. J Clin Microbiol 52:1501–1510. [PMID: 24574290](https://www.ncbi.nlm.nih.gov/pubmed/24574290/). [↩](#a13)<br>


## Changelog

* v0.1 (29.06.2016)
