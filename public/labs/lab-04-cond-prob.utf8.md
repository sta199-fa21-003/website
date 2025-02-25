---
title: "Lab 04: Examining smoking and health outcomes"
subtitle: "due Wed, Sep 16 at 11:59p"
output: 
  tufte::tufte_html:
    tufte_variant: "envisioned"
    highlight: pygments
    css: "./sta199-labs.css"
    toc: true
    toc_depth: 1
link-citations: yes
---



# Introduction 

The goal of today's lab is to practice visualizing and calculating probabilities using the tidyverse. Before we get to that, however, we will look at something that may happen as you collaborate with your lab team (or any other team!) in GitHub.

# Merge Conflicts (uh oh)


<p><span class="marginnote shownote">
<!--
<div class="figure">-->
<img src="img/04/merge-no-conflict.png" alt=" " width="1052"  />
<!--
<p class="caption marginnote">--> <!--</p>-->
<!--</div>--></span></p>

You may have seen this already through the course of your collaboration last 
week in Lab 03. When two collaborators make changes to a file and push the file 
to their repository, git merges these two files.

<p><span class="marginnote shownote">
<!--
<div class="figure">-->
<img src="img/04/merge-conflict.png" alt=" " width="1052"  />
<!--
<p class="caption marginnote">--> <!--</p>-->
<!--</div>--></span></p>


If these two files have conflicting content on the same line, git will produce a
**merge conflict**. Merge conflicts need to be resolved manually, as they require a human 
intervention:

<img src="img/04/merge-conflict-identifiers.png" width="1172"  />

To resolve the merge conflict, decide if you want to keep only your text, the 
text on GitHub, or incorporate changes from both texts. Delete the conflict 
markers `<<<<<<<`, `=======`, `>>>>>>>` and make the changes you want in the 
final merge.

**Assign numbers 1, 2, 3, and 4 to each of your team members** (if only 3 team 
members, just number 1 through 3). Go through the following steps in detail, 
which simulate a merge conflict. Completing this exercise will be part of the 
lab grade.

## Resolving a merge conflict

**Step 1: Everyone** clone the **lab-04-whickham** assignment repo in RStudio and open file **merge-conflict.Rmd**. Don't forget to configure git if you haven't already done so:


```r
library(tidyverse) 
library(usethis)
use_git_config(user.name="your github username", user.email="your email")
```

**Member 4** should look at the group’s repo on GitHub.com to ensure that the other 
members’ files are pushed to GitHub after every step.

**Step 2: Member 1** Change the team name to your team name. *Knit, commit, and push*.

**Step 3: Member 2** Change the team name to something different (i.e., not your
team name). *Knit, commit, and push*. 

You should get an error.

**Pull** and review the document with the merge conflict. Read the error to your teammates. You can also show them the error by sharing your screen. A merge conflict occurred because you edited the same part of the 
document as Member 1. Resolve the conflict with whichever name you want to keep,
then knit, commit and push again.

**Step 4: Member 3** Write some narrative in the space provided. You should get an error.

This time, no merge conflicts should occur, since you edited a different part of
the document from Members 1 and 2. Read the error to your teammates. You can also show them the error by sharing your screen. 

Click to pull.  *Then, knit, commit, and push.*

# Packages

In this lab we will work with the `tidyverse` and `mosaicData` packages.


```r
library(tidyverse) 
library(mosaicData) 
```

Note that these packages are also loaded in your R Markdown document.

# The data

Today's data comes from a study of conducted in Whickham, England. In this study, the researchers recorded each participant's age, smoking status at the start of the study, and their health outcome 20 years later. 

The data is in the `mosaicData` package. You can load it with


```r
data(Whickham)
```

Take a peek at the codebook with


```r
?Whickham
```


# Exercises

**Write all R code according to the style guidelines discussed in class.** Be
especially careful about staying within the 80 character limit, as demonstrated 
by your lab TAs! Finally, make sure your team name is correct. *Only one* 
submission should be made per team.

**All team members must commit and push to receive full credit.**

1. How many observations are in this dataset? What does each observation 
   represent?

1. How many variables are in this dataset? What type of variable is each? 
   Display each variable using an appropriate visualization.
   
1. What would you expect the relationship between smoking status and health outcome to be?

1. Create a visualization depicting the relationship between smoking status and health outcome.

1. Calculate the conditional probabilities of health outcome for each smoking status. Briefly describe the relationship, and evaluate whether or not it is what you expected. Use the visualization from the previous exercise and the conditional probabilities to support your narrative.  

1. Create a new variable called `age_cat` using the following scheme:

    - `age <= 44 ~ "18-44"`
    - `age > 44 & age <= 64 ~ "45-64"`
    - `age > 64 ~ "65+"`

1. Re-create the visualization from Exercise 4, this time faceting by `age_cat`.


1. Extend the table from Exercise 5 by breaking it down by age category. 

1. Compare the visualization from Exercise 7 and the table from Exercise 8 to what you previously observed in Exercises 4 and 5. What changed, and what might explain the change? Use the table you calculated in Exercise 8 to support your narrative. 

# Submission

Knit to PDF to create a PDF document. Knit and commit all remaining changes, 
and push your work to GitHub. Make sure all files are updated on your GitHub 
repo.

Please only upload your PDF document to Gradescope. Associate the "Overall"
graded section with the first page of your PDF, and mark where each answer is 
to the exercises. If any answer spans multiple pages, then mark all pages.

<br> 

<hr> 


*This lab was adapted from [Data Science in a Box](https://datasciencebox.org).*


