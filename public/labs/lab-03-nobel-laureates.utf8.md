---
title: "Lab 03 - Nobel laureates"
output: 
  tufte::tufte_html:
    tufte_variant: "envisioned"
    highlight: pygments
    css: "./sta199-labs.css"
    toc: true
    toc_depth: 2
link-citations: yes
---



# Meet your team! 

See [STA 199 Teams](https://prodduke-my.sharepoint.com/:x:/g/personal/mt324_duke_edu/EWHnLjejWF5Ghwj_Vk59nZ0BwG4drTrwwAjo7Hw996V10Q?e=KnVbbn) to see your team assignment. This will be your team for labs and the final project. 

Before you get started on the lab assignment, we will take a few minutes to help you develop a plan for working as a team. 

✅ Come up with a team name. I encourage you to be creative! Your TA will get your team name by the end of lab. 

✅ Identify something everyone on the team has in common that's not necessarily in common with everyone else in the class. 

✅ Fill out the team agreement. This will help you figure out a plan for working together during labs and outside of lab times. You can find the team agreement in the GitHub repo **team-agreement-[github_team_name]**. 
  
  - Have **one person** from the team clone the repo and start a new RStudio project. This person will type the team's responses as you discuss the sections of the agreement. Share your screen, if possible, so the rest of the team can see the updates. No one else in the team should type at this point but should be contributing to the discussion.
  - Be sure to push the completed agreement to GitHub. Each team member can refer to the document in this repo or download the PDF of the agreement for future reference.
  
# Lab 03

In January 2017, Buzzfeed published an article titled ["These Nobel Prize Winners Show Why Immigration Is So Important For American Science"](https://www.buzzfeednews.com/article/peteraldhous/immigration-and-science). In the article they explore where many Nobel laureates in the sciences were born and where they lived when they won their prize.

In this lab we will work with the data from this article to 
recreate some of their visualizations as well as explore new questions.

The learning goals of this lab are:

- Manipulate and transform data to prepare it for visualization.
- Recreate visualizations.
- Summarize data.
- Practice working on a team.

## Clone assignment repo + start new project

A repository has already been created for you and your teammates. Everyone in your team has access to the same repo.

- Go to [course organization](https://www.github.com/sta199-fa20-002) on GitHub.

- In addition to your private individual repositories, you should now see a repo named lab-03-nobel-[github_team_name]. Go to that repository.
  
- Each person on the team should clone the repository and open a new project in RStudio. **Do not make any changes to the .Rmd file until the instructions tell you do to so.**

## Workflow: Using git and GitHub as a team

**Assign each person on your team a number 1 through 4. For teams of three, Member 1 can take on the role of Member 4.**

The following exercises must be done in order. **Only one person should type in the .Rmd file and push updates at a time.** When it is not your turn to type, you should still share ideas and contribute to the team's discussion.

## Update YAML 

**Team Member 1: Change the author to your team name and include each team member's name in the `author` field of the YAML in the following format. `Team Name: Member 1, Member 2, Member 3, Member 4`.**


## Packages

We'll use the **tidyverse** package for this analysis. Run the following code in the Console to load this package.


```r
library(tidyverse)
```

## The data

The dataset for this assignment can be found as a csv file in the `data` folder of your repository. You can read it in using the following.


```r
nobel <- read_csv("data/nobel.csv")
```

The variable descriptions are as follows:

- `id`: ID number
- `firstname`: First name of laureate
- `surname`: Surname 
- `year`: Year prize won
- `category`: Category of prize
- `affiliation`: Affiliation of laureate
- `city`: City of laureate in prize year
- `country`: Country of laureate in prize year
- `born_date`: Birth date of laureate
- `died_date`: Death date of laureate
- `gender`: Gender of laureate
- `born_city`: City where laureate was born
- `born_country`: Country where laureate was born
- `born_country_code`: Code of country where laureate was born
- `died_city`: City where laureate died
- `died_country`: Country where laureate died
- `died_country_code`: Code of country where laureate died
- `overall_motivation`: Overall motivation for recognition
- `share`: Number of other winners award is shared with
- `motivation`: Motivation for recognition

In a few cases the name of the city/country changed after prize was given (e.g. in 1975 Bosnia and Herzegovina was part of the Socialist Federal Republic of Yugoslavia). In these cases the variables below reflect a different name than their counterparts without the suffix `_original`.

- `born_country_original`: Original country where laureate was born
- `born_city_original`: Original city where laureate was born
- `died_country_original`: Original country where laureate died
- `died_city_original`: Original city where laureate died
- `city_original`: Original city where laureate lived at the time of winning the award
- `country_original`: Original country where laureate lived at the time of winning the award

## Exercises

### Get to know your data

<div class = "commit">
<b>Team Member 1</b>: Type the team's responses to exercises 1 and 2.
</div>

1. How many observations and how many variables are in the dataset? Use inline code to answer this question.

There are some observations in this dataset that we will exclude from our analysis to match the Buzzfeed results.

2. Create a new data frame called `nobel_living` that filters for
  - laureates for whom `country` is available
  - laureates who are people as opposed to organizations (organizations are denoted with `"org"` as their `gender`)
  - laureates who are still alive (their `died_date` is `NA`)
  
Confirm that once you have filtered for these characteristics you are left with a data frame with 228 observations.

<div class = "commit">
✅ ⬆️ <b>Team Member 1</b>: Knit, commit and push your changes to GitHub with an appropriate commit message again. Make sure to commit and push all changed files so that your Git pane is cleared up afterwards.

</b>All other team members</b>: <b>Pull</b> to get the updated documents GitHub. Click on the .Rmd file, and you should see the responses to exercises 1 and 2. **

<b>Team Member 2</b>: It's your turn! Type the team's response to exercise 3.
</div>

### Most living Nobel laureates were based in the US when they won their prizes

... says the Buzzfeed article. Let's see if that's true.

First, we'll create a new variable to identify whether the laureate was in the US when they won their prize. We'll use the `mutate()` function for this. The following pipeline mutates the `nobel_living` data frame by adding a new variable called `country_us`. We use an if/else statement to create this variable. The first argument in the `if_else()` function is the condition we're testing for. If `country` is equal to `"USA"`, we set `country_us` to `"USA"`. If not, we set the `country_us` to `"Other"`.

<label for="tufte-mn-" class="margin-toggle">&#8853;</label><input type="checkbox" id="tufte-mn-" class="margin-toggle"><span class="marginnote"><span style="display: block;">Note that we can achieve the same result using the <code>fct_other()</code> function (i.e. with <code>country_us = fct_other(country, "USA")</code>).</span></span>


```r
nobel_living <- nobel_living %>%
  mutate(
    country_us = if_else(country == "USA", "USA", "Other")
  )
```

Next, we will limit our analysis to only the following categories: Physics, Medicine, Chemistry, and Economics.


```r
nobel_living_science <- nobel_living %>%
  filter(category %in% c("Physics", "Medicine", "Chemistry", "Economics"))
```

For the next exercise work with the `nobel_living_science` data frame you created above. This means you'll need to define this data frame in your R Markdown document, even though the next exercise doesn't explicitly ask you to do so.

3. Create a faceted bar plot visualizing the relationship between the category of prize and whether the laureate was in the US when they won the nobel prize. Note: Your visualization should be faceted by category. For each facet you should have two bars, one for winners in the US and one for Other. Flip the coordinates so the bars are horizontal, not vertical. Interpret your visualization, and say a few words about whether the Buzzfeed headline is supported by the data.

<div class = "commit">
✅ ⬆️ <b>Team Member 2</b>: Knit, commit and push your changes to GitHub with an appropriate commit message again. Make sure to commit and push all changed files so that your Git pane is cleared up afterwards.*

<b>All other team members</b>: <b>Pull</b> to get the updated documents GitHub. Click on the .Rmd file, and you should see the responses to exercise 3. 

<b>Team Member 3</b>: It's your turn! Type the team's response to exercises 4 - 5.
</div>


### But of those US-based Nobel laureates, many were born in other countries

<label for="tufte-mn-" class="margin-toggle">&#8853;</label><input type="checkbox" id="tufte-mn-" class="margin-toggle"><span class="marginnote"><span style="display: block;"><strong>Hint:</strong> You should be able to <del>cheat</del> borrow from code you used earlier to create the <code>country_us</code> variable.</span></span>

4. Create a new variable called `born_country_us` that has the value `"USA"` if the laureate is born in the US, and `"Other"` otherwise.

5. Add a second variable to your visualization from Exercise 3 based on whether the laureate was born in the US or not. Your final visualization should contain a facet for each category, within each facet a bar for whether they won the award in the US or not, and within each bar whether they were born in the US or not. Based on your visualization, do the data appear to support Buzzfeed's claim? Explain your reasoning in 1-2 sentences.

<div class = "commit">

✅ ⬆️ <b>Team Member 3</b>: Knit, commit and push your changes to GitHub with an appropriate commit message again. Make sure to commit and push all changed files so that your Git pane is cleared up afterwards.

<b>All other team members</b>: <b>Pull</b> to get the updated documents GitHub. Click on the .Rmd file, and you should see the responses to exercises 4 and 5. 

<b>Team Member 4</b>: It's your turn! Type the team's response to exercise 6.
</div>


### Here’s where those immigrant Nobelists were born

<label for="tufte-mn-" class="margin-toggle">&#8853;</label><input type="checkbox" id="tufte-mn-" class="margin-toggle"><span class="marginnote"><span style="display: block;">Note that your bar plot won’t exactly match the one from the Buzzfeed article. This is likely because the data has been updated since the article was published.</span></span>

6. In a single pipeline, filter for laureates who won their prize in the US, but were born outside of the US, and then create a frequency table (with the `count()`) function for their birth country, `born_country`, and arrange the resulting data frame in descending order of number of observations for each country.

<div class = "commit">
✅ ⬆️ <b>Team Member 4</b>: Knit, commit and push your changes to GitHub with an appropriate commit message again. Make sure to commit and push all changed files so that your Git pane is cleared up afterwards.

<b>All other team members</b>: <b>Pull</b> to get the updated documents GitHub. Click on the .Rmd file, and you should see the team's completed lab!
</b>


## Wrapping up

Go back through your write up to make sure you followed the coding style guidelines we discussed in class (e.g. no long lines of code).
 
Also, make sure all of your R chunks are properly labeled, and your figures are reasonably sized.


<b>Team Member 2:</b> Make any edits as needed. Then knit, commit, and push the updated documents to GitHub if you made any changes. 

All other team members can click to pull the finalized document. 

## Submission 

<b>Team Member 3<?b>: Upload the team's PDF to Gradescope. Be sure to include every team member's name in the Gradescope submission Associate the "Overall" graded section with the first page of your PDF, and mark where each answer is  to the exercises. If any answer spans multiple pages, then mark all pages.

There should only be **<u>one</u>** submission per team on Gradescope. 

## Interested in how Buzzfeed made their visualizations?

The plots in the Buzzfeed article are called waffle plots. You can find the code used for making these plots in Buzzfeed's GitHub repo (yes, they have one!) [here](https://buzzfeednews.github.io/2017-01-immigration-and-science/). You're not expected to recreate them as part of your assignment, but you're welcomed to do so for fun!
© 2020 GitHub, Inc.


<hr> 

*This lab was adapted from [Data Science in a Box](https://datasciencebox.org).*

