## Command Line Bootcamp

*Original slides and activity were developed by Thomas Padilla and have been lightly altered*

### Introduction
[Slides here](https://docs.google.com/presentation/d/1ikyXzrrbHEa9JUi14quuGZFMnEkye8tNtKaCVYJawAw/edit?usp=sharing)

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

[Note: The BWRP is temporarily offline, so we’re using a version stored at the Internet Archive]

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

## Searching & Mining

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

`$ grep -c woman *htm`

Count only whole words using **grep -cw**

`$ grep -cw man *htm`

## Creating a Loop
You're going to combine this collection with texts from other sources, and you want to remember that you got these from UC Davis's BWRP (British Women Romantic Poets) project. Why don't we add 'bwrp' to the beginning of each filename? Hit enter after each line:

*first, we'll take a look at the way a loop works*

`$ for file in *.htm`    we're making "file" a variable that carries each file ending in .htm through the loop
`$ do`                   we're setting a list of instructions for each file
`$ print $file`          [**type the $s within the line**] the `$` is used to access the value of the variable - it's just printing the filename
`$done`                  this signals that we're done with the code and it can all run.

*now let's rename the files

`$ for file in *.htm`
`$ do`                   
`$ mv $file bwrp_$file`  this renames each file with 'bwrp_' followed by the filename it had already
`$done`


## Further Resources

[*Sourcecaster*](https://datapraxis.github.io/sourcecaster/)

Library Carpentry. [Shell Lessons for Librarians](https://librarycarpentry.github.io/lc-shell/)

Idan Kamara, [*Explain Shell*](http://explainshell.com/)

Learn Code The Hard Way, [*Linux Bash Shell Cheat
Sheet*](http://cli.learncodethehardway.org/bash_cheat_sheet.pdf)

Learn Code the Hard Way, [*The
Setup*](http://cli.learncodethehardway.org/book/ex1.html)

Ian Milligan and James Baker, [*Introduction to the Bash Command
Line*](http://programminghistorian.org/lessons/intro-to-bash)
