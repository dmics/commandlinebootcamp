## Command Line Bootcamp

### Nuts and Bolts

During this session you will be introduced to the command line. The
command line is a text based method for interacting with your computer.
There are a great deal of things you can do from the command line, but
for our purposes we’ll just be covering:

-   **Navigation** - moving in and out of directories, figuring out
    where you are, etc.

-   **Creation** - creating folders, moving content around

-   **Manipulation** - reading files, renaming files, and more

In what follows I’ll signal commands you should enter with a '$'
symbol. Only enter the text that comes after the ‘$’. Note that capitalization matters!

Download the following file to your desktop -
[***archive.zip***]@@update this link later@@

For OS X users open the **Terminal** program.

For Windows users, open a program called **Gitbash.**

### Protips

-   You can drag files into the Terminal rather than type out their filepath (think of this like an address to your file)

-   Pressing the up and down arrow will let you recall commands you enter in the Terminal. Think of this like a command history that you can reuse so you don't need to keep retyping that same command.

-   CTRL A - move cursor to the start of the line

-   CTRL D - move cursor to the end of the line

### Navigation & Creation

Generally speaking most of the stuff you interact with on your computer
is organized according to a hierarchical folder structure that is partially obscured through the GUI. When you first start your command line interpreter, you’ll want to find where you are located in that structure.

Find your location in the filesystem using print working directory
**pwd**

`$ pwd`

List the folders and files at your location using list directory **ls**

`$ ls`

Navigate to your Desktop using change directory **cd**

`$ cd Desktop`

List the folders and files on your Desktop **ls**

`$ ls`

Create a project and corpora folder on your Desktop using make
directory **mkdir**

`$ mkdir project`

`$ mkdir corpora`

Move the corpora folder into the project folder using move **mv**

`$ mv corpora project`

Navigate to your corpora folder from your desktop using change
directory **cd**

`$ cd project/corpora`

Navigate up one directory **cd ..**

`$ cd ..`

Navigate to your home directory using change directory **cd**

`$ cd`

Move Archive.zip file into the corpora folder using **mv** and a path

`$ mv Desktop/archive.zip Desktop/project/corpora`

Navigate back down to corpora using **cd** and a path

`$ cd Desktop/project/corpora`

## Manipulation

By this point we’ve figured out how to find our breadcrumbs if we got lost (pwd), and how to figure out what’s around us (ls), how to move up and down levels (cd / cd .. ), how to create new folders, and how to move content into different folders. Now we are going to engage in a bit of basic manipulation of content within the Archive.zip file you downloaded at the beginning of the workshop, currently residing in the corpora folder that you created in the previous section.

Unzip the Archive.zip file in the corpora folder using **unzip**

`$ unzip archive.zip`

`$ ls`

Result:

```
ActoEPoems.htm 
BailJColle.htm 
sevenagesofwoman 
ladyavarie.htm
AddiRPoetr.htm
BailJFamil.htm
iriswmagic.htm
rdme.txt
AikilEpist.htm
LadyAOrigi.htm
ladyaelija.htm
archive.zip
```

You probably don't need that zip anymore get rid of it using remove **rm**

`$ rm archive.zip`

`$ ls`

Result;

```
ActoEPoems.htm
BailJColle.htm
sevenagesofwoman
ladyavarie.htm
AddiRPoetr.htm
BailJFamil.htm
iriswmagic.htm
rdme.txt
AikilEpist.htm
LadyAOrigi.htm
ladyaelija.htm
```

Display the first and last ten lines of a text using **head** / **tail**

`$ head ActoEPoems.htm`

`$ tail ActoEPoems.htm`

Whoops, it looks like you forgot a book. Fix that with **curl**

[Note: The BWRP is temporarily offline, so we’re using a version stored at the Internet Archive\]

`$ curl
https://web.archive.org/web/20170819124439/http://digital.lib.ucdavis.edu:80/projects/bwrp/Works/BannATales.htm`

`$ ls`

Where did that go? It just displayed the file in the Terminal. Direct it to a file with **>**

`$ curl
https://web.archive.org/web/20170819124439/http://digital.lib.ucdavis.edu:80/projects/bwrp/Works/BannATales.htm > BannATales.htm`

`$ ls`

`$ head BannATales.htm`

----

**MAC OS X ONLY:**

That HTML is annoying. Let’s get rid of it with textutil

`$ textutil -convert txt *.htm`

`$ head BannATales.txt`

`$ rm *htm`

`$ ls`
----


rdme.txt is a readme, lets just call it that. rename the file using **mv**

`$ mv rdme.txt readme.txt`

`$ ls`

readme.txt belongs in the project folder, move it up there using **mv**

`$ mv readme.txt ..`

### Optical Character Recognition (OCR)

*Sometimes we get page images, but what we really need is plain text. Tesseract is free OCR software available in lots of languages that can generate text from images at a large scale.*

Navigate to the sevenagesofwoman folder

`$ cd sevenagesofwoman`

List files in the sevenagesofwoman folder

`$ ls`

Convert one tif file to one txt file using Tesseract OCR

`$ tesseract sevenagesofwoman_thebride.tiff sevenagesofwoman_thebride`

Using your GUI, compare the tif file to the txt files you generated

While we’re here, why don’t we just OCR all of them in one batch?

`$ for i in *.tiff ; do tesseract $i $i; done;`

----
*FYI for Windows Users*

Find tesseract.exe (it’s probably in Program Files (x86)) and drag it
in. You can also try the path below and then hunt down the file if it
doesn’t work

`$ '/c/Program Files (x86)/Tesseract-OCR/tesseract.exe' sevenagesofwoman_thebride.tif sevenagesofwoman_thebride`

Using your GUI, compare the tif file to the txt files you generated

While we’re here, why don’t we just OCR all of them in one batch?

`$ for %i in (*.tif) do '/c/Program Files
(x86)/Tesseract-OCR/tesseract.exe' %i %i`

----

### Searching & Mining

Move back to the poetry books

`$ cd ..`

Find out how many lines and words there are in a text of your choosing using **wc -l -w**

`$ wc -l -w ActoEPoems.htm`

Results:

```
3861 15603 ActoEPoems.htm
```

Do some very basic searching with grep

`$ grep europe *htm`

`$ grep Europe *htm`

`$ grep America *htm`

Do some very basic counting with **grep -c**

`$ grep -c man *htm`

`$ grep -c woman \*htm`

Count only whole words using **grep -cw**

`$ grep -cw man *htm`

### Further Resources

[*Sourcecaster*](https://datapraxis.github.io/sourcecaster/)

Idan Kamara, [*Explain Shell*](http://explainshell.com/)

Learn Code The Hard Way, [*Linux Bash Shell Cheat
Sheet*](http://cli.learncodethehardway.org/bash_cheat_sheet.pdf)

Learn Code the Hard Way, [*The
Setup*](http://cli.learncodethehardway.org/book/ex1.html)

Ian Milligan and James Baker, [*Introduction to the Bash Command
Line*](http://programminghistorian.org/lessons/intro-to-bash)
