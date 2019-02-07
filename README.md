---
title: Markdown to PDF Conversion Test File
#subtitle: Something so you can see what a lot of the formatting will look like
author: Craig Parker (that's Pahkah in Maine)
email: <craig@fossfolks.com>
subject: A markdown file, pandoc command, LaTeX template, and resulting PDF containing all the formatting scenarios I could think of.
keywords:
date: \today{}
---

## General notes

This README actually doubles as a PDF guinea pig. I used to to test every scenario I could think of, making PDF files from it as I went. It's also got instructions about how to get the whole process up and going, at least on a Linux machine or a Mac. I've not tested on Windows yet, but it probably isn't that difficult.

The funky stuff you see up at the beginning of this file actually translates into different things in the final document, mostly on the title page.

## How to

Getting the environment set up involves installing a few packages. I've tested on Ubuntu and MacOS in Ubuntu, but the package names should be similar on different operating systems. Here's how I got the environment set up on my own machine.

### Installing software

#### On Ubuntu

Grab Pandoc from Github. I started at 2.3.1, but was at 2.5.1 by the time I got done:  
```
sudo dpkg -i <DOWNLOADED PANDOC FILE>.deb
```

Then get LaTeX installed:  
```
sudo apt-get install texlive texlive-xetex texlive-fonts-recommended texlive-fonts-extra \  
texlive-font-utils
```

#### On a Mac

##### Homebrew  

  1. If Homebrew is NOT installed yet:  
  ```
    /usr/bin/ruby -e "$(curl -fsSL \  
    https://raw.githubusercontent.com/Homebrew/install/master/install)"   
  ```  

  2. If Homebrew IS installed:  

      ```
      brew update
      ```  

##### Pandoc  

  - Install Pandoc with Brew:  
      ```
      brew install pandoc
      ```

### Templates

Templates sit in the, you guessed it, `templates` directory. It's in the same level of the file tree as this markdown file. Put it wherever you want, just remember to alter the `pandoc` command when you run it.

### Fonts
In the same directory as wherever we've got `templates`, there's a `fonts` directory. Set which fonts you want to use in the LaTex template, then make sure the font files themsleves are sitting in that fonts directory. I've included an open source font (IBM Plex) with this package.


### Running pandoc

Commands are all going to be run like this:  
```
pandoc -s --template="./templates/template.latex" markdown_file.md --pdf-engine=xelatex \
-o pdf_file.pdf
```

Here, replace markdown_file.md and pdf_file.pdf with whatever actual filenames you're dealing with. Now that I've used this a bit, I tend to find the markdown in whoever's folder, then dump the PDF locally until I'm done.

## Headings

The biggest heading I've used is the LaTex equivalent of an HTML h2. I realize that I can use h1, but I also copyedit things on blogs, and h1 there is already being used as a title. I can't use it.

  - Bulleted List
    - There's a way to do this with things besides bullets (Roman numerals, numbers, capital and lowercase letters, numbers, etc) but I just need bullets, so here they are.
    - There is also a way to get other charcters, like textopenbullet, but I haven't found a font yet that contains it. Use textbullet, and experiment from there, using the Great Big List of LaTeX Symbols I've included in the `help_stuff` directory.
  - Another point
    - Level 2
      - Level 3
        - Level 4
          - Level 5
            - Level 6
              - Level 7
                - Level 8
                  - Level 9
  - A third point
    - Sub-bullet
      - Another one
    - Sub-bullet 2
  - A fourth point  

And a link will look like [this link](http://fossfolks.com)

## H2

LaTeX calls it the thesubsection

### H3  

LaTeX calls it the thesubsubsection

#### H4  

LaTeX calls it the theparagraph

##### H5  

LaTeX calls it the thesubparagraph  

***Beware the last two*** -- if you don't have a newline after them, it will crap out with an error. I believe it's because I'm dorking with them a little later in the template. They were, by default, having the following text show up on the same line. I fixed that with the makeatletter section, but that must somehow break things a bit so that you need the empty line in markdown between the heading and the following text.  

It's easier to read the markdown with the empty line, so I didn't get too worried about it.

---


## Block quotes


> This is a block quote Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
>> And this is nested blockquote.

> ##### This is an H5 type header, inside a quote, with a quoted list under it:
>
> 1.   This is the first list item.
> 2.   This is the second list item.
>
> Here's some example code (four spaces):
>
>     return shell_exec("echo $input | $markdown_script");
>
> And then some more with three backticks
>
>```
>return shell_exec("echo $input | $markdown_script");
>```

## Tables

### Table 1 (LaTex with booktabs package)  

\begin{table}[h!]
\centering
 \begin{tabular}{|c|r|c|r|}
 \hline
 \textbf{Password} & \multicolumn{1}{c|}{\textbf{Base}} & \textbf{Length} & \multicolumn{1}{c|}{\textbf{Combinations}} \\ \hline
 password          & a-z    26                          & 8               & 208,827,064,576                            \\ \hline
 Password          & a-z,A-Z    52                      & 8               & 53,459,728,531,456                         \\ \hline
 Passw0rd          & a-z,A-Z,0-9    62                  & 8               & 218,340,105,584,896                        \\ \hline
 P@ssw0rd          & a-z,A-Z,0-9,@    94                & 8               & 6,095,689,385,410,816                      \\ \hline
 P@s5              & a-z,A-Z,0-9,@     94               & 4               & 78,074,896                                 \\ \hline
 \end{tabular}
\end{table}  

\  

\  

### Table 2 (just markdown with longtable package)  

| **Password** | **Base** | **Length** | **Combinations** |
|--------|------|------|------|
| password | a-z 26 | 8 | 208,827,064,576 |
| Password | a-z,A-Z  52 | 8 | 53,459,728,531,456 |
| Passw0rd | a-z,A-Z,0-9 62 | 8 | 218,340,105,584,896 |
| P@ssw0rd | a-z,A-Z,0-9,@ 94 | 8 | 6,095,689,385,410,816   |
| P@s5 | a-z,A-Z,0-9,@ 94 | 4 | 78,074,896   |
