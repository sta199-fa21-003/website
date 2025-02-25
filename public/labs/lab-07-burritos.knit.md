---
title: "Lab 07: Two-sample inference"
subtitle: "due Wed, Oct 21 at 11:59p"
output: 
  tufte::tufte_html:
    highlight: pygments
    css: "sta199-labs.css"
link-citations: yes
---




# What makes a good burrito?

The goal of today's lab is to practice two-sample statistical inference using
both simulation- and CLT-based approaches.

Use the lecture notes, readings, and application exercises to help you complete the lab. You can also use [this chart on simulation-based inference](sim-inference-chart.png) to help you determine the appropriate sampling scheme when conducting simulation-based inference.

# The Data

Today's dataset has been adapted from Scott Cole's *Burritos of San Diego* 
project, located [**here**](https://srcole.github.io/100burritos/). The goal 
of the project was to identify the best and worst burritos in San Diego, 
characterize variance in burrito quality, and generate predictive models for 
what makes a burrito great. 

As part of this project, 71 participants reviewed burritos from 79 different 
taco shops. Reviewers captured objective measures of the burrito (such as 
whether it contains certain ingredients) and reviewed it on a number of metrics 
(such as quality of the tortilla, the temperature, quality of meat, etc.). For 
the purposes of this lab, you may consider each of these observations to be an
independent, representative sample of all burritos.

The subjective ratings in the dataset are as follows. Each variable is ranked
on a 0 to 5 point scale, with 0 being the worst and 5 being the best. 

- `tortilla`: quality of the tortilla
- `temp`: temperature of the burrito
- `meat`: quality of the meat
- `fillings`: quality of non-meat fillings
- `salsa`: quality of the salsa
- `mfr`: meat-to-filling ratio
- `uniformity`: whether each bite contains a uniform slew of ingredients (e.g.,
a bite entirely composed of tortilla and sour cream would probably be terrible)
- `synergy`: how well it all comes together

In addition, the reviewers noted the presence of the following burrito
components. Each of the following variables is a binary variable taking on 
values `present` or `none`:

- `guac`: guacamole
- `cheese`: cheese
- `fries`: fries (it's a thing, [look it up.](https://en.wikipedia.org/wiki/Burrito#San_Diego))
- `sourcream`: sour cream
- `rice`: rice
- `beans`: beans

The data for today's lab may be found by cloning your repository available at 
the class GitHub repository. Load the data into your RStudio environment, and
don't forget to configure GitHub beforehand.

To following resource provides code needed to make useful symbols. You may use
the code to typeset the characters of interest in the *narrative* of your
document:

- $\mu$: `$\mu$`
- $\alpha$: `$\alpha$`
- $\ge$: `$\ge$`
- $\le$: `$\le$`
- $\neq$: `$\neq$`
- $H_0$: `$H_0$`
- $H_a$: `$H_a$`


# Exercises

**At the start of each exercise that requires simulation, set a random seed**
**equal to the exercise number in the R chunk.**

1. Sour cream on burritos: yay or nay? Explain.
2. Suppose you are worried that the presence of sour cream adversely affects the 
perceived temperature of the burrito. Comprehensively evaluate the hypothesis 
that the mean temperature of burritos with sour cream is lower than burritos 
without sour cream using a simulation-based approach.
3. Construct and interpret a 95% two-sided confidence interval for the 
difference you investigated in Exercise 1 using a simulation-based approach. 
4. Now suppose you are worried that sour cream adversely affects the perceived
*uniformity* of the burrito. Comprehensively evaluate the hypothesis that
the mean uniformity of burritos with sour cream is less than burritos without 
sour cream using a CLT-based approach.
5. Construct and interpret a a 95% two-sided confidence interval for the 
difference you investigated in Exercise 4 using a CLT-based approach.
6. Suppose you perform 10 independent hypothesis tests at the $\alpha = 0.05$
level, and further suppose that in reality, the null hypothesis is TRUE for all
10 tests. What is the probability that you make at least one type 1 error?
7. Let's say you just really hate sour cream and are trying to demonstrate to
others that it's associated with lower rating scores for tortilla quality,
salsa quality, meat-to-filling ratio, uniformity, synergy, etc. Describe the
potential ethical ramifications of performing all of these tests and reporting
only the significant results from the tests that support your narrative. 
Consider your answer from Exercise 6 in crafting this narrative.
8. Create a new variable for overall burrito quality by taking the average
scores for all ratings (tortilla quality, temperature, meat quality, etc.) in
the dataset. Is there evidence that burritos with guacamole have a different
average overall perceived quality score compared to burritos without guacamole?
Comprehensively evaluate this hypothesis using any method of your choice.
9. In the previous analyses, we've treated these variables as numeric variables.
Evaluate the merits of this approach: is it appropriate? Could it potentially be
misleading?
10. The San Diego burrito is known for including fries in it (as a convenient
way for surfers to top off their energy in a quick, convenient, and tasty 
format). Create a new categorical variable for overall burrito quality (from 
Exercise 8) under the following scheme, and comprehensively evaluate whether
there is a relationship between this variable and whether the burrito has fries:
- Overall burrito quality $\le$ 3: `alright`
- Overall burrito quality $>$ 3 and $\le 4$: `solid`
- Overall burrito quality $>$ 4: `whoa!`



# Submission

Knit to PDF to create a PDF document. Knit and commit all remaining changes, 
and push your work to GitHub. Make sure all files are updated on your GitHub 
repo.

Please only upload your PDF document to Gradescope. Associate the "Overall"
graded section with the first page of your PDF, and mark where each answer is 
to the exercises. If any answer spans multiple pages, then mark all pages.
