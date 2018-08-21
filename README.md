## OCD Framework: A Comparison of Code Similarity Analysers
### [Chaiyong Ragkhitwetsagul](https://cragkhit.github.io), [Jens Krinke](http://www0.cs.ucl.ac.uk/staff/j.krinke/index.html), [David Clark](http://www0.cs.ucl.ac.uk/staff/D.Clark/)
#### [CREST centre](http://crest.cs.ucl.ac.uk/), Department of Computer Science, University College London

Additional material to:

Chaiyong Ragkhitwetsagul, Jens Krinke, David Clark: A Comparison of Code Similarity Analysers. (Please email the authors for a copy.)

As an extension to:

Chaiyong Ragkhitwetsagul, Jens Krinke, David Clark: Similarity of Source Code in the Presence of Pervasive Modifications. 16th International Working Conference on Source Code Analysis and Manipulation (SCAM), Raleigh, NC, USA, October 2016.

### Abstract
Source code analysis to detect code cloning, code plagiarism, and code reuse suffers from the problem of code modifications. We are interested in two types of code modifications in this study: pervasive modifications, i.e. transformations that may have a global effect, and local modifications, i.e. code changes that are contained in a single method or code block. We evaluate 30 similarity detection techniques and tools using five experimental scenarios for Java source code. These are (1) pervasively modified code, created with tools for source code and bytecode obfuscation, and boiler-plate code, (2) source code normalisation through compilation and decompilation using different decompilers, (3) reuse of optimal configurations over different data sets, (4) tool evaluation using ranked-based measures, and (5) local+global code modifications. Our experimental results show that with the presence of pervasive modifications, some of the general textual similarity measures can offer similar performance to specialised code similarity tools, while in the presence of boiler-plate code, highly specialised source code similarity detection techniques and tools outperform textual similarity measures. Our study strongly validates the use of compilation/decompilation as a normalisation technique. Its use reduced false classifications to zero for three of the tools. Moreover, we demonstrate that optimal configurations are very sensitive to a specific data set. After directly applying optimal configurations derived from one data set to another, the tools perform poorly on the new data set. Code similarity analysers are thoroughly evaluated not only based on several well-known pair-based and query-based error measures but also on each specific type of pervasive code modification. This broad, thorough study is the largest in existence and potentially an invaluable guide for future users of similarity detection in source code.

