# R Markdown {#rmarkdown}

What is R Markdown: https://vimeo.com/178485416 created by RStudio

R Markdown documents consist of three components.

* Code Chunks
* Text
* YAML Metadata



## What is R Markdown and R Notebook

R Markdown provides an authoring framework for data science. You can use a single R Markdown file to both

* save and execute code
* generate high quality reports that can be shared with an audience

R Notebooks are an implementation of Literate Programming that allows for direct interaction with R while producing a reproducible document with publication-quality output.

An **R Notebook** is an R Markdown document _with chunks that can be executed independently and interactively, with output visible immediately beneath the input_.

(Reference: [R Markdown: The Definitive Guide, 3.2 Notebook](https://bookdown.org/yihui/rmarkdown/notebook.html))



### Two Goodies

* **Important**: Implementation of Reproducible Research and Literate Programming

* **Useful** to Render into Various Formats: R Notebook (HTML), R Markdown (HTML), PDF, MS Word, MS Powerpoint, Ioslides Presentation (HTML), Slidy Presentation (HTML), Beamer Presentation (PDF), etc.



## Reproducible Research and Literate Programming

### Literate Programming by D. Knuth

Literate programming is an approach to programming introduced by Donald Knuth in which a program is given as an explanation of the program logic in a natural language, such as English, interspersed with snippets of macros and traditional source code, from which a compilable source code can be generated.

### [D. Knuth](https://www.brainyquote.com/quotes/donald_knuth_181634)
Let us change our traditional attitude to the construction of programs: Instead of imagining that our main task is to instruct a computer what to do, let us concentrate rather on explaining to human beings what we want a computer to do.



### Reproducible Research - Quote from a [Coursera Course](https://www.coursera.org/learn/reproducible-research)

Reproducible research is the idea that data analyses, and more generally, scientific claims, are published with their data and software code so that others may verify the findings and build upon them.  The need for reproducibility is increasing dramatically as data analyses become more complex, involving larger datasets and more sophisticated computations. Reproducibility allows for people to focus on the actual content of a data analysis, rather than on superficial details reported in a written summary. In addition, reproducibility makes an analysis more useful to others because the data and code that actually conducted the analysis are available. 



### R Markdown workflow, [R for Data Science](https://r4ds.had.co.nz/r-markdown-workflow.html#r-markdown-workflow)

R Markdown is also important because it so tightly integrates prose and code. This makes it a great analysis notebook because it lets you develop code and record your thoughts. It:

* Records what you did and why you did it. Regardless of how great your memory is, if you don’t record what you do, there will come a time when you have forgotten important details. Write them down so you don’t forget!

* Supports rigorous thinking. You are more likely to come up with a strong analysis if you record your thoughts as you go, and continue to reflect on them. This also saves you time when you eventually write up your analysis to share with others.

* Helps others understand your work. It is rare to do data analysis by yourself, and you’ll often be working as part of a team. A lab notebook helps you share why you did it with your colleagues or lab mates.



### Records of EDA and Communication

1. Memo on a scratch paper: R Scripts
2. Record on a notebook: R Notebook (an R Markdown format)
3. Short paper or a digital communication: R Notebook
3. Paper or a report: R Markdown (html, pdf, MS Word, etc.)
4. Presentation (html, pdf, MS Powerpoint, etc.)
5. Publication of a Book
  * [BOOKDOWN: Write HTML, PDF, ePub, and Kindle books with R Markdown](https://bookdown.org). Free online document is provided in [pdf as well](https://bookdown.org/yihui/rmarkdown/rmarkdown.pdf)
  - [Arxive Page](https://bookdown.org/home/archive/) 



## Let's Get Started

1. Start R Studio - _Update R Studio if old_
2. Create a Project
3. Tool > Install Packages `rmarkdown`
    * Or on Console: `install.packages("rmarkdown")`
4. Tool > Install Packages `tinytex` (for pdf generation)
    * Alternatively, `install.packages('tinytex')`
    * If TeX is not installed: `tinytex::install_tinytex()`  \# install TinyTeX
      - If you are not sure, please check on `Terminal` in the left below pane: 
        + which latex, which mktexlsr - Mac or Linux
        + where mktexlsr - Windows
5. Let's try!  
    a. File > New File > R Notebook
    b. Save with a file name, say, test-notebook
    c. Preview by [Preview] button
    d. Run Code Chunk `plot(cars)` and then Preview again.
    e. Knit PDF, Word (and HTML)



## Templates

### RNotebook_Template

Template to submit your assignment of this course: [`RNotebook_Template.nb.html`](https://icu-hsuzuki.github.io/da4r2022_note/RNotebook_Template.nb.html)

```
title: "Title of R Notebook"
author: "ID and Your Name"
date: "2023-12-04" 
output:
  html_notebook: null
```


#### YAML

* Change the title
* Write ID and your name
* Date is auto-generated and inserted. If you wish, you can replace "2023-12-04" by your favorite date style.



#### Code Chunk

* When you execute or run a code within the notebook, the results appear beneath the code.
* Try executing this chunk by clicking the Run button, a triangle pointing right, within the chunk or by placing your cursor inside it and pressing Ctrl+Shift+Enter (Win) or Cmd+Shift+Enter (Mac).
  - Ctrl + Shift + Enter (Windows) or Cmd + Shift + Enter (Mac): Runs the current code chunk and advances to the next one.
  - Ctrl + Alt + C (Windows) or Cmd + Option + C (Mac): Runs all the code chunks in the document.
* Add a new chunk by clicking the Insert Chunk button on the toolbar or by pressing Ctrl+Option+I (Win) or Cmd+Option+I (Mac).
* When you save the notebook, an HTML file containing the code and output will be saved alongside it (click the Preview button or press Ctrl+Shift+K (Win) or Cmd+Shift+K (Mac) to preview the HTML file).
* The preview shows you a rendered HTML copy of the contents of the editor. Consequently, unlike Knit, _Preview does not run any R code chunks. Instead, the output of the chunk when it was last run in the editor is displayed_.
* We will use the pipe command `%>%` very often later in this class.
  - The shortcut for the pipe operator (%>%) in Rmarkdown on Windows and Mac OS is:
    + On Windows: Ctrl + Shift + M
    + On Mac OS: Cmd + Shift + M

### Testing R Markdown Formats

Various Output Formats: [`test-rmarkdown.nb.html`](https://icu-hsuzuki.github.io/da4r2022_note/test-rmarkdown.nb.html)

```
title: "Testing R Markdown Formats"
author: "DS-SL"
date: "2023-12-04"
output:
  html_notebook:
    number_sections: yes
  pdf_document: 
    number_sections: yes
  html_document:
    df_print: paged
    number_sections: yes
  word_document: 
    number_sections: yes
  powerpoint_presentation: default
  ioslides_presentation:
    widescreen: yes
    smaller: yes
  slidy_presentation: default
  beamer_presentation: default
```

### Comments on Presentation Formats and Options

* For slides, a new slide starts at \#\#, the second-level heading.
* `---` is page break for presentation formats.
* For Word and Powerpoint, you can add your template. See the documents in References
  - Use R Markdown to create a Word document [similar for PowerPoint]
  - Save the rendered Word file as: `ref-doc-style.docx`
  - Edit the styles of the file `ref-doc-style.docx`
  - Add `ref-doc-style.docx` as reference_doc in YAML with indention as below

```
  word_document: 
    number_sections: yes
    reference_doc: ref-doc-style.docx
  powerpoint_presentation: 
    reference_doc: ref-ppt-style.pptx
```

* You can use `Output Options` at the bottom of the gear icon next to Preview/knit button.



## Markdown Language -- or use WYSIWYG editor

* Headers: \#, \#\#, \#\#\#, \#\#\#\#
* Lists: 1. 2. \ldots, * 
* Links: [linked phrase](http://example.com)
* Images: `![alt text](figures/filename.jpg)`
* Block quotes" > (block) 
* \LaTeX\  equations: e.g. `$\frac{a}{b}$` for $\frac{a}{b}$
* Horizontal rules: Three or more asterisks or dashes (*** or  - - - )
* Tables
* Footnotes
* Bibliographies and Citations
* Slide breaks
* _Italicized text_ by `_italic_`, **Bold text** by `**bold**`
* Superscripts, Subscripts, Strikethrough text



### Visual R Markdown

>R Studio introduced Visual Editor towards the end of 2021. It seems to be stable but it is not perfect to go back and forth from the original editor using tags. I always use the original editor and I am confident on all the functions of it but I do not have much experience on Visual Editor. [My Note in QALL401 2021]

Please refer to the document in the following link. You can switch between the `Source` editor and the `Visual` editor using the button on the top left pane's left top corner. The document below is a bit old, and the switch button is shown at the top right corner of the top left pane.

  * https://rstudio.github.io/visual-markdown-editing/



## References

* Posit Primers: [Report Reproducibly](https://rmarkdown.rstudio.com/lesson-1.html?_ga=2.60708591.317621277.1671142614-2004472742.1671142614)
* Markdown Quick Reference: Top Menu Bar \> Help \> Markdown Quick Reference
* Cheat Sheet (Top Menu Bar: Help \> Cheat Sheets): RMarkdown Cheat Sheet, RMarkdown Reference Guide
* Books:
  - In Textbook: [R for Data Science: Communicate](https://r4ds.had.co.nz/communicate-intro.html#communicate-intro)
  - [R Markdown: The Definitive Guide](https://bookdown.org/yihui/rmarkdown/) by Yihui Xie, J. J. Allaire, Garrett Grolemund
  - [R Markdown Cookbook](https://bookdown.org/yihui/rmarkdown-cookbook/) by Yihui Xie, Christophe Dervieux, Emily Riederer
* Markdown: R Markdown is based on the Markdown language of Pandoc
  - [Pandoc's Markdown](https://pandoc.org/MANUAL.html#pandocs-markdown): Detailed Information
  - [Markdown Tutorials](https://www.markdowntutorial.com): Interactive Practicum
  - [DARING FIREBALL: Markdown](https://daringfireball.net/projects/markdown/) (detailed explanation and editor as Dingus)
* Post error messages to a web search engine.



