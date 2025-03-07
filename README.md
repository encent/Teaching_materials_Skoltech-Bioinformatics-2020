### Introduction: Bioinformatics seminars at Skoltech

**Disclaimer:** the entire repository is forked from Aleksandra Galitsyna with her permission. 

Welcome to the Seminar 4 of this term at Skoltech! 
We're through the course on Bioinformatics by Mikhail Gelfand, and I (Nikolai Bykov) will be your TA for this seminar on 
sequence alignments and motif search. 

The slides and datasets for this seminar can be found in [this folder on github](https://github.com/encent/2021_Skoltech_Bioinformatics_course_seminar_4/). 

The home assignments and table with files distribution can be found in Canvas. 


## Seminar 4. Multiple Alignments

Nikolai Bykov 10/11/2021

### Location of the files

The files for this hometask are located in this github repository: 

https://github.com/encent/2021_Skoltech_Bioinformatics_course_seminar_4/tree/master/data/

If you need to view the file, the link will be: 

https://github.com/encent/2021_Skoltech_Bioinformatics_course_seminar_4/blob/master/data/upstreams.fasta

If you need to download raw file, you can press `"Raw"` in GitHub window with file and the link will be: 

https://raw.githubusercontent.com/encent/2021_Skoltech_Bioinformatics_course_seminar_4/master/data/peaks.fasta

### Task 1. Multiple alignment

In this part of the task you will work with alignments with three popular aligners: MUSCLE, ClustalW and T-COFFEE. 

To access these aligners you can use either **web server interface** (and work on local computers), 
or **command line interface (CLI)** (and run aligners remotely though bash interface). 

> To increase the diversity of your skills and get the best of the course, I highly recommend you 
> to combine both approaches and try CLI for some aligners and web interface for other. 
>
> If you select the web server interface, please, follow the instructions denoted with "a". 
> If you select the CLI, follow the instructions with "b"

1.1. Download the file with upstream regions of bacterial orthologs (upstreams.fasta).
 
1.1.a. To download the files on the local computer, follow the links, e.g.:

https://github.com/encent/2021_Skoltech_Bioinformatics_course_seminar_4/blob/master/data/upstreams.fasta


1.1.b. If you select CLI, log in to server in Putty, or in bash: 

```bash
ssh yourname@mg.uncb.iitp.ru
```

Then create a folder for this seminar: 

```bash
mkdir Seminar4
cd Seminar4
```

To download the files in the terminal, use: 

```bash
wget https://raw.githubusercontent.com/encent/2021_Skoltech_Bioinformatics_course_seminar_4/master/data/upstreams.fasta
```

Useful commands to check the result of download: 
```bash
ls                   # list the files in the directory
pwd                  # check the current location
less upstreams.fasta # view the content of the file
```

1.2. Select one of the aligners to run on these sequences. Your aim is to find small (up to 16 bp) regulatory regions of DNA in the 
upstream sequences of bacterial genes. To improve the quality of the alignment, you can try to vary the parameters. 
Please, note these parameters, you will be asked to report them in the assignment. 

Helpful links:

| Aligner  | Web server link                            | CLI manual                                                               | Original paper |  Type |
|----------|------------------------------------------|--------------------------------------------------------------------------|----------------|---|
| MUSCLE   | https://www.ebi.ac.uk/Tools/msa/muscle   | [`muscle` manual](https://www.drive5.com/muscle/manual/options.html)                       |     [Edgar 2004](https://bmcbioinformatics.biomedcentral.com/articles/10.1186/1471-2105-5-113)           | Global alignment  |
| ClustalW | https://www.genome.jp/tools-bin/clustalw | [`clustalw` manual](http://manpages.ubuntu.com/manpages/bionic/man1/clustalw.1.html)          |     [Thompson et al. 1994](https://academic.oup.com/nar/article-abstract/22/22/4673/2400290?redirectedFrom=fulltext)           | Global alignment  |
| T-COFFEE | http://tcoffee.crg.cat/                  | [`t_coffee` manual](https://tcoffee.readthedocs.io/en/latest/tcoffee_main_documentation.html) |     [Notredame et al. 2000](https://www.sciencedirect.com/science/article/abs/pii/S0022283600940427?via%3Dihub)           |  Global and local alignment |

1.2.a. If you select web server interface, follow the instructions on the website, for example: 

![Web Server Instructions 1](https://github.com/encent/2021_Skoltech_Bioinformatics_course_seminar_4/blob/master/images/Figure1.png?raw=true)

![Web Server Instructions 2](https://github.com/encent/2021_Skoltech_Bioinformatics_course_seminar_4/blob/master/images/Figure2.png?raw=true)


1.2.b. In terminal, to get the documentation of the aligners, type one of these: 

```bash
man muscle
man clustalw
man t_coffee
```

To run the aligners with default parameters, you can use something like:
```bash
muscle -in upstreams.fasta -out muscle_alignment.fasta
t_coffee upstreams.fasta -run_name t_coffee_alignment
clustalw -infile=upstreams.fasta -outfile=clustalw_alignment.aln
```

Check the output of these commands. What is the file format of the output? 

> Hint: typically the output is represented in [FASTA](https://blast.ncbi.nlm.nih.gov/Blast.cgi?CMD=Web&PAGE_TYPE=BlastDocs&DOC_TYPE=BlastHelp) 
>or [CLUSTAL](http://scikit-bio.org/docs/0.2.1/generated/skbio.io.clustal.html#:~:text=Format%20Specification,in%20the%20alignment%20%5BR152%5D.) format. 

1.3. Download the output files with alignments, or copy full alignments to the clipboard. 

1.4. Visualize the alignment using MView provided by EMBL-EBI: [https://www.ebi.ac.uk/Tools/msa/mview/](https://www.ebi.ac.uk/Tools/msa/mview/)

This tool allow you to paste your alignment and highlight it based on sequence conservation. 

Pay extra attention to: 
- Type of sequence you upload/paste (DNA)
- Input format of your alignment. The full list of MView-accepted formats can be found [here](https://www.ebi.ac.uk/seqdb/confluence/display/JDSAT/MView+Help+and+Documentation#MViewHelpandDocumentation-informat). 
The examples of different formats can be found [here](https://www.hiv.lanl.gov/content/sequence/HelpDocs/SEQsamples.html)

> Do not paste the original upstreams.fasta at this step! Your alignment should contain gaps ("-" symbols). 

1.5. Propose a region that might be conserved regulatory sequence of DNA in the alignment of gene upstreams of bacteria. 
There is no ultimately right answer, so concentrate on the best candidate you observe and describe your conclusion. 

Consider the following criteria for conserved regulatory sequence: 
- Should it be present in all the sequences? (probably yes)
- Should it contain the gaps? (probably no)
- Should it be located close to the gene start? (probably yes)

1.6. Try another aligner. Has the result changed? 

Try all three aligners, select the one that results in most full and realistic regulatory sequences. 

Visualize the best aligner output at the location of the best candidate regulatory sequence alignment. 
You may highlight the candidate regulatory sequence by graphics editor.

Save the information about the aligner and the image. **This will be part of your home assignment (Task 1).**

1.7. Copy the best candidate regulatory sequence alignment only and manually convert it into FASTA file. 
Use text editor for this task to save the selected block of the alignment as a separate file. 
You may use Word, Notepad/TextEdit to create only the alignment; 
advanced users might use `vim` block-selection opportunity (see below). 

The resulting file should contain something like:

```
>1
GGTCAATTCACTGCCTT
>2
GGCCAATTTACGGCCTT
>3
GGTCAGTTCACGGCATT
>4
TCCTAATTTACAGCAGC
>5
GGTCAGTTCACGGCATT
>6
GGCCAATTTACTGCGTT
>7
AACCAGCTTGAGACAGC
```

Save this file and download it to your local computer. **This will be your input for the construction of PWM (Task 2).**

> Hint for advanced bash users. 
> If you copy the output to console, it’s easy to use **vim** command line text editor to retrieve the blocks of sequences. 
>
> Create new file with alignment:  	`vim tmp.algn`
> 
> 1. Position the cursor at the beginning of the text you want to copy
> 2. Press `“Ctrl+V”` **ONCE** to select the block of interest (starting from the first row and first position), 
> 3. Move the cursor to the end of the text to be copied
> 4. Type `“y”` to copy the text, 
> 5. Type `“:wq”` to exit vim. 
>
> Open empty new file:
>
>	```vim tmp.fasta```
>
> Type `“P”` to insert the copied sequences. 
> Format them in insert mode (`“i”`) to match fasta format. 
> Then press `“Esc”` and exit vim. You an save this file and exit `“:wq”` or simply copy the result to console.


### Task 2. Construction of position weight matrix (PWM)
 
You will use the output of Task 1 (1.7) for the construction of consensus sequence and PWM. 

2.1. Do the following steps:
- Go to RSAT web tool: http://embnet.ccg.unam.mx/rsat/ 
- Click -> `"Matrix tools"` from left menu 
- -> `"convert matrix"`
- Select matrix format `“sequences”`
- Paste alignment of conserved sequences in FASTA format to the field, or upload the file
- Check the boxes "consensus", "counts", "frequencies", "weights", "profile" and "Compute reverse complement" (if they are not selected). 
Set all other parameters to default. Press “GO”. 

2.2. In the RSAT output you can observe the transition from alignment to nucleotides counts matrix, 
frequencies matrix, then to weights, profile and logo. 

Save the forward logo to your local computer. **This will be part of your home assignment (Task 2).**

### Task 3. Automated search of motifs in the sequences with MEME. 

3.1. Now let’s switch to some more automated tool, Multiple Expression motifs for Motif Elicitation (MEME, http://meme-suite.org/tools/meme). 

- Upload the upstreams.fasta file
- Select `"One occurence per sequence"` for `"Select the site distribution"`
- Press “Advanced options”, set “How wide can motifs be?” **from 5 to 15**. **Don't forget this step, otherwise you will wait for your results for quite some time (Why?)**
- Submit and wait for results
- Go to `"MEME HTML output"` and check the result

The initial submission form should look similar to this one: 

![MEME Instructions](https://github.com/encent/2021_Skoltech_Bioinformatics_course_seminar_4/blob/master/images/Figure3.png?raw=true)


Are any of the found motifs similar to your result obtained manually in Task 2? 
Try to submit the most significant motif to Tomtom program to find similar motifs in public libraries (click `Submit/Download`, select `Tomtom`, click `Submit`, adjust parameters to the prokaryotes search).
Save the resulting report to your local computer. **This will be part of your home assignment (Task 3).**

### Task 4. Motif search in ChIP-Seq data

Now you will use MEME-ChIP for search of motifs in ChIP-Seq dataset. 
Your input is the peaks from ChIP-Seq experiment on __Gallus gallus__ (chicken) for CTCF protein. 
We will use this knowledge for a test run of MEME-ChIP. 

- Download ChIP-Seq peaks ([peaks.fasta](https://github.com/encent/2021_Skoltech_Bioinformatics_course_seminar_4/blob/master/data/peaks.fasta)). 
- Go to MEME-ChIP web interface: http://meme-suite.org/ -> MEME-ChIP
- Do not change the options, submit the peaks.fasta file

The result will look as following: 

![MEME ChIP output](https://github.com/encent/2021_Skoltech_Bioinformatics_course_seminar_4/blob/master/images/Figure4.png?raw=true)

To interpret this result, take a look at:
- Number of found motifs
- E-values of the hits (What would you consider significant?)
- Discrepancy between E-value of the best hit and E-values of suboptimal hits (Do you expect high discrepancy for meaningful hits?)
- Known or similar motifs to the hit obtained by TOMTOM tool 
(You can press the links in this field to learn more. Are the TOMTOM hits significant?)
- Complexity and the length of the logo. 
(Can you expect the motif to too short or contain only 2-4 informational positions?) 
- Distribution of the possible binding sites around the centers of the peaks 

> Hint on how to select the best motif. 
> You work with ChIP-Seq peaks, which represent the DNA sequences bound by CTCF protein.
> In ChIP-Seq, the protein is bound preferentially at the center of peaks. 
> If you observe some motif in the peaks sequences with good E-value and central enrichment, 
> this is a sign of true motif of the binding protein of interest.
> Even more, if you observe significant similarity to other vertebrates' CTCF, you must be sure you've found the right motif.

> If you observe some other motifs significantly enriched in your peaks, it might be the co-occuring binding of chromatin factors. 

Now, as you've learned to work with MEME-ChIP, you can download your own file with ChIP-Seq. You do not have the information 
about the factor or species. You need to derive this information from MEME-ChIP output. 

4.1. Find your name and corresponding file in the table provided in Files section for this seminar in **Canvas**

4.2. Download your file with peaks from the "data/unknown_peaks" folder from this repository: 

https://github.com/encent/2021_Skoltech_Bioinformatics_course_seminar_4/tree/master/data/unknown_peaks

4.3. Run MEME-ChIP and **answer to the questions in the Assignements (Task 4)**. You may need to download the MEME-ChIP report for that. 

### Home assignments

Your home task will be in Canvas "Assignments" section. 
The assignments will test your understanding of the topic. 
You are expected to learn how to use T-COFFEE, Muscle and ClustalW, 
build global and local alignments (and tell the difference between them), 
build the motifs from the given alignment and perform __de novo__ search of the motifs.
The home assignment will test the correct output of the tools in your hand, your ability to observe and interpret the results, 
and express your opinion on the results. 

The deadline for the accomplishment of the home task is 12:00 on Wednesday, November 17. 

### Afterword from TA

I hope it was fun to learn about alignments, motifs search and analysis of ChIP-Seq peaks. :) 
Write me at Skoltech e-mail, search it in Outlook by Nikolai Bykov.

### Acknowledgement

Special thanks to Dr. Aleksandra Galitsyna for the materials and discussion.
