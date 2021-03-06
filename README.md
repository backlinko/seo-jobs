# The 2020 SEO Jobs Report

This is the Github repository for Backlinko´s 2020 SEO Jobs Report.

- 📝 The full data report can be found below.
- 🔨 The study was conducted with the statistical programming language [R](https://www.r-project.org/).
- 📊 [The code for the analysis and plots](https://github.com/backlinko/seo-jobs/blob/master/rmd/analysis.Rmd)
- 💾 [The datasets (excluding Linkedin due to its size)](https://github.com/backlinko/seo-jobs/tree/master/raw_data) 


&ensp;
### Contributors ✨
- Cédric Scherer and Daniel Kupka (both frontpagedata.com)
- Brian Dean (backlinko.com)


# 0. Introduction

We use two data sets:

* Glassdoor data (original) with 2,651 observations
* LinkedIn data (original) with 144,519 observations
  - subset for "SEO": with 5,856 observations
  - subset for "SEO" and English-speaking offers: with 984 observations

The LinkedIn data contain global job offers while the GlassDoor data only jobs from the US. The LinkedIn data including only job offers with the term `SEO` (or `seo`) contain 5,856 offers overall, 984 offers from English-speaking countries (USA, Canada, UK, Ireland, Australia, South Africa) and 862 from the USA and the UK (links starting with `www.linkedin.com`).

We merged both data sets and kept as many variables as possible, manually creating new variables for both datasets (GlassDoor: `seniority` and `employment type`; LinkedIn: `sector`) based on text matching of job titles and descriptions. We also removed as many duplictaed entries as possible by matching job title, employer and job location. The final worldwide data set contains 7,051 observations.

Because the job offers are collected from all over the world, a lot of foreign terms are included. Thus, we merged the GlassDoor data also with the English subset of the LinkedIn data and kept again as many variables as possible by manually creating new variables for both data sets. **The final "All English" data set contains 2,569 observations.**

The GlassDoor data are cleaner with regard to job titles and description than the LinkedIn data. Consequently, some plots using the GlassDoor data do a better job so we provide for now both version (the merged "All English" data set and the GlassDoor data set).

Also, the GlassDoor data contain information that are missing from the LinkedIn data such as `estimated salary range`, `rating`, `employer`, `industry`, and `size (no. of employees)`.



# 1. Job Title

## 1.1 Most Popular SEO Jobs

### Which words are the most popular in the job title?

We analyzed the data on job titles using text mining techniques. In a first step, we tokenize the job titles into single words and visualize their frequency. Stop words and words that appeared less than 7 times were removed to make the graph easier to grasp.


![](./plots/png/1_1_jobs_word_1.png)



### Which consecutive term sequences are the most popular in the job title?

In a second step, we analyzed sequences of words in the job title. The sorted bar plot shows the most popular consecutive sequences of words (5 or more occurrences), colored by category.


![](./plots/png/1_1_jobs_cat_1.png)



### Are technical terms in job titles more popular? Which technical and non-technical terms are most popular?

We  manually classified in technical and non-technical positions, removing all words that are no specific to any of the both categories:

* technical ~  `analy|special|engine|develop|technic|optimi`
* non-technical ~  `manage|direct|writ|consult|coordinat|edito|market|sale|social|strateg|supervis`

The modified stacked bar plot shows the number of words found per job category and, additionally as another stacked bar next to it, the most common words per category (with labels for words that occured at least 20 times). The height of the stacks indicates as well the number, the width is arbitrary.

![](./plots/png/1_1_jobs_tech_adj_1.png)



# 2. Location

**Note:** For now we focussed on the job offers from the US in terms of cities, states and counties. This decision was based on two reasons: First, we believe US data is of most interest; secondly, we center all our analyses on job offers from English-speaking countries only so a world map would be in contrast here. Of course, if you think it is valuable, we can also create a world map.


## 2.1 Hot Spots: Cities (Bubble Map)

![](./plots/png/2_1_map_states_cities_1.png)

![](./plots/png/2_1_bars_cities_1.png)


## 2.2 Hot Spots by States

### Chloropleth Map


![](./plots/png/2_2_map_states_chloro2_1.png)


### Hexagonal Tile Map

![](./plots/png/2_2_map_states_hex_1.png)


## 2.3 Hot Spots by US Counties

![](./plots/png/2_3_map_counties_chloro_1.png)



# 3. Company Info

## 3.1	Size

#### How large are companies that hire?

![](./plots/png/3_1_size_histo_1.png)



## 3.2	Revenue

#### How much revenue do hiring companies make? 

-> Counts of unique companies per revenue class

![](./plots/png/3_2_revenue_histo_1.png)



#### What type of skill sets are required by high-revenue companies?

I tokenized the description and removed stop words and numbers as well as manually non-sense/non-skill-related words. There might be more but if we keep it we can have a closer look I would say. The wordclouds show the 75 most common words per group.


![](./plots/png/3_2_revenue_words_horizontal_1.png)


## 3.3	Sector/Industry

#### Which sectors do mainly hire SEOs?

![](./plots/png/3_3_sector_counts_1.png)


#### Which industries are interested in filling SEO positions?

![](./plots/png/3_3_industry_counts_1.png)


## 3.4	Company Rating

#### Do more low- or high-rated companies hire? 

The following graphs show counts of unique companies per rating, first for each rating score found in the data (including 1 decimal place) and then as a histogram grouped into ranges of 1.


![](./plots/png/3_4_rating_lolli_1.png)

![](./plots/png/3_4_rating_histo_1.png)

#### Which companies have the highest ratings?

![](./plots/png/3_4_rating_best_1.png)
![](./plots/png/3_4_rating_worst_1.png)

**Note:** Since there were many companies with the highest rating of 5 (see plots before), we decided to modify the conditions and to remove companies with revenues below $10 million. There were anayway only seven companies with the lowest rating possible, so we did not apply any filtering in that case.



# 4	Job Responsibilities

This is a simple wordcloud of words mentioned in the job descriptions with a frequency of 10 or more. That way, we can scan through the list and select those that are of interest.

Words that occured at least 100 times:

![](./plots/png/4_cloud_word_upper_1.png)


Words that occured at least 1000 times:

![](./plots/png/4_cloud_word_1000_upper_1.png)

**Note:** Consecutive sequences of words (*ngrams*) in the job desciptions do not bring any insightful, a lot of phrasings and fill words.



# 5	Job Requirements

## 5.1	Education

We extracted from the job descriptions the required/desired degree:

* Bachelors ~ `b.ba.|b.sc.|bba|bsc|\\bbachelor\\b`
* Masters ~ `"m.ba.|m.sc.|mba|msc|[(to|will)]\\s\\bmaster\\b`
* Doctorates ~ `ph.d.|phd|doctora`

In total we found 792 positions mentioning Bachelors, 204 Masters and only 11 belonging to the Doctorate category (out of 2,651 job offer descriptions). 

Afterwards, we determined the minimimum degree required (Doctorate > Masters > Bachelors), yielding 792 Bachelors, 146 Masters and 7 Doctorates.


#### What type of degrees are most often required (Bachelor vs Master vs Doctorate)?

![](./plots/png/5_1_require_edu_histo_1.png)
![](./plots/png/5_1_require_edu_histo_non_1.png)

For example, ["SEO Manager" by Quizlet in San Francisco, CA](https://www.glassdoor.de/job-listing/seo-manager-sf-denver-quizlet-JV_IC1147401_KO0,21_KE22,29.htm?jl=3563120344&countryRedirect=true), with an estimated average salary of $107.5K has listed no degree requirements .


#### Do larger companies require a formal education?

**Note:** There are many ways one could look at those numbers: absolute, proportional across all job offers and proportional within all that list any educational requirement.


A) Absolute nubmer of job offers requiring a qualification (but thus no information about the overall number of job offers - coult be added but would make most of the plot grey = no requirement...):

![](./plots/png/5_1_require_edu_size_n_1.png)
![](./plots/png/5_1_require_edu_size_n_non_1.png)

B) Proportional across all job offers (i.e. number of offers with [education] / sum(job offers)):

![](./plots/png/5_1_require_edu_size_rel_1.png)
![](./plots/png/5_1_require_edu_size_rel_non_1.png)

C) Proportional of all job offers requiring a qualification (i.e. number of offers with [education] / sum(job offers with any education required)):

![](./plots/png/5_1_require_edu_size_rel100_1.png)


#### Which education level is required by high-revenue companies?

A) Absolute nubmer of job offers requiring a qualification (but thus no information about the overall number of job offers - coult be added but would make most of the plot grey = no requirement...):

