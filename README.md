# Receptor-Binding-Domain-Analysis-of-Covid-Spike-Glycoprotein
Analyzing the receptor binding domain(rbd) of Covid Spike Glycoprotein samples collected in various parts of the United States


# INTRODUCTION
This program utilizes multiple libraries and search algorithms to collect the rbd protein
sequences of collected samples of the COVID-19 surface glycoprotein sequences from the
United States. The samples, originally on one Fasta file, are broken up into separate categories
based on state, geographic region, rate of vaccine, absences of mask mandate, and
enforcement of outdoor gathering restrictions. A Fasta file is made for each of these categories,
with a total of 60 Fasta Files created in total (50 files for each state; 1 file for each region:
Northeast, Midwest, Southeast, Southwest, Mountain, and Pacific; 1 file for low vaccine rates, 1
file for high vaccine rates, 1 file for no enforced mask wearing mandate, 1 file for enforced
limited outdoor gathering rules).
After files are created, the program will also run a Multiple Sequence Alignment (MSA) using
clustalw. The function to call the MSA will return 2 additional files after the MSA is performed.
One file is the alignment file, .aln, and the other is the phylogenetic tree file, .dnd. The program
will also draw the Phylogenetic tree. At the end of this program's run, a total of 180 fasta files
will be created.



# OBJECTIVE
The objective of this program is to create analytical data from the raw sequences of the
proteins. Numerous files will be created to allow analysis of sequences by geographic region
and analysis on the impact of laws and regulations concerning COVID-19. Multiple Sequence
Alignment will allow researchers to find gaps or variation in the sequences, and phylogenetic
trees will show the relation of variants and which variant is dominating a given population.
This program will run 6,000 rbd sequences from 60 fasta files containing 100 sequences each.
Full fasta files will also be created in addition to the files with the first 100 sequences.

# FLOWCHART ANALYSIS OVERVIEW
One function is called to start the program: makeFiles(pathToBaseFile). This function requires
one argument, the path to the file containing the samples of COVID-19 surface glycoprotein
sequences. This is the only function the user interacts with. Once makeFiles(pathToBaseFile) is
called, it calls three more functions: makeIndividualStateFiles(pathToBaseFile),
makeRegionalFiles(pathToBaseFile), and makeCategoryFiles(pathToBaseFile). These three
functions also take the path to the file containing the samples of COVID-19 surface glycoprotein
sequences, and use it to make the desired categories and files.
In addition to these five key functions, four more functions are used to aid functions
makeIndividualStateFiles(pathToBaseFile), makeRegionalFiles(pathToBaseFile), and
makeCategoryFiles(pathToBaseFile) in making clean Fasta, alignment, and phylogenetic tree
files. They are, pullState(description), formatDescription(description),
makeSmallDataFileMSA(pathToBaseFile, regionOrStateFile),
makeMSAwithClustal(pathToFasta, regionOrStateFile), and findRBD(seq, rbdPatternFile).
These functions are helper functions, and are key to cleaning up files specific to the assignment.
Further details of what each function does will be found in the Materials and Methods section.


# MATERIALS AND METHODS
Note: paths were originally for windows user directory. Please adjust directories
Libraries used for this program include: Bio for biopython and re for python's regular
expressions library, and Clustalw command line. Programs and interfaces used are SeqIO,
AlignIO, Bio.Align.Applications, and Phlyo. Clustalw must be installed on the user's personal
computer in order for the program to run.

*User Input*
Under the comment '"CONSTANTS":', the user must input the path of the location of the surface
glycoprotein sequences, the surface glycoprotein receptor binding sequence, and the path for
where files should be saved. A variable for the Clustalw path is also created, and the user must
enter the path there.
USERPATH < - path to folder where user wants to save files
CLUSTALPATH < - path of where the clustalw program lives on users' personal computer
ALLSURFGLYCPATH < - path of the surface glycoprotein sequences file
SURFACEGLYCPATH <- the surface glycoprotein receptor binding sequence

*Lists*
Lists were made for states, regions, and separate categories that contain the state initial
applicable to the region or category. These lists will be used to separate the files accordingly.

# OVERVIEW OF EACH FUNCTION
pullState(description)
This function takes the description string in the fasta sequences and splits it into a list. After the
list has been made, it returns the item at index four, which is the state initials.

formatDescription(description)
The desired description format in the assignment pdf and the format of the description in the
given sequence file are different. Therefore, to fit the style of the description in the assignment,
this function rearranges the order of the description string by splitting it into a list. After the list is
created, a new string is made by concatenating items in the list into an order that fits the desired
format. The created string is then returned.

findRBD(seq, rbdPatternFile)
This function opens the file with the receptor binding domain sequence, and isolates the
sequence from the definition line. The function then looks at another given sequence (the
argument ‘seq’), and uses the regular expression search() function to find the best matching rbd
sequence in the given sequence. It returns the rbd sequences found in the given sequence.

makeMSAwithClustal(pathToFasta, regionOrStateFile)
Clustalw is a separate command line program that can be called by python via the
Bio.Align.Applications program. This function writes to the command line with the infile created
by the user path and name of unaligned fasta file. After the command line call, the program will
automatically produce the alignment file and phylogenetic tree file. After these files are
generated, this function will print the .aln file and draw a tree using the Phylo.draw() function.

makeSmallDataFileMSA(pathToBaseFile, regionOrStateFile)
This function has three main jobs. First, it creates a smaller version of each file by limiting it to
only 100 sequences. This allows for faster alignment and runtime to fit the assignment deadline.
The second job is to use the findRBD function and pull the receptor binding domain from the
sequence. Once the receptor binding domain is found, the program will write that to the new file.
The final job is calling the makeMSAwithClusta function, which will take the new file made and
create the alignment and Phylogenetic tree files.

makeIndividualStateFiles(pathToBaseFile)
Calling this function will split the COVID-19 surface glycoprotein sequences into 50 files for each
individual state. It will iterate through the COVID-19 surface glycoprotein sequences file using
SeqIO parser and will open and write to a new file named after the state.

makeRegionalFiles(pathToBaseFile)
Calling this function will split the COVID-19 surface glycoprotein sequences into 6 files for each
region. It will iterate through the COVID-19 surface glycoprotein sequences file using SeqIO
parser and will open and write to a new file named after the state.

makeCategoryFiles(pathToBaseFile)
Calling this function will split the COVID-19 surface glycoprotein sequences into 4 files for each
category. It will iterate through the COVID-19 surface glycoprotein sequences file using SeqIO
parser and will open and write to a new file named after the state.

makeFiles(pathToBaseFile)
Calling this function will activate all the aforementioned functions and begin the program
process.
