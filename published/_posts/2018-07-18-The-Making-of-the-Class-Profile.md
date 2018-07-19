---
layout: post
title:  "The Making of the Class Profile"
date:   2018-07-18 12:00:00
extra_css:
categories: []
published: true
---

## Overview
After seeing the Systems Design Engineering 2017 Class Profile, I was deeply inspired to create a class profile for my class. I owe a lot to my class and my program, and felt incredibly lucky to be a part of it. I’m originally from Montreal, so coming to University of Waterloo originally never occurred as an option. Prior to university, I barely even knew what software engineering was, let alone code. If it weren’t for a friend of mine that convinced me to come to University of Waterloo, I wouldn’t be where I am today.

I wanted to create a class profile capturing what I wished I knew before university. I wish I knew what software engineering was like, what opportunities were available, how much debt I’d graduate with, if it’s too late for me to start coding, etc. There’s a lot of focus by the media on what software engineers in the industry are like, but the path connecting their beginnings to employment is still blurred.

The goal of our class profile is to share the life of software engineering students, covering topics such as co-op, academics, lifestyle, and much more, and to increase the transparency of the transition from a high school student to a full-time software engineer.

You can check out the final result [here](https://classprofile.andyzhang.net).

## Researching the topics
I gathered what people wanted to know about Software Engineering students through a survey. The goal of the survey is to gather questions from the target audience. In this project, the target audience is composed of students who are either interested or new to software engineering.

I created a Google Form to collect questions current SE students wanted to learn more about, or wish they knew during high school. SE students were asked because they were students who were once interested in SE and are possibly still new to SE (depending on the year). In total, I collected 152 questions from 40 survey responses across 5 class of SE students.

I went through all of the questions and collapsed any questions that were redundant. I then classified the question type:

- One dimensional: Can be answered by one data point. Ex: How many hackathons did students attend?
- Two dimensional: Can be answered by two data points. Ex: Do grades affect salary?

Afterwards, I removed questions that were too specific or could not be included in the survey (dating life, sex, etc.). The latter questions were separated into a second anonymous class survey and is not associated with this class profile.

## Designing the survey
The main challenge with surveying our class was to get a high response rate. My goal was to get an 80% response rate, so I made several compromises to the survey:

- It should take 15 minutes to respond, meaning we had to cut questions.
- Its responses should not be seen by any students including myself. The technicalities are discussed in the section below.

Once the questions were fully sorted, the questions were broken down into individual survey questions. Some questions were also shortened for brevity. For example, hackathon attendance per term was shortened to hackathon attendance throughout university.

I did a beta test on a small group of students to gather feedback on the survey. The feedback consisted of catching edge cases (ex: there’s no numerical grade during an exchange term, some people skipped a co-op). After addressing the feedback, I was ready to launch the class survey.

## Surveying the SE class of 2018
To further incentivize the class to fill out the survey, I talked to several professors to see how they’ve incentivized students in the past to fill out faculty surveys. Luckily, Derek Rayside, our FYDP professor, was supportive of the class profile and offered to add marks for everyone if the survey reached a good response rate.

In addition, Patrick Lam, the director of Software Engineering, agreed to teach our weekly class wearing a silly outfit if we could reach an 80% response rate.

The survey closed with a 79.6% response rate.

## Working with anonymous data
Processing the data became fairly tricky because the survey data was on Patrick Lam’s computer. This was an important constraint because many students expressed concerns on their personal data and didn’t want it to be seen by any students including myself. As a result, Christopher Luc and I came up with a system to process the data anonymously.

Before programmatically processing the data, the data needed to be formatted consistently. For example, company names needed to be standardized (ex: Snap, Snapchat, Snap Inc becomes Snap).

To view a column without being able to infer which row it belonged to, the system shuffles each column independently from each other. Once each column is shuffled, it creates a local file storing the shuffled column as well as the original row indices. These indexes are a key piece to rebuilding the original data.


![](https://d2mxuefqeaa7sj.cloudfront.net/s_C06BD5FE808963B501FC9DC320DB063FF82ADE2A7F2CC68E30CA7CFA6F42ED55_1531151148334_Group.png)


Patrick only sent me the shuffled columns and held on to the original indices. I manually normalized the data, fixed any typos and ensured that answers were properly formatted so that they could be processed programmatically.

Once I finished normalizing the whole dataset, I sent back the shuffled columns so that Patrick could stitch each modified shuffled columns into a new dataset.


![](https://d2mxuefqeaa7sj.cloudfront.net/s_C06BD5FE808963B501FC9DC320DB063FF82ADE2A7F2CC68E30CA7CFA6F42ED55_1531151148330_Group+2.png)



## Transforming the data

There were two types of findings that we were looking for: one dimensional (how many X in the class?), and two dimensional (does X affect Y)? I already had the data I needed for the one dimensional findings, but needed more work to gather data for the two dimensional findings.

I wrote several scripts to transform the raw data into a structured format that didn’t reveal anything about a student. This was done by minimizing the coupling between each column of a row. For example, if I wanted to see the effect of grades on salary, I grouped each grade with the corresponding salary into a pair. Each of these pairs were disconnected from the pairs from other terms.

![](https://d2mxuefqeaa7sj.cloudfront.net/s_C06BD5FE808963B501FC9DC320DB063FF82ADE2A7F2CC68E30CA7CFA6F42ED55_1531153008026_Group+3.png)


In this example, disconnecting data from each term prevents me from identifying a recognizable salary (i.e. outliers), and then reading the row. Since the terms are disconnected, I could not see the data from the person’s other terms.

These scripts were shared with Patrick Lam so that he could run them on the normalized data sets. He then sent me back the structured datasets for me to process.


## Learning from the data

After I finished transforming the data, I visualized each data set to determine whether there was something interesting in the data. Since the structure of each data set was similar, I was able to reuse my visualizations easily, enabling me to figure out what had potential.

Although visualizations didn’t help me figure out if something was statistically significant, it did help me filter out what was not statistically significant.

![](https://d2mxuefqeaa7sj.cloudfront.net/s_C06BD5FE808963B501FC9DC320DB063FF82ADE2A7F2CC68E30CA7CFA6F42ED55_1531153807167_image.png)


In this example, it was easy to tell that there was a low chance of there being a correlation between parental education and salary per term.


![](https://d2mxuefqeaa7sj.cloudfront.net/s_C06BD5FE808963B501FC9DC320DB063FF82ADE2A7F2CC68E30CA7CFA6F42ED55_1531153995773_image.png)


In this example, I was plotting hackathon attendance vs salary. I noticed that there was a difference between students who didn’t attend hackathons and students who did. This led me to running more rigorous statistical tests to see if there was a correlation.


## Statistical verification

After visualizing all of my transformed data sets, I narrowed my focus down to the data sets with potential. I consulted with Christopher Luc, a two time Data Science intern (meaning he’s legit!), what methods he would recommend for the data I had. There were two methods I used: one way ANOVA, and finding correlation coefficients.

I ran the one way ANOVA on data sets involving groups of distributions. For example, gender vs salary had two groups. Each entry from a student was their average salary. The aggregation of each average salary led to a distribution for both male and female students.

I evaluated the one way ANOVA p-value from the groups to determine if there was a significant difference. If the p-value was lower than 0.05, it means that there is a significant difference between the groups. In statistical terms, it meant that there was a dependent variable who’s value can be affected by the independent variable. In most cases, grades and salary were the dependent variables.


## Writing the content

By this point, I had all of the findings I needed to start writing the content accompanying the findings. I worked on prioritizing all of the findings based on the story I wanted to share with prospective and current students.

I split the content based on the types of audiences: those who want to skim the profile, and those who want to read more in-depth. Similar to the SYDE 2017 class profile, for each section, I focused on a one-liner, answering “If there was one takeaway from this section, what would it be?” Below the one-liner, I focused on elaborating on the findings, providing extra explanations if needed.


## Designing the page

As I wrote the report, I borrowed a lot of inspiration from other reports such as SYDE 2017 class profile, HackerRank’s Developer Skills Report, and more. The report needed to be representative of what brought our class together, and that was software engineering.

I wanted the report to be readable, but also resemble to a command line. I settled with a monospace and a sans serif font pairing for the content. I borrowed colours from my favourite terminal colour schemes such as Solarized, and also handpicked several desaturated colours that complimented the colour scheme.

For the cover photo, I wanted to have things that were common in the daily lives of software engineers. This included coffee, code, web browser, laptop, servers, etc. I put them all together into an isometric-styled illustration, and applied a suitable blue and purple colour gradient on it. Purple is a colour that represents engineering in Canada, and blue is a colour common in tech companies (Facebook, Dropbox, Twitter, Dell, IBM, etc.)

![](https://d2mxuefqeaa7sj.cloudfront.net/s_C06BD5FE808963B501FC9DC320DB063FF82ADE2A7F2CC68E30CA7CFA6F42ED55_1531971588293_cover+photo+no+text.png)



## Building the website

It seemed fitting to build the class profile given it’s about a software engineering class. One of the main priorities for the class profile was that it was a good reading experience across platforms. Therefore, it needed to load quickly, and also be responsive for mobile.

To reduce load time and increase performance, the use of images was minimized. Although creating images of charts would be straightforward with existing native software, I built the visualizations using D3 in order to reduce load time as well as optimize for responsiveness. Building the visualizations from scratch also allowed reusability and better customization.

The final website has a total bundle size of 1.5MB. In contrast, Reddit’s homepage has a total bundle size of 1.7MB.


## Launch the class profile

The launch date was set to be at the beginning of a week on a Monday under the assumption that more people will read this on a weekday than on a weekend. That way, the lifespan of the content will last a full 5 days rather than get cut by the weekend. I was hoping that it would also be a great conversation topic for the week for readers, allowing it to gain more potential traction.

I introduced the class profile through a Medium post, similar to the SYDE 2017 class profile. This showcased some of the highlights from the class profile, and linked to the full class profile should the reader want to learn more.

Since prospective students were the target audience, I also worked with the Software Engineering department to include a link to the class profile on the program’s website. This helps prospective students learn more about what studying software engineering is like.


## Conclusion

This was one of the most challenging but exciting projects I’ve worked on. Nothing excites me more than seeing so many different pieces come together into one final result. There’s still so much I would want to include in this post, but I didn’t want to make this as long as the class profile itself. The process involved a wide range of responsibilities such as research, talking to stakeholders, engineering, design, data science, etc., all of which are responsibilities that I deeply enjoyed.

There was something new to learn in each part of the process. For example, learning how to make isometric illustrations, familiarizing myself with Jupyter notebook, studying ANOVA on Wikipedia, and much more. Applying these learnings was just as fulfilling as learning them, making the process enjoyable from start to finish.

If you’re interested in learning more about the process behind our class profile, I’d love to chat! You can reach out to me via email ([andzhng@gmail.com](mailto:andzhng@gmail.com?subject=Hello)) or give me a shout on [Twitter](https://twitter.com/andyzg3)!