![](./plots/png/5_1_require_edu_revenue_n_small_1.png)
![](./plots/png/5_1_require_edu_revenue_n_non_small_1.png)


B) Proportional across all job offers (i.e. number of offers with [education] / sum(job offers)):

![](./plots/png/5_1_require_edu_revenue_rel_small_1.png)


![](./plots/png/5_1_require_edu_revenue_non_small_1.png)

C) Proportional of all job offers requiring a qualification (i.e. number of offers with [education] / sum(job offers with any education required)):

![](./plots/png/5_1_require_edu_revenue_rel100_small_1.png)


## 5.2 Programming Languages

#### What programming languages are most often required?

I for now use the programming languages listed by the SO yearly survey:
JavaScript, HTML/CSS, SQL, Python, Java, Bash/Shell/PowerShell, C#, PHP, C++, TypeScript, C, Ruby, Go, Assembly, Swift, Kotlin, R, VBA, Objective-C, Scala, Rust, Dart, Elixir, Clojure, WebAssembly + Julia

![](./plots/png/5_2_require_prog_1.png)


#### What languages are most often required in combination (e.g. HTML and CSS)

![](./plots/png/5_2_require_prog_comb_1.png)



## 5.3	Knowledge of Popular Tools

We searched for given tool names within the description of the job offer. The following list of (popular) tools was used for the the analysis:

