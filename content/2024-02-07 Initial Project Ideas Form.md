---
date: 2024-02-07
week: 2
time:
  - task: "[[Initial Ideas]]"
    time: 1.25 hours
    progress: 20
---
Date: Wednesday, Feb 7, 2024
# Work Undertaken Summary
- Decide on which project idea to progress
- Re-write project statement into Amanda's form format
# Problems encountered and how you overcame them
Not Applicable

# Time Spent
```dataview
TABLE WITHOUT ID
link(meta(entry.task.top-level-task).subpath) As "Top Level",
entry.task as "Second Level",
entry.time As "Time",
entry.progress as "Progress (%) this week est"
WHERE time != null
WHERE file = this.file
flatten time as entry
sort date desc
```

# Questions for Tutor
Thoughts on the idea.

# Next work planned
TMA01 Tutorial

# Raw Notes

![[2024-01-14 Project Ideas#Reasoning]]

## Document
Please complete the following template and email it back to me

1.Student name:- Luke Foreman - K2746451 - lf5853

**2.Project title:- Using language models to transform 7 years of User Stories into a complete software specification**

**3.Paragraph to summarise your project idea:-**

**For the last 7 years I have been working full time as a software engineer, primarily on a single very large software solution. This software solution has been developed in an incremental and agile manor, with approximately 3000 user stories generated and approximately 14 years of engineer development time.**

**The software solution is incredibly complex, and has evolved quite considerably since initial development. Occasionally with a flip-flop between what is and isn't allowed / the system needs to handle as requirements evolve. As a result only 2 people know the entire history of the software solution and how everything interrelates. The goal of the project is to produce a single accurate specification for the software solution which can then be maintained going forward.**

**The OU project would involve running the user stories through various large language models (LLM) to generate a specification from them.**

**4.Aims and Objectives – number each one, I recommend you have 6-7 of these:-**

**Producing a specification through use of LLM’s.**

**1) The output of the LLM, the specification, will then be evaluated on several metrics:**

**a) Accuracy - Number of errors - categorised e.g. Hallucinations vs outdated information**

**b) Conciseness - To be a useful specification it must not repeat information and must be legible to the reader**

**c) Completeness - To be useful for describing the system it must cover everything to a sufficient level of detail**

**2) The process will be repeated for different LLM models:**

**d) GPT-4 (OpenAI/Microsoft)**

**e) LLama 2 (Open Source/Meta)**

**f) Gemini Pro (Google)**

**3) And repeated for different styles of generation:**

**g) Train on complete dataset and then produce specification**

**h) Incrementally introduce User Stories to evolve specification over time.**

4) Potentially can compare different techniques such as variations on prompts.

5) I will then compare the different specifications, with some data analysis. To determine the ‘best’ specification and to detail any learnings which may be carried forward in any future LLM project.

5.How do the following relate to your initial project proposal idea:-

a)The L3 course(s) that will be the base for this project is/are…

Data management and analysis (TM351) - Manipulating the large dataset +analysing the results

Software engineering (TM354) - The specification process, agile development, building of software to run the large language models against the dataset.

b)The problem is .... no specification for the software project exists, the only documentation are the user stories.

c)The stakeholders are .... myself, my dev team, the QA team and the client who will use the specification in discussions about future expansion.

d)The users are …… myself

e)I will be able to find out more by talking to….. fellow developers at work

f)The skills I have from my L3 study include these which are relevant to the problem – answered in part a?

g)The ways in which I will be moving my skills and knowledge beyond the L3 module(s) are .. Working with a real large dataset, creating a working software solution and working with LLM’s.

h)Any legal or ethical ramifications that might occur…. I've been cleared to use the data set but would not be able to provide the complete dataset or final specification as it would include business IP. But I would be able to discuss challenges with the process and provide relevant excepts.

i)The end product I will deliver will be .... A redacted specification and a report on the configurations that provide the best results / how different factors relate to each other. E.g. comparing different LLM’s, impact of model density, style of training etc.