### Contents
1. [The Experimental Framework](#the-experimental-framework)
2. [Tools and Techniques](#tools-and-techniques)
3. [Scenario 1: Pervasive Modifications (data set)](#scenario-1)
4. [Scenario 2: Decompilation (data set)](#scenario-2)
5. [Scenario 3: Reused Boiler-Plate Code (data set)](#scenario-3)
6. [Scenario 4: Ranked Results](#scenario-4)
7. [Scenario 5: Local + Global Modifications (data set)](#scenario-5)
8. [Results](#results)
9. [Research Question 1 (Performance comparison)](#research-question-1)
10. [Research Question 2 (Optimal Configurations)](#research-question-2)
11. [Research Question 3 (Normalisation by Decompilation)](#research-question-3)
12. [Research Question 4 (Reuse of Configurations)](#research-question-4)
13. [Research Question 5 (Ranked Results)](#research-question-5)
14. [Research Question 6 (Local + Global Code Modifications)](#research-question-6)

### The Experimental Framework

The general framework of our study as shown below consists of 5 main steps. In Step 1, we collect test data consisting of Java source code files. Next, the source files are transformed by applying pervasive modifications at source and bytecode level. In the third step, all original and transformed source files are normalised. A simple form of normalisation is pretty printing the source files which is used in similarity or clone detection. We also use decompilation. In Step 4, the similarity detection tools are executed pairwise against the set of all normalised files, producing similarity reports for every pair. In the last step, the similarity reports are analysed.

![Experimental Framework](https://github.com/UCL-CREST/ocd/blob/master/1.png)

### Tools and Techniques

Several tools and techniques were used in this study. These fall into three categories: obfuscators, decompilers, and detectors. The tool set included source and bytecode obfuscators, and two decompilers. The detectors cover a wide range of similarity measurement techniques and methods including plagiarism and clone detection, compression distance, string matching, and information retrieval. All tools are open source in order to expedite the repeatability of our experiments.

#### Obfuscators, Decompilers

Type	| Tool |	Link
------|------|------
Source code obfuscator	| Artifice	| [Download](https://www.tu-braunschweig.de/isf/research/artifice/index.html)
Bytecode obfuscator	    | ProGuard  |	[Download](http://proguard.sourceforge.net/)
Decompiler	            | Krakatau  |	[Download](https://github.com/Storyyeller/Krakatau)
Decompiler              | Procyon	  | [Download](https://bitbucket.org/mstrobel/procyon/wiki/Java%20Decompiler)

#### Similarity Detection Tools

| Tool/technique	| Similarity calculation |	Link |
|----------------|------------------------|------|
| Clone detectors |   |  |
| ccfx	| tokens and suffix tree matching	| [Download](http://www.ccfinder.net/) |
| deckard	| characteristic vectors of AST optimised by LSH | [Download](https://github.com/skyhover/Deckard) |
| iclones | tokens and generalised suffix tree	| [Download](http://www.softwareclones.org/iclones.php) |
| nicad	| TXL and string comparison (LCS)	| [Download](http://www.txl.ca/nicaddownload.html) |
| simian |	line-based string comparison	| [Download](http://www.harukizaemon.com/simian/) |
| Plagiarism detectors | | |
| jplag-java |	tokens, Karp Rabin matching, Greedy String Tiling	| [Download](https://jplag.ipd.kit.edu/) |
| jplag-text |	tokens, Karp Rabin matching, Greedy String Tiling | [Download](https://jplag.ipd.kit.edu/) |
| plaggie	| N/A (not disclosed) | [Download](https://www.cs.hut.fi/Software/Plaggie/) |
| sherlock |	digital signatures | [Download](http://sydney.edu.au/engineering/it/%20scilect/sherlock/) |
| simjava	| tokens and string alignment	| [Download](http://dickgrune.com/Programs/similarity_tester/) |
| simtext	| tokens and string alignment | [Download](http://dickgrune.com/Programs/similarity_tester/) |
| Compression | | |
| 7zncd	| NCD with 7z	| |
| bzip2ncd |	NCD with bzip2 | |
| gzipncd	| NCD with gzip |	|
| xzncd	| NCD with xz	| |
| icd		| ![ICD](https://github.com/UCL-CREST/ocd/blob/master/2.png) | |
| ncd	| ncd tool with bzlib & zlib | [Download](http://complearn.org/ncd.html) |
| Others | | |
| bsdiff | ![bsdiff](https://github.com/UCL-CREST/ocd/blob/master/3.png) | |
| diff | ![diff](https://github.com/UCL-CREST/ocd/blob/master/4.png) | |
| py-difflib | Gestalt pattern matching	| [Download](https://docs.python.org/2/library/difflib.html) |
| py-fuzzywuzzy |	fuzzy string matching	| [Download](https://github.com/seatgeek/fuzzywuzzy) |
| py-jellyfish | approximate and phonetic matching of strings py-ngram fuzzy search based using n-gram | [Download](https://github.com/jamesturk/jellyfish) |
| py-sklearn | cosine similarity from machine learning library | [Download](http://scikit-learn.org/stable/) |

### Scenario 1
#### Pervasive Modifications

The data set in this scenario is created to simulate pervasive modifications made to source code by using source and bytecode obfuscators: Artifice, and ProGuard. The total number of pervasively modified source code files is 100. The process of code transformations is displayed below. The data set is called OCD (Obfuscation/Compilation/Decompilation).

![Scenario 1](https://github.com/UCL-CREST/ocd/blob/master/5.png)

##### Data set: Obfuscation/Compilation/Decompilation (OCD)

### Scenario 2
#### Decompilation

In this scenario, the data set is based on the same set of 100 source code files generated in Scenario 1. However, we added normalisation through decompilation to the post-processing (step 3 in the framework) by compiling all the transformed files using javac and decompiling them using either Krakatau or Procyon.

##### Data set: OCD<sup>decomp</sup> (krakatau)
##### Data set: OCD<sup>decomp</sup> (procyon)

### Scenario 3
#### Reused Boiler-Plate Code

In this scenario, we want to analyse the tools' performance against a data set that contains files in which fragments of (boiler-plate) code are reused with or without modifications applied. We choose the training set of SOCO (SOurce COde re-use) data set that has been provided in a competition for discovering monolingual re-used source code amongst a given set of programs. The files in the SOCO data set are adapted from the study by Arwin et al. (2006). We found that many of them share the same or very similar boiler-plate code fragments which perform the same task. Some of the boiler-plate fragments have been modified to adapt them to the environment in which the fragment is re-used.

##### Data set: the SOCO data set can be obtained from the competition website (http://users.dsic.upv.es/grupos/nle/soco/). 
##### Fixed answer key: the answer key for SOCO java training data set containing 97 pairs of reused code download

### Scenario 4
#### Ranked Results

In our three previous scenarios (Ragkhitwetsagul et al., 2016), we compared the tools’ performances using their optimal F-scores. The F-score offers weighted harmonic mean of precision and recall. It is a set- based measure that does not consider any ordering of results. Instead of looking at the results as a set and applying a cut-off threshold to obtain true and false positives, we consider only a subset of the results based on their rankings. We adopt three error measures mainly used in information retrieval: precision-at-n (prec@n), average r- precision (ARP), and mean average precision (MAP) to measure the tools’ performances.

##### Further reading: Manning et al., Introduction to Information Retrieval, Cambridge University Press. 2008.

### Scenario 5
#### Local + Glocal Modifications

We have two objectives for this experimental scenario. First, we are interested in a situation where local and global code modifications are combined together. Second, we shift our focus from measuring how good our tools are on finding all similar pairs of pervasively modified code as we did in Scenario 1 to measure how good our tools are on finding similar pairs of code based on each pervasive code modification type. 
The table below presents the 10 pervasive code modification types; including the original (O), source code obfuscation by Artifice (A), decompilation by Krakatau (K), decompilation by Procyon (P<sub>c</sub>), bytecode obfuscation by ProGuard and decompilation by Krakatau (P<sub>g</sub>K), bytecode obfuscation by ProGuard and decompilation by Procyon (P<sub>g</sub>Pc), and four other combinations (AK, AP<sub>c</sub>, AP<sub>g</sub>K, AP<sub>g</sub>P<sub>c</sub>); and ground truth for each of them. The number of code pairs and true positive pairs of A to AP<sub>g</sub>P<sub>c</sub> are twice larger than the Original (O) type because of asymmetric similarity between pairs, i.e. Sim(x,y) and Sim(y,x).

<table border="1" class="contenttable"> <tbody><tr> <td rowspan="2">Type</td><td rowspan="2">Modification</td> <td colspan="2">Obfuscation</td><td rowspan="2">Decomp.</td><td rowspan="2">Pair</td><td rowspan="2">TP</td> </tr> <tr> <td> Source</td><td>Bytecode</td></tr> <tr> <td>O</td><td>Original</td><td></td><td></td><td></td> <td align="right"> 1,089</td> <td align="right">55</td> </tr> <tr> <td>A</td><td>Artifice</td><td align="center">X</td><td></td><td></td> <td align="right"> 2,178</td> <td align="right">110</td> </tr> <tr> <td>K</td><td>Krakatau</td><td></td><td></td><td align="center">X</td> <td align="right"> 2,178</td> <td align="right">110</td> </tr> <tr> <td>Pc</td><td>Procyon</td><td></td><td></td><td align="center">X</td> <td align="right"> 2,178</td> <td align="right">110</td> </tr> <tr> <td>PgK</td><td>ProGuard + Krakatau</td><td></td><td align="center">X</td><td align="center">X</td> <td align="right"> 2,178</td> <td align="right">110</td> </tr> <tr> <td>PgPC</td><td>ProGuard + Procyon</td><td></td><td align="center">X</td><td align="center">X</td> <td align="right"> 2,178</td> <td align="right">110</td> </tr> <tr> <td>AK</td><td>Artifice + Krakatau</td><td align="center">X </td><td></td><td align="center">X</td> <td align="right"> 2,178</td> <td align="right">110</td> </tr> <tr> <td>APc</td><td>Artifice + Procyon</td><td align="center">X</td><td></td><td align="center">X</td> <td align="right"> 2,178</td> <td align="right">110</td> </tr> <tr> <td>APgK</td><td>Artifice + ProGuard + Krakatau</td><td align="center">X</td><td align="center">X</td><td align="center">X</td> <td align="right"> 2,178</td> <td align="right">110</td> </tr> <tr> <td>APgPc</td><td>Artifice + ProGuard + Procyon</td><td align="center">X</td><td align="center">X</td><td align="center">X</td> <td align="right"> 2,178</td> <td align="right">110</td> </tr> </tbody></table>

We measured the tools' performance on each Sim<sub>m</sub>(F) set. By applying tools on a pair of original and pervasively modified code, we measure the tools based on one particular type of code modifications at a time.

![RQ6 Equation](https://github.com/UCL-CREST/ocd/blob/master/rq6_eq.png)