`Bing Webmaster Tools`, `Botify`, `Bright Local`, `Browseo`, `Clusteric`, `ContentKing App`, `DareBoost`, `DeepCrawl`, `EasyRedir`, `Forecheck`, `Google Analytics`, `Google Mobile-Friendly Test`, `Google PageSpeed Insights`, `Google Search Console`, `Google XML Sitemaps`, `GTmetrix`, `HeadMasterSEO`, `LinkPatrol`, `Lipperhey`, `OnCrawl`, `Panguin Tool`, `Raven Tools`, `Screaming Frog`, `Seobility`, `Seomator`, `SERPmetrics`, `Siteliner`, `Topvisor`, `Varvy SEO Tool`, `Whitespark`, `Woorank`, `Yoast`, `Zadroweb`, `Answer The Public`, `ClearScope`, `Exploding Topics`, `FAQfox`, `Google Keyword Planner`, `Google Location`, `Google Trends`, `Google Data Studio`, `Gookey`, `GrepWords`, `HitTail`, `Imforsmb`, `iSpionage`, `Jaaxy`, `Keyword Eye`, `Keyword Revealer`, `Keyword Snatcher`, `Keyworddit`, `KeywordIn`, `Keywords Everywhere`, `KeywordSpy`, `KeywordTool.io`, `Kombinator`, `kwfinder`, `Long Tail Pro`, `Power Suggest Pro`, `QuestionDB`, `SanityCheck`, `SECockpit`, `Seed Keywords`, `SEMrush`, `SERPStat`, `SimilarWeb`, `Soovle`, `SpyFu`,
`StoryBase`, `TermExplorer`, `TwinWord`, `UberSuggest`, `Webtexttool`, `Wondersearch`, `Wordstream's Free Keyword Tools`, `WordTracker`, `Wordtracker Scout`, `Advanced Web Ranking`, `Agency Analytics`, `AMZ Tracker`, `Authority Labs`, `GeoRanker`, `Microsite Masters`, `NightWatch`, `Pro Rank Tracker`, `Rank Ranger`, `Rival IQ`, `SE Ranking`, `Search Latte`, `Serpfox`, `SERPs.com`, `SERPWoo`, `Sistrix`, `WebCEO`, `WordTail`, `Animalz Revive`, `BuzzSumo`, `Can I Rank`, `ClickFlow`, `Google SERP Preview Tool`, `Keys4Up`, `LSIGraph`, `MarketMuse`, `MetaTags.io`, `nTopic`, `Positionly`, `Ryte`, `SEOptimer`, `TrendSpottr`, `Upcity`, `WordLift`, `Ahrefs`, `cognitiveSEO`, `Kerboo`, `Majestic`, `Moz`, `MozBar`, `SEO PowerSuite`, `SEOGadget`, `ShareMetric`,
`URL Profiler`, `WebMeUp Backlink Tool`, `Morningfame`, `Social Blade`, `TubeBuddy`, `VidIQ`, `YTCockpit`, `AuthoritySpy`, `Buzzstream`, `DIBZ`, `disavow.it`, `Domain Hunter Plus`, `GroupHigh`, `HARO`, `JustReachOut`, `Linkbird`, `Linkody`, `Linkstant`, `MailShake`, `Muck Rack`, `Ninja Outreach`, `Ontolo`, `Pitchbox`, `Remove'em`, `Rmoov`, `ScrapeBox`, `Tableau`, `qlik`, `Power BI`


