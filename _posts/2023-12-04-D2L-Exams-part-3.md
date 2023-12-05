---
layout: post
title: Quiz Questions in D2L Brightspace part 3, Arithmetic Questions in 2 ways
mathjax: true
---
 <script src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"></script>

*This Project lives [on Github](https://github.com/amygoldlist/D2L_exams)*

Bet you thought we were done with this series!  In our last two posts, we covered creating multiple choice and FMB (fill multiple blanks) type questions.  What was missing was a short answer question, where the answer was numeric, so here are two methods that we can use to accomplish this.

### Part 1: Why are you doing this?
Great question fictional reader!  We have a project underway to update some of our self-paced online classes.  We would like to include some built in understanding type questions - and not just multiple choice ones.  These can be created within D2L Brightspace, but I have a file with hundreds of questions - I would like it to be easier than this!

As well, D2L is not one of the major LMS platforms, but it's the one that I work with.  In my earlier posts, we used the Blackboard option to create D2L question in the R/exams package.  This works pretty well, but since the code is different, we lose the ability to do some technical things such as:
* Create arithmetic questions!
* Make a Multiple Choice Question with shuffling answers!
This is all my attempt to make up for these shortcomings

#### What this project is and is not
This method won't create truly algorithmic questions just yet, even though I could expand to that in the future.  However, each question is different, it may be easier to just work within D2L itself.  Moreover, most of the functions I'm looking for (Derivatives! Probability distributions! Annuities!) are missing from the D2L code.  If you need this type of question, there are many other great platforms out there.  

This method has a specific framework:  Given a spreadsheet of questions, create a module that can be uploaded directly to D2L, with each question.  The questions themselves are static, but they should have a given unenforced tolerance, and a specific precision / margin of error.  For example, if the answer is 2, I want to accept 2.0 and 2.00000 as valid answers.  Sometimes, I want a margin of error, so if the answer is 3.14159, I will accept 3.14 $\pm$ 0.005.

## Methodology
This is the fun part!  Even when creating arithmetic questions in Respondus, I wasn't getting the behaviour I wanted.  What I did was create a quiz with several questions in it in a Sandbox D2L course.  I exported this quiz, and inspected the results. Inside the zipped folder were two xml files.  I ended up going full Beautiful Mind here, and printed out code and taped it up around my office, so I could highlight all of the attributes I was looking for.


<h5 align="center">
  <br>
<img src="/images/exams_images/xml_mess.jpg" alt = "My whiteboard" width="300">
<br>
</h5>

 I copied and altered the file, looking at the results, until I was satisfied that I understood how the file was working.  Then I asked around and figured out how people would want to organize their questions (answer: a spreadsheet), and continued with the work below.


## Step 2: The Spreadsheet.
All of these files live in the github repo posted above, so feel free to follow along.  

Right now, I've done this as an Excel file, as a lot of our questions exist in Excel.  This way, you can use Excel's built in randomizing tools (see previous posts in this series)

Here is my demo file, and yes, these questions are quite easy.

| N    | Question     | Answer | Precision | Title     | Tolerance | Hint                    | feedback                                           |
| ---- | ------------ | ------ | --------- | --------- | --------- | ----------------------- | -------------------------------------------------- |
| 1001 | What is 1+1? | 2      | 2         | adding 2  | 0.01      | This is a hint.  2      | feedback is this was an easy question              |
| 1002 | What is 2+1? | 3      | 1         | adding 3  | 0.005     | This is a hint, type 3  | your feedback is 3                                 |
| 1003 | What is 3+7? | 10     | 0         | adding 10 | 0.5       | This is a hint, it's 10 | feedback, you should have known the answer was 10! |


The answer to question 1001 is $2.00 \pm 0.01$, so 1.99 and 2.01 will all be accepted as correct. While this is not how I'd ask students to add, it's still an option I want to be able to code in.

You may want to use built in Excel commands to create 100 versions of the same question, which is fairly straightforward, if you are used to using the `Rand()` and `Randbetween()` functions.  If you want some help with Excel randomizing, I have some examples at ["On my Github"]("https://github.com/amygoldlist/Excel_fun/blob/master/Randomizing/random_variables.xlsx")

## Method 1: Microsoft only (mail merge option)
This method is incredibly straightforward, and it took me very little time to put together, once I understood the file structure.
1. Fill out the Excel file (or create your own).  You may leave the Hint and Feedback empty, if you'd like.
2. Open up the Word mail merge, and make sure that it is attached to the Excel file.  If not, use the mail merge wizard, and link it.  It should look something like this:

```
<item d2l_2p0:id="«N»" ident="OBJ_«N»" label="QUES_«N»" d2l_2p0:page="1" title=«Title»>
<itemmetadata>
	<qtimetadata>
		<qti_metadatafield>
			<fieldlabel>qmd_computerscored</fieldlabel>
			<fieldentry>yes</fieldentry>
		</qti_metadatafield>
```


3. Complete your Mailmerge, `Mailings | Finish and Merge | Print Documents`.  The top should look something like this:


```
<item d2l_2p0:id="1001" ident="OBJ_1001" label="QUES_1001" d2l_2p0:page="1" title=adding 2>
<itemmetadata>
	<qtimetadata>
		<qti_metadatafield>
			<fieldlabel>qmd_computerscored</fieldlabel>
			<fieldentry>yes</fieldentry>
		</qti_metadatafield>
		<qti_metadatafield>
			<fieldlabel>qmd_questiontype</fieldlabel>
			<fieldentry>Arithmetic</fieldentry>
		</qti_metadatafield>
```

4. Select all and copy (`Ctrl-A Ctrl-C`).
5. Open up the file `mail_merge_upload\questiondm.xml` in a program that you can write to - I've been using WordPad, but a simple text reader should work just find.  This is the preamble, or section information.  If you want, you can manually change the title, it's in the 4th line, in all-caps.  You can also move 5 rows down, and change the attribution to your own name (as opposed to `Created by Me`)


```
<?xml version="1.0" encoding="UTF-8"?>
<questestinterop>
	<objectbank ident="QLIB_1" xmlns:d2l_2p0="http://desire2learn.com/xsd/d2lcp_v2p0">
		<section d2l_2p0:id="1" ident="SECT_1" title="TITLE GOES HERE">
			<presentation_material>
				<flow_mat>
					<flow_mat>
						<material>
							<mattext texttype="text/plain">Created by Me</mattext>
						</material>
					</flow_mat>
				</flow_mat>
			</presentation_material>
			<sectionproc_extension>
				<d2l_2p0:display_section_name>no</d2l_2p0:display_section_name>
				<d2l_2p0:display_section_line>no</d2l_2p0:display_section_line>
				<d2l_2p0:type_display_section>0</d2l_2p0:type_display_section>
			</sectionproc_extension>
```

6. Paste your mailmerge in and save.  Your folder should now have two xml files in it.
7. Zip that folder! In Windows 10, which I am working with, you right-click the folder and hit `Send To | Compressed (Zipped) Folder`
8.  Go into D2L Brightspace and upload your zipped folder.  You should now have a section of questions, and you can do whatever you'd like with them.



## Method 2: Using R
Not going to lie, the mail merge method is quick and satisfying.  But, I reasoned to myself, there are too many steps!  In R, you wouldn't need to combine the steps - it could be all in one.  SO even though it isn't arguably the best use of my time, I went ahead and redid this work in R.  I decided to use the Tidyverse XML package, `xml2`, instead of the original `XML` library, and once I mastered it, I found it fairly straightforward.  Please look at my ["R script"](https://github.com/amygoldlist/D2L_exams/blob/main/Arithimetic_Type/XLSX_to_XML.R) if you are using this method!

### Steps to xml handling in R
* Read in an xml file via:
`xml_qq <- read_xml("data/questiondb_base.xml")`
* Find a Node, so that you can alter it:
`qq_node <- xml_find_all(xml_qq, xpath = ".//section")`
* Nodes have both text and attributes.  Inspect both via `xml_text(qq_node)` and `xml_attrs(qq_node)`.  Sometimes you will need to modify text, and sometimes attributes.
* Write a new attribute as:
`xml_attr(qq_node, attr = "title") <- filename`
* Write new text as:
`xml_text(qq_node) <- df$Question[i]` (here `df$Question[i] = "What is 1 + 1?"`)
* Note: When you find a node (such as `qq_node`) in my examples, you haven't created a new object.  `qq_node` is just a path to the original xml file, so changing the attribute or text does so in the original xml file.
* Write via `write_xml(xml_qq, "questiondb.xml")`

## Using the R file:
1. Step 1, Fill out the Excel file (or create your own).  You may leave the Hint and Feedback empty.
2. Alternatively: Use any R code you'd like to create a dataframe with your own questions in it:

```
df <- data.frame("N"= integer(),
                 "Question"= character(),
                 "Answer" = character(),
                 "Precision" = integer(),
                 "Title"= character(),
                 "Tolerance"= double(),
                 "Hint" = character(),
                 "feedback" = character())
```

3. You can modify the R script, changing the `file_name` or the data file.
4. Run!  You should now have a new folder with 2 xml files in it.  Zip them!  
5. Upload.

*Note: you can zip within the R script, but in running this on various computers, I came into too many permissions issues.  If you have a better way, let me know.*

## Limitations
There are a lot of limitations to this method!  
* If you want students to hand in written work with a question, this needs to be checked manually, It is part of the course package, not the question xml file.
<h5 align="center">
  <br>
<img src="/images/exams_images/1066.png" alt = "Handing in supporting documents" width="300">
<br>
</h5>

* No unit testing.  The reason I haven't made algorithmic questions, is that each question would need to be tested, to ensure that the code works.  This is simpler to do in R or Excel (or Python!), so for now, use one of these methods to print a csv
* Wait, it's an xlsx file, not a csv!  True, but the R code only needs `read_xlsx()` to be changed to `read_csv()` or `read.csv()`.  I was using an Excel data table, but it could easily be a read_csv

## Further Questions
To be honest, it's been 3 years, and I didn't expect to still be working on this years later. So for now, I'm saying I'm done, but the future could hold other things!
Theoretically, my next Blog post should be an announcement that another Open Textbook is ready to view, but it's still in draft as of today.
