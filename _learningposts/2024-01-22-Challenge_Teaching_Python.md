---
layout: post
title: How to Teach Python and Pandas
date: 2024-01-21
tags: [learning design, python, desirable difficulties]
cover-img: /assets/img/PathCNN/Histopath.png
mathjax: true
---

## The Challenge of Teaching Python

In my role as a Product Manager of Curriculum at 2U, I made frequent use of Python to automate the creation of data reports for university partners. These reports contained data about student satisfaction and faculty activity in the online environment - data that changed frequently, but was always presented in the same way. 

I was the beneficiary of a fantastic Python course in business school, and I put the knowledge to good use, but I have often thought about what the best way to share that knowledge with my peers would have been. I made my code available to those who were interested, but I wonder if I could have taught my colleagues how to customize their own reports. This post is my attempt to think through how I would do that.

I know generative AI makes this exercise a bit outdated, but it is always prudent to read anything ChatGPT produces. While proofreading is rapidly turning into a more useful skill than coding from scratch, it is still useful to know the basics of how to code in Python.

For this exercise, I will focus on automating PivotTables, which was the most common use case in my last job.

In this post, I will outline:

* What a PivotTable is
* How I would construct an online learning module to teach PivotTables in Python

## Pivoting Perspective
For readers who may not know, PivotTables are a way to visualize information in spreadsheets to find trends. 

It makes a lot more sense when you see it, so in the same grand tradition as my Python professor, I will demonstrate using my custom Pokemon stats spreadsheet.

The image below shows the base Pokemon spreadsheet:

<img src="{{ site.url }}{{ site.baseurl }}/assets/img/PathCNN/Pic1.JPG">

A PivotTable would allow you to compare stats between types by aggregating all the information associated with, for example, the "Type 1" column, which is what the image below shows:

<img src="{{ site.url }}{{ site.baseurl }}/assets/img/PathCNN/Pic2.JPG">

The PivotTable above shows all Type 1 tags sorted by average attack. For example, in row 1, the PivotTable has provided the average of the "Attack" values of every pokemon with the value "Fight" entered into the "Type 1" column in the source spreadsheet. You can see that Pokemon with "Fight" as their first type have the highest average attack. 

While this information might seem trivial, you can use this same process to see what courses in a graduate degree program have the highest net promoter score, for example.

To create this PivotTable in Excel, I:

* Moved to the "Insert" tab
* Clicked PivotTable
* Added "Type 1" to the rows section
* Added "Attack" to the values section
* Changed the default "Sum of Attack" to "Average of Attack"
* Left clicked the Attack column in the PivotTable
* Changed the settings to reduce the number of decimal points to 0
* Sorted the PivotTable by the Attack column from largest to smallest

Phew! That's a lot of clicks, especially when you have to do that for every data report you create.

That's where Python comes in handy. Writing a script would take care of those steps every time you need a report. All you would need to change is the data source in the code, then you just make one click: "Run".

## Designing a Module to Teach Python

To teach PivotTables in Python, I would rely on a design emphasizing desirable difficulties. This approach stretches students to the limit of their ability and primes their long term memory for the correct answer. 

Another reason for this approach is to teach students about the value of Stack Overflow as a resource. Stack Overflow is an online community of coders where anyone can ask questions, and experienced coders almost always know the answers. The range of examples on Stack Overflow is so robust that I have never had to ask a question - the answer is already on the website, because someone else has had the same question.

The learning design to teach Python is as follows:

##### 1. Ask students, "How would you create a PivotTable in Excel or Google Sheets?"

This step primes previous knowledge, preparing students to incorporate what they are learning into long term memory.

##### 2. Ask students, "Try to write a script using pandas (a software library integrated into Python) to accomplish the same task. You may look at Stack Overflow and other online resources for this exercise."

This step challenges students to push themselves, teaching them about online resources that will be useful to them in the future.

##### 3. Reveal the correct answer in a lecture or live demonstration, so students can see the code being written.

This demonstration reveals expert thinking on the topic, showing students how they can think while coding to be successful.

##### 4. Ask students to complete the script using pandas and referring to the lecture as a guide.

This question provides another practice opportunity to reinforce what students learned in the lecture.

##### 5. Ask students to reflect on their attempt from step 2. What did they get right in their first attempt? How was the instructor example different?

This step prompts metacognitive thought as students reflect on the learning process and what the key takeaways are.

## Conclusion

Who knows if my colleagues would have been patient enough for this approach. After all, the first impression of this pedagogical approach is, "What do you know already? Great, now figure it out for yourself." 

But for students who are willing to go through the learning exercise from beginning to end, I think this is the best way to ingrain the knowledge in their minds. Python is another language, after all, and there's no better way to learn another language than to be thrown into an immersive experience.

Finally, for those who are interested, here's how you can code a PivotTable in Python. The "#"s mark author notes to explain the purpose of the individual line of code:


```python
#import the libraries necessary to complete the task, pandas and numpy
import pandas as pd
import numpy as np

pokemon = # the file path to the Pokemon spreadsheet (ensure it is a csv file)

#import the pokemon file
pokemon_pd = pd.read_csv(pokemon)  

#show the first few lines of the file
pokemon_pd.head()

#"groupby" is the code used for PivotTables in pandas. You can create a new PivotTable from the old spreadsheet with the following code

PokePivot = pokemon_pd.groupby(["Type 1"])

#The following code gives you the mean of all the stats associated with the "Type 1" value
Pokemon_stats = PokePivot.mean() 

#check your work by looking at the first few rows:

Pokemon_stats.head()

#You can sort your table by Attack stats with the following code:

ordered_mean = Pokemon_stats.sort_values('Attack', ascending = False)

#Check your work

ordered_mean.head()

#This code should get you exactly what the second image in this post showed, except all the other stats are listed too

#to save this as a new excel sheet, you can use this code

ordered_mean.to_csv("output/Pokemon_Type_1_Attack_Average.csv")

#This will save the new table as a csv in your files

```

All of that code might seem complicated to write, but you only have to do it once. After that, any time a new pokemon is created (as they so often are), you can plug the new data into your source spreadsheet, run the code, and have the new information on how each type compares in a few seconds. 

Imagine the possibilities for all the reports we create manually.