#### How often is the knowledge of tools required?

![](./plots/png/5_3_require_tools_1.png)

New version showing proportions none versus 1+:
![](./plots/png/5_3_require_tools_perc_1.png)


#### What tools are most often required?

![](./plots/png/5_3_require_tools_ind_1.png)


## 5.4	Years of Experience

#### How much experience is required?

Still not sure how to approach that in a better way. For now I have filtered the descriptions for the following strings:

* `[0-9]+ years experience` and `1 year experience`
* `experience: [0-9]+ year`
* `experience [0-9]+ year`
* `experience of [0-9]+ year`

Note: I checked some manually, especially the high values. An experience of 23+ years is really required by two job positions, but one with 30 years experience was a mistake that was likely to occur—it was part of the employer description: "the language recruitment specialist with over 30 years experience" and was thus removed.

![](./plots/png/5_4_require_experience_1.png)

Only up to 10 years:
![](./plots/png/5_4_require_experience_reduced_1.png)



# 6	Salaries

## 6.1	Salary Ranges

#### What are the typical salary ranges for SEO jobs?

![](./plots/png/6_1_salary_histo_1.png)


## 6.2	Salaries per Location

#### Where do companies pay the most/least?


![](./plots/png/6_2_salary_cities_1.png)

![](./plots/png/6_2_salary_states_1.png)



## 6.3	Salaries per job requirement

#### Do positions with programming languages pay significantly more?

![](./plots/png/6_4_salary_req_prog_1.png)

Median only:
![](./plots/png/6_4_salary_req_prog_med_1.png)

Bars showing average and standard deviation:
![](./plots/png/6_4_salary_req_prog_avg_bars_1.png)

For example, ["SEO Director" by Etsy in Brooklyn, NY](https://www.glassdoor.com/job-listing/seo-director-etsy-JV_IC1132200_KO0,12_KE13,17.htm?jl=3567392143), requires JavaScript, HTML and CSS with an estimated average salary is \$116K (estimated range \$108-123K). The average salary in the state of New York is \$71.6K and \$70K as median salary.


## 6.4	Salaries per Company Rating

#### Do lower rated companies pay less (salary)?

![](./plots/png/6_5_rating_salary_1.png)



# 7. Dates of Job Offer Posting

## 7.1 Job offers by week and year


All countries:
![](./plots/png/7_1_dates_weeks_all_1.png)

Only English-speaking countries:
![](./plots/png/7_1_dates_weeks_en_1.png)

#### Did the number of job offers decline during the COVID-19 pandemic?

![](./plots/png/7_1_dates_weeks_2020_1.png)

(The date in parenthesis indicates the week that covered the first of each month.)


## 7.2 Weekday of Posting

#### Are there favorite weekdays for job postings?

![](./plots/png/7_2_dates_weekday_1.png)